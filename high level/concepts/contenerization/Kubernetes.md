# Theory
## What is it?
A container orchester. Not container creation, it should never be compared with [[docker]], nor docker-compose. It's real alternative is docker swarm, a smaller and less capable tool, swarm does not include autoscailng, monitoring etc...

Kubernetes relies heavily on multiple machines and the auto scaling of this, for this reasons it needs a cloud provider to use it effectively, if you want only local stuff use minikube

## Why and when to use is

When you absolutelly want high [[Availability]]. And want the servers to autoscale, manage [[network]] and anything in beetween by themselfs

When you want to automate how my containers ([[docker]]) will scale, will get balanced and may other things. It's automating infrastructure 

Kubernetes will always be alive, always checking stuff allways ready to scale and change at runtime

## what it offers
- **Auto scalling**
- **load balancing**
- **Storage orchestration**
- **Automated rollouts and rollbacks** You define the state that you want and kubernetes stops containers and puts new ones seamlessly
- **efficient and automatic resource management**
- **Self-healing** 
- **Secret and configuration management**
- **Batch execution**
- **Horizontal scaling**
- **IPv4/IPv6 dual-stack**

## glossary

- **Cluster**: System deployed on kubernetes
- **Control plane**: The brain of the operation, exposes a [[API]] to manage internal and external requests
- **Nodes**: worker machines ([[server]])
- **Kublet**: What each machine runs, it communicates with the **control plane**
- **Pod**: Smallest deployable unit. The container that you are running. each pod gets it's own [[IP]] address (and if restarted it changes)
- **Service**: permanent [[IP]] for a pod, it's the name of what i will run, the communication between pods
	- **internal service**: only accessible from within (a [[mid level/databases/Database|Database]])
	- **external service**: the one that can speak with the world (an [[API]])
