Advance Topics:

Kubernetes intro
---

Kubernetes comes into play when you want to manage hundreds or even thousands of containers across multiple machines. 

K8s takes container management to the next level with some of these advanced features:
-Container orchestration
-Automatic scaling

K8s is the powerful amnager that oversees all the containers to make sure that they are deployed correctly, can scale up or down and automatically recover from failure. Kubernetes also helps developers to focus
more on application code instead of infrastructure and managing individual containers.


Docker Swarm vs Kubernetes
---

**Docker Swarm** is Docker's native clustering and orchestration tool that is built into docker - Easy to setup and use if you're familiar with docker environments.
This tool is mainly used in smaller deployments that are straightforward 

**K8s** is developed by Google and is a much more complex and feature rich container orchestration platform. It is used to manage containers at scale as it offers great flexibility and scalability which is essential
for large scale enterprise deployments.

<img width="1711" height="744" alt="image" src="https://github.com/user-attachments/assets/a1156d3a-616f-455b-839c-fd961e401276" />


Docker Swarm:
=No auto scaling
-Good community support
-Easy to start a cluster

K8s
-Auto scaling
-Great active support community
-Difficult to start a cluster
-Managed services in AWS, GCP, Azure

Depending on what type of project you're doing, you can pick between the two for example a much smaller project that needs to be done fast = use Docker swarm

A large project with complex needs = use Kubernetes as it's much more powerful and feature rich.
