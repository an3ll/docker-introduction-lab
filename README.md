# Docker Introduction Lab
Introduction to working with docker

## 1.Installation

### Install Docker CE
Docker Community Edidion can easily be installed from the official docker website.
Be sure to use the link that matches your operating system.

Docker store: https://store.docker.com/search?type=edition&offering=community

### Test that your Docker installation is up and running
A comfortable way to assure that the installation is correct,
try to run the docker hello-world image by opening the terminal and type:

```bash
docker run hello-word
```

This will pull the hello-world image from docker-hub repo and run it in a container in 
your Docker environment.

The output in the terminal should be looking something like:
```bash
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
 ```

If this matches your output, congratulations, docker is up and running!

## 2.Create a custom Dockerfile and run it in a container
This excercise will create a simple executable docker image from a custom made Dockerfile that compiles and runs a java application.

### Create a simple Hello World java application.
* Before starting, be sure to create a new folder called dockerlab/hellodocker. 
* Go to the created directory
* Create a new java file called HelloWorld.java and add the following content:
```java
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello Docker!");
  }
}
```

### Create a DockerFile
* Create a new file called Dockerfile in the same directory as before. Add the following content:
```
FROM openjdk:8-jdk-slim

COPY HelloWorld.java /src/HelloWorld.java

RUN javac src/HelloWorld.java
CMD java -cp /src HelloWorld
```

* FROM - tells us that this docker file is based on an image from dockerhub called openjdk:8-jdk-slim
* COPY - COPY the file HelloWorld.java from our host to the docker image
* RUN - compile the HelloWorld.java
* CMD - run the compiled HelloWorld.class

### Build a Docker Image
* Open a terminal and go to the directory were the Dockerfile and HelloWorld.java is located.
* Build an image from the Dockerfile by executing:
```bash
docker build -f Dockerfile -t hello-docker .
```
* Make sure you see the created Docker image by executing:
```bash
docker images list
```
Should produce something like this:
```bash
REPOSITORY                          TAG                 IMAGE ID            CREATED             SIZE
hello-docker                        latest              2bf826fc0bfc        37 hours ago        740 MB
```
This means the 'hello-docker' image is saved in our local docker environment.
### Run the image in a container
To run an instance of the 'hello-docker' image execute:
```bash
docker run hello-docker
```
If done correctly there should now be an output in the terminal like:
```bash
Hello Docker!
```


