# DevOps-Learning---Docker-Module
Docker notes and learning

Common interview question
---

***Containers vs VMs difference***

**VMs***
So let's start with virtual machines, and we'll refer to the diagrams to help visualise these concepts. A virtual machine allows multiple operating systems to run on a single physical machine. At the base, you have the infrastructure. This is your physical or virtual hardware. On top of that sits the host operating system, which is basically the primary operating system managing all the resources. Above the host OS, we have the hypervisor. The hypervisor is responsible for creating and managing virtual machines by allocating resources like CPU, memory, and storage. Each virtual machine runs a full guest operating system, which is completely isolated from others. Within each virtual machine, you have the guest operating system, which is essentially another complete operating system running on top of the host. So if your host operating system is a macOS, then the guest operating system could be Ubuntu, for example, the same way we've done it in the Linux section. Now, each VM also has its own binaries, libraries, and anything an application would need to run. So within the setup, there's a strong isolation. It also means each virtual machine is resource-heavy, which consumes significant CPU, memory, and storage.

**Containers**
On the other hand, we have containers. Containers are a more lightweight and efficient way to isolate applications. They share the host operating system just like virtual machines. But instead of using a hypervisor, they will run on the Docker engine. The Docker engine sits on top of the host operating system and is responsible for running containers. Containers are isolated from each other at the process level, but they share the underlying OS kernel, which makes them much lighter than VMs. The difference is they don't have the guest operating system because they share the host operating system. And that's what makes them lighter than virtual machines. Within each container, once again, you have the application and its dependencies. So you have your binaries and libraries, but without the need for a full guest operating system. This setup allows containers to start up quickly and use far fewer resources compared to VMs.

**The difference**

-The startup time as VMs can take minutes to boot up and containers share the host operating system which can start in seconds

-Resource usage as VMs include a full operating system which consums significant resources

-Isolation is strong in VMs as it has a full operating system and Containers only offer process level isolation (They share the host OS kernel but they're isolated within the container itself. The process is running within the container)

-Portability as VMs are less portable due to their size and dependencies and Contains are highly portable and can run consistently across different environmnents.

<img width="1710" height="830" alt="image" src="https://github.com/user-attachments/assets/5f9d815c-9f26-4cd1-8e0d-e6633f048ac4" />
