#todo

https://github.com/containers/podman-compose

Podman compose are run as containers, you can simply tell it (after running the container) to create the pod. And the container will use the pod

## common errors
### docker
when having [[docker]] on the same computer you get some problems as they use some shared components. It seems that (sometimes) you can't run both at the same time. 

### docker2
reffering to this error:
```bash
Cannot connect to Podman. Please verify your connection to the Linux system using `podman system connection list`, or try `podman machine init` and `podman machine start` to manage a new Linux VM
Error: unable to connect to Podman socket: failed to connect: ssh: handshake failed: read tcp 127.0.0.1:63192->127.0.0.1:53369: wsarecv: An existing connection was forcibly closed by the remote host.
```
docker is taking resources like last time. Oddly enough i got this error at a random time, i was actively using podman (had used docker hours before) and it just happened