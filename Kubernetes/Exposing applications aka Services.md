
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

Service is only reachable within the cluster




