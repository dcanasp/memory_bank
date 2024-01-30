A **Message Broker** is an intermediary [[program]] module that translates a message from the formal messaging protocol of the sender to the formal messaging protocol of the receiver. Message brokers allow for differing systems to communicate with each other. They play a crucial role in dealing with high loads and a variety of message types and targets in modern distributed systems and [[microservices]] architecture.

Thrives in scenarios where immediate feedback is not crucial, like sending notifications, processing large datasets, or handling background tasks. Its decoupled nature fosters a more resilient and scalable environment. a central part of [[Communication]]
### Key Concepts

- **Message Queuing**: Enables asynchronous communication between different parts of a system, where messages are stored in a queue until they can be processed.
- **Publish-Subscribe Model**: In this model, messages are published to a specific class or topic, and subscribers to that class or topic receive the messages.
- **Routing**: The process by which the message broker decides how and where to send messages based on specific rules and logic.

### Types of Message Brokers

- **Point-to-Point Brokers**: These brokers use queues where each message is consumed by a single consumer.
- **Publish-Subscribe Brokers**: These brokers use topics instead of queues. A single message can be received by multiple subscribers.
- **Comparison**: Point-to-Point is ideal for task distribution and balancing workloads, while Publish-Subscribe is suited for broadcasting messages to multiple subscribers.

### Popular Message Broker Technologies

- **[[RabbitMQ]]**: Open-source message broker that uses the Advanced Message Queuing Protocol ([[AMQP]]). Known for its reliability, flexibility, and support for multiple messaging protocols.
- **Apache Kafka**: A distributed streaming platform that goes beyond traditional pub/sub models to allow replaying of messages. It excels in high-throughput use cases like event streaming.
- **AWS SNS/SQS**: Amazon Simple Notification Service (SNS) is a pub/sub service, while Amazon Simple Queue Service (SQS) is a message queuing service. They provide scalability and flexibility for cloud-based applications.
- **Others**: ActiveMQ and ZeroMQ are other notable examples, each with unique features suitable for different scenarios.