![image](https://github.com/user-attachments/assets/edafb865-56a0-4d0d-b89a-3df3130181c7)# Docker Foundation
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
