- **ingress**: The entry point for your application, it connects to a external service, (it's like a [[proxy]])
- **ConfigMap**: A file with the connection data, ip's, urls, and those things. THIS IS NOT SECURE.
- **secret**: another configMap but this one is **secure**, you save the password, certificates here (environmental variables)
- **Volume**: the way to have data permanence, it connects to a permanent storage
- **Deployment** the process where you say how many pods and services you want, and k8s manages all

## data permanence / storage
Kubernetes does **NOT** manage any **data permanence**. If you have your database in a pod. And it has to restarted or changed, the data would be lost. For this you have to use a **Volume**. It attaches a fiscal storage to your pod. This can be a local storage or a remote storage 
## Deployment (scaling / availability)
to avoid down time, you create multiple replicas this is done via deployments, you don't interact with pods, you just say how many nodes you want and it creates them and manages the load balancer.
[[mid level/databases/Database]] can't be scaled using deployments as you would get inconsistent data and errors, for that you use the 
**Stateful set** (this is not easy). It's better to maintain you databases outside the nodes

## Basic architecture
You have a cluster with multiple nodes (worker nodes) and multiple master nodes. The master nodes will have less computacional power, and there will be less of them compared to worker nodes 

- on each node (worker nodes) there are always 3 process running, the **container runtime** where the aplication lives, **Kublet** and and the **Kube proxy** an inteligent request handler

- on each master node there are always 4 process running 
	- **API server** like a cluster [[ApiGateway]] it manages autentication, querys, request. These are load balanced between master nodes
	- **Scheduler** the one who decides who to send that request, to what node, it just decides who to send it to. 
	- **Controller manager** detects errors, and state changes, it calls the scheduler once again, 
	- **ETCD** the database, it's like the brain where you store all the important parts, like what nodes are running, the health of this etc. These are distributed between master nodes
- 
## namespaces:

a namespace is a section inside of a **cluster**, like a virtual cluster. You should use them to keep the cluster clean, separating the stuff in a logical order (a namespace for db, one for the ingress...). Also do it when you want to reuse components, a **logging** component will be used multiple times in your application.

Another good use case is to **limit access** and resources, for example you create a namespace that would delete all of the servers, data etc, you give access to that namespace **only** to the pod that actually should do it, so any other pod wouldn't be able to access the delete namespace, even if you are being attacked via a [[some attacks#Cross-Site Scripting (XSS)|injection or XSS attack]]. In the other case, you want your logger to only use x amount of [[RAM]] or [[Physical memory]], you give only that service a limit with a namespace

there are some default ones

- *default*. if you don't create a namespace. your components are done here 
- *kube-node-lease*. It has the information of each node, it's state and how they are doing
- *kube-public*. publicly accessible data, a configmap with the cluster information
- *kube-system*. NOT FOR YOUR USE, system process from master and kubectl

### sharing
Each namespace must have it's own configmaps and secrets, they **can not** share them, even if they are the same. But the services can be access from other namespacese.

Also some components cannot be separeted in a namespace, these are volumes and nodes, you can't isolate them


## ingress
This is not an external service, it's not just an [[ip]] to your pod. This is a way to give a name to the whole app or namespace

The ingress works like a proxy, you create some rules and redirect to the service you want

you also need an implementation for the ingress, a *ingress controller*, it evaluates the ingress rules and manages all redirections.

This ingress controller has to be downloaded separately, one it's nginx ingress controller; normally your kubernetes implementation has one, *minikube* has the nginx one. 
## under the hood

has multiple replica set's ready, so if it needs to switch them, or add them it's instantaneous the availability
uses a **etcd**, [[mid level/databases/Database#key-value|Key-value]] database 

## minikube / kind

Whenever you want to test a feature locally, or just develop on local machine first you use minikube, this runs a virtualBox (or docker) with the master and worker process on the same machine. It's a 1 node k8s cluster

# Practice
## kubectl
After following the [install guide](https://kubernetes.io/releases/download/) you end up with `kubectl` the command line tool for kubernetes (if on windows use powershell not cmd). It manages any kubernetes cluster

### commands

#### get data
- `kubectl get namespaces`
- `kubectl get deployment` shows deployments
- `kubectl get nodes` returns the nodes running
- `kubectl get services`
- `kubectl get pod` returns a list of **pods**
- `kubectl get replicaset`
#### deployments
You never create pods or replicasets. You just create deployments and it manages the details.
- `kubectl create deployment [deployment name] --image=[imageName]` creating a deployment based on a docker image (*Names* must be *lowercase*)
- `kubectl apply -f [filepath.yaml]` to create a new deployment based on a .yaml file (or *editing* if already exist you can use `create` instead of `apply` if you want only creating)
Creating a deployment will create a configuration file you can edit it and it opens a text editor
- `kubectl edit deployment [deployment name]`
when you edit a configuration file for a running deployment, it will instantly create a new (pod, replicaset and services) and delete the outdated ones

#### logging / debbuging
first you create the deployment then
- `kubectl logs [depl name]`
- `kubectl describe pod [pod name]`
If you want to access the machines that you run on k8s you can
- `kubectl exec -it [pod name] -- /bin/bash` now you are on the console. That is assuming that the containers are using [[Linux]] (they should)

#### deleting
Remember that you only interact with deployments, not anything bellow, so if you delete the deployment all bellow get's deleted as well
- `kubectl delte deployment [deployment name]`

## configuration files
This is what you actually create, you **never** create components in the terminal.
### parts
All configuration files must have 3 parts And these are written in .yaml. These configuration files will have a *kind* attribute, this can be the deployment, a part of the deployment like a service, pod, secret. It's very important the order of this config file. If a deployment references a secret it has to be created before
#### metadata
the metadata of the file, the main structure is
```yaml
apiVersion:
kind: (Deployment,Pod,Service...)
metadata:
  name: 
  labels:
    app: (important name)
```
#### specification
this is called `spec` and is the details of everything

Example for **deployment** config
```yaml
spec:
  replicas: 
  selector:
    matchLabels:
      app: (the one on metadada)
  template:
    metadata:
      labels:
        app: (the one on metadata)
    spec:
      containers:
        - name: 
          image: (docker image)
          env:
            - name: SOME_ENV
              value: $SOME_ENV
          ports:
            - containerPort: 8080
```
#### status

This is **NOT** written by the user, it's auto generated by k8s, if the status does not match the specification it starts the self healing and the repairment process. It will do it automatically .The etcd is what holds the current status. But you can access it if you do a `kubectl get [component]`

### examples
#### deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80
```
#### service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: example-service
spec:
  selector:
    app: example
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```
#### pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  labels:
    app: example
spec:
  containers:
    - name: example-container
      image: nginx:latest
      ports:
        - containerPort: 80
```
#### secret
this will be where you store your passwords, remember to always store the secret values in **base64**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque
data:
  mongo-root-username: ZGFjYXM1
  mongo-root-password: Q29sZWdpbzU=
```
#### namespacces:

you can also create them in command line, but it's better on file
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
  namespace: serverName
data:
  database_url: mongodb-service.database
```
in this examples there are two namespaces, a *mongodb-service* and *serverName*, the serverName is connecting to the mongodb-service

> [!important]
> to access components inside of a namespace on kubectl you actually have to use `-n [namespace name]`
> 
> so for example, `kubectl get deployment -n mongodn-service`
> 
> you can use *kubens* or *kubectx* to manage this (these are tools you need to download)

#### ingress
you have to create ingress rules, what and when to allow things
```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: dashboard-ingress
  namespace: kubernetes-dashboard
spec:
  rules:
  - host: dashboard.com
    http:
      paths:
      - backend:
          serviceName: kubernetes-dashboard
          servicePort: 8080
```
the host has to be a valid domain name, and it has to be the address to your kubernetes access point. To make the access point reachable you edit the etcd/hosts file

finally here on ingress you put the [[SSL]] certificates
## minikube 
A tool to create a setup for kubernetes **Locally**, (setting up on virtualBox is harder. Use `minikube start --driver=docker`). To install follow the guide [minikube install](https://minikube.sigs.k8s.io/docs/start/). Don't forget to start the docker minikube container

### commands
- `minikube start --driver=docker` To *start* a cluster
- `minikube dashboard` a dashboard with all the information about your cluster
- `minikube service mongo-express-service` 
- `minikube addons enable ingress` to start the in

>[!important]
>want to create a external ip adress?
>you have to run `minikube service [service name]`

