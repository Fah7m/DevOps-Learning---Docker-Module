The Task
---

Create a multi-container application that consists of a simple Python Flask web application and a Redis database. The Flask application should use Redis to store and retrieve data.

How to run
---

This is after going into the directory where you have built app, dockerfile and the compose file.

Dir=~/docker/challenge


1. ***Make sure that the image is built***
```
docker build -t count-app:v4 .
```

2.***initialise swarm***
```
docker swarm init
```
We used swarm to load balance between our different nodes - replicated the web service (web container) 2 more times so we had 3 instances running and docker swarm handled the load balancing.

no need for reverse proxy in compose file

3. ***Check the stack***
We can check this by doing the following and can see how many replicas we have.

```
docker service ls
```
<img width="945" height="119" alt="image" src="https://github.com/user-attachments/assets/3cdd7db8-69d0-46ca-9f80-c71611329c1c" />


***We can further go into each the web stack by doing***
```
docker service ps mystack_web
```
<img width="1331" height="137" alt="image" src="https://github.com/user-attachments/assets/0eb92b9b-84d7-4c54-9980-a37618896a3c" />


