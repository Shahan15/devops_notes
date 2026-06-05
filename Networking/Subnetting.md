Subnetting - dividing large networks into smaller manageable sub-networks 

CIDR - Classless Inter-Domain Routing 
This is a method for allocating IP Addresses and routing IP packets

Format: 
IP_address/prefix_length
192.168.1.0/24 

the /24 is the first 24 bits are the network path address 
#### Binary

101010

![[Screenshot 2026-05-22 at 16.31.28.png]]

Total = 42. 


IP Address to Binary

Example: 192.168.1.1

![[Screenshot 2026-05-22 at 16.32.56.png]]


#### Calculating Subnets

Subnetting essentially determines which part on the IP address is the *network portion* and which part is the *host portion.* 

Subnet mask - Defines network and host portions.
helps routers which part of an IP address is network and host 

![[Pasted image 20260522163854.png|405]]

- The difference between the Class's are is simply the scale.More devices can be connected. 

When a router looks at an IP address e.g. `192.168.1.1`, it looks at the subnet mask you gave it, to figure out what the 'neighbourhood' is.

each bit that is 'ON' i.e. 255. it means that the slot is locked and cannot change and every device you plug into that router, the device IP must start with those numbers. i.e for example if we apply Class C to an IP address then every device must start with 192.168.1

Only the last bit can change. The last bits remaining are the '***Host ID'*** 


192.168.1.0/26 

IP address has 32 switches (bits) inside it. 
![[Screenshot 2026-05-22 at 16.55.28.png]]

so 8 x 4 = 32.  (8 being each *bit*)

the /26 just mean the first 26 bits are ***locked*** for the network ID.

8 + 8 + 8 = 24 so we need to take 2 bits from the last block to get 26. so we have 6 switches (bits) left. 

so if we do we get $$2^6 = 64\text{ total combinations}$$
so we have 64 total IP addresses we can assign. 

192.168.1.0/26 


**Example 2:**
192.168.1.0/32 --> how many combinations does this have? 

so 32/8 = 4 

8 + 8 + 8 + 8 = 32. --> all switches filled. 
$$2^0 = 1\text{ total combinations}$$


**Example 3:**
192.168.1.0/24 --> How many combinations?

32-24 = 8 switch left 
$$2^8 = 256\text{ total combinations}$$




1) the Network Address is: `192.168.1.0`
2) Broadcast Address: This is the absolute **last address**. If a device sends data to this specific number, the data is automatically broadcasted to _every_ device on the street at the same time.- `192.168.1.63`
3) Usable IP Addresses: Everything between the Network Address and the Broadcast Address.`192.168.1.1` through `192.168.1.62`. so 62

#### NAT (Network Address Translation)

 Converts private IP's you have at home or office into a single public IP that can be used on the internet. - Done by the Router. 

this is because internet only understands private IP's

![[Screenshot 2026-05-22 at 17.05.51.png]]


**Types of NAT:** 

- Static NAT - Maps single private IP address to a single Public IP address 
- Dynamic NAT - not 1:1. maps a private IP address to one of many public IP's. 
- PAT (Port Address Translation) - Allows multiple private IP addresses to map to a single public IP address. 

So if: 

Shahan wants to Connect to www.google.com

Router translates private IP to public IP. 

Google sees the public IP


this conserves public IP address, enhances network security. Simplifies network management. 