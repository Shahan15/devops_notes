What is an Elastic Block Store (EBS) - is a network drive you can attach to your instances  
	 This is a virtual hard drive for your EC2 instances. It is a network attached block storage system. 
	 What this means is that upon server failure or something, its not wiped. you can just plug it into another instance. 

Amazon Machine Image (AMI) - it is a pre-packaged blueprint/template used to boot an EC2 instance up. It contains OS, pre-installed software, configs and permissions. You can choose specific AMI's for your needs. 
	- For example if you want to run a WordPress website, instead of booting a blank Linux server and spending hours installing PHP, MySQL, and WordPress manually, you can choose a "WordPress AMI". 
	 - You can also Create your own. Imagine you spend three hours configuring an EC2 instance: you patch the security settings, install your company's proprietary automation tools, download your code repositories, and tweak the network settings. You don't want to do that manually ever again.

Amazon EFS  - Elastic File System
- This is a managed, shared network file drive for our EC2 instances. Its like a OneDrive that different EC2 Instances can access. 
- It grows automatically. 
- expensive 