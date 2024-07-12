# Service Creation next steps
- namespaces for application stack
- Deployment calls Replicaset calls replication of pods
- Deployment has update and release strategies
- Service calls Deployments

  ![image](https://github.com/user-attachments/assets/25ec7049-3d02-44dc-b5ca-4bc20db1d2d9)

**  Configmaps, Secrets, Persistent Volumes, CNI/Network, Network Policies, Helm Package Manager,RBAC:**
  - for the configuration of application using Configmaps
  - share and inject credentials we use Secrets
  - Saving the data persistently using persistant volumes
  - Network Policies defines the what goes in and what goes out of Cluster using namespaces
  - Packaging Service the entities like apt in linux. 
  - RBAC gives Role binding, Authentication and authorization.Rolebased Accesss Controlers.
  - Horizontal scaling pods works for deployments, Increasing servers, Vertical scaling is increasing the server hardware.
## Deployments
Each namespace running more than one instance of node.
![image](https://github.com/user-attachments/assets/9f69d6c7-0e3b-4536-a942-10db2dff4ba0)

**Deamonsets**
Running a particular instance logging let's say.The Deployment kind will be Deamon set.It needs to run on every host/node.

**Statefulset**
- Deployments support dynamic provising. mount volumes while creating pods.
- It does not come with an endpoints. You may need to communicate between same pods. lets say cassendra nodes/pods.
- Statefulsets launches the deployments on the same server. If host not available it keeps on pending never lauch it.
- It has a constant identifier located on server.
![image](https://github.com/user-attachments/assets/09e606c0-50b0-4252-ba2c-590e92e00bf4)

**cron**
- Certain jobs schedule using crons.
![image](https://github.com/user-attachments/assets/96b4d7fd-2fa4-4fbc-8807-cbe2a0c4b288)




