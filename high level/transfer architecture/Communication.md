how do things communicate through a [[network]], they normally exchange a document, or some format (JSON file, HTTP header ...)  mainly 2 distinctions, syncronous and asyncronous, 
# based on synchrony 
### syncronous 
Synchronous communication is a method where the sender **waits** for the receiver to process the message and return a response. This communication type is common in various application programming interfaces (APIs), particularly those using HTTP protocol.
#### Key Characteristics
- The sender blocks and waits for the receiver to process and respond.
- Utilizes protocols like [[REST]], [[RPC#gRPC||gRPC]], and [[GraphQL]].
- Predominantly used in [[API]]s over [[HTTP]]. The sender must know the receiver's specific address or endpoint.
#### Limitations

- **Lack of Resilience**: If one part of the communication chain fails, it can lead to a breakdown of the entire process.
- **Inefficiency**: Waiting for responses can lead to increased latency and reduced overall system efficiency.

### asyncronous
In asynchronous communication, the sender does not wait for an immediate response from the receiver. This method is more **flexible** and often more resilient to failures.
#### Key Characteristics
- The sender sends a message and continues its process without waiting for a response.
- Commonly uses protocols like [[AMQP]] and [[NATS]].
- Typically implemented in conjunction with a [[Message Broker]]. The sender doesn't need to know the specific consumer; it sends messages to the broker, which then routes them appropriately.
#### Advantages
- **Resilience**: More robust against failures. If a server is down, it does not immediately disrupt the communication process.
- **Efficiency**: Enhances overall system efficiency by eliminating the need for response waiting.

# Some Communication Methods

####  [[WebSocket]]
- **Persistent, Full-Duplex Communication**. Allows for real-time, two-way communication between client and server.
- Ideal for applications requiring **continuous** data flow, like chat applications or live updates.
- build over [[http]]

#### [[RPC#gRPC||gRPC]] (Google Remote Procedure Call)
- **Modern RPC Framework**, Utilizes HTTP/2, Protocol Buffers, and offers features like authentication and load balancing.
- Suitable for connecting microservices or backend services with clients.

#### Server-Sent Events (SSE)
- Creates a **Unidirectional Communication** from [[server]] to client, real-time updates over HTTP.
- Ideal for scenarios where clients require real-time updates from the server, like live notifications. But don't need to speak to the server at all

#### Service Mesh
- **Infrastructure Layer** for **Microservices** that provides enhanced control and reliability in microservices communication.
- Manages how different parts of an application share data, ideal for complex microservice architectures.
- Creates a [[Sidecar]] with [[proxy]]s and [[microservices]] containers to talk to each other  

#### MQTT (Message Queuing Telemetry Transport)
- **Lightweight Messaging Protocol**. Designed for low-bandwidth, high-latency, or unreliable networks.
- Extensively used in IoT for efficient device-to-device communication.
### coAP (Constrained Application Protocol)
- designed for resource-constrained devices and networks. 
- It is a lightweight protocol similar to HTTP but optimized for constrained environments such as **IoT** (Internet of Things) devices.

### real life
The world of server communication isn't limited to these two distinct modes. In reality, hybrid approaches often blend synchronous and asynchronous communication to achieve specific goals. For instance, a [[server]] might use synchronous calls with rest for critical transactions while leveraging AMQP queues for background processing and a server-sent event to respond when is done