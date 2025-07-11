Docker is a set of platform-as-a-service (PaaS) products that use [[OS]]-level virtualization to package applications and their dependencies into lightweight, portable **containers**. These containers can run consistently across different environments, ensuring that the application behaves the same way regardless of the underlying infrastructure.
# Theory

## Why/Use Cases

- **Consistent Development Environments** 
- **Isolation** 
- **Portability**
- **Efficient Resource Utilization** specially compared to virtual machines
- **DevOps** Easier to do DevOps if the architecture is a non factor

## Basics

### Images

Docker images are lightweight, standalone, read-only software templates that include give you the full blue prints of the system you want to build. Images are used to create Docker containers.

Docker images are composed of multiple layers, each layer representing a set of changes from the previous layer. This layered architecture allows for efficient sharing and **caching** of image layers. This layers are stored on the *storage drivers* In most cases when building from a image already created all if not most would be cached and done instantly. Each layer is identified with a unique SHA-256 [[hash]]

There are mainly two types of images. The *parent* images and the *base* images. The parent images are the ones we commonly use, These are the `From alpine` or any other image. The base images are `FROM scratch` and you create all for them.
### Containers

Docker containers are lightweight, standalone, executable packages that contain everything needed to run an application, including the code, runtime, system tools, system libraries, and settings. Containers are created from Docker images and run in an isolated environment, sharing the host's operating system kernel while remaining **isolated** from other processes on the host. 

When you create a new container you add a new layer to the image. This is called the *container layer*. While the image layers are read only, the container one is Read-Write
![[DockerContainerLayers.png]]
Containers by definition are stateless on delete. What this means is that after you clear it any data you had is lost. They only store the information while they are alive. There are a few state they can be in
Created, Running, Deleted, Restarting, Exited, Paused, Dead.

### Volumes

Docker volumes are persistent storage areas that can be mounted into containers. They allow data to be shared and persisted between containers and the host system. Volumes are particularly useful for storing data that needs to persist beyond the lifecycle of a container, such as databases or logs. These will be explain more in the [[docker#Data persistence]|Data persistence]] section
### Networks

Docker's networking allows containers to communicate with each other and with the outside world. Docker supports different types of [[network]]s, including bridge, host, overlay, and macvlan networks. These networks enable containers to communicate securely and efficiently within the same host or across multiple hosts.
### Secrets

Docker secrets is a feature that helps manage sensitive data such as passwords, tokens, and ssh keys. Using Docker secrets, sensitive data is encrypted during transit and at rest, providing a safer way to use confidential data.
### Docker Compose

Docker Compose is a tool that allows you to define and run multi-container Docker applications. It uses a YAML file to specify the services, networks, volumes, and other configurations for the application. Docker Compose simplifies the process of running and managing complex applications that consist of multiple containers.

### Docker Swarm

[[Docker Swarm]] is a clustering and scheduling tool for Docker containers. It allows you to create and manage a cluster of Docker nodes, making it easier to deploy and scale applications across multiple hosts. This is similar to [[Kubernetes]] as an orchester 

### Docker Registry

A Docker Registry is a storage and **distribution** system for **Docker images**. It allows you to push and pull Docker images to and from a central location, making it easier to share and distribute images across different environments or teams. *Docker Hub* is a public Docker Registry hosted by Docker, but you can also set up private registries for your organization.

## cli options
...
## Dockerfile
...
### tags
...
## docker compose
...
## Data persistence
![[DockerPersistence.png]]
### volumes
### mount binds
#### big problem
they need more permises and some times fail
### tmpf

## uses
## runtime
runc, changable
## common errors

### Mount binds
A lot of times Mount binds data persistence wont be able to create files or delete them, this is because of it's dependence on the host machine, this is something that does not happen on volumes
### windows vs linux
On [[windows]] by default `host.docker.internal` is defined, but on [[Linux]] it does NOT exist by default, you have to add this flag `--add-host=host.docker.internal:host-gateway` (or putting the ip if it's a http request)
### podman
when having [[podman]] on the same computer you get some problems as they use some shared components. The fix that worked for me is stopping the task `winssh-proxy.exe` (That is located in the redhad/podman program files folder). Seems that (sometimes) can't run podman and docker at the same time

# Practice
#todo
## Dockerfile
... 
## docker compose
...
### Health
healthcheck:   
      test: ["CMD-SHELL", "rabbitmqctl status"]
      interval: 30s
      timeout: 5s
      retries: 4
      start_period: 2m

  in this case i will execute the command `rabbitmqctl status` on the CMD-SHELL every 30 seconds and it must give me an answer before 5 seconds pass. If not it will retry 4 times. The *start_period* means that for the first 2 minutes the failed attemps will **NOT** decrese the retry amount, therefore the server will still be making health checks every 30 second, But only at the second minute they will affect the retry amount



docker compose pull

#todo 
podman push northamerica-northeast1-docker.pkg.dev/mystic-tempo-416400/leare/apigateway-leare-gateway:gcp northamerica-northeast1-docker.pkg.dev/mystic-tempo-416400/leare

  
  

gcloud auth print-access-token | podman login -u oauth2accesstoken --password-stdin us.gcr.io

  
  

gcloud auth configure-docker

gcloud auth configure-docker northamerica-northeast1-docker.pkg.dev