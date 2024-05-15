
... what it is ...

it created to scale

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

as I've encountered it, on [[linux]] (DinD) those ports are open by default, but on [[windows]] they are not, and you have to change your [[firewall]] rules

### docker compose
swarm has a different purpose than [[docker#Docker Compose|Docker compose]], therefore a docker compose file won't always works, as swarm is meant to scale.
Things like `mem_limit`, health checks, setting container names, setting *aliases*, the bridge (and default) network driver (it needs overlay), among others. don't work, you have to remove it.

### old files
if you had already builded the application as a docker compose it will use those builds, and wont' chengk changes
