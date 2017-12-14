## 1. Installation

### Install Docker CE
Docker Community Edition can easily be installed from the official docker website.
Be sure to use the link that matches your operating system.

Docker store: https://store.docker.com/search?type=edition&offering=community

### Test that your Docker installation is up and running
A comfortable way to assure that the installation is correct,
try to run the docker hello-world image by opening the terminal and type:

```bash
docker run hello-world
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

## 2. Run a docker image from docker hub

### Find your image!
In this lab we will run an instance of activemq i a docker container.
Browse and search for activemq from docker hub - https://hub.docker.com/explore/

Example: https://hub.docker.com/r/webcenter/activemq/

### Run the image in a container
Run an instance of the image in a container by using the docker client from terminal:
```
docker run webcenter/activemq
```

Try to access the amq web console by going to 
```
localhost:8161/admin
```

Nothing happens! Why?

The container does not expose the port 8161 from the container to the docker host!

Stop the container and restart it with the new argument
```
docker run -p 8161:8161 webcenter/activemq
```

Try to access the amq web console again by going to 
```
www.localhost:8161/admin
```
Default password is admin/admin

This time the webconsole should be accessible.


## 3. Run a custom docker image in a container
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
hello-docker                        latest              3b124e73a8e2        36 hours ago        244 MB
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

## 3. Spring boot application in a docker container
In this exercise we will create a simple spring boot rest application and run it in a container.

### Test the application

* make a git clone of following repository into a new directory: https://github.com/spring-guides/gs-rest-service.git
* open the project in your IDE and run the springboot application
* go to localhost:8080/greeting in a browser to try the rest service.

The response should look something like:
```
{
    id: 1,
    content: "Hello, World!"
}
```

### Build the application
Open a terminal and go to the projects 'complete' directory

Create a jar-file of the application by running:
```
mvn clean package
```
Verify that a jar file is located in the 'target' directory

### Create a dockerfile
Create a new dockerfile called 'Dockerfile' with the content below.
The 'EXPOSE' command describes that the compiled image should expose its port 8080 to the docker host when running.
```
FROM openjdk:8-jdk-slim

EXPOSE 8080

COPY springboot-rest-0.1.0.jar /src/springboot-rest-0.1.0.jar

CMD java -jar /src/springboot-rest-0.1.0.jar
```

Copy the generated jar-file from the 'target' folder to the same folder as the Dockerfile

Build the Dockerfile by executing:
```
docker build -f Dockerfile -t springboot-rest .
```
Verify that the image is available in your local docker environment:
```
docker images
```
```
REPOSITORY                          TAG                 IMAGE ID            CREATED             SIZE
springboot-rest                     latest              47e210ed91c9        2 days ago          259 MB
```

To be able to access the port 8080 in the container from the docker host, we must add the flag '-p' to the docker run command.
The '-p' flag binds the port inside the docker container to a port on the docker host.
```
docker run -p 8080:8080 springboot-rest
```
Try the rest service again in the browser or from a rest client.
