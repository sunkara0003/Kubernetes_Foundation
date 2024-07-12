# High availability of cluster nodes
- Having nodes tolerance. 3/5 failures for example. RAFT is protocol used by K8s. It is distributed consistency protocol.
- maintains the multiple manager nodes and etcd to maintain fault tolerance.
- Connect with other Load Balancers and worker nodes.
- ![image](https://github.com/user-attachments/assets/1d646037-6f38-4f0c-b05f-980933845526)
- Monitoring elastic search grafana,Splunk for log management, and persistent volumes which are ephimeral.
- ![image](https://github.com/user-attachments/assets/30777784-0fdd-4637-9549-ee4db18e2d6a)
- Read more on Namespaces and GCP: https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-organizing-with-namespaces
- Best Practices using K8s https://www.youtube.com/watch?v=wGz_cbtCiEA&list=PLIivdWyY5sqL3xfXz5xJvwzFW_tlQB_GB
- Read about pods: https://kubernetes.io/docs/concepts/workloads/pods/
- Read about Replicasets: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
- https://www.mirantis.com/blog/kubernetes-replication-controller-replica-set-and-deployments-understanding-replication-options
- Service Discovery is an important feature of K8s. Learn more by reading the following article.

