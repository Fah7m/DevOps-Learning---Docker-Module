# DevOps-Learning---Docker-Module
Docker notes and learning

Creating a web app to containerize
---

1. We run VS code and use the WSL terminal we installed to:

-Create a directory for the App

-"pip3 install flask" to install the flask framework for web apps in python

-"touch app.py" to create the application - can paste command here

-Since we are running this in the WSL terminal we can do "code app.py" to open a remote window of VS code - may need to put the full directory if your not in the same dir as the app

<img width="1197" height="851" alt="image" src="https://github.com/user-attachments/assets/d455a636-f9a5-43f6-81e9-3f0e809e6f01" />

***This is how it will look***

2. We write the Dockerfile

-do a "touch Dockerfile" to create the file and make sure it has a capital D

-We now write the instructions in the docker file

<img width="328" height="145" alt="image" src="https://github.com/user-attachments/assets/866d95b4-04d0-4167-a35f-7a5685489bd0" />

-Finally we build it by doing "docker build -t hello-flask ." 

- ***docker build*** will initiate the build process, ***-t hello-flask*** will tag the image with a name in this case it will be called hello-flask, finally the ***dot at the end*** represents the current directory so in other cases you may want to point to a certain directory and this is where it is done.

```
docker build -t hello-flask .
```

3. We now run the container once it has been built

-The -d flag runs the container in detached mode which means running it in the background, -p maps the ports 5002 on my machine to the 5002 port in the container, finally the name of the image we are using which is hello-flask
```
docker run -d -p 5002:5002 hello-flask
```

Linking containers together
---
Here we will add a database on top of our application to return a value to imitate a real world scenario 

1. This is the updated code that will connect to a MySql database

<img width="522" height="451" alt="image" src="https://github.com/user-attachments/assets/aa23645f-5a1a-4cf4-b9ee-5cb1eb09377f" />


2. The Dockerfile now needs to be updated so the dependencies for MySQL is installed as well as the mysqlclient which provides the tools needed to connect the database from within our application

<img width="384" height="253" alt="image" src="https://github.com/user-attachments/assets/a4319427-5563-4a2b-b2df-eddfba82a05e" />

***An extra RUN instruction has been added now to install the system dependencies for the mysqlclient*** - Also, we now RUN the mysqlclient too

3. Creating a custom network for containers to communicate with each other

=The command basically creates a custom network that we will use later to connect the flask and mysql containers
```
docker network create my-custom-network
```

4. running the mysql container

-Here we first do a docker run -d for running in the background and then define the name of the container, then we set the network to the network we created before, we use the -e flag to set the root password for MySQL database (should be saved somewhere), and finally we specify the version of MySQL which is 5.7 

```
docker run -d --name mydb --network my-custom-network -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:5.7
```

5. Here we build the docker image for the Flask app with the updated Dockerfile

-we run this to build the docker image but we add in mysql and point to the current directory which is where the Dockerfile is

```
docker build -t hello-flask-mysql .
```

6. We run the flask application this time

-We define the name as myapp this time and use the same custom-network we can connect the database container, and the application container

```
docker run -d --name myapp --network my-custom-network -p 5002:5002 hello-flask-mysql
```

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



Docker commands
---

This command checks the version of docker your running 
```
docker --version
```

A comprehensive overview of your environment which is useful for troubleshooting or understand the systems current state
```
docker info
```

To run a docker container - it first checks if the "hello world" image is present on your machine, if not it pulls the image from docker hub and then a container is made from this image.
```
docker run hello-world
```

This command shows you the containers that are running and more information
```
docker ps

docker ps -a - to see all containers even if stopped
```

This command will show the logs of a container - good for troubleshooting and debugging
```
docker logs mycontainername
```
