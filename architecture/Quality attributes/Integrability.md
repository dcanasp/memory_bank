A core feature of [[system architecture]]. The problem is having a system *S* and multiple components *C* that don't quite fit together. This mainly because they have to agree on what elements they share,  and what these shared values will mean, Taking into account that these might be mutable and live on different architectures and [[network]]s

# Tactics
## limit dependencies
- **Encapsulate**: it's the most important part to develop an integrable system, It creates an explicit interface to an element and ensures that all access to the element passes through this interface.
- **Intermediary**: Instead of talking directly, an intermediary steps in and makes communication between services, decoupling it. An example of an Intermediary is a  [[Message Broker]] In a [[pub/sub]] environment.
## adapt
- **Discover**: You should never call an external [[API]] or service with an static [[IP]]. Use a discover instead, It's a map where you find the services only with the name, this decouples your services. An example of this is a [[DNS]]
- **Configure Behavior**: Don't marry with a configuration, the settings should be changeable with a simple restart with other flags
## coordinate
- **Orchestrate**: Instead of relying on every *C* to talk to each other, have a *control plane* that will take care of that, it will talk with each *C* and all have to report to it. The components remain unaware of each other. This is the base of [[Kubernetes]]
- **Manage Resources**: Don't allow the *C* to access shared resources directly, Make them request the resources from a **resource manager**, This allows you to enforce what ever policies you want (x process must have more resources). This is what an [[OS]] does

# Patterns

- **Wrappers**: Make a component *C* that only you can access, and any one who needs that component *C* will talk to you. You can translate for *C*, add some values that it might need but you don't get
- **Bridges**: designed to connect components by translating "requires" assumptions of one component into "provides" assumptions of another, without being tied to any specific component. A bridge is not always needed, only on specific problems
- **Mediator**: Mediators combine aspects of both bridges and wrappers but introduce a critical feature: a planning function that allows for runtime determination of the translation. This dynamic capability means that mediators can adapt their translation strategy based on the current state of the system or the specific interactions taking place.

## Dynamic Discovery
Enable the discovery of service providers at runtime. This way Even if you change components you don't have to restart everything
## SOA

The Service-Oriented Architecture Pattern. When you have to many services and to many providers, in this pattern you have a service broker, This broker is like a phonebook. The services ask for a specific service, the broker says where is it, And then they talk to each other (the two services). In other words SOAs provide reusable components that are assumed to be heterogeneous and managed by distinct organizations. 

