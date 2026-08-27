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