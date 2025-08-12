Docker compose
---

Docker compose is a tool that allows you to define and manage multi-container docker applications. Instead of starting and stopping containers one by one, we can use Docker Compose to define 
all the services in a single file and manage them collectively.

At the heart of Docker compose is a YAML file which lists all the services your application needs - it operates as a blueprint that describes each container and specifying details like which image to use and what port to expose

This is useful because with just one command we can spin up our entire environment. The simplexity of it is another major benefit as running docker compose up will bring up the containers defined in the YAML file

Docker compose also created a network for your containers which saves time as before we had to create a custom network, then make sure each container had that customer network defined when building the image.

