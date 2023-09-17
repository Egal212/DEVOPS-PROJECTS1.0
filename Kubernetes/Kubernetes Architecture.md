Each Kubernetes node can have multiple pods in it running two or more containers, but to be able to do that three processes must be installed on every node that is used to schedule and manage pods.

* Container Runtime: is the first process that needs to be running and installed.

* Kubelet: is the process of Kubernetes that has an interface with both container runtime and the machine node itself, Kubelet interacts with both the container and node. it is also responsible for taking the configurations and running a pod or starting a pod with a container inside and reassigning resources that node to the container like CPU, RAM, and MEMORY.

* KUBE-PROXY: is the second process responsible for communication via services between nodes which is like a load balancer that catches and matches the request directly to the pod or the app  databases and forwards it to the respective recipient.

Kube-proxy has an intelligent forwarding logic inside that ensures communication also moves in a performant way with low overhead.

  # MASTER NODE.
  
The main processes on Kubernetes are done by the Master node.

1. API-SERVER: We interact with the API-server using clients to deploy new application services. The client could be the Kubernetes dashboard, CLI, or UI. The API server is like a cluster gateway that gets the initial request of any updates into the cluster, or even the queries also act as a gatekeeper for authentication.

2. SCHEDULER: is what decides on which node the new pod should be scheduled. The process that starts the pods on the node is the kubelet which gets the request from the scheduler.

3. CONTROLLER MANAGER: is what detects that nodes have died and reschedule those pods on another node. It detects state changes of nodes and pods, and schedules or restarts another.

4. etcd: is the key/value store of a cluster state. etcd is the cluster brain. Every change or state is saved in the key/value store of etcd. All the configuration of the scheduler and controller manager works because of etcd data in the key/value store.

Note: The actual application data is not stored in the key/value store but in the database running in the cluster.
Master nodes need fewer resources like CPU, RAM, and STORAGE.
Worker node needs more resources because they do the actual work.

To add a new master /node server.
1. Get a new bare server
2. Install all master process/worker node processes.
3. Add it to the cluster.

