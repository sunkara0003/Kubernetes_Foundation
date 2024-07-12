![image](https://github.com/user-attachments/assets/197cc995-62d2-4295-a3f9-d557245983e8)# Kubernetes Architecture
- CLI client kubectl talks to Kubernetes Engine API server. Dashboards talks to APIServer.
- ![image](https://github.com/user-attachments/assets/9122bbc3-ac53-44df-ad49-b876222bcd1f)
- Master Plane has Scheduler, API server, etcd, Controller Manager.
- Scheduler schedule the pods
- etcd maintains the data/state of cluster it is same as backup for instances.
- ![image](https://github.com/user-attachments/assets/5099d9b9-b096-4801-b6d1-c1ff18d577e6)
- Kubeproxy maintains route/ip tables network related maintainance, Kernal level stuff.
- ![image](https://github.com/user-attachments/assets/88442737-c2cc-4d2b-9ca2-09a7233f5fda)



