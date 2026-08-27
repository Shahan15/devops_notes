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

