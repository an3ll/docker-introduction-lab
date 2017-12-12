## 1. Create a Docker compose file from template

Create a new file called 'my-compose-file.yml' and add the content below.
```
version: '3.1'

services:

  db:
    image: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
```

Use the docker-compose tool to run both services in docker by executing:
```
docker-compose -f my-compose-file.yml up
```

## 2. Make your own Docker Compose file!
1. Use the same project from springboot-rest-exercise or clone it again from https://github.com/spring-guides/gs-rest-service.git

2. Build the project with maven to produce a jar-file.

3. Create a Dockerfile and build an image.

4. Create a new docker compose file that contains one service based on the image and expose its rest-endpoint on 8080.


## 3. Make your own Docker Compose file with multiple services!
1. Modify the docker compose file so that it contains two services based on the same image and expose their rest-endpoints on different ports on the docker host.

2. Run the container with docker-compose and try to access both rest-endpoints.

