# Why do we need Container Orchestration Engine?
1. Docker is a great tool.It is limited to run on a single host
2. Docker Compose can run a application stack of inter connected components like apis,db,frontend. It is also single host limited.
3. In production/staging environment we need to manage all 100+ the hosts/servers to make reliable, 0 tolerance services.
4. Instead of human intervenience K8s bring into picture Container Orchestration Engine.
5. It will take a pool of servers and orchestrate the nodes as a Cluster.It will schedule the jobs/process on multiple servers.

# Why K8s?
1. Swarm is more easy to create and manage containers, Container Clusters.
2. K8s is robust, feature rich.More usecases in industry standards.
3. Mesos is not purely Container orchestration engine. Its like a pool of jobs submitted to  cluster of similar types cron jobs,container jobs,apache jobs etc.

# Features of COE- Container Orchestration Engine:
- K8s gives container as a service.It can built on top of a cloud. Easy to work on deployments.
- Dynamic provisioning infrastructure as load grows.Horizontal scaling is also useful with K8s.
- Fault Tolerence if container goes down it will re-provision the containers/pods on other host/servers.
- Stateless using persistant volumes, Databases.
- It was created by Google. Inspirated by google infrastructures management.
- It is battle hard. Manages 1000s of containers.
