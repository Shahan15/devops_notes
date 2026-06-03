also called SG's

These are fundamentals of network security in AWS. 

SG's control the traffic of whats allowed in or out of our EC2 instance 
	They only contain allow rules
	they are Stateful meaning - if you allow inbound traffic they automatically allow outbound traffic

these differ from traditional Firewalls (AWS Network Firewall) because: 
- SG's are stateful 
- SG's only have Allow rules
- Traditional Firewalls are basically guarding the entrance to the network, So any data that enters is first vetted, however this can be overwhelmed if too much data is being sent. SG's are rules you implement at the door to each EC2 instance. The Hypervisor controls all the EC2 instance, and this is what vets the data before it even reaches the door of the EC2 instance


**Note**:
When you boot up an EC2 instance, it isn't a physical computer; it’s a slice of software running on a massive physical host server. The master software that manages all these virtual slices on the physical hardware is called the **hypervisor** (AWS uses a custom one called Nitro).


Security groups regulate: 
- Access to Ports
- Authorised IP ranges 
- control of inbound network (from other to instance)
- Control of outbound network (from instance to other)

How do they actually work?

![[Screenshot 2026-06-02 at 16.30.46.png]]

You have to configure inbound and outbound rules. 


Security Groups good to know: 
- Can be attached to multiple instances
- Locked down to region/VPC combination
- Lives outside EC2 
- You should have separate SG for SSH access
- If your application is not accessible (time out), its a SG issue
- if application gives a "Connection refused" error, then its an application error or its not launched.
- All inbound traffic is blocked by default
- All outbound is authorised by default

what if you have an EC2 instance and you want to allow inbound traffic from other EC2 instances? 
	- Here you can what is called -*reference* - other SG's 
	![[Screenshot 2026-06-02 at 16.42.19.png]]


#### Classic Ports to Know

![[Screenshot 2026-06-02 at 16.44.24.png|308]]

#### Extra information
![[Screenshot 2026-06-02 at 16.53.42.png]]

When you stop and restart an EC2 instance it would be assigned a new public IP, public IP's are assigned dynamically. 
	 Elastic IP is a public IP you own as long as you don't delete it. You can attach it to one instance at a time
	 You get charged when it is NOT in use

You can get Elastic IP from AWS itself.

Why use Elastic IP?
- You can mask the failure of an instance or software by rapidly remapping the address to another instance in your account. 
However you can only have 5 elastic IP's (but can ask AWS to increase that)

avoid it when you can