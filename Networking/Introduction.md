Network --> a group or more computer systems connected via cables, radio waves or satellites to exchange data.


LAN --> local area network. a group of devices connected to each other allowing share of information. 

WAN --> wide area network. connects multiple LAN's together 

#### Key Networking Components

switches --> Connect devices within the same network. manages data flow

Router --> Directs traffic between networks, connects different networks e.g. home nework (LAN) to the internet (WAN)

Firewall --> Protects network from unauthorised access, monitors and controls incoming & outgoing traffic

IP --> Unique identifier for devices on a network
	IPv4: example - 192.168.0.5 - 32 bit address. Most common
	IPv6: example - 2001 : 0db8.... - 128 bit address of four hexadecimal digits. 

IPv6 is important because we are running out of IPv4 addresses. it was introduced in 1980 and it provides 4.3 billion addresses. Currently we are using a Network Address Translation (NAT) system. This is when an internet provider provides a house one *single* public IPv4 address and splits this address amongst devices. 


MAC Address --> 48 bit address. Unique addresser assigned to a Network Interface Card (NIC) which allows your device to connect to a network. Operates at data link layer. 


##### Ports and protocols:

Ports --> Logical endpoints for communication. its like a door. Ports are virtual doorways inside an OS used to sort and route incoming network traffic to the correct program.
	**Port 80:** Standard web traffic (HTTP)
    **Port 443:** Secure web traffic (HTTPS)
    **Port 22:** Secure shell remote access (SSH)
    **Port 25:** Sending emails (SMTP)

often a port and IP address would be written together. this is called a **Socket**: 
`192.168.1.50:443`

443 being the port. 



Protocols --> Rules of governing data transmission. 


###### TCP (Transmission Control Protocol)

- Connection Orientated. Meaning a connection is made between the devices before any data is sent 
- Requires a 'handshake'. both devices agree to send and receive data
- reliable data transfer. data will be sent if not received on other end
- Ensures data is delivered in order 
- Error checking and flow control 
- Any bidirectional communication. 

###### UDP (User Datagram Protocol)

- Simple protocol to send and receive data
- No prior communication needed. Data sent immediately. but no guarantee
- Connectionless
- Fast but less reliable. Data sent one at a time
- Suitable for real time applications (e.g. video streaming, Online gaming)
- DNS 
- VPN
  










