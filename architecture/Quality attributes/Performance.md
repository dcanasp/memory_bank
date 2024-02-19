A core feature of [[system architecture]]. And the most asked for quality attribute. Performance is not only algorithm speed[^1]: . It includes disk operations, connection pools, communication bottle necks. The architect is the one who has to manage all of those things, You can have the best algorithm and still have the worse performance. 

[^1]: In terms of system architecture as i mentioned there are a lot of important parts of performance. But algorithmic and data structure performance is also a great part. Also, understanding the technologies (including [[hardware]]) that you use and optimizing can be the biggest part of achieving high performance

But mainly there are two problems that hinder performance[^1]:. **Resource management**, how to manage the resources i currently have (things like catching or queues) and **controlling resources demands** (not allowing race conditions, limiting the amount of events at a time).

This note does not focus on Scalability. That is not the only solution for performance, this note takes a look of what to do when you can't handle so much load, there are still great options that don't include scaling vertically or horizontally.

# problem

You have to understand that as with everything software there is a trade-off. In this case the main 3 players are **Time**, **Space** and [[network]] [[bandwidth]]. When speaking of time, this is [[CPU]] speed, the time can be high but the [[CPU]] usage can be low. This players are also related to cost, But you have to decide how to solve a performance problem based on those 3 conditions

# Tactics
## Control Resource Demand
One way to increase performance is to carefully manage the demand for resources. This can be done by reducing the number of events processed or by limiting the rate at which the system responds to events.

The following are very similar
- **Manage event arrival**: Normally you would want to manage as many request as possible, but this is a handicap some times (your system is not designed for so many things). You can put in place a service level agreement (**SLA**) that specifies the **maximum** event **arrival rate** that you are willing to support. If they send more, the response is not guaranteed
- **Limit event response**: After setting the max arrival rate, limit them. You have to decide if you are going to *queue* the events, *log* them, or *loose* them; Also, will you notify the users about this decision?
- **Prioritize events**: Some event are live threatening. Do something, implement a priority scale and always manage those first
- **Co-locate communicating resources**: some times reaching another network and changing the context is more cost full than the logic itself. You can *co-locate* component on the same [[network]] or processor to alleviate this costs
- **Periodic cleaning**: any system that uses virtual memory like a [[hashmap]] can become clocked and create a knot on the system, clean them once in a while
- **Bound execution times**: Preferably don't leave thing on an infinite waiting time. You can create a race timeout so that you don't wait for ever
## Manage Resources

- **Increase resources**: as the name implies, but not always the best solution
- **Multiple copies** of *computations*: Same as increasing resources but now with a [[Load balancer]] and added problems.  
- **Multiple copies** of *data*: Some times the problem is data retrieval, for this cases caching is king, can be done with a [[CDN]] or some tool like [[redis]]
- **Introduce concurrency**: Whenever time is a problem, but [[CPU]] usage is not this is a great option
- **Schedule resources**: Not all the time should your [[server]] run at max capacity, you can schedule more network, processors, data replication for those moments
# Patters

## Service mesh 
Used heavely on [[microservices]]. It's similar to a [[Sidecar]] But instead of being alone, it allows multiple services to run along side each microservice. **Co-locating** the components so that it works better.

This mesh allow for extra customizability. They are able to be customizable based on the context, allowing somethings like [[Deployability#Patterns|Special kinds of testing]]
## Load balancer
[[Load balancer]]. But in short, with this pattern you can have as many [[server]]s as you need
## Throttling

It is used to **limit access** to some important resource or service. In this pattern, there is typically an **intermediary**(a throttler) that monitors requests to the service and determines whether an incoming request can be serviced. This can be added to a load balancer to create some special algorithms 
## Map-Reduce

This is a very complex pattern and algorithm that can be useful if **data processing** is the **bottleneck**. Firstly it sends the data to a server where to process (Map and reduce) start. Extremely large, unsorted data sets can be efficiently analyzed through the exploitation of parallelism. 

A failure of any instance has only a small impact on the processing, since map-reduce typically breaks large input datasets into many smaller ones for processing, allocating each to its own instance. 