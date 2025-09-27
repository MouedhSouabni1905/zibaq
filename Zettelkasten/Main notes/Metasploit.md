**Tags:** [[Linux]] [[Cybersecurity]]
### > Encoders
Tools that encode a payload so that threat scanners and antivirus can't detect the malicious code.
### > Evaders
Unlike encoders, they actually try to evade the scanning software altogether.
### > Exploits
Ready-made exploits for specific targeted systems that facilitate pentesting.
### > NOPs
A set NOP instructions in different ISAs for the different procssors that exist.
### > Payloads
A set of different programs that open a shell on the vulnerable system targeted for pentesting.
#### Adapters
A kind of wrapper that takes a payload and wraps it into a command that can be run directly from a shell to execute the code.
#### Singles
Standalone payloads that don't need other pieces of code to be loaded to execute.
#### Stagers
Programs that open a connection between the target system and metasploit to load malicious code on the target system.
#### Stages
Payloads that require other pieces of code to be loaded onto the targeted system to be able to execute, usually through a stager.

In metasploit, "shell_reverse" refers to a single reverse shell payload whereas "shell/reverse" refers to a staged reverse shell payload.
### > Post
Used for the post-exploitation process (privilege escalation, etc).

### Commands

Exploits are ranked from low ranking to excellent ranking based on how likely they are to succeed, how easy they are to use and whether they can detect the targeted vulnerability automatically or not.

The `use` command allows to enter the context of the module passed as an argument. To list the required parameters that need to be set, type `show options`. Setting parameters happens by entering `set PARAMETER_NAME VALUE`.

"Contexts" are modules that are used as a type of configuration which can help narrowing down the possible exploits for the targeted system ( `info {path/to/module}` provides detailed information on the specified module). The command `info -d` generates complete documentation for the module and opens it in a browser.

The `?` command prints out the help page for msfconsole.

`meterpreter >` means a metasploit agent has infiltrated the target system and connected back to you. It's one of the available payloads to execute on a target system.

`exploit` runs the current module. Alternatively, run can be ised since it makes more sense for modules that are not exploits (like scans).
### Module options

You can use `set` and `unset` to change or clear the options on the current model. Such options are: RHOSTS (Remote Hosts, ie. the target system), RPORT (ie. the port to connect to on the target system), LHOST and LPORT (the same but local, ie. the machine you are using). To keep these changes through other modules, use `setg` and `unsetg` (g stands for global). The `back` command allows you to leave the current context.

### Sessions

When you enter a `meterpreter >` session, you can `background` it (or ctrl+z) to continue using other exploits, then use the `sessions` command to list all opened sessions then `sessions -i SESSION_NUMBER` with `SESSION_NUMBER` being the number listed from the previous command.


********************************
- **Note:** Using db_nmap when inside msfconsole will add the information discovered from the scan to the `hosts` information, which you can check with that last command.

**********************************

### Writing custom Metasploit scripts

We create a class that inherits from the `Msf::Auxiliary` class, which indicates that it is an auxiliary module in the context of metasploit.
We then define an initialize funtion which defines information about the module, like the name, descritption, author and licence.
Then we call a `register_options` method and `deregister_option` method to define the relevant options to the exploit (eg. RHOST, RPATH, etc).
Then we define a run method, which is the method that will be called when the script is executed.
After finishing the script and saving it, we can find it (after entering the msfconsole prompt) using `search script_name` then `use PATH_TO_SCRIPT` to enter the context of the script.
Then after `show options` we can set the relevant options (eg. if the script does a request to a server, we would `set RHOST host_name`, and so on with the other options).
Finally, we use `exploit` to execute the script, and we get the result.

*See more on this at: https://www.offsec.com/metasploit-unleashed/introduction/
And: https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html