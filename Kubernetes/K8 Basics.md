K8 just lets you handle/manage containers on a massive scale.

![[Screenshot 2026-08-27 at 12.47.40.png]]


**What problem is K8's solving?**

lets say you have an application, with image version 1.1 deployed on an EC2 instance. as we scale we can have 3 instances running. 

![[Screenshot 2026-08-27 at 12.54.11.png]]

now a dev makes changes to the image and deploys it - now we have version 1.2 of the image. But the ***issue*** is that we have to deploy 3 instances of the EC2 instance before destroying the previous versions.  Now we are using 16 cores and 12GB RAM for just 3 containers. 

![[Screenshot 2026-08-27 at 12.57.35.png]]


Kubernetes uses a ***SINGLE NODE*** and manages resources for you


#####  **When NOT to USE K8's**

K8s adds a lot of complexity - control plane, manifests, networking and security. 

if app is small, 1-2 containers - low traffic, infrequent deploys  --> then use docker compose / ECS Fargate.

##### How containers run in a K8s cluster

*Note: kubectl apply is like terraform apply. it applies a configuration file you define to match your desired state.* 

![[Screenshot 2026-08-27 at 13.07.08.png]]

 **User $\rightarrow$ Kubernetes Master (API Server):** 
 So when a user runs an *kubectl apply* or whatever talks to your cluster - this goes straight to the **KUBERNETES MASTER** via the **KUBERNETES API**. Nothing is applied. 

**Kubernetes Master $\rightarrow$ Kubernetes Node (Internal APIs):**
The master decides which worker machine (**Node**) has enough CPU and RAM.
it sends a message over **internal API** to an agent running on that node telling it that it needs to run this container. 

**Kubernetes Node $\rightarrow$ CRI-O (CRI gRPC)**
The node agent contacts **CRI-O** (the high-level container engine) using a standard communication line (**CRI gRPC**).
CRI-O downloads the container image (e.g. from Docker Hub) and sets up the network.

**CRI-O $\rightarrow$ runc (FORK / EXEC)**
CRI-O passes the heavy lifting down to **runc** (the low-level worker tool) using basic system commands (**FORK / EXEC**)

**runc $\rightarrow$ Linux Kernel / Container (FORK / CLONE)** 
**runc** talks directly to the **Linux Kernel** using **FORK / CLONE** commands.
The kernel puts walls around the process (namespaces) and limits its CPU/RAM usage (cgroups).
**Your container is now live and running!**


What actually runs the container is the Runtime Engine. Kubernetes is just the orchestrator. 
it talks to the engine via the CRI (Container Runtime interface)![[Screenshot 2026-08-27 at 19.20.20.png]]

**Key Terms:**
- K8s Cluster - is a collection of nodes that provide computer, memory and networking resources.
	- K8s uses these resources to run the various work loads/ infrastructure.
- Nodes - This is one host e.g. like a VM or Physical machine. Each Node can run several components of K8s. 
- Control Plane/Master Node - This is the command centre that controls everything in the cluster. 
- Kube API Server - This is the entry point of all administrative commands
- ETCD - This stores cluster data and state, its like the K8s memory
- Kube Controller Manager - Cluster supervisor - it makes sure the desired state matches the reality. 
- Kube Schedular - This decides which work nod your Pod uses. 
- Cloud Controller Manager - Connects with Cloud provider API 
- Pod - a collection of a containers that are co located on a single machine - these are the smallest units within K8s world. These are wrappers around containers. 
- Service - this is a load balancer that can bring traffic down to a collection of pods 
- Deployment/Replica set - used for replicating a container multiple times for availability or scalability. 

**Worker Node Terms:** 
- Kublet - an agent that talks to the master node making sure the containers are running as it should be. 
- Kube-Proxy - Ensures each pod in the Node can communicate with other nodes in the cluster
![[Screenshot 2026-08-27 at 19.44.18.png]]


We can use 'kind' which is a tool that lets you run K8s locally. 
We made this yaml file:
![[Screenshot 2026-08-30 at 11.13.26.png|333]]

we run `kind create cluster --config kind-config.yaml --name k8s-demo`
to create a k8 cluster

and using `kubectl cluster-info --context kind-k8s-demo` we can see the cluster running. 

with `kubectl cluster-info dump` we can see more info about our nodes:

![[Screenshot 2026-08-30 at 11.16.41.png|586]]


we can run a pod with `kubectl run pod nginx --image=nginx`
and see the pods running with `get pods`

![[Screenshot 2026-08-30 at 11.17.27.png]]


we can deploy this with:
`kubectl create deployment nginx --image=nginx`

we can see the deployment with: 
`kubectl get deploy`


##### K8 Namespaces

Namespace allows you to partition your cluster:

![[Screenshot 2026-08-30 at 11.31.08.png]]