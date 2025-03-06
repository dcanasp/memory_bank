#todo 

There are two types of virtualization,

bare metal hypervision (type 1)
and type 2
# Virtualization vs containerization


- **Virtualization** allows you to run multiple operating systems on a single [[hardware]]'s [[OS]] layer. Each VM has its own dedicated resources, and is isolated from the host system and other VMs. It's for heavyweight jobs  
- **Containerization**, on the other hand, involves packaging an application and its dependencies into a lightweight, portable container that **shares** the **host's** operating system **kernel**. Containers are more lightweight and efficient than VMs because they don't require a separate operating system for each instance. However, they provide a lower level of isolation compared to VMs. Docker is on this division
