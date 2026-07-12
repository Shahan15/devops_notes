
#### Cache Mounts

By default, a docker container is isolated. it doesn't have access to your hard drive. Also docker containers are ephemeral (temporary). So when a specific step in the `Dockerfile` is run, the temporary container instance is deleted and any temporary files are thrown away. 

a **Mount** is a bridge between these isolated instances and your hard drive. When we attach a mount we are telling docker write the files to this location in the hard-drive. This allows the files to exist even after the container is off. 

##### So how is this related?

When we run Go application. the code is compiled. it translates every line and saves these files (called `.a` files) into a local folder called `Compiler Cache` 

So when we run it a second time, with a mount attached - like for example if we change a print statement or something. Docker checks the local hard-drive sees the compiled code and packages and sees these haven't changed. so it uses that. 


#### AWS networking/Infrastructure how it all ties together

We have our image in ECR - Elastic Container Registry. This is just a repo to store your image

Then we have ECS Cluster - Elastic Container Service. Cluster just means 'grouping' for your container deployments. like you might have a cluster for production or staging etc. 
	 ECS makes you handle the infrastructure required to run the containers. 

For Serverless ECS we can use Fargate 

However to Run the ECS - We need a Task Definition - This is a JSON blueprint that tells Amazon HOW to run your Docker Containers - its like a docker-compose. 


##### ALB 

Next we have an Application Load Balancer - This Sits INFRONT of our ECS and it distributes traffic and allows different microservices to use the same URL and also balances traffic i.e. if you have multiple EC2 instances, makes sure one isnt getting all the traffic. 

###### So how is this relevant to our project?

Although we don't have different microservices such as frontend, backend since Go consumes the frontend assets into the backend and serves the frontend files directly. So Everything is in one container.

Here ALB functions as a way to ensure High Availability. We would run multiple copies of that One container. So if there is loads of traffic the ALB will distribute the traffic to the identical containers. 
It also handles SSL/TSL termination - https

##### Security Group

We place security group to allow inbound traffic from port 80/443 (Http/Https)

##### Route 53

This is AWS's managed DNS service - scalable, fully managed.  

Here we will point our domain to the ALB.  So our user hits Route53 when they type in the Domain and then that will redirect to our ALB. 

##### ACM Certificate

AWS Certificate Manager - this is a managed SSL/TSL certificate provided by Amazon. 

We will attach ACM certificate to our ALB for HTTPS.

##### WAF vs SG's

WAF - Web Application Firewall 

So SG's sit INFRONT of the ALB , they decide what traffic is allowed in and out. They specifically look at IP Addresses, ports and protocols. 
*Note: We don't apply SG to the VPC itself, we apply the SG to the resource itself. Hence that why its attached to the ALB  

a WAF sits INFRONT of the resource, they inspect the HTTP/HTTPS Headers, cookies, query strings and request bodies. 

Traffic flow goes as follows: 
1. The Edge (WAF): Traffic hits your public endpoint first - like an ALB, then WAF intercepts this request and reads the HTTP Headers and body, if it sees an SQL injection it drops the request. 
2. The Security Group: if WAF says request is clean, the traffic moves forward to the SG, this evaluates if it the protocol and port is allowed. 
3. then the traffic reaches the application code/endpoint/target group

##### VPC Endpoints
So normally for resources to talk to services outside of its private subnet, it has to travel through the public internet, via a NAT gateway and then hit the AWS service endpoint. 
	 This introduces security risks, and NAT gateway is expensive to run.

so what do we do instead? 
we use AWS PrivateLink - This places an Elastic Network Interface (ENI) - essentially a virtual network card with a private IP address - this is directly in the private subnet.  but this is for the Resource itself. so we provide the ENI to the ECS inside the Private subnet 

So When lets say your ECS Service wants to pull new image from ECR, then AWS would update your local VPC DNS. Application will send a request to ECR using its private IP address inside its own subnet. the ENI will then route the traffic to ECR across AWS's private backbone. 

*Note: ECR images are actually hosted in an S3 Bucket behind the scenes.* 

The way ECR works under the hood is that it has two endpoints: 
1) API Endpoint (`.ecr.api`) - this checks your IAM permissions, authenticates your ECS Task and verifies the repo actually exists. 
2) The Docker Registry Endpoint (`.ecr.dkr`) - this is what initiates the docker pull, this is all the heavy lifting. 

However as noted, the ECR images are actually hosted in an S3 bucket behind the scenes, so you also need an S3 Gateway Endpoint. otherwise the Docker Registry Endpoint wont be able to actually see the S3 bucket and get the image. 



##### Route Tables
So lets say my EC2 instance is in my private subnet. i want it to send some data to store in a S3. It checks the subnet Route tables to see where its allowed to send data. if its 0.0.0.0/0 it means it can freely send data over public internet (via a NAT gateway or internet Gateway). if its the same as our VPC then it means it cant send data outside the VPC. 

Every packet looks at its subnet Route Table and sees where the subnet can/is able to route data to. 



##### IAM 

IAM encompasses IAM Roles and IAM Users - Users is actual users for humans to use with set permissions. 

IAM Task Roles - These are roles you assign tasks so they can execute tasks on your AWS account. Like if an ECS service wants to spin up a container, it needs permission to do that because by default it is not allowed to just do that. 

when we make an IAM Role - this is empty and useless till we attach a policy which actually provides the permissions we want to provide to the role. So always remember ROLE + IAM POLICY + IAM ROLE POLICY ATTACH
	 so we create the role --> Create the policy --> attach the policy. 




