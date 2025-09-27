**Tags:** [[Sysadmin]] [[Cybersecurity]]
# Capture filter Syntax
- `host IP_ADDRESS` filters traffic to only the traffic involving the specified host
- `net NETWORK_ADDRESS/CIDR` filters based on the given network address and subnet mask
- `port` filters traffic coming through a specified port
- `protocol` filters traffic based on the specified protocol (`tcp`,`udp`,etc)
- Combined with logical operators `and`, `or`, `not`