# Real-World-Network-Architecture-and-Cyber-Security-Lab

## Objective

The Real World Network Architecture and CyberSecurity Lab aims to establish a controlled environment simulating and detecting cyber attacks, setup up and secure Routers, Switches using security best practices, User provisioning and deprovisioning, as well as other system administration responsibilities. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real world attack scenarios, perform system and network documentation. 

This hands-on experience was designed to deepen understanding of network security, Network architecture, attack patterns, and defensive strategies. 

### Skills Learned
- Advanced understanding of SIEM concepts and practical application.
- Proficient in analyzing and interpreting network logs.
- Enhanced knowledge of network protocols and security vulnerabilities
- Development of critical thinking and problem-solving skills in cybersecurity and networks.
- Proficient with cisco IOS to configure Routers and Switches

### Tools Used
- Security Information and Event Management (SIEM) system log ingestion and analysis.
- Network analysis tools (Wireshark, Advanced IP Scanner) for capturing and examining network traffic.
- Network Documentation (Packet Tracer)
- Firewall tool (Pfsense) for protecting the network.
- Cisco Router (csr1000v) for routing packets
- Windows 11 Ent Client for client machines
- Windows 2016 Core Server for issuing IP, dns and WINS configurations to client machines
- Windows 2016 GUI Server for managing the network (Router, Firewalls, and computers)

### Features
- VPN that is setup to be Point-to-Point.
- Active Directory Domain Service (Forest and Child Domain), Redundant Domain Controllers for Authentication, Authorization and Availability. 
- Pfsense Firewall and created Firewall Rules, blocking unnecessary ports.
- Routing rules Blocking specific Ip Addresses.
- Hyper-V Virtualization using Virtual Network Adapters to connect all Virtual Machines in this lab.

### Resources
https://techgiovanni1.imgur.com/all

## Steps
<p align="center">
<img src="https://i.imgur.com/IMgwPno.png"/>
<p>Ref 1: Network Diagram</p>
</p>
<p>The Final Network Architecture including (Security Operations Center, Attack Network, System Administration, Virtual Private Networks, Office & Corporate Envrironments, and the Intermediary Devices Cisco Router Csr1000v and Windows Routing)</p>


### Configuring the VPN IP Address
<p align="center">
<img src="https://i.imgur.com/vVH1zwR.png"/>
<p>Ref 13: Windows VPN just to setup PFsense-FW3</p>
</p>
<p>We ned an IP Address to communicate to other end-point devices. IN this case its the firewall. The default gateway is the Pfsense Firewall. The is directlt connected to the PFsense, so it is faster to configure it using this server than configuring the WDS01 and routers just to get to the Firewall to get internet.</p>

### Setup Pfsense-FW3 to get Internet Access on the Internal LAN
<p align="center">
<img src="https://i.imgur.com/DlwV84Y.png"/>
<p>Ref 2: Pfsense Firewall IP address setup</p>
</p>
<p>This allows up to get access to the Pfsense web interface to further do firewall configurations, rules and download packages.</p> 
<p>Our VPN server is directly connected to LAN 4, as well as the LAN interface side of the Pfsense-FW3. The WAN interface side of the Pfsense-FW3 is automatically getting a IP Address from the Internet Service Provider and using NAT to translate internal IP addresses into a single address for connecting out onto the internet.</p>

- 

### Pfsense-FW3 Initial Configurations Web Interface
<p align="center">
<img src="https://i.imgur.com/U5yhbFY.png"/>
<p>Ref 3: Setting DNS, and Domain</p> 
<img src="https://i.imgur.com/NBdm7o1.png"/>
<p>Ref 4: Setting the Timezone for my current location</p>
<img src="https://i.imgur.com/R5UVnDa.png"/>
<p>Ref 5: Updating Pfsense to its latest version to mitigate vulnerability in the software</p>
<img src="https://i.imgur.com/Jnlm3c0.png"/>
<p>Ref 6: Change the default PFsense web interface to use HTTPS instead of HTTP</p></p>

- 

### Pfsense-FW3 Setting up TCP & UDP Aliases and Firewall Rules to be able to access the internet on the LAN interface
<p align="center">
<img src="https://i.imgur.com/j6KCKA0.png"/>
<p>Ref 7: Creating a TCP group of Ports called an Alias to use for convenience instead of having single Port rules.</p>
<img src="https://i.imgur.com/cHjPxcT.png"/>
<p>Ref 8: Creating a UDP group Alias.</p>
<img src="https://i.imgur.com/Kc23syW.png"/>
<p>Ref 9: Using the TCP Aliase in a firewall Rule to Allow Traffic on these ports</p>
<img src="https://i.imgur.com/kjbqntR.png"/>
<p>Ref 10: Using the UDP Aliase in a firewall Rule to Allow Traffic on these ports</p>
<img src="https://i.imgur.com/BtdBC6y.png"/>
<p>Ref 11: Creating a Rule to Allow ICMP Traffic (Echo Request, Echo Reply, Destination Unreachable, Time Exceeded and Parameter Problem on the LAN Interface ) For pinging</p>
<img src="https://i.imgur.com/4wFJqW9.png"/>
<p>Ref 12: Reject ANY traffic that is not on the Allow Rules</p></p>






### Title
<p align="center">
<img src=""/>
<img src=""/>
<img src=""/>
<img src=""/>
<p>Ref 2: </p>
</p>
<p></p>
<p></p>
<p></p>














