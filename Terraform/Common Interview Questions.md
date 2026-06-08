- What is Terraform
	- Terraform is a open source infrastructure as code tool, so it lets you manage your infrastructure using code, such as deploying and configuring your resources. It is cloud agnostic and ensures idompotence.  

- What is the difference between Infrastructure orchestration and config management?
	- The difference here is that infrastructure orchestration is the literal management of your resources such as what resources you deploy like an EC2 instance, however config management is the OS inside it that you manage, so if you ssh into the EC2 instance and download core dependencies such as Node.js, Nginx etc

- What are the benefits of using IaC
	- IaC provides automation, consistency and repeatability in infrastructure management. it enables safer deployments.  

- What is the difference between terraform plan and terraform apply 
	- Terraform plan tells you what terraform apply will be doing. It compares your desired state with your actual state and sees what changes need to be implemented to achieve that state. Terraform apply, actually applies those changes and executes the plan

- What is a terraform provider
	- terraform provider is simply a plugin that interacts with api's of cloud providers and SaaS providers to manage resources i.e. AWS. 

- Explain the role of State in Terraform 
	- 