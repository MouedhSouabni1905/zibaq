**Tags:** [[Networking]]
## IP
Internet Protocol, used to split up the data sent from one computer to the other and manage their adressing scheme. In CIDR notation, /24 for example means that there are 24 bits in the address's binary representation that are reserved for representing the network. Thus, the dot separated decimal represention of the LAN's address would be the bits to decimals translation of the first 24 bits as is and the rest as 0s (IPv4 is 32 bits long). The subnet mask corresponds to an ip address with the first 24 bits set to 1 (in the context of the last example) and the rest set to 0. An ISP (Internet Service Provider) can have for example an IP address with a CIDR notation ending in /8, meaning it has 24 bits to address hosts (machines on the network), so a total of $2^{24}$ machines. Obviously it doesn't provide these as they are, but would split this into multiple subnets and subnets of subnets and so on to sell different networks for specific needs (specific number of machines).
## DHCP
Domain host configuration protocol, this is what assigns IP addresses to the new machines coming into the network.
## NAT
Network address translation, sits between private networks and the public internet and acts as the middleman, organising what data gets sent to which machine on the local private network. Usually routers in home networks use this.
## ARP
Address Resolution Protocol, translates IP addresses to MAC addresses (MAC are the addresses of the network interfaces on connected devices).
## DNS
Domain name system, translates a domain name to an IP address.
## TCP
Defines how the information is sent and recieved and check its integrity. Client sends a SYN request, server responds with SYN-ACK, then client responds back with ACK. This connects the two sockets on the client and server together, and allows the data to be sent. TCP checks data integrity with a checksum.
## UDP
Same level as TCP but doesn't check data integrity and doesn't need the sockets to connect, just sends the data to a specific port without further consideration.

# 