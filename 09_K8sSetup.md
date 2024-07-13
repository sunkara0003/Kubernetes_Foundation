# Kubernetes Setup
- Install minikube single worker node for practice.
- check the status
```sh
minikube status
```
```sh
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```
- Launch a kubernetes dashboard
```sh
minikube dashboard
```
- Setting up docker environment
```sh
minikube docker-env
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.100:2376"
export DOCKER_CERT_PATH="/Users/gouravshah/.minikube/certs"
export DOCKER_API_VERSION="1.23"
# Run this command to configure your shell:
# eval $(minikube docker-env)
```
Run the command given above, e.g.
```sh
eval $(minikube docker-env)
```
Now your docker client should be able to connect with the minikube cluster

# Setup a 3 node K8s cluster

![image](https://github.com/user-attachments/assets/d2c4ecc7-7c99-41ed-a20c-e05914088e4c)

- Create 2 ec2 instances with same security group
![image](https://github.com/user-attachments/assets/a4951c4f-24b8-4e42-84fd-e1b7ef7fad08)

- Connect to EC2 instances via ssh
- Run apt get update on all the machines
- Run apt upgrade
- Rename the server names
```sh
sudo hostnamectl set-hostname <k8s-workernode1>
```
```sh
sudo hostnamectl set-hostname <k8s-workernode2>
```
```sh
sudo hostnamectl set-hostname <k8s-controlnode>
```

  ![image](https://github.com/user-attachments/assets/b25a9a5f-5871-406a-85cc-527c1a7ffd2e)

Watch this video gives brief overview and implementation of K8s 1 master node and 2 worker nodes
https://www.youtube.com/watch?v=k3iexxiYPI8

