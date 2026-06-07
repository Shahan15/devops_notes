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

you can store Statefile locally or remotely like a S3 or Terraform Cloud

##### How to use a S3 bucket to store a Statefile

We create a S3 Bucket as so: 
![[Screenshot 2026-06-07 at 19.31.59.png]]

and add it as backend in our desired.tf file

![[Screenshot 2026-06-07 at 19.30.37.png]]
##### Terraform Providers

This how Terraform actually is able to deploy resources.

A provider is just a plugin
Example: AWS
![[Screenshot 2026-06-07 at 15.54.19.png]]

we run the following commands: 
`terraform init` - initialises required plugins 
`terraform plan` - Represents our desired state, it shows you what terraform will be doing
	 ![[Screenshot 2026-06-07 at 16.09.03.png]]
`terraform apply` - This makes things happen, it deploys the code. 

`terraform destroy` - destroys all remote objects managed by a particular Terraform configuration. it deletes everything.


**Resource Block:** 
This defines a resource you want to manage in your terraform config
![[Screenshot 2026-06-07 at 16.17.32.png]]

`"aws_instance"` (The Resource Type) - This is a predefined keyword owned by AWS provider  --> it tells Terraform what kind of infrastructure to provision. in this case its a EC2 virtual server instance. 
`"Test` (The Local Resource Name) - Custom nickname we invent. 
`"ami"` (Amazon Machine Image) - tells AWS which OS to install in your EC2 instance. 


`Terraform import `- bringing existing resources into terraform management. 

Code block: 
![[Screenshot 2026-06-07 at 19.03.23.png]]![[Screenshot 2026-06-07 at 19.05.24.png]]



#####

`terraform Init` - Initialises a working directory containing terraform config files and downloads providers defined

`terraform validate` - Validates the terraform configuration files in the responsive directory. Makes sure they are syntactically valid and internally consistent 

`terraform plan` - creates an execution plan, it shows you all that will happen when you do `terraform apply`. compares your current state with desired state.

`terraform apply` - applies the plan. 


##### Variables

Variables in terraform are a way to parameterise your configurations. so instead of hardcoding values such ami, region etc. you can use variables - The normal stuff

Its like if we treat our `tf` file as a function. we can pass in Variables in the function. 

We have different types of Variables:

- **Input Variables** are the parameters passed _into_ the function (arguments).
    
- **Local Variables** are internal temporary variables used _inside_ the function to clean up repetitive logic (local scope variables).
    
- **Output Variables** are the return values passed _out_ of the function when it finishes running (return statements).


We would make a `variables.tf` file: 
This would be the Input variables

```Terraform
variable "server_size" {
  type        = string
  description = "The hardware footprint for our EC2 instances"
  default     = "t2.micro" # Optional fallback value
}

variable "environment" { type = string }
```

then in our main infrastructure files (e.g. `ect.tf`), we reference the variable using the prefix `var` followed by variable name: 

```Terraform
resource "aws_instance" "web" {
  ami           = "ami-06422669907866d20"
  instance_type = var.server_size # ◄ Variable injected here
}
```


We also use a `terraform.tfvars` - How does this work alongside the `variables.tf` file we make? 
`variables.tf` is like a blueprint 
`terraform.tfvars`is the pen we fill the blueprint out with. 

So for example in our `terraform.tfvars` we could have: 
```Terraform
instance_type = "t3.micro" 
environment = "production"
```
