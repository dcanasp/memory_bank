# Theory

REST, which stands for Representational State Transfer, is an **architectural style** commonly used in the design of networked applications. RESTful architectures are widely adopted for building scalable and maintainable web services.

Mostly is used over [[HTTP]] or [[HTTPS]] but in reallity rest is just a pattern, so it's not tied to any protocol and can be used on basically any of the [[Communication]] methods

## Key Principles

REST is based on several key principles that guide its design and implementation:

- **Statelessness**. Each request from a client to a server must contain all the information needed to understand and fulfill the request. The server should not store any information about the client's state between requests.
    
- Using a **Client-Server Architecture**. The client and server are separate entities that communicate over a [[network]]. This separation allows for improved scalability and flexibility in the system.
    
- RESTful services should have a consistent and **uniform interface**. This principle is achieved through the following sub-principles:
    
    - **Resource Identification:** Resources (e.g., data or services) are identified by URIs.
    - **Resource Manipulation through Representations:** Resources can be manipulated using representations (e.g., JSON or XML).
    - **Self-Descriptive Messages:** Each message sent from the server to the client should include enough information to describe how the client should process the response.

## Key Components

RESTful systems typically consist of the following key components:

- **Resources**, These are the key abstractions in a RESTful system. Resources can represent entities like data objects or services.
    
- **URI (Uniform Resource Identifier)** Each resource is identified by a unique URI, which is used to access and manipulate the resource.
    
- **HTTP Methods:** RESTful services use standard [[HTTP]] methods for interaction with resources.
    
- **Representation** Resources are represented in a format such as JSON or XML. Clients interact with resources by exchanging these representations.
    

## Advantages of REST

- **Simplicity** and making it easy to understand and implement.
    
- **Scalability** as the stateless nature of RESTful services allows for easy scalability by adding more servers to the system.
    
- **Interoperability**. REST can be easily integrated with other web services, and it is platform-independent.
    
- **Flexibility**. The uniform interface allows for flexibility in the design and evolution of a system.
# practice

You always use a framework/library that helps you with creating this services. Some of them are [[Backend app#Express setup|Express]],[[Fastify]] or nest for [[typescript]] and mux or gin for [[Go]] 
