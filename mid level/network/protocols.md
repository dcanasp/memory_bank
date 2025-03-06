Network protocols are sets of **rules** or standards that dictate **how data** is **transmitted** and received in a [[network]]. They ensure reliable and secure communication between devices. Protocols define everything from the format of data packets to error handling and data compression methods.
The big two will always be **TCP** and **UDP**, as the other protocols use them, for example [[HTTP]] will use deep down TCP, so to structure this node i will tell the protocol, the [[port]] and if it uses TCP or UDP (or both)
# TCP (Transmission Control Protocol)
Ensures reliable, ordered, and error-checked delivery of data. Uses the [[three way handshake]]
# UDP (User Datagram Protocol)
A simpler, connectionless protocol for applications that do not require ordered data.

# Main Network Protocols
- [[IP]] **(Internet Protocol)**
    - Responsible for delivering packets from the source host to the destination host based on IP addresses. 
    - Port: N/A
    - It's actually **used** both by TCP and UDP
- [[HTTP]] **(Hypertext Transfer Protocol)**
    - Used for transferring web pages over the Internet.
    - Port: 80
    - TCP
	    - There is also HTTP/3 and it uses UDP
- [[HTTPS]] **(HTTP Secure)**
    - An extension of HTTP with security features for encrypted communication.
    - Port: 443
    - TCP
	    - Same as HTTP/3 it works on UDP
- **FTP (File Transfer Protocol)**
    - Used for transferring files between a client and a server on a computer network.
    - Port: 20 and 21
    - TCP
- **SSH (Secure Shell)**
    - Provides a secure channel over an unsecured network, commonly used for logging into remote machines.
    - Port: 22
    - TCP
- [[DNS]] **(Domain Name System)**
    - Translates domain names into IP addresses.
    - Port: 53
    - TCP
- **SMTP (Simple Mail Transfer Protocol)**
    - Used for sending emails.
    - Port: 25
    - TCP
# Types of Network Protocols
- **Communication Protocols**
    Govern the direct communication between devices ( TCP, UDP).
- **Routing Protocols**
     Manage the paths along which data travels in the network (BGP, OSPF).
- **Security Protocols**
     Ensure data security and integrity during transmission ([[SSL]]/TLS).