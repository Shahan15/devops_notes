Amazon VPC - Virtual Private Cloud

CIDR - Classless Inter-Domain Routing. 
This is a method for allocating IP Addresses and routing IP packets

Format: 
IP_address/prefix_length
192.168.1.0/24 

the /24 means the first 24 bits are the network path address 
	 The smaller this number is the larger the range of IP's

![[Screenshot 2026-06-05 at 14.44.48.png]]


Refer to [[Subnetting]]

Example: 198.168.0.0/16 --> how many combinations does this allow

32 - 16 = 16 
$$2^{16} = 65536\text{ total combinations}$$

**Public vs Private IP (IPv4)**

![[Screenshot 2026-06-05 at 15.05.21.png]]


**Default VPC Walkthrough**
- All AWS accounts have a default VPC. 

![[Screenshot 2026-06-05 at 15.08.00.png]]

Subnet - This is smaller network within your VPC. However these can be public or private. 
	 - AWS reserves 5 IP addresses in each subnet and are not available for use. 
		 - This means if you make a CIDR of /28 which would give you 16 combinations. 5 of those are reserved by AWS 
	It is for the following reasons:![[Screenshot 2026-06-05 at 15.14.10.png]]


**Internt Gateway (IGW)**
- This allows resources in a VPC to connect to the internet - This scales horizontally meaning its highly available and redundant 
- This is Attached to your VPC - you have to create it separately. 

#### **Bastion Host**

This is a highly secure, specialised server used as a single, controlled entry point to access private servers inside a network. 

The problem it solves: 
When you set up a cloud network (AWS VPC), you have your: 
- Public Subnet: Accessible from internet
- Private Subnet: Hidden from internet (actual application server, databases, backend)

So if you want to do maintenance, or deploy code you cant **SSH** into them from your personal computer or at the office. - This is because they private Subnet does not even have a public IP. 

 ##### **How a Bastion Host Works:**
 
Instead of exposing all your backend servers, you deploy **one single, hardened EC2 instance** inside the **Public Subnet**. This is your Bastion Host.

When you need to access a private database or application server, the process looks like this:

1. **Step 1:** You connect (via `SSH`) from your laptop to the **Bastion Host** in the public subnet.
    
2. **Step 2:** Once you are safely inside the Bastion Host, you initiate a second `SSH` connection from that bastion server over the internal private network to the **Private Server**.

Because you "jump" from the bastion to the private backend, the bastion host acts as a middleman


##### NAT Gateway

NAT - Network Address Translation

Allows your instances in a private subnet to connect to the internet. - However it only lets the servers **OUTGOING** traffic. but Completely blocks any **INBOUND** traffic

NAT Gateway is AZ specific.  - it is highly available but only in a AZ.
	 This poses an issue, if it the AZ goes down the application would go down as any instances inside the private subnet would be unable to send any outgoing data. 
	 So you have to deploy multiple NAT Gateways where your instances are also hosted. like if you have your instances Hosted in multiple AZ's

![[Screenshot 2026-06-05 at 15.29.45.png]]


##### NACL 
Network Access Control List ( NACL)

This is like a firewall which control traffic from and to subnets.
![[Screenshot 2026-06-05 at 15.34.21.png]]

