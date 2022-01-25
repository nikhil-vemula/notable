---
title: Docker
created: '2020-10-02T07:23:00.949Z'
modified: '2020-10-02T15:19:45.609Z'
---

# Docker

* Docker is a shift in the infrastructure. It is based on containerization.
* Image is the application which you want to run.
* Container is an instance of that image.
* Single image can have multiple containers.

## Docker setup

### Installation

https://hub.docker.com/editions/community/docker-ce-desktop-mac

### Shell completion

https://docs.docker.com/docker-for-mac/#install-shell-completion

## Commands

```cmd
docker container run --publish 80:80 --detach --name webhost nginx
```

`docker container run` will fetch the nginx image from the docker hub and run it.

`--publish` will expose 80 port of container to 80 port on the computer.

`--detach` run container in background

`--name webhost` created a contaienr with name "webhost"

### List containers

```cmd
docker container ls
```

### Stop container

```cmd
docker container stop <container-id>
```

### Run vs Start

```cmd
docker container start webhost
```

run - creates new instance of container.  
start - simply starts an existing container.

### Logs

```cmd
docker logs webhost
```

Show logs for a specific container.

### Clean up

```cmd
docker container rm <con-id> <con-id>
```

### Terminal for container

```cmd
docker container run -it <con-id> bash
docker container start -ai nginx
```
 
```cmd
docker container exec -it <con-id> bash
```

## Docker Networking

* Docker creates a virtual network called bridge/docker0.
* bridge/docker0 is the default docker virtual network which is NAT'ed behind the IP.
* Containers connected to same virtual network can talk to each other freely.
* To talk to container from host we need to expose the port using `-p` command.

### List networks

```cmd
docker network ls
```

* `bridge` is the default virtual network.
* `host` network can be used using `--network host` to skip the virtual network but sacrifies the docker container security.

### Inspect

```cmd
docker network inspect
```

### Create network

```cmd
docker network create <network_name>
```

creates an network with default `bridge` driver.

### Attach container to network

```cmd
docker network connect
```

### Dettach container to network

```cmd
docker network disconnect
```

## Docker images

* Image contains the metadata and information how to run the image.
* Docker hub is an image registry.
* Docker image is made up of layers.
* Docker container uses COW(Copy on write) for the changes we make. The base image is read only.

```cmd
docker image history <image_name>
```

```cmd
docker image inspect <image_name>
```

## Tags

```cmd
docker image tag [iamge:old-tag] [image:new-tag]
```

## DockerFile

* FROM - Minimal distribution
* ENV - Environmental variables
* RUN - run shell command
* EXPOSE - out ports
* CMD - run this command when container is launched

### Build images

```cmd
docker image build -t customnginx .
```

### Extending images

```dockerfile
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY index.html index.html
```

## Docker SOC (Seperation of concerns)

* Persistant data: The data which doesn't change when container is changed like version of container

### Volumes

* Volumnes outlive the containers
* They need to be cleaned manually

#### Named volumes

```cmd
-v mysql-db:/var/lib/mysql
```

### Bind mounts

* Mounts the host location to docker location

```cmd
-v hostlocation:dockerlocation
```

## Docker compose file

* Not a production level tool, good for local development

```cmd
docker-compose up
docker-compose down
```

```dockercompose
version: "2"
services:
  drupal:
    image: drupal
    ports:
      - "8080:80"
    volumes:
      - drupal-modules:/var/www/html/modules
      - drupal-profiles:/var/www/html/profiles
      - drupal-sites:/var/www/html/sites
      - drupal-themes:/var/www/html/themes
  postgres:
    image: postgres
    environment: 
      - POSTGRES_PASSWORD=admin
  
volumes:
  drupal-modules:
  drupal-profiles:
  drupal-sites:
  drupal-themes:
```
