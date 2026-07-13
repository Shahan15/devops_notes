
For AWS Resources to communicate with other AWS Resources it usually has to traverse the public internet to hit an endpoint on the resource it wants to communicate with.  
	 If the resource is in a private subnet this can be done with adding a NAT gateway. However these are expensive 

the packet usually travels like this:
- **Inside VPC:** Instance $\to$ Route Table (Default route `0.0.0.0/0`) $\to$ **NAT Gateway**.
    
- **The "Internet" Hop:** The NAT Gateway translates your private IP to a public IP and sends the request out to the **Public Internet**.
    
- **The Destination:** The request travels over the public internet until it reaches the AWS public endpoint for that service.

However this is **expensive and slow**

When we use a VPC Endpoint we have two types: 
###### 1. If it's an Interface Endpoint (AWS PrivateLink)

Terraform instructs AWS to:
- **Provision an ENI:** AWS creates a "Virtual Network Interface" inside your specified subnet. This ENI gets a **private IP address** from your VPC's pool.
    
- **Update DNS:** If you enable "Private DNS," AWS automatically hijacks the standard public DNS name for that service (e.g., `sqs.eu-west-1.amazonaws.com`). Instead of resolving to a public IP, it resolves to the **private IP** of your new ENI.
    
- **The Result:** Your instance sends a request to what it _thinks_ is the public service, but the packet never leaves the VPC. It hits that ENI, and the AWS backbone network "steals" the traffic and routes it directly to the service within the internal AWS cloud.

###### 2. If it's a Gateway Endpoint (S3/DynamoDB)

Terraform instructs AWS to:

- **Update the Route Table:** It adds an entry to your route table that looks like this: `Destination: pl-123456 (S3 Prefix List) | Target: vpce-xxxxxxx`.
    
- **The Result:** When your instance tries to talk to S3, the VPC route table looks at the packet, sees it is destined for S3, and says, "Don't send this to the NAT Gateway! Send it straight to this special Gateway Endpoint object."

