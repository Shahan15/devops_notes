
Open Systems Interdisciplinary Reference Model. This is a communication model. Explains how data moves from one computer to another across a network. 

Universal blueprint for internet communication

Without these models, applications would need to understand the underlying network. Upgrading network equipment would be difficult. Innovations can happen in each layer without affecting the entire system

#### 7 Layers of the OSI Model

![[Screenshot 2026-05-20 at 13.49.13.png]]

mnemonic: 
    *"**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing"*


##### Layer 1: Physical Layer

This layers transmits raw bit streams over a physical medium. Meaning hardware like cables, hubs. This is like shouting in a room but no one can hear it i.e. No one to receive the data. This is solved by Layer 2

##### Layer 2: Data Link

Responsible for node to node data transfer. Organises the data. It puts your data into frames - this is like an envelope to send the data. This is done by switches and mac addresses

##### Layer 3: Network Layer

Determines how data is sent to the recipient. Manages packet forwarding, it decides the best path for data to travel through. Including routing through intermediate routers. 

Here data is organised into packets, which are little parcels that carry data from device to another. IP addresses handle where these packets go to. Routers direct the packets. 

##### Layer 4: Transport Layer

Responsible for providing reliable data transfer services to the upper layers. Segments and reassembles data: 
TCP and UDP.

##### Layer 5: Session Layer

Establishes, Maintains and terminates connections between applications. Sessions as in a login session

##### Layer 6: Presentation Layer

Syntax layer essentially. Translates data for application layer to understand. 

Like encryption and data formatting 

##### Layer 7: Application Layer

This is where the user is interacting. Browsing, file transfers and emails. 

protocols: HTTP, FTP, SMTP

#### TCP/IP Model

backbone of the internet. Condensed version of OSI model. 

![[Screenshot 2026-05-20 at 14.04.42.png]]


##### Layer 1: Application Layer

same as OSI model. this is where HTTP, DNS and such operate. 

##### Layer 2: Transport Layer

end to end communication happen here. protocols such as TCP and UDP operate here 

##### Layer 3: Internet Layer

responsible for logical addressing and routing data across different networks. IP operates here. IP handles delivery of the packets from the source to the destination across multiple networks. 

##### Layer 4: Network Access Layer

This is the physical and data processing together.  Ethernet, wireless, LAN



#### Example of OSI Usage: 

when a client sends a POST (create/update a resource) request to a HTTP web page. 

![[Screenshot 2026-05-20 at 14.16.53.png]]


![[Screenshot 2026-05-20 at 14.18.18.png]]