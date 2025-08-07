Containers Summarized
---

Containers are lightweight, portable units for running applications. Containers bundle application with all its dependencies, ensuring it runs consistently across different environments. 

For example, if you have an application and you want to run every part of the application. Containers will include the code, the runtime, the libaries and anything I need with all its dependencies that the application needs to run.

Containers Sit above the docker engine and each container has the app, its binary and libaries which the application needs to be able to run.

The docker engine sits in line with the host operating system and that sits above the infastructure which essentially is your Laptop or Computer.

<img width="1258" height="797" alt="image" src="https://github.com/user-attachments/assets/981a4d3e-b168-4c8f-a244-ec6c4abd61d4" />

**Summary**

-The infastructure as mentioned, represents the physical or virtual hardware where everything runs.
-Above that we have the host operating system which is the OS that runs directly on the infrastructure
-Then we have the docker engine which is what makes containeriation possible as it provides the environment to build, run and manage containers. 
-Finally we have the docker contains. As previously mentioned each container will have all the dependencies needed for the application to run in that container. 

The ***isolation*** ensures that each app runs consistently regardless of the environment. This is another benefit of Docker containers as whatever happens on App A won't affect App B/C etc.

A real life example of Docker containers would be shipping containers. Each shipping container hold everything needed for goods to be transported and can be easily moved from ships to trains and to trucks.

Whereas Docker containers hold everything needed for the software application to run and can be easily moved from one environment to another. 


***An important thing to note is that each container shares the underlying Docker enginer but they don't share the environment that is being run within the container itself. This is what makes them lightweight and efficient unlike virtual machines which take a 
subset of operating system***


**Benefits of Containers would be**
1. Each container is its own isolated environment meaning one container can be running a app on Python 2.7 and another can be running an app on Python 3.8. They are kept in isolation so they don't clash because of the different versions.
2. Containers remove issues like "It doesn't work on my machine" etc. This is a issue where the application can work on a developer's computer but failts to run properly on another environment due to missing dependencies or different configs. Contains provide consistent
   environments for applications to be run on.
3. Containers share the host kernel as it sits above the Host operating system (Device OS) - This means contains are essentially sharing the whole system's kernel like the operating system which reduces overhead and allows for more contains to be run on the same hardware.


**Images and Containers**
Images are templates for creating containers - Basically a snapshot of a container at a certain point so essentially it's like a specific setting that you want to load for your container to run.

Container run instances of images - So a Image would be the recipe of a dish and the container would be the actual dish you create from it. 

***These are created by a file called Dockerfile which is used to build Docker Imagess***

<img width="620" height="416" alt="image" src="https://github.com/user-attachments/assets/d6c5306d-502d-4d2f-8188-ed76aa45c304" />


Docker
---

Docker is a PAAS application that allows for developing, shipping and running applications in containers - Docker simplifies the process of managing Containers therefore making it easier to build, deploy and run apps.

**Docker Components**
Docker Engine - This is the core service that runs and manages containers - This is what powers the whole thing and is responsible for creating and running containers based on isntructions set in the Dockerfile and Images

Docker Hub - This is basically a repository where you can find and share container images like an App store for docker images. You can pull oficial images, community-contributed images or even share own images. 

Docker Compose - Is the tool for defining and running multi container Docker apps - Docker Compose manages more than one of these containers. It's like writing a recipe for how your entire application should run, what services are needed, how they interact, and what 
resources they require. For instance, if your application needs a web server, a database, and a cache, Docker Compose helps you define and orchestrate these components together because these components are required in essentially a single application.
