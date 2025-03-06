A MAC (Media Access Control) address is a unique identifier assigned to [[network]] interfaces for communications at the data link layer of a network segment. The primary purpose of a MAC address is to ensure that each device on a network has a unique, hardware-based identifier for the local network. This is crucial for controlling access and maintaining the integrity of the network.

MAC addresses six octets in hexadecimal separated by colons or hyphens (`00:1A:2B:3C:4D:5E`).

MAC addresses are typically assigned by the manufacturer of a network interface controller and are stored in its hardware, such as the card's read-only memory or some other firmware mechanism. Take into account that in [[docker|containerization]] [[podman|]] [[Kubernetes|]] you define the MAC

During data transmission over a network, the MAC address is used to ensure that the data reaches the correct destination on a local network segment.

MAC addresses can be [[some attacks|spoofed]], which is a vulnerability in network security. However, they are not routable over the internet, unlike IP addresses.