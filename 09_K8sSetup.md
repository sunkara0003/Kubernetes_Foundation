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

# Kubernetes cluster setup on digitalocean
- create 3 nodes and add the this script in userdata
- https://gist.github.com/initcron/40b71211cb693f541ce35fe3fb1adb11
```sh
#!/bin/bash 

apt-get update
apt-get install -y git wget

# Install Docker
apt-get install -yq \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
apt-get update

apt-get install -yq docker-ce docker-ce-cli containerd.io

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

sudo cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF

sudo apt-get update -y

sudo apt-get install -y  kubelet kubeadm kubectl kubernetes-cni nfs-common

# Install Docker Compose 
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose


sudo sysctl net.bridge.bridge-nf-call-iptables=1
sudo swapoff -a

sudo rm -rf /var/lib/kubelet/*

sudo apt-get install nfs-common -y
```

Faced many issues below is resolution
```sh
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

sudo apt update

sudo apt install -y kubelet kubeadm kubectl
```

Encountered many issues
```sh
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
	[ERROR CRI]: container runtime is not running: output: time="2024-07-13T13:05:42Z" level=fatal msg="validate service connection: validate CRI v1 runtime API for endpoint \"unix:///var/run/containerd/containerd.sock\": rpc error: code = Unimplemented desc = unknown service runtime.v1.RuntimeService"
, error: exit status 1
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
```
Resolution

```sh
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

sudo apt update

sudo apt install -y kubelet kubeadm kubectl

```

Another issue
```sh
root@kube-01:~# apt remove containerd
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package 'containerd' is not installed, so not removed
0 upgraded, 0 newly installed, 0 to remove and 4 not upgraded.
root@kube-01:~#  apt update, apt install containerd.io
E: Invalid operation update,
root@kube-01:~# kubeadm init --apiserver-advertise-address 139.59.87.129 --pod-network-cidr=192.168.0.0/16^C
root@kube-01:~# apt install containerd.io
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
containerd.io is already the newest version (1.7.18-1).
0 upgraded, 0 newly installed, 0 to remove and 4 not upgraded.
root@kube-01:~# rm /etc/containerd/config.toml
root@kube-01:~# systemctl restart containerd
root@kube-01:~# kubeadm init --apiserver-advertise-address 139.59.87.129 --pod-network-cidr=139.59.87.1/16
[init] Using Kubernetes version: v1.30.2
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
W0713 13:07:49.405527   11433 checks.go:844] detected that the sandbox image "registry.k8s.io/pause:3.8" of the container runtime is inconsistent with that used by kubeadm.It is recommended to use "registry.k8s.io/pause:3.9" as the CRI sandbox image.
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
```

### Resolution:
```sh
    [init] Using Kubernetes version: v1.24.1
    [preflight] Running pre-flight checks
    error execution phase preflight: [preflight] Some fatal errors occurred:
            [ERROR CRI]: container runtime is not running: output: time="2023-01-19T15:05:35Z" level=fatal msg="validate service connection: CRI v1 runtime API is not implemented for endpoint \"unix:///var/run/containerd/containerd.sock\": rpc error: code = Unimplemented desc = unknown service runtime.v1.RuntimeService"
    , error: exit status 1
    [preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
    To see the stack trace of this error execute with --v=5 or higher
```
### Solution:
By searching the web it appears this is an issue with the old containerd provided by Ubuntu 20.
I solved it with the following steps (as root):
1. Set up the Docker repository as described in https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository
2. Remove the old containerd:apt remove containerd
3. Update repository data and install the new containerd: apt update, apt install containerd.io
4. Remove the installed default config file: rm /etc/containerd/config.toml
5. Restart containerd: systemctl restart containerd
```

**issue:**
 kubectl get nodes 
E0713 13:15:57.697420   15834 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp [::1]:8080: connect: connection refused
E0713 13:15:57.697839   15834 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp [::1]:8080: connect: connection refused
E0713 13:15:57.699588   15834 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp [::1]:8080: connect: connection refused
E0713 13:15:57.700370   15834 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp [::1]:8080: connect: connection refused
E0713 13:15:57.701691   15834 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp [::1]:8080: connect: connection refused
The connection to the server localhost:8080 was refused - did you specify the right host or port?


**Resolution:**
```
#On the control plane server configure kubectl using commands in the output and you are all set:

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
``






