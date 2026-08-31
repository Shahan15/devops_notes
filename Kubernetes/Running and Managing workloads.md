![[Screenshot 2026-08-31 at 16.52.39.png]]![[Screenshot 2026-08-30 at 12.13.16.png]]

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


> [!NOTE] > *Deployment* in K8s is a NOUN - it is a specific API resource object defined by a YAML file which manages application rollouts and scaling. 

> [!NOTE] >  it is like an AWS ECS Service. 



**Deployments YAML**

![[Screenshot 2026-08-31 at 16.24.07.png]]

Replicas - this means "Always keep 3 copies running"

after writing the above YAML file. we ran: 
`kubectl apply -f nginx-deploy.yaml` and with `kubectl get deploy` we can see the deployment: 
![[Screenshot 2026-08-31 at 16.51.02.png]]

and we can see the pods running with `kubectl get pods`

![[Screenshot 2026-08-31 at 16.52.39.png]]

if we were to delete one pods. kubectl would automatically bring up another. because we set `replica set` to 3.  Our Deployment is the ***Boss***

so to delete the deployment we have to run
`kubectl delete deploy nginx-deployment`