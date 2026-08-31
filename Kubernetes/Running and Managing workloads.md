![[Screenshot 2026-08-30 at 12.13.16.png]]

A pod is the smallest element that you can create in a Kubernetes cluster. 
it represents one instance of the image that has been generated from an application. 



![[Screenshot 2026-08-30 at 12.18.09.png]]


*note: 0 is successful*  
###### Pod Lifecycle
- Pending --> Pod accepted by API Server but not yet running
- Running --> At least one container is running
- Succeeded --> All containers exited successfully 
- Failed --> All containers terminated, one or more failed (non zero exit code)
- Unknown --> Kubelet cant report state (e.g. node issue or network loss)

#### Deploying apps on K8s

Deployment is a powerful kubernetes controller - lets automatic scaling, easy upgrades or roll backs

**Deployments YAML**

![[Screenshot 2026-08-31 at 16.24.07.png]]