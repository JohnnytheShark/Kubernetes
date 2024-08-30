# Kubernetes 

## Explanation:
Kubernetes is a deployment platform for containers.

Think of containers as a unit that hosts your code and its dependency scripts inside of it to be ran inside an isolated environment. 

Kubernetes is the container orchestrator to run your containers on a resource of (cluster) machines. 

Benefit from using K8s is the high availability for our applications. 

Containers are grouped into Pods. A Pod is a group of containers treated as one single unit.

## Containerization 

Running docker: 
    docker run -it ubuntu bash

    apt-get update
    apt-get install -y python3

For info on the container: 
    docker ps -a

Cleaning up images off your system: 
    docker system prune -a

Compiling can be done in the containers themselves:
    FROM openjdk
    COPY . /app
    WORKDIR /app
    RUN javac Hello.java
    CMD java Hello

The better route is to do a multistage container build. This lessens the attack surface of your application, and debloats the application

Example Multistage Build: 

    FROM openjdk:11 AS buildstage
    COPY . /app
    WORKDIR /app
    RUN javac Hello.java

    FROM openjdk:11-jre-slim #Notice we are using a smaller image
    COPY --from=buildstage /app/Hello.class /app/
    WORKDIR /app
    CMD java Hello
