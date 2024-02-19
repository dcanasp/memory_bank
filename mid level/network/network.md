A network in computer science refers to a collection of **interconnected devices** (like [[computer]], [[server]], and [[Router]]) that can communicate and share resources. Networks are essential for the exchange of data, facilitating communication, and enabling resource sharing, which includes software, hardware, and data.

# Types of Networks

## Local Area Networks (LAN)

A LAN connects computers and devices within a limited area, such as a office building. It allows for high-speed data exchange and resource sharing within this confined area.

Normally LANs are connected through cables, and they are under the same [[Router]], that is what allows it's communication. The send the information to the router, and if it finds the device requested it sends that information 

## Wide Area Networks (WAN)

WANs cover broader geographical areas, connecting multiple smaller networks like LANs. They can be thought like a collection of LANs. The largest one is the internet we use. This is how we mostly communicate

## Metropolitan Area Networks (MAN)

MANs are larger than LANs but smaller than WANs. They cover a city or a large campus, providing high-speed networking resources to connect multiple LANs within a metropolitan area. These for example would be a network like the ones found on universities campus. They are accessible for anyone inside the premises

## Personal Area Networks (PAN)

PANs are intended for personal use within a range of a few meters. They include technologies like **Bluetooth** and infrared that connect personal devices such as phones, laptops, and personal digital assistants.

## Virtual Private Networks ([[VPN]])

As i said in that note, VPN are a tunnel for your data
# Network Topologies
How do i set up my network. These are it's possible architectures, In this context a node is any type of computer or device:
- **Bus**: There is a single cable and each node is connected to it. **Data** sent by a node is **available** to **all** other **nodes**, but only the intended recipient processes it.
- **Star**: features a **central** connection **point**, typically to a hub or switch, to which **all nodes** are **connected**. The nodes talk to this switch and it is responsible to send the information to the correct node. It offers better performance and reliability but can be more expensive to install and maintain.
- **Ring**: each node connects to exactly **two other nodes**, forming a ring. Data travels in one direction, and each device retransmits what it receives to the next until finding the expected one.
- **Mesh**: In a full mesh, **every node** is connected to **every other node**, offering high redundancy and reliability, but making it faster than any other topology.
- **Tree**: is a combination of the **star** topology **and** the **bus**  topology. where the central nodes of star networks are connected to a main bus. This forms a hierarchy of nodes, resembling a tree structure. (all switches connected on a bus to each other)
- **Hybrid**: Some times you need a special answer where you combine multiple standard topologies 
# Network Protocols

First of all let's remember the [[OSI]] model, That is a fundamental on how the network communicates. And also remember how an [[IP]] and [[Socket]] works. With that in mind also here is a list of the main [[protocols#Main Network Protocols|Protocols]]

# Network Hardware

- [[Router]]: are devices that forward data packets between different networks. They manage traffic and determine the best path for data transmission across networks.
- **Switches**: Network switches connect devices on a LAN. They receive data packets and forward them to the intended device on the network.
- **Modems**: Modems modulate and demodulate signals for communication over telephone lines. They enable internet access by converting digital data from a computer into an analog signal.
- **Hubs**: A hub is a basic networking device that connects multiple devices on a LAN. It broadcasts data received from one device to all other connected devices.
- [[firewall]]

# Wireless Networking
There are multiple ways to access a network wirelessly

- **Wi-Fi** allows devices to connect to a wireless LAN network. It uses radio waves to provide high-speed internet and network connections without physical wires.
- **Bluetooth** is a short-range wireless technology standard for exchanging data over short distances using UHF radio waves. It connects and exchanges data between devices like mobile phones, laptops, and headsets.
- **NFC (Near Field Communication)** enables communication between devices within a very short range (usually a few centimeters). It's widely used for **contactless payment** systems and simple data exchange between devices.

# Network Security

If the network gets infected any malicious problem could arise. it's very important that any communication is done using [[HTTPS]], here is a list of [[some attacks]]
