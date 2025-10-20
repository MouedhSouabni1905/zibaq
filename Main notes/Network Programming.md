**Tags:** [[Networking]]
## Proxy
Sort of "relay" servers that take data and forward it to the destination the sender specifies. In hacking and cybersecurity, they can be used to access servers unaccessible from the outside, do fuzzing or reveal sensitive information through packet interception.
### How traffic interception using a proxy works:
The proxy takes in the request from the client, buffers it, then does whatever operation it's meant to do (fuzzing, dumping to analyze traffic, etc) and then sends it to the requested server. The request from the original client should have the FULL url in the path (after the GET), including http:// and all. The proxy parses all of that and sends a correct request (eg. GET / and correct hostname without http://), then after receiving the responses sends it back to the original client.
### How firewall evasion and bypassing using a proxy works:
Basically you need a proxy that has an ip adress that the server firewall accepts for example.
Or if the firewall is blocking a certain port you want to send on, the proxy recieves through a different port and then sends, recieves and transmits your data for you.
### Reverse proxy
Whereas a proxy acts on behalf of a client, a reverse proxy acts on behalf of a server. It is commonly used for load balancing (distributing requests across multiple servers), caching, handling encryption and decryption to remove that load from the servers, hiding the identity and characteristics of servers to protect them of outside attacks, and directing requests to the appropriate server based on specified criteria.