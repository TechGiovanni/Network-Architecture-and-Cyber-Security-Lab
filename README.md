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

<h2>## Steps</h2>
<p align="center">
<img src="https://i.imgur.com/IMgwPno.png"/>
<p>Ref 1: Network Diagram</p>
</p>
<p>The Final Network Architecture including (Security Operations Center, Attack Network, System Administration, Virtual Private Networks, Office & Corporate Envrironments, and the Intermediary Devices Cisco Router Csr1000v and Windows Routing)</p>


<h2>Using the VPN Server on LAN 4 to setup Pfsense-FW3 that is directly connected to the internet</h2>
<h2>## Setup Pfsense to get Internet Access on the Internal LAN</h2>
<p align="center">
<img src="https://i.imgur.com/DlwV84Y.png"/>
<p>Ref 2: Pfsense Firewall IP address setup</p>
</p>
<p>This allows up to get access to the pPfsense web interface. Our VPN server is directly connected to LAN 4, as well as the LAN interface of the Pfsense-FW3 LAN interface. The WAN interface is automatically getting a IP Address from the Internet Srevice Provider and using NAT to translate internal addresses into a single address for connected out onto the internet.</p>

- 

<h2>Operating Systems Used </h2>


