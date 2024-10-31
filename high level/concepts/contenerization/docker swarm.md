#todo

... what it is ...

it created to scale
# Theory
## nodes
nodes connect to each other
## Networks
the default network should be overlay, 
### ingress
it's global for all you application
### host
only on that node it's available
## volumes
if you need a way for multiple nodes to share information from a volume (for example writing on disk some file that all will consume) you use a [[NFS]] volume 

## namespaces
as a docker swarm project is composed of multiple services they will be deployed inside a namespace, this is like a common parent, this concept is never used but is relevant in [[Kubernetes]], i just wanted to mention it's also present here 
## services
.....
if you restart a service using `docker restart <container-id>` it won't be picked up by the swarm and swarm will create a new container

# Practice
to be able to use swarm:
`docker swarm init`
`docker stack deploy -c .\file.yaml demo`

## common errors
### ports
quoting the official documentation:

>Open protocols and ports between the hosts
   The following ports must be available. On some systems, these ports are open by default.

>Port *2377* TCP for communication with and between manager nodes
  
>Port *7946* TCP/UDP for overlay network node discovery

> Port *4789* UDP (configurable) for overlay network traffic

as I've encountered it, on [[linux]] (DinD) those ports are open by default, but on [[windows]] they are not, and you have to change your [[firewall]] rules for the swarm to work. But it won't tell you what is wrong

### docker compose
swarm has a different purpose than [[docker#Docker Compose|Docker compose]], therefore a docker compose file won't always works, as swarm is meant to scale.
Things like `mem_limit`, health checks, setting container names, setting *aliases*, the bridge (and default) network driver (it needs overlay), among others. don't work, you have to remove it.

### old files
if you had already builded the application as a docker compose it will use those builds, and wont' chengk changes
