Domain Name Server - Converts domain names to IP addresses 

DNS has Two main components: 

#### Name Servers

Without this DNS wouldn't function. Name servers load: 
- configuration settings
- settings
- respond to queries from clients or other servers

two types of Name servers: 
- Authoritative - Hold the actual DNS records. when queried they provide a definitive answer. IP address and domain name 
  
- Recursive - Do not hold the final answer. they query the other name servers on behalf of the client to find correct DNS record. They also cache the info they retrieve to speed up future queries.  

for example if you want to know which Name servers google.com is hosted on you can do:

`dig ns google.com`

which would return: 
`ns2.google.com.
`ns1.google.com.`
`ns3.google.com.`
`ns4.google.com.`

#### Zone files 

- Stores information about the domain
- Organised and readable format![[Screenshot 2026-05-21 at 22.43.03.png]]

#### Records

a Zone file is comprised of multiple resource records. each record containing specific information about hosts. Some of the Components of a record: 

![[Screenshot 2026-05-21 at 22.45.05.png]]



DNS Record types:

![[Screenshot 2026-05-21 at 22.46.01.png]]

CNAME example: www.google.com --> google.com

MX --> handles emails sent to the domain. Points to a **mail server name** (e.g., `mail.google.com`) to catch your incoming emails.

TXT --> Used to prove you own the domain. 


### DNS Processes

Domain Resolution, DNS hierarchy, walking the DNS Tree

#### Domain Resolution

process of converting domain names to IP addresses. 

##### DNS Hierarchy and Distribution 

This is the entire engine. How it works from top to the end.  

1) DNS Root - **The Boss** - This is the top of the hierarchy. Does not store details about specific domain. Keeps high level info to find top level domains underneath it
   
2) Top level Domains (TLD) - **Department Head** - familiar extensions: ( .com ) ( .net ) ( .org ). Each TLD stores information about domains within its scope
   
3) Authoritative Name servers - **Managers** - they host zones for domains. They have detailed records for those domains. 
   
4) Domain - **employee** - Each domain has its own zone and zone file. Zone is like a team in the department, zone file is detailed list of record for that domain. Specific info such as IP address etc is stored here. 

![[Screenshot 2026-05-21 at 23.08.43.png]]


So when we type google.com into the browser what happens?

1) Browser sends request to ---> **DNS Resolver** - Runs a query and starts looking for the IP address. Checks local cache if not moves on
   
2) Even if its not in cache it queries the ---> **Root Server** - Has information about where to look for TLD (Top Level) i.e. the `.com` TLD server
   
3) TLD Server --> This doesn't have IP Address but knows which authoritative Server to ask 
   
4) This DNS Resolver queries the --> Authoritative Server - This sends back the IP to the DNS Resolver and back to the User.


You have **Domain Registrar** and **DNS Hosting Provider**

- Registrar - Allows you to buy and register a Domain e.g. goDaddy, Google Domains etc
  
- DNS Hosting provider - They run Authoritative Name servers, they hold the DNS records. e.g. Cloudflare, Route 53 (AWS)

can be same company such as Cloudflare, which it can provide both. 


### DNS tools 

`nslookup` - Basic DNS query tool 

```bash
nslookup google.com
```

```bash
dig google.com
```
  
dig is alot more details than nslookup 


##### /etc/hosts file 

- Local file on your computer
- Maps domain names to IP addresses 
- Computer checks here if IP address is listed here