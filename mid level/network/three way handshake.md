The TCP three-way handshake is a method used in the [[protocols|TCP/IP]] protocol to establish a **reliable connection** between a client and a server. Essential for initiating a communication session in a TCP/IP [[network]].

This process Verifies that both the sender and receiver are ready to communicate and that the receiver is able to receive data. And Establishes initial sequence numbers to be used during the session, ensuring ordered data transfer.

# Steps for starting 

**Step 1: SYN**
    The client sends a SYN (synchronize) packet to the server, indicating the start of a communication and the initial sequence number.
**Step 2: SYN-ACK**
    The server acknowledges the client's SYN packet by sending a SYN-ACK (synchronize-acknowledge) packet back. This packet contains the server's own initial sequence number.
**Step 3: ACK**
    The client sends an ACK (acknowledge) packet back to the server, acknowledging the server's SYN-ACK packet. This completes the handshake, and the connection is established.

![[ThreeWayHandshake.png]]

# steps for ending
When you want to stop communicating you use the **Four-Way Handshake** a slightly more complicated process 

**Step 1: FIN from Client to Server**
	The client, which decides to end the communication, sends a FIN (finish) packet to the server. This indicates that the client has finished sending data, but can still receive data from the server.
    The client then enters a FIN_WAIT_1 state.


**Step 2: ACK from Server to Client**
	The server acknowledges the FIN packet from the client by sending an ACK (acknowledge) packet back.
    The client, upon receiving this ACK, moves to the FIN_WAIT_2 state, where it waits for the server to finish sending its data.


**Step 3: FIN from Server to Client**
	Once the server is ready to terminate the connection, it sends a FIN packet to the client.
    The server then enters the LAST_ACK state, waiting for the final acknowledgment from the client.


**Step 4: ACK from Client to Server**
    The client sends an ACK in response to the server's FIN packet.
    After sending this ACK, the client enters the TIME_WAIT state. This state is maintained for a period long enough to ensure that the ACK packet has been received by the server.



Once the server receives the final ACK from the client, it closes the connection.
The client waits for a designated timeout period in the TIME_WAIT state before fully closing the connection. This is to ensure that the final ACK was indeed received by the server and to handle any delayed packets that are still in the network.

![[FourWayHandshake.png]]