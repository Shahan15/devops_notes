This is AWS's managed DNS service - scalable, fully managed. 

You have full control of DNS records - also a domain registrar. 100% availability. 

So Route 53 directs traffic - its a switchboard - Each domain and subdomain you own it needs a record that tells Route 53 how to handle requests coming for it.
	 - Record Type - A --> Maps to a domain of an IPv4. AAAA ---> Maps to a domain of an IPv6 -- > Refer to: [[DNS]]
	 - Routing Policy: This is how you want Route 53 to respond to your queries. Like one domain points to one static resource. Or you can split incoming traffic across multiple servers. 
	 - TTL - amount of time the record is cached at DNS resolvers
		 - High TTL - e.g. 24 hours, possibly outdated records
		 - Low TTL - e.g. 60 sec, Better if you are updating servers frequently. But more traffic to Route 53 so more cost
		 - *Note: TTL is mandatory for each DNS record, besides Alias records**

![[Screenshot 2026-06-06 at 19.26.59.png|360]]

**CNAME VS Alias?**
- CNAME - this points a hostname to ANOTHER hostname. (app.mydomain.com => blabla.anything.com). Only for NON ROOT DOMAIN
- Alias - points a hostname to an AWS resource (app.mydomain.com => amazon.amazonaws.com). THIS WORKS FOR ROOT DOMAIN AND NON ROOT DOMAIN

**Alias Records Targets:** 
![[Screenshot 2026-06-06 at 19.34.36.png]]

##### Hosted Zones
- A hosted zone is a Container that Holds all records for a domain. Tells Route 53 how to route the traffic 
	- Public Hosted Zones - Contains records that specify how to route traffic on the internet. - so hence is good for a domain that will be accessible from internet
	- Private Hosted Zones - Contains records that specify how you route traffic within one or more VPC's

##### Routing Policies: 
- Defines how Route 53 responds to DNS queries. 
	- it doesn't direct traffic though - it is not a load balancer - it only responds to DNS queries. 

- Route 53 Supports the following Routing Policies: 
	- Simple - This simply returns the same IP address every time someone queries your Domain, or route traffic to a single resource
	- Weighted - Split traffic to different servers. Like 5% to Server A, 30% to Server B.
	- Failover - Route traffic to backup server if something goes wrong 
	- Latency Based - Route users to the server that responds the fastest - good if you have loads of servers across regions/globe 
	- Geolocation - Route traffic based on where user is located. Meaning you can show different content to different locations
	- Health Checks - Re-routes traffic based on health of your resources.
		 ![[Screenshot 2026-06-06 at 19.53.34.png]]
	- 
