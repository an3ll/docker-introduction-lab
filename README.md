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
