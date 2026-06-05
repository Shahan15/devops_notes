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


