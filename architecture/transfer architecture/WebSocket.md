# Theory

WebSockets provide a **persistent**, **full-duplex** communication channel over a single **TCP** connection, facilitating real-time data exchange between a client and a server. Unlike traditional [[HTTP]] requests that are stateless and closed after a response is sent, WebSockets keep the connection open, allowing for ongoing communication with minimal overhead. This is particularly useful for real-time applications such as chat applications, live feeds, and interactive games.

Compared to HTTP, WebSockets offer lower overhead due to persistent connections and binary framing, reducing latency and server load. By design, the WebSocket protocol handshake **uses [[HTTP]]** so WebSockets can be utilized in existing HTTP servers and other HTTP-based technologies. But, **once** the WebSocket **handshake is finished**, only the WebSocket protocol is used, **not HTTP** anymore.

## Usecases

WebSockets are used in scenarios where real-time bidirectional communication is essential. They provide a **transport** layer for messages to be exchanged between [[web browser]] (or between a browser and a server) with lower latency compared to polling or long-polling HTTP requests.

The most notable examples are:
(this are not all of the use cases, but as new [[Communication]] methods are created they take the job that WebSockets could also do )
### Chat

For one-on-one chats, WebSockets facilitate real-time message exchange, ensuring that messages are **delivered instantly** as they are sent, without the need for the recipient to refresh their browser or wait for a polling interval.

### Chat Rooms

WebSockets can efficiently manage **multi-user** environments like chat rooms, But this is not a native property of WebSockets. You need to implement it yourself or use a library such as Socket.IO, where you can leverage room functionality to broadcast messages to all participants in a chat room without sending messages individually. To do this you

- create a **good** room implementation like **Socket.IO Rooms** That utilizes maps to manage connections and rooms efficiently there are 2 maps. The main map with all of the sockets and a secondary with all the rooms and what sockets are inside of it. Reducing the need to iterate over every connection for broadcast operations.

- When scaling is critical, integrating a **[[pub/sub]]** model can address scalability and reliability concerns by distributing messages through topics (each representing a chat room), improving performance as the number of participants grows. You can connect directly to the [[message broker]] avoiding the WebSockets if you have low amount of connections (<10k). If you have more, you should have maintain the WebSockets on your [[server]] and it manages the connection to the broker.

## Problems

### [[HOL Blocking]] (Head-of-Line)

WebSockets can suffer from HOL blocking, where a slow or large message can delay the delivery of all subsequent messages in the queue. This is inherent to any TCP-based communication but can be mitigated by message chunking or using separate connections for high-priority messages.

### Browser Limitations

- [[web browser]]s may automatically close WebSocket connections after a period of inactivity. Implementing heartbeat messages (ping/pong frames) can keep the connection alive.

- Mobile apps will close the WebSocket if they are closed. So any app that uses them (like WhatsApp) will to implement complex systems (Google Cloud Messaging)
### scaling
- There is **limited** horizontal **scaling** with WebSockets as they are stateful connections, You would need to have a cache storage to scale it. This can make your application vulnerable  

-  Compared to simpler HTTP requests, WebSockets introduce **additional complexity** in managing connections, handling messages, and handling potential scalability challenges. Careful design and implementation are crucial for efficiently handling large numbers of connections.
### security
- WebSockets require careful security measures to prevent unauthorized access, data breaches, and malicious attacks. Implementing authentication, authorization, and encryption mechanisms is essential.
## Alternatives
- The main ones are **long polling**, **Webhooks** and mostly Server-Sent Events:
	- For applications requiring only one-way communication from server to client, **Server-Sent Events** (SSE) might be a more suitable and efficient choice. SSE maintains an open connection for pushing updates from the server to the client but does not support client-to-server messages.
- Once again. Remember that there are other [[Communication]] methods like WebTransport and WebRTC that can do the same jobs as sockets

# Practice

```js
const socket = new WebSocket('ws://your-server-url');
socket.onopen = () => {
  console.log('WebSocket connection opened');
};
socket.onmessage = (event) => {
  console.log('Received message:', event.data);
};
socket.onerror = (error) => {
  console.error('WebSocket error:', error);
};
socket.onclose = () => {
  console.log('WebSocket connection closed');
};
socket.send('Hello from the client!');
```
