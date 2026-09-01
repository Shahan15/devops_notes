![[Screenshot 2026-08-31 at 20.47.42.png]]![[Screenshot 2026-08-31 at 16.52.39.png]]![[Screenshot 2026-08-30 at 12.13.16.png]]

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


##### Imperative declarations

when we write out the YAML code and everything - that is Declarative 

imperative is when we run a command to generate the boilerplate code :
`kubectl create deploy nginx-deployment --image=nginx --replicas=2`


##### ReplicaSets

Replicas - this means "Always keep 3 copies running" or whatever number we set

Replicas are simplest K8s pod controller resource. 

Deployment is like the queen bee - it maintains order and keeps everything running smoothly. it overseas everything. 
	 under deployments you can have 2 different versions of your application running 

![[Screenshot 2026-08-31 at 20.45.07.png|435]]


##### CrashLoopBackOff

![[Screenshot 2026-08-31 at 20.47.42.png]]

to debug this we can try: 
- `kubectl describe pod_name` - check events at the bottom
- `kubectl get logs --previous`

##### Init Containers

![[Screenshot 2026-08-31 at 22.56.34.png]]

these run before any other Containers 

##### Sidecar Pattern

This is a helper container that runs alongside the main app
Both share the same Pod > same network and volumes 
extends functionality without modifying the main app

![[Screenshot 2026-08-31 at 23.03.20.png|417]]


##### Adapter Pattern

![[Screenshot 2026-08-31 at 23.06.29.png]]


##### Ephemeral Containers

 these are used for debugging. Temporary Containers. You inject the container into the pod
 
![[Screenshot 2026-09-01 at 21.56.11.png]]


QoS = Quality of Service - defines how the scheduler prioritises Pods during resource pressure

![[Screenshot 2026-09-01 at 22.11.53.png]]![[Screenshot 2026-09-01 at 22.14.21.png]]


##### Probes

Probes are health checks that run by the Kubelet to monitor container state. 

![[Screenshot 2026-09-01 at 22.17.05.png]]

![[Screenshot 2026-09-01 at 22.47.51.png|426]]

- LivenessProbe checks if the container is still Alive. If this doesnt pass the other probes wont run. 

##### Deployment Strategies

###### Rolling Update

![[Screenshot 2026-09-01 at 22.59.27.png]]

so at any stage of the update - you have a mix, old and new pods

you have two settings during this:
- maxSurge: This is how many extra pods can exist during the rollout. Default 25%
- maxUnavailable: This is how many pods can be down at once. Default 25%

###### Recreate
- All Existing Pods are killed first, then the new ones are created. 
- Causes downtime upgrade. 

this is useful when:
	 App cannot run multiple versions simultaneously
	 Shared storage conflicts between versions.


##### Deployment Rollbacks
- Deployments keep history of previous ReplicaSets
- You can rollback to an earlier revision when a rollout fails 
- K8s simply scales the old ReplicaSet back up. 

![[Screenshot 2026-09-01 at 23.14.19.png]]


##### Resource Requests & Limits

Every Container in K8s can specify: 
- requests - minimum guaranteed CPU/memory the container needs
- limits - maximum allowed CPU/memory it can use![[Screenshot 2026-09-01 at 23.16.23.png]]



##### Limit Ranges

![[Screenshot 2026-09-01 at 23.30.44.png]]