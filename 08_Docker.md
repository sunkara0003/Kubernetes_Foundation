# Docker Foundation
The URL for docker related stuff playing remotely login with gmail
https://labs.play-with-docker.com/p/cq8nfc2im2rg00e3bns0#cq8nfc2i_cq8nfdqim2rg00e3bnsg
- Docker for containerization of applications
- ![image](https://github.com/user-attachments/assets/e7ddcec4-8c3e-4646-ba2a-f10d9ae7dcfe)
- building alpine image and running the uptime.
- Before building an image it will check in local namespace not found then search in Docker hub and pulling to build
- The below is an emphimeral container not persistent.
```sh
docker container run alpine:latest uptime
```
for Checking the container
```sh
docker ps
```
For renaming the container name
```sh
docker rename <old> <new>
```
loging the container
```sh
docker logs <container_id>
```
login into container
```sh
docker container -exec -it <contianer_id> sh
```

detailed information about container
```sh
docker inspect
```
coping files from local to container
```sh
docker container cp <file.txt> <container_name>:/opt
```
after container creation checking the changes
```sh
docker contianer diff <container_name>
```
Stopping the container
```sh
docker stop <contianer_id>
```
Removing the container. We cant remove the container while it is running need to stop then remove. 
```sh
docker rm <container_id>
```
Docker labs:
https://kubernetes-tutorial.schoolofdevops.com/operating-docker-containers/

Docker contianer managing and monitoring running which are running local host and upgraded version has much more features
https://docs.portainer.io/start/install-ce/server/docker/linux

Cloning github for premethues stack
```sh
git clone https://github.com/vegasbrianc/prometheus.git
```
create container form the images
```sh
docker-compose up -d
```
list the containers running
```sh
docker ps -l
```
build an image with this source code
https://github.com/schoolofdevops/facebooc/tree/master
create a Dockerfile 
```sh
FROM ubuntu

WORKDIR /opt/facebooc

RUN apt-get update && apt-get install -yq build-essential make libsqlite3-dev sqlite3

COPY . /opt/facebooc

RUN make all

EXPOSE 16000

CMD "bin/facebooc"
```
















