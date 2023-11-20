it creates a virtual machine 

On [[windows]] by default `host.docker.internal` is defined, but on [[linux]] it does NOT exist by default, you have to add this flag `--add-host=host.docker.internal:host-gateway` (or putting the ip if it's a http request)

#todo 