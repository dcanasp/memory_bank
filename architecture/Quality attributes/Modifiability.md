A core feature of [[system architecture]]. Some times modifiability is misunderstood, it's not just being changed easily, it has multiple names and parts, **Scalability**, **Variability**, **Portability**, **location** independence, Are all part of a modifiable system.

**Most of the cost** in software systems occurs **after** it has been **initially released**, if you want a modifiable system. You have to wonder what can change, what is the likelihood of change, when and who is going to do those changes, what is the cost of changing. Making a system modifiable comes with a cost, you have to ponder if you really need it. If the difficulty of making it modifiable outweighs the value of it, don't do it

is also important in systems that need to accommodate **peak loads**, such as online shopping during holiday seasons or sudden spikes in user activity due to viral events. Or changing some features for the holidays and returning to the original months later


What are the main problems with modifiability?

- **coupling**: Whenever you have multiple services that rely on each other or another component, making changes on those components mean that you also have to change the depending ones
- **cohesion**: The measure that modules only do a single task or related to them, they should not be doing infinite stuff
- **size** of **modules**: self explanatory, and normally a bigger size also has lower cohesion
- binding **time** of **modification**: am i able to take changes in latter stages of development?, if not cost will rise
# Scaling
Scaling is an escencial part of a modifiable system. There are mainly two types of scalability in modern systems
## Vertical scaling
Vertical Scaling is adding more resources to the [[server]] where you are running your code. These are more commonly [[CPU]] or [[RAM]]
## Horizontal scaling
Horizontal scaling is adding more [[server]]s to the existing pool of machines. these new machines will handle a part of the load that arrives usually using techniques as. [[Load balancer|load balancing]], sharding, partitioning, and distributed processing. 
# Tactics
## Increase Cohesion
- **Split module**: Each module should only do what they are required, No god classes[^1]: 
- **Redistribute responsibilities**: The common responsibilities should be on a single module, If it still the same thing, is shouldn't be separate 

[^1]: when a class does a little bit of everything, If that class fails all fails. They are created when there is a bad organization and structure of code 
## Reduce Coupling
- **Encapsulate** and **Intermediary**: ![[Integrability#limit dependencies]]
# Patterns

## Client-Server Pattern

Having a server that feeds and manages information that the (unknown) clients send, The clients can implement their own logic, therefore making the server a loosely coupled. This is the same logic that [[REST]] uses 	
## Plug-in (**Microkernel**) Pattern

You create a microkernel, it will manage some core functionality that you define, and allow the creation of plugins, these will connect to the microkernel and consume the core functionality.
## Layers Pattern

Having multiple layers that are unidirectional. The layer *C* will consume the public methods of layer *B*. This is an example of the N-tier pattern, Where you first go through a security layer, that relays you to the business layer, logic layer and finally database layer.
## Publish-Subscribe Pattern

A very common patter implemented with [[Message Broker]]s. You have a publisher, that send the messages, and some subscribers that get the messages of certain topics. You can change the publishers or the subscribers without changing any other parts

