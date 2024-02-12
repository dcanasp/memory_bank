Software architecture is the set of structures needed to reason about the system. These structures comprise software elements, relations among them, and
properties of both.

Architecture is in every software system, not all are good, but there is **no perfect** one. If it works and fits your necessities it's a good one

# Architectural structures
a way to organize what the elements and relations can be
## Component-and-connector structures
focuses on the way the **elements interact** with each other at **runtime** to carry out the system’s functions. These focus on those *Components* (services, clients, [[server]], any element) and *Connectors* (ways of [[Communication]])

examples:
- service structures: the way to communicate between different nodes, they talk to the service
- **concurrency** structures: it allows to map and structure possible parallelism


## Module structures
show how a system is **structured** as a set of code or data units that have to be constructed or procured. Modules are assigned specific computational responsibilities and are the basis of work assignments for programming teams. These can be *classes*, *packages*...

Examples:
- Decomposition structure
- Uses structure
![[structureModules.png]]

## Allocation structures
establish the mapping from software structures to the system’s non-software structures, such as its **organization**, or its development, test, and execution **environments**, include *directories*, [[OS]], [[computer]] parts

examples
- **Deployment** structure
![[structuresDeployment.png]]
- implementation structures
- work assignment structures



# How to architect

## problem scope

## define architecture style


# Requirements
These are the Non-functional requirements (NFRs) or Quality attributes. Even though they are non functional they are as **important** as the functional ones. They are defined on the ISO/IEC 25010 

A good mnemotechnic to remember this is *PASSME* ([[performance]], [[availability]], scalability, [[security]], maintainability, extensibility)

in each article i explain this ones in detail, what they are, their patterns and tactics. But before that let's define some common ground.

These NFR have 6 parts
## parts

| scenarios | description | Posible values |
| ---- | ---- | ---- |
| **stimulus** | A new event on the project | Request sent |
| stimulus **source** | Who did it, was it a human? was it a trusted author? | User clicked web |
| **Response** | How will i act after the stimulus | Serve a response  |
| Response **measure** | There is a measure for any response | latency, encryption |
| **Environment** | Where am i running it, is it production, testing, what machine was it? | Production [[server]] |
| **Artifact** | a collection of systems, the whole system, or one or more pieces of the system | the code that runs |

## NFR

## [[Availability]]
## [[deployability]]
## [[integrability]]
## [[modifiability]]
## [[performance]]
## [[safety]]
## [[security]]
## [[testability]]
## [[usability]]