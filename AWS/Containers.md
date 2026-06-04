![[Screenshot 2026-06-04 at 01.23.03.png]]

Note: AWS Fargate - serverless compute engine for containers. Before if you wanted to run ECS or EKS then AWS made you manage the underlying EC2 instances that those containers sat on. Now with Fargate you hand AWS your docker image, tell it how much CPU and RAM you need and AWS will run it. 
	 its like serverless containers.


When you configure AWS ECS to run Docker containers, AWS will ask 'What is your Launch Type'
	 This is how you want to provision and manage the infrastructure that your containers will run on.

**IAM Roles for ECS:** 

These are roles you assign to a service. like a role you assign to a EC2 instance or ECS

EC2 instance profile (EC2 Launch Type only):
- Used by the ECS agent
- Makes API calls to ECS Service. 
- Send container logo to CloudWatch Logs.
- Pulls Docker images from ECR

ECS Task Role: 
- Allows each task to have a specific role 
- Use different roles for different ECS services you run
- Task role is defined in the task definition


**Load Balancer integrations with ECS:**

ALB - Supported and works for most use cases
NLB - Supported, for high throughput and low latency.
CLB - classic load balancer, still supported but not recommended. 


ASG is also supported with ECS. Scaling Strategies include: 
![[Screenshot 2026-06-04 at 16.38.03.png]]



##### EKS

Amazon Kubernetes Service. It is a way to launch and manage Kubernetes Clusters. 
	 This can also be used with Fargate. 

K8 can be used in any cloud. 