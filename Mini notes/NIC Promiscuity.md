**Tags:** [[Sysadmin]]

To turn on promiscuity mode for an interface:

`sudo ip link set INTERFACE_NAME promisc on`

To turn off:

`sudo ip link set INTERFACE_NAME promisc off`

To view whether it's on or not (`promiscuity 1`=it's on):

`ip -d link | grep promiscuity`