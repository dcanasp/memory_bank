serves as a communication **endpoint**, allowing data to be sent and received between two processes on a [[network]]. The union of an [[IP]] address and a [[port]] number uniquely identifies a socket, enabling communication with specific processes on a computer.

`127.0.0.1:3000` represents a socket where `127.0.0.1` is the IP address, and `3000` is the port number.

Any [[protocols]], such as HTTP (port 80) or HTTPS (port 443), have default port assignments. While these are commonly used, it's advisable to **avoid them**, especially for sensitive services like databases, to enhance security.


This concept is different of a [[WebSocket]]