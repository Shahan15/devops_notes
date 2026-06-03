Scalability means that an application/system can handle greater loads by adapting
There are two kinds of scalability: 
- Vertical Scalability - this is increasing or decreasing the power of a single resource. Common for non distributed systems e.g. Database
- Horizontal (elasticity) - this is when you add more instances to handle more load 

High availability means running your application / system in at least 2 data centres. (== Availability zone). Goal of this is to handle data centre loss. 


High Availability & Scalability for EC2:
- Vertical scaling would be increasing RAM, or CPU power 
- Horizontal would be adding more instances of EC2
- High Availability would be deploying the instance to multiple data centres. or across multiple Availability zone's. 
	- You would place a Load Balancer to distribute load across EC2 instances in the different AZ's. 

Reverse Proxy = Generic networking term. piece of software that handles traffic on behalf of a web server. It hides the IP addresses of servers and passes requests to them. 
	 Load balancing is a feature OF reverse proxy. and AWS ELB is a specific reverse proxy service. 

Load Balances are servers that forward traffic to multiple servers (e.g. EC2 Instances) downstream. This means traffic comes in and the ELB would decide where to direct that traffic. 
	 In AWS this is Elastic Load Balancer (ELB)
	 Load Balancers also do regular health checks and provide SSL termination - this means it decrypts encrypted traffic. 

Health check - this is done on a port and a route (/health is common) if the response is 200 (OK) then the instance is healthy.
	 If its unhealthy, the load balancer will stop sending traffic to it. 

ELB - This is a managed load balancer, its managed by AWS. costs less to set up your own buts its a lot of effort. 
Different types of load balancers offered by AWS: 
	![[Screenshot 2026-06-02 at 22.15.16.png]]

We also apply SG's to load balancers - we configure its inbound traffic and outbound rules. So then we configure out EC2 to ONLY accept traffic from the load balancer, so we don't accept any traffic from public.  

#### Application Load Balancer (ALB)

A Target Group is a logical bucket or "label" you create in AWS to group together identical servers.
	- **Target Group A** might contain 3 EC2 instances running your **Frontend Website**
	- **Target Group B** might contain 2 completely different EC2 instances running your **Payment API**.
	- **Target Group C** might contain Docker containers running your **User Search Service**.

Health checks are done at the target group level too - they check the health of the target group. if the resource is functioning as intended. 

ALB's can load balance to multiple HTTP applications across machines (target groups) - This means ALB can act as the smart router for your entire software ecosystem, splitting traffic up based on the actual URL path the user types in. - Modern web applications are broken down into smaller, independent mini-applications called **Microservices**.
  
ALB's function in the HTTP layer (layer 7) 
- This means that it understand whats going in the request itself. 
- It can also Load balancing to multiple application on the same machine (e.g. Containers)	  

Classic Load Balancer you would need one for each Microservice. 

**Extra info:**
- Each Load Balancer has a fixed host name - in the format: `XXX.region.elb.amazonaws.com` This URL is what client would use to access your services THROUGH the load balancer - Amazon provides this domain name for you - if you want custom you would use ***Route53*** --> another AWS service. 
- Requests to your services appear to come through the load balancer - this is the IP you will see, Load Balancer Private IP. To see the client IP this is passed in from a special header - 'X-Forwarded-For'
	- if you need the port another HTTP header would be provided 'X-Forwarded-Port' and protocol 'X-Forwarded-Proto' 

#### Network Load Balancer (v2) (NLB)

**All People Seem To Need Data Processing**
	 A - Application Layer 7
	 P - Presentation Layer 6
	 S - Session Layer  5
	 T - Transport Layer 4
	 N - Network Layer 3
	 D - Data Link layer 2
	 P - Physical Layer 1 

Operate in Layer 4 - Transport Layer

This NLB allows you to: 
- Allows you to handle millions of requests per second. 
- Less latency - 100ms (vs 400ms for ALB)
- Forward TCP & UDP traffic to your instances
- NLB has one static IP per AZ, supports assigning Elastic IP 
- not in the AWS free tier though


How does it work with TCP based traffic?

Recall: TCP (Transmission Control Protocol) - This is a protocol that includes a 'handshake' between devices. It establishes a connection between the devices before sending data. This ensures data is send in order and is actually received by the other end, good for security and data integrity

We set up the Rules - i.e. Allow certain ports or such. and when traffic comes in the NLB directs it to the appropriate target group. 
	 it doesn't inspect HTTP headers or handle SSL termination (decrypts HTTPS traffic) - this means that it cant route based on URL's like `/api or /login` 



######

Stick Sessions (Session Affinity)  - Ensures that all subsequent requests from a specific user during a session re consistently routed to the exact same backend server.  
Load Balancers usually distribute traffic evenly - Like request #1 goes to Server A, #2 to Server B etc. 
	 So for a duration of a visit, Sticky sessions maps a specific user's browser to a specific server backend for duration of their visit.
		 For example when you fill up your shopping cart on an e-commerce site you need the site to remember what was in your cart when you proceed to check out.
	 So this is done via the ALB leaving a 'sticky marker' (usually HTTP cookie). So every action done by the user henceforth is handled by one specific server. 
	 NLB's cannot read cookies (cant read HTTP headers) So it relies on ***Source IP Affinity***. It looks at your public IP address  and any traffic from that IP address is routed to Server A for example.




