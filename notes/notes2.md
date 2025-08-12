Docker compose
---

Docker compose is a tool that allows you to define and manage multi-container docker applications. Instead of starting and stopping containers one by one, we can use Docker Compose to define 
all the services in a single file and manage them collectively.

At the heart of Docker compose is a YAML file which lists all the services your application needs - it operates as a blueprint that describes each container and specifying details like which image to use and what port to expose

This is useful because with just one command we can spin up our entire environment. The simplexity of it is another major benefit as running docker compose up will bring up the containers defined in the YAML file

Docker compose also created a network for your containers which saves time as before we had to create a custom network, then make sure each container had that customer network defined when building the image.

<img width="347" height="288" alt="image" src="https://github.com/user-attachments/assets/ad616486-eb5b-421b-9ab0-fe67efeaf6d0" />

***example of a docker-compose.yml file***

The file breakdown:

1. First we specify which version of the docker-compose file we use which is 3.8
2. We now add in the services and in this case we use the web service for our flask application and the database service.
3. Next we have build . - this tells docker compose to build the web service from the docker file in the current directory
4. Next for the web app container we map the host machine port 5002 to the container port 5002
5. Lastly, we have a depends on which essentially just waits for the database container to start up before launch the web app container

The same thing is done for the database container
1. We first set the image that we will use for the database
2. Next we set the environment variable for adding a root password.

To run this we do 

```
docker-compose up -d
```
***We parse -d flag to run it in the background***

