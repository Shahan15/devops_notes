
#### EC2

Elastic Compute Cloud - This is a VM. 
the elastic just means you are able to change size of your server/VM in terms of increase RAM or storage or whatever. 
	 ASG - Auto Scaling Group, scales EC2 automatically. If more traffic then ASG will automatically add more instances. 
	 ELB - Load Balancing, Distributes load across machine
	 You choose the OS, CPU power, RAM, Storage space, Firewall rules

When you launch an EC2 instance you can provide 'User Data' script.  - This is for bootstrapping the instance. 
	This means that you can launch commands as soon as a machine starts. Which is only run once. It runs with the root user - as in Root User in Linux now an AWS account. 

Different Types of EC2 Instances: 
- **General Purpose** 
- **Compute Optimised** - Extra CPU power for complex calculations, tasks that require a lot of processing  
- **Memory Optimised** - big data processes, 
- **Storage Optimised** - Large data sets, or need quick access to storage 
- **Accelerated Computing** - GPU heavy tasks, Machine learning 
- **HPC Optimised** - High performance Computing, Intensive computing tasks

Naming Conventions: 
`m5.2xlarge`

m - this is the type of instance i.e. m would be memory, C would be Compute Optimised etc

5 - generation of the instance. Each new generation is more powerful 

2xlarge - size within that instance class. the bigger the size the more resources i.e. CPU, RAM. the bigger the more expensive. 


on AWS we could see something like - `2t.micro` - 't' here means Burstable General Purpose 

![[Screenshot 2026-05-31 at 23.22.16.png]]



### 
ECS - Elastic Container Service - Allows management of Containers and lets you scale, monitor, deploy them easily. 
	 Kubernetes Does the exact same job they are competitors. 
	 But since K8 is so popular, amazon offers Elastic Kubernetes Service (EKS).

Lambda - Like Azure Functions. You can run code without worrying about infrastructure. usually for small pieces of codes or automation. AWS runs the code, scales and provides OS patches and such

