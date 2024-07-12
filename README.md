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
    Run a test container image that includes a webserver.**output: deployment.apps/hello-node created**
``` sh
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
```
To view the created deployment in the dashboard runt the command below.
```sh
minikube dashboard --url
```

View in Dashboard

![image](https://github.com/user-attachments/assets/9329e206-614c-4743-a31e-eb4e2d52f2e6)

Command to View the Deployment:
```sh
kubectl get deployments
```
To view pods
```sh
kubectl get pods
```
To view Cluster events
```sh
kubectl get events
```
Output
```sh
LAST SEEN   TYPE     REASON                    OBJECT                            MESSAGE
11m         Normal   Scheduled                 pod/hello-node-ccf4b9788-22xqv    Successfully assigned default/hello-node-ccf4b9788-22xqv to minikube
11m         Normal   Pulling                   pod/hello-node-ccf4b9788-22xqv    Pulling image "registry.k8s.io/e2e-test-images/agnhost:2.39"
11m         Normal   Pulled                    pod/hello-node-ccf4b9788-22xqv    Successfully pulled image "registry.k8s.io/e2e-test-images/agnhost:2.39" in 11.218s (11.218s including waiting)
11m         Normal   Created                   pod/hello-node-ccf4b9788-22xqv    Created container agnhost
11m         Normal   Started                   pod/hello-node-ccf4b9788-22xqv    Started container agnhost
11m         Normal   SuccessfulCreate          replicaset/hello-node-ccf4b9788   Created pod: hello-node-ccf4b9788-22xqv
11m         Normal   ScalingReplicaSet         deployment/hello-node             Scaled up replica set hello-node-ccf4b9788 to 1
20m         Normal   Starting                  node/minikube                     Starting kubelet.
20m         Normal   NodeAllocatableEnforced   node/minikube                     Updated Node Allocatable limit across pods
20m         Normal   NodeHasSufficientMemory   node/minikube                     Node minikube status is now: NodeHasSufficientMemory
20m         Normal   NodeHasNoDiskPressure     node/minikube                     Node minikube status is now: NodeHasNoDiskPressure
20m         Normal   NodeHasSufficientPID      node/minikube                     Node minikube status is now: NodeHasSufficientPID
20m         Normal   RegisteredNode            node/minikube                     Node minikube event: Registered Node minikube in Controller
20m         Normal   Starting                  node/minikube                     
```
To View the config
```sh
kubectl config view
```
Output:
```sh
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://A6FC5ED00ECD8A1B19917FF2B02C3C1B.gr7.us-east-1.eks.amazonaws.com
  name: arn:aws:eks:us-east-1:533834059331:cluster/demo-cluster
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://9830C1AF138AB657D0FA3F0555A549E0.gr7.us-west-2.eks.amazonaws.com
  name: arn:aws:eks:us-west-2:533834059331:cluster/three-tier-cluster
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://A6FC5ED00ECD8A1B19917FF2B02C3C1B.gr7.us-east-1.eks.amazonaws.com
  name: demo-cluster.us-east-1.eksctl.io
- cluster:
    certificate-authority: /home/sunkara/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Fri, 12 Jul 2024 17:26:44 IST
        provider: minikube.sigs.k8s.io
        version: v1.32.0
      name: cluster_info
    server: https://192.168.49.2:8443
  name: minikube
contexts:
- context:
    cluster: arn:aws:eks:us-east-1:533834059331:cluster/demo-cluster
    user: arn:aws:eks:us-east-1:533834059331:cluster/demo-cluster
  name: arn:aws:eks:us-east-1:533834059331:cluster/demo-cluster
- context:
    cluster: arn:aws:eks:us-west-2:533834059331:cluster/three-tier-cluster
    user: arn:aws:eks:us-west-2:533834059331:cluster/three-tier-cluster
  name: arn:aws:eks:us-west-2:533834059331:cluster/three-tier-cluster
- context:
    cluster: demo-cluster.us-east-1.eksctl.io
    user: iam-root-account@demo-cluster.us-east-1.eksctl.io
  name: iam-root-account@demo-cluster.us-east-1.eksctl.io
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Fri, 12 Jul 2024 17:26:44 IST
        provider: minikube.sigs.k8s.io
        version: v1.32.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: arn:aws:eks:us-east-1:533834059331:cluster/demo-cluster
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - --region
      - us-east-1
      - eks
      - get-token
      - --cluster-name
      - demo-cluster
      - --output
      - json
      command: aws
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
- name: arn:aws:eks:us-west-2:533834059331:cluster/three-tier-cluster
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - --region
      - us-west-2
      - eks
      - get-token
      - --cluster-name
      - three-tier-cluster
      - --output
      - json
      command: aws
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
- name: iam-root-account@demo-cluster.us-east-1.eksctl.io
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - eks
      - get-token
      - --output
      - json
      - --cluster-name
      - demo-cluster
      - --region
      - us-east-1
      command: aws
      env:
      - name: AWS_STS_REGIONAL_ENDPOINTS
        value: regional
      interactiveMode: IfAvailable
      provideClusterInfo: false
- name: minikube
  user:
    client-certificate: /home/sunkara/.minikube/profiles/minikube/client.crt
    client-key: /home/sunkara/.minikube/profiles/minikube/client.key
```
To view the pod logs
```sh
kubectl logs hello-node-ccf4b9788-22xqv
```
Output:
```sh
I0712 12:05:52.208483       1 log.go:195] Started HTTP server on port 8080
I0712 12:05:52.208639       1 log.go:195] Started UDP server on port  8081
```
# Creating a Service
- By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster.
- To make the hello-node Container accessible from outside the Kubernetes virtual network, you have to expose the Pod as a Kubernetes Service.
  >> Warning:
The agnhost container has a /shell endpoint, which is useful for debugging, but dangerous to expose to the public internet. Do not run this on an internet-facing cluster, or a production cluster.
1.Expose the Pod to the public internet using the kubectl expose command:
```sh
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
```
The --type=LoadBalancer flag indicates that you want to expose your Service outside of the cluster.
The application code inside the test image only listens on TCP port 8080. If you used kubectl expose to expose a different port, clients could not connect to that other port.
## View the Service you created:
```sh
kubectl get services
```
On cloud providers that support load balancers, an external IP address would be provisioned to access the Service. On minikube, the LoadBalancer type makes the Service accessible through the minikube service command.This opens up a browser window that serves your app and shows the app's response.
Run the following command:
```sh
minikube service hello-node
```
#List the currently supported addons:
```sh
minikube addons list
```

## Clean up
Now you can clean up the resources you created in your cluster:
```sh
kubectl delete service hello-node
kubectl delete deployment hello-node
```

Stop the Minikube cluster
```sh
minikube stop
```







