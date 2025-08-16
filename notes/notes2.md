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


Docker Registries
---
Docker registry is a storage and distribution hub for docker images - simply put, it is an online library that stores our docker images so it can be reused if needed.

There are public registries which is basically docker hub (A library of images shared by others that can be used for your own environment) 

There is also private registries so that you can keep images to yourself


Docker hub
---

**How to push and pull images from docker hub**

1. first in the CLI do
```
docker login
```

2. Next we build our image and tag is correctly but first create a repositry in docker hub so we can store the image on docker hub
```
docker build -t f1him/flask-mysql:v1 .
```
After docker build we reference the username for your docker account, then the repositry name, then we give it a tag (v1 in this case), finally we tell docker to use the current directory to look for the Dockerfile

3. Now this can be pushed on to Docker hub by doing
```
docker push f1him/flask-mysql:v1
```
SImply uploads the image to the repositry you created in docker hub and names that image v1

4. We can also pull images from docker hub by doing
```
docker pull f1him/flask-mysql:v1
```
The same as push but we just change it to pull and run it in the CLI


AWS ECR
---
Elastic Container Registry is great for storing and managing private images especially if working within the AWS 

First ran this command to login to our private repo in AWS.
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 200110254966.dkr.ecr.us-east-1.amazonaws.com
```

We then build the image by doing the normal build command for docker

```
docker build -t flask-mysql .
```

Now run the tag command with the ECR repo URL
```
docker tag flask-mysql:latest 200110254966.dkr.ecr.us-east-1.amazonaws.com/flask-mysql:latest
```

Finally we run a push to get the image in our ECR repo
```
docker push 200110254966.dkr.ecr.us-east-1.amazonaws.com/flask-mysql:latest
```

We can also switch push with pull to grab the image.

<img width="812" height="623" alt="image" src="https://github.com/user-attachments/assets/5c491bba-9e27-4ce2-b5ec-d8130dcc5a39" />


Using multistage builds to save space
---

After checking how much size my flask app has taken with the below command, I have decided to make my Dockerfile multistage which will essentially use multiple FROM statements  that will use one for Build stage and another for a much lighter finals tage. 

```
docker images <image name>
```

There is a part that requires all the dependencies to build the app, but all the dependencies are not required in the actual final image. This approach lets you discard unnessary files and dependencies which results in a smaller optimized image. By reducing the size, the deployments will be much faster and efficient. 

```
# stage 1: build stage
FROM python:3.8-slim as Build

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    python3-dev \
    libmariadb-dev \
    pkg-config

COPY . .

RUN pip install flask mysqlclient

# STAGE2: Prod

FROM python:3.8-slim

WORKDIR /app

COPY --from=Build /app /app

EXPOSE 5002

CMD ["python", "app.py"]
```
***Example of a multistage build***

After you have edited the dockerfile to be "multistage deployment", you just need to do the following 

```
docker build -t my-flask-app:multistage .

docker-compose up -d
```

After building and editing my compose file to make this build mutlistage, I can see the size is now much smaller compared to what it was before 

```
fahim@DESKTOP-CNID5Q9:~/docker/hello_flask$ docker images my-flask-app:multistage
REPOSITORY     TAG          IMAGE ID       CREATED        SIZE
my-flask-app   multistage   e2e4141cbae9   19 hours ago   311MB
```

