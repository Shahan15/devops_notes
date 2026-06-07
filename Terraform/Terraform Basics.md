Terraform is a infrastructure as Code tool - this is basically deploying resources in cloud using code.  - Terraform is a CLI tool

Terraform is a cloud agnostic tool - meaning it can deploy to any cloud provider. 

IaC can be used with Version Control i.e. git
##### Infrastructure Orchestration vs Config Management: 

![[Screenshot 2026-06-07 at 14.51.42.png]]

IaC - So IaC deploy resources using the cloud provider API's, they build the environment. 

Config Management - This is to configure software and OS settings INSIDE an already EXISTING server.

So once IaC spins up an empty EC2 instance. the config management would log into the OS via `ssh` and run commands to turn it into a working web server (e.g. install Node.js, setting up Nginx, pulling application code etc.)


##### Tips for Using Terraform
- Terraform documentation 
- Terraform registry - public directory, used to share IaC assets. 
	- If you want Terraform to interact with a specific cloud provider, you can pull that from here. 
- Testing and Validation - very important as you can delete and create useless resources that will cost money
- Start with the MVP 
- apply DRY principles. 

##### Terraform State file 

Terraform state file `(terraform.tfstate)`- this is how Terraform manages your cloud infrastructure. it is a BLUEPRINT. - This holds all your dependencies, like the VPC's ID,  and holds a record of your existing infrastructure. Ensures **Idempotence**
	Idempotencey is the principle that no matter how many times you run an operation, the outcome remains the same. 

Desired vs Current state:
- Current State - is your up to date state file `(.tfstate)`
- Desired State `(.tf)`- this is your terraform config, it is your goal expressed as code. it is your declaration of how you want your cloud infrastructure to look, function, and connect when everything's built

$$\text{Desired State} - \text{Current State} = \text{Action Required}$$

Based on this Terraform will either Scale up, Scale down, cleanup

Note: We don't create the `.tfstate` file this is automatically created after the first `terraform apply` where all resources from the desired state is applied. 


##### Terraform Providers

This how Terraform actually is able to deploy resources.

A provider is just a plugin
Example: AWS
![[Screenshot 2026-06-07 at 15.54.19.png]]