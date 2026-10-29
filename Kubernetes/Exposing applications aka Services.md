
Kubernetes services are like the connectors in your application - it makes sure everything that needs to talk CAN talk. e.g. Internal Pods or External resources. 

***Note: Services is a resource*** 

For example - you have groups of pods. One running the DB, another Frontend and another Backend. 

![[Screenshot 2026-10-27 at 21.59.23.png|383]]

How can services identify pods? --> Via labels. 

Different types of Services: 
- Cluster IPs - gives you a stable internal IP that your pods can use to talk to each other 
- Node Port - Exposes your service on a specific port on each node in your cluster. Simple way to make sure a service is accessible from outside cluster 
- LBs 


##### Cluster IP 

When you create a service with Cluster IP Kubernetes gives it a unique internal IP address called the Cluster IP 
- This is only reachable within the cluster. So if you need pods to communicate with each other but not be exposed to the outside world - use Cluster IP


##### Node Ports 

Thos builds upon Cluster IP and exposes your application to external traffic outside the cluster. It opens a Static port across every single worker node's IP address. Its also used when you dont need the full power of a load balancer

|**Port Field**|**YAML Key**|**What It Is**|**Who Uses It**|
|---|---|---|---|
|**NodePort**|`nodePort`|The external port opened on every cluster node (Range: `30000-32767`).|External clients communicating with the cluster.|
|**Service Port**|`port`|The internal virtual IP port exposed by the Service object within the cluster.|Internal pods or services trying to reach this service.|
|**Target Port**|`targetPort`|The actual port your container/application inside the Pod is listening on.|The application container running inside the Pod.|

So **Target port** is the port your actual application is listening to INSIDE the container. 

Service port is the internal virtual port for the Kubernetes Service itself. Inside the cluser Pods don't directly talk to each other. They talk to the Service internal IP address at this Service Port. 

Node port is a port on the outside of the physical (or virtual) machine RUNNING your cluster. 
	 here i was thinking why is it called Node Port? why not ClusterPort? because this is essentially the port of the Cluster our Nodes are running on? right? --> The reason is because a cluster is just a group of Nodes. NodePort exposes a port on EVERY SINGLE Node.  

Traffic has to hit a specific node. 


> [!NOTE] >  A Node is literally just a EC2 Instance or VM. It is NOT the Container or our App

Our container/app lives in a POD - which is a collection of containers.

So this is how traffic flows: 

$$\text{User Browser} \longrightarrow \text{Node IP} \mathbf{:30080} \text{ (NodePort)} \longrightarrow \text{Service IP} \mathbf{:80}\longrightarrow $$
$$ \longrightarrow \text{ (Service Port)} \longrightarrow \text{Pod IP} \mathbf{:8080} \text{ (Target Port)}$$

User hits the Node IP + Port. The Nodes `kube-proxy` catches that traffic on the **NodePort**
Then it passes the traffic to the Service's internal address on **Service Port (`80`)**
The Service Load Balances the request and forwards it to the **Container Port (`8080`)**


##### Load balancer 

This is a Service. This automatically provisions an external load balancer from a cloud provider. This will distribute traffic between your Pods. 