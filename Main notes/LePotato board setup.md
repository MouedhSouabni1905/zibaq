# First try
- Installed the ubuntu image from the libre computer downloads page and wrote it to the microsd card. The green light turns on and the blue light flickers but I can't find it using `arp -a` (since I'm on a laptop I can't do graphical install so I want to do it via ssh). I guessed it didn't auto install so I tried modifying the image like this and then tried a different image.

# Didn't work
First you procure the image you want from the libre computer website's downloads section of the board you have. You can choose from different OS images with different releases and make sur the model in the image's name matches your board's module. I chose ubuntu server as I dont have a monitor or a usb to hdmi cable so I needed something with the possibility of headless auto-install and ssh from the get-go.

After installing the image, I set up the environment in which I will configure the image for headless installation using `nix-shell -p cdrtools cloud-init p7zip` which is a nix command that creates a devenv where I can use these tools without it polluting my user environment. `cdrtools` contains `mkisofs` which I used later on. 

The ubuntu server image configuration is done through a couple of YAML files, *user-data* and *meta-data*, the latter being irrelevant in my use case so I only needed to create it as an empty file.

I proceeded to extract the iso image with `xz -d ISO_IMAGE` inside my nix shell environment. After that, looking at the documentation on [canonical's website](https://canonical-subiquity.readthedocs-hosted.com/en/latest/tutorial/creating-autoinstall-configuration.html), I started writing my user-data configuration file. I decided to add reporting using [webhook](https://webhook.site)  and make it run a ping command at the beginning towards my laptop, and so I would use `sudo tcpdump icmp` to check whether it has connected or not. I also used `ssh-keygen` to generate an ssh key pair for direct access and added it but just in case something went wrong I allowed password login in ssh. And the last thing was an error command that sends logs through netcat to my laptop, again in case something goes wrong.  I used `mkpasswd --method=SHA-512` to make the password hash. 

Since this is a `.img` file, the extraction was done in 2 stages. First ` 7z -y x ubuntu-22.04.3-preinstalled-server-arm64+aml-s905x-cc.img` which outputs 2 files, then ` 7z -y x 0.img -osource-files` which will output the boot filesystem. Then, I copied my user-data.yaml configuration file to replace the user-data file inside the source-files directory. Then, in the cmdline.txt file in the source-files directory, I add `autoinstall` after the `quiet` argument. After that, I move all the files in source-files into a subdirectory inside source-files called boot then move the 1.img file into the source-files directory. Then I used `mkisofs -o myimage.img source-files` to generate the image and finally `sudo dd if=myimage.img of=/dev/sda` to write the image to my inserted microSD card.

# Other attempt, didn't work either
- Downloaded the `ubuntu-25.10-live-server-arm64.iso` ubuntu image
- `[nix-shell:~/Code/embedded/test/unpack]$ 7z -y x ../ubuntu-25.10-live-server-arm64.iso -ounpack/`
- Modified boot/grub/grub.cfg to include this:
```
menuentry "Try or Install Ubuntu Server" {
        set gfxpayload=keep
        linux   /casper/vmlinuz quiet autoinstall ds=nocloud\;s=/cdrom/ainstall/
        initrd  /casper/initrd
}
```
- And copied my user-data and meta-data files into `ainstall` directory that I created at the root of the unpack directory
User-data:
```yaml
#cloud-config

autoinstall:
  version: 1
  reporting:
    hook:
      type: webhook
      endpoint: https://webhook.site/f76ff53f-ebaa-4641-bce4-c121f1ac7cfd
  early-commands:
    - ping -c1 192.168.0.47
  locale: en_US
  identity:
    hostname: homeserver
  ssh:
    install-server: yes
    auhtorized-keys:
      - $ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGPyR1hE5pIMzGB+e/UwF06hx7Iy2uGbfGLXC60QfKqk lubbaragaki@nixos
    allow-pw: yes
  user-data:
    users:
      - name: admin
        gecos: 'Homeserver admin'
        passwd: '$6$faQCovnGZTGIsnLB$ACdmGcU8DdN4TsnK3wIebkJ./SG/jhI8nV2iBRqc.9qPC9t3XA4s3IuXnHpcvq.ymYRVU0ZohE.P/OGjX4srK1'
        groups: sudo
        shell: /bin/bash
        lock_passwd: false
  error-commands:
    - tar -c /var/log/installer/ | nc 192.168.0.47 8080
    - journalctl -b | nc 192.168.0.47 8080
```

# Other try
- Installed rpi-imager from nixos pkgs
- `chmod o+w /dev/sda` to allow the raspberry pi imager to write to it
- Configure the user and enable ssh, I chose the raspberry pi OS lite image
- Proceed to writing the image and wait
- No ssh, so I decided to try modifying the partitions flashed on the SD card like the libre computer pointed out for raspbian image
- `sudo mount /dev/sda2 ./mpoint` after having creating the mpoint directory, this mounts the filesystem allowing us to modify it without having to extract and recompile the whole thing
- `touch ssh` just as the guide says and then create and edit a file named userconf.txt where I added only one line `username:encrypted_password` after generating the encrypted password using `openssl passwd -6` (root permission necessary to create and edit the files since I'm editing a mounted filesystem)
- Leave the directory where I mounted and then unmount `sudo umount /dev/sda2`

# Final attempt (successful)
- Downloaded Armbian image for le potato
- Configured my nixos installation to create a subnetwork at the ethernet interface, connected via NAT to my wifi interface making it connect to the internet
- Flash the image on a microSD card using rpi-imager
- Insert the image and plug in all the cables to boot the board
- `tcpdump -i ETHERNET_INTERFACE_NAME` to monitor the traffic of the board and make sure it works
- `nmap -A IP_ADDRESS` to see if ssh service is running (it should appear as a service running on port 22)
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
```
- Proceed with the installer after ssh-ing into it
- `sudo ip addr add 198.168.10.173 dev end0` to add a static ip address to the board
- Install pi-hole using the command on their website 
- Configure my nixos to use the pi-hole as the dns server
- Set the dns server of the lepotato to itself `nameserver 127.0.0.1`in /var/tmp/resolv.conf
- Remove the auto-dns added by nixos, suggested by the home wifi router (still haven't figured that out)
- 

---
**References:**
- https://blog.arsfeld.dev/posts/2025/07/18/nixos-router-getting-started/
- https://documentation.ubuntu.com/public-images/public-images-how-to/use-local-cloud-init-ds/
- https://hub.libre.computer/t/ubuntu-22-04-1-jammy-lts-server-release-notes/63
- https://hub.libre.computer/t/troubleshooting-boot-issues-on-libre-computer-aml-s905x-cc/46
- https://www.pugetsystems.com/labs/hpc/How-To-Make-Ubuntu-Autoinstall-ISO-with-Cloud-init-2213/#Outline_for_creating_the_autoinstall_ISO
- https://man7.org/linux/man-pages/man1/dd.1.html
- https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started
- https://documentation.ubuntu.com/public-images/public-images-how-to/use-local-cloud-init-ds/
- https://cloudinit.readthedocs.io/en/latest/reference/index.html
- https://canonical-subiquity.readthedocs-hosted.com/en/latest/intro-to-autoinstall.html