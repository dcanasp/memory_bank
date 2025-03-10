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

firstly you define the users that are going to consume your product, how many of them? at what hours? what are the time concerns? what are the availability concerns? what are the security concerns? how much budged do we have? What does the user want?
## define architecture style
after answering all of the previous questions, start thinking on what architectural style suits your needs best, if it is a highly intensive program microservices might be the best, if availability is not a concern a monolith should suffice.
# Requirements
These are the Non-functional requirements (NFRs) or Quality attributes. Even though they are non functional they are as **important** as the functional ones. They are defined on the ISO/IEC 25010 

A good mnemotechnic to remember this is *PASSME* ([[Performance]], [[Availability]], scalability, [[architecture/Quality attributes/security]], maintainability, extensibility)

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
Here are the most common NFR. (Most of) These have a note of their own, Please check it to see what they are, the tactics and patterns

## [[Availability]]
## [[Deployability]]
## [[Integrability]]
## [[Modifiability]]
## [[Performance]]
## [[architecture/Quality attributes/security|security]]
## safety
A very important but sometimes overlook factor in system architecture is the safety of your code, specially when working with real world data. You have to be sure that you don't miss interpret important data from sensors, facial recognition tools or even [[AI]], Doing so could harm or put in harm's way some unsuspecting user.

This is a very specific problem, therefore if you face it, please research more about it.

- Patterns:
	- **Redundant sensors**: two sensors are one and one is none. Don't risk it
	- **Monitor-actuator**: Before doing something, quantify the expected output (roughly). If it fails something might be wrong
	- **Separated safety**: There are some parts that critical, have those audited as often as possible, the non critical can have their own server
## usability
>People ignore design that ignores people

If the system is not easily usable is a system meant to fail, usability entails; easing the **learning** and **using** the system, **Minimizing** the impact of **users mistakes**, adapting to the users need and Increasing the user satisfaction and feedback, letting them know they are doing the correct things.

Here is important to mention UI/UX. User experience is the main part of front end development, the application should be thought for the user.  

### Patterns
- **MVC**: model view controller it's an old pattern, but it separates the views and what the user uses, from the business logic, this makes the  system more usable