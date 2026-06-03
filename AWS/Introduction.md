#### Global Infrastructure 

AWS Regions - Regions AWS has data centres
	How to choose a region?
	 - Distance - you want something close to users to minimise latency
	 - Compliance with local laws on data and such 
	 - Price
	 - Available services within a region. New services and features are not available in every Region.

Availability Zone - Distinct, Isolated location within a region (UK South, UK North) that houses one or more data centres.  - but each zone has its own power and infrastructure. 

multiple Availability zones are connected together to form a **Region**. 


AWS Points of Presence (Edge Locations) (PoP) - these are part of AWS Content Delivery Network (CDN) - These are highly specialised data centre, specifically for getting content as physically close to end user as possible. These are caching servers and networking equipment. 

![[Screenshot 2026-05-30 at 21.47.39.png]]




ClickOps is like going into AWS console and manually creating everything - Can use **AWS CLI** - this allows you to make all the resources in the CLI 

**AWS SDK** - this is a package/library you can import to interact with AWS natively - SDK for different languages JS, Python etc

**Access Key** - used to authenticate **programmatic requests**:
 - **Access Key ID:** This is the public part of the pair. It acts like a **username**. It usually looks like a string of random uppercase letters (e.g., `AKIAIOSFODNN7EXAMPLE`).
    
- **Secret Access Key:** This is the private part of the pair. It acts like the **password**. It is a much longer string of mixed-case characters and symbols (e.g., `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`).

**IAM Roles For Services**
Some AWS Services will need to perform actions on your behalf like maybe an EC2 Instance needs to interact with an S3 Bucket or other aws services. we attach a role to the service. 

IAM Credentials Report (account-level) - A report that lists all your accounts user credentials

IAM Access Advisor (User-level) - Shows permissions granted to a user and when those services were last accessed 



AWS Lambda - Serverless Computer Service. allows you to run code without managing or scaling servers. 

S3 Bucket - Object Storage Service. Infinitely scalable, flat folder designed to store any type of file. 