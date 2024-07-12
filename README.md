# Kubernetes_Foundation
# Basics
- Deploy a containerized application on a cluster.
- Scale the deployment.
- Update the containerized application with a new software version.
- Debug the containerized application.

## What can Kubernetes do for you?
- With modern web services, users expect applications to be available 24/7, and developers expect to deploy new versions of those applications several times a day. Containerization helps package software to serve these goals, enabling applications to be released and updated without downtime.
- Kubernetes helps you make sure those containerized applications run where and when you want, and helps them find the resources and tools they need to work.
- Kubernetes is a production-ready, open source platform designed with Google's accumulated experience in container orchestration, combined with best-of-breed ideas from the community.
  ![image](https://github.com/user-attachments/assets/b3536cfc-d59a-4392-9981-09eff4705427)
# What is a Cluster?
- A set of individual machines tagged to single name.
- Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.
- Kubernetes allow you to deploy containerized applications to a cluster without tying them specifically to individual machines. To make use of this new model of deployment,applications need to be packaged in a way that decouples them from individual hosts: they need to be containerized.
- <b> How deployment happen before k8s? </b> Containerized applications are more flexible and available than in past deployment models, where applications were installed directly onto specific machines as packages deeply integrated into the host
-  Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way. Kubernetes is an open-source platform and is production-ready.

## A Kubernetes cluster consists of two types of resources:
- The Control Plane coordinates the cluster
- Nodes are the workers that run applications

  ![image](https://github.com/user-attachments/assets/4be623e4-f8d0-4cf7-8c59-23e181d2b78f)
- The Control Plane is responsible for managing the cluster. The Control Plane coordinates all activities in your cluster, such as scheduling applications, maintaining applications' desired state, scaling applications, and rolling out new updates.
- A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster.
- Each node has a Kubelet, which is an agent for managing the node and communicating with the Kubernetes control plane. The node should also have tools for handling container operations, such as containerd or CRI-O.
-  A Kubernetes cluster that handles production traffic should have a minimum of three nodes because if one node goes down, both an etcd member and a control plane instance are lost, and redundancy is compromised. You can mitigate this risk by adding more control plane nodes.

# How containers run on K8s?
- When you deploy applications on Kubernetes, you tell the control plane to start the application containers.
- The control plane schedules the containers to run on the cluster's nodes.
- Node-level components, such as the **kubelet**, **communicate with the control plane using the Kubernetes API**, which the control plane exposes.
- End users can also use the Kubernetes API directly to interact with the cluster.
## Where can K8s can be deployed?
- A Kubernetes cluster can be deployed on either physical or virtual machines
# For practice the K8s and get handson experience
- To get started with Kubernetes development, you can use Minikube. Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node. Minikube is available for Linux, macOS, and Windows systems.
- The Minikube CLI provides basic bootstrapping operations for working with your cluster, including start, stop, status, and delete.

# Working with Minikube works in single node
## Create a Deployment 
**Pod:** A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking.
**Deployments:** A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.
**Steps:**
1. Use the kubectl create command to create a Deployment that manages a Pod. The Pod runs a Container based on the provided Docker image.
    Run a test container image that includes a webserver.output: deployment.apps/hello-node created
   ``` sh
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
  ```
  To view the created deployment in the dashboard runt the command below.
  ```sh
minikube dashboard --url
```

View in Dashboard

![image](https://github.com/user-attachments/assets/9329e206-614c-4743-a31e-eb4e2d52f2e6)


2. 







