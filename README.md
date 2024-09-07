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
- (Snort, Suricata, PfBlockNG) Security Information and Event Management (SIEM) system log ingestion, Analysis and Blocking Malicious IPs.
- Network analysis tools (Wireshark, Advanced IP Scanner) for capturing and examining network traffic.
- Network Documentation (Packet Tracer, GitHub)
- Firewall tool (Pfsense) for protecting the network.
- Cisco Router (csr1000v) for routing packets
- Windows 11 Ent Client for client machines
- Windows 2016 Core Server for DHCP, DNS and WINS IP configurations to client machines as well as Windows Server as a Router
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


### Configuring the VPN Server IP Address on LAN 4
<p align="center">
<img src="https://i.imgur.com/vVH1zwR.png"/>
<p>Ref 2: Windows VPN just to setup PFsense-FW3</p>
</p>
<p>We ned an IP Address to communicate to other end-point devices. IN this case its the firewall. The default gateway is the Pfsense Firewall. The is directlt connected to the PFsense, so it is faster to configure it using this server than configuring the WDS01 and routers just to get to the Firewall to get internet.</p>

### Setup Pfsense-FW3 to get Internet Access on the Internal LAN
<p align="center">
<img src="https://i.imgur.com/DlwV84Y.png"/>
<p>Ref 3: Pfsense Firewall IP address setup</p>
</p>
<p>This allows up to get access to the Pfsense web interface to further do firewall configurations, rules and download packages.</p> 
<p>Our VPN server is directly connected to LAN 4, as well as the LAN interface side of the Pfsense-FW3. The WAN interface side of the Pfsense-FW3 is automatically getting a IP Address from the Internet Service Provider and using NAT to translate internal IP addresses into a single address for connecting out onto the internet.</p>

- 

### Pfsense-FW3 Initial Configurations Web Interface
<p align="center">
<img src="https://i.imgur.com/U5yhbFY.png"/>
<p>Ref 4: Pfsense Web Interface for firewall configurations</p> 
<img src="https://i.imgur.com/U5yhbFY.png"/>
<p>Ref 5: Setting DNS, and Domain</p> 
<img src="https://i.imgur.com/NBdm7o1.png"/>
<p>Ref 6: Setting the Timezone for my current location</p>
<img src="https://i.imgur.com/R5UVnDa.png"/>
<p>Ref 7: Updating Pfsense to its latest version to mitigate vulnerability in the software</p>
<img src="https://i.imgur.com/Jnlm3c0.png"/>
<p>Ref 8: Change the default PFsense web interface to use HTTPS instead of HTTP</p></p>

- 

### Pfsense-FW3 Setting up TCP & UDP Aliases and Firewall Rules to be able to access the internet on the LAN interface
<p align="center">
<img src="https://i.imgur.com/j6KCKA0.png"/>
<p>Ref 9: Creating a TCP group of Ports called an Alias to use for convenience instead of having single Port rules.</p>
<img src="https://i.imgur.com/cHjPxcT.png"/>
<p>Ref 10: Creating a UDP group Alias.</p>
<img src="https://i.imgur.com/Kc23syW.png"/>
<p>Ref 11: Using the TCP Aliase in a firewall Rule to Allow Traffic on these ports</p>
<img src="https://i.imgur.com/kjbqntR.png"/>
<p>Ref 12: Using the UDP Aliase in a firewall Rule to Allow Traffic on these ports</p>
<img src="https://i.imgur.com/BtdBC6y.png"/>
<p>Ref 13: Creating a Rule to Allow ICMP Traffic (Echo Request, Echo Reply, Destination Unreachable, Time Exceeded and Parameter Problem on the LAN Interface ) For pinging</p>
<img src="https://i.imgur.com/4wFJqW9.png"/>
<p>Ref 14: Reject ANY traffic that is not on the Allow Rules</p></p>


### Install PFBlockerNG  
<p align="center">
<img src="https://i.imgur.com/SlOIRHd.png"/>
<p>Ref 15: </p>
<img src="blob:https://imgur.com/a6a816d3-ad6a-4b03-9aed-a91a0399524f"/>
<p>Ref 16: </p>
</p>
<p>PFBlocker assigns many Ip Address Url lists such as IBlock Lists into a single Alias and choosing a Rule action to block Counrties, DNS and IP Block list Ranges. </p>
<p>It aggregates several IP and DNS block lists into a single Alias that can be checked. </p>
<p>This Stops traffic before the DNS Name resolution is even complete. Reducing the processing.</p>


### Install Snort - An Intrusion detection system (IDS) and Intrusion Prevention System (IPS)
<p align="center">
<img src="https://i.imgur.com/SlOIRHd.png"/>
  <p>Ref 17: Installed Snort</p>
<img src="https://i.imgur.com/tl4391S.png"/>
<p>Ref 18: Snort Running on Both Interfaces WAN & LAN</p>
<img src="https://i.imgur.com/QPCjuUf.png"/>
<p>Ref 19: LAN Configuration of Snort</p>
<img src="https://i.imgur.com/aZMimrp.png"/>
<p>Ref 20: WAN Configuration in snort</p>
<img src="https://i.imgur.com/VTfsMOQ.png"/>
<p>Ref 21: Snort Global Configurations 1</p>
<img src="https://i.imgur.com/59Fd0pa.png"/>
<p>Ref 22: Snort Global Configurations 2</p>
<img src="https://i.imgur.com/kfnom77.png"/>
<p>Ref 23: Snort Global Configurations 3</p>
<img src="https://i.imgur.com/Yf7dP28.png"/>
<p>Ref 24: Create a Passlist on snort to allow your internal network to flow threw and not get blocked</p>
<img src="https://i.imgur.com/YuGSgbV.png"/>
<p>Ref 25: If you realize you dont have internet or you cant ping the firewall, you were maybe blocked.</p>
<p>Remove yourself from the block list buy just clicking the "x" on the right side. Now you should be able to ping and have internel access.</p>
<img src="https://i.imgur.com/SRVUHvv.png"/>
<p>Ref 26: Include the Pass list on the snort LAN interface</p>
</p>

<p>Snort does signature based and Protocol Based Detection</p>
<p>Snort shows alerts and Blocks suspected IP Addresses</p>




### Setup LANR1-4-6 (Windows Core Server as a LAN Router)
<p align="center">
  <p>sconfig</p>
  <p>Change the Computer Name</p>
  <p>Update the timezone if necessary</p>
  <img src="https://i.imgur.com/wtbEs0G.png"/>
  <p>Ref 27: Allow Remote Management and update the IP Adrdesses of Each INterface</p>
  <ul>
    <li>winrm Quickconfig</li>
    <li>set-netfirewallrule -Profile Public,Private,Domain -DisplayGroup "Windows Remote Management" -Enabled True</li>
  </ul>
  
  <img src="https://i.imgur.com/rQxMlxQ.png"/>
  <img src="https://i.imgur.com/d5mP42q.png"/>
  <p>Ref 28: Rename Net Adapter Name</p>
   <ul>
    <li>rename-Netadapter -name "Ethernet 2" -newname "LAN1"</li>
    <li>rename-Netadapter -name "Ethernet" -newname "LAN4"</li>
    <li>rename-Netadapter -name "Ethernet 3" -newname "LAN6"</li>
  </ul>

  <p>And then Set the IP Addresses for Each LAN Interface: </p>
  <ul>
    <li>new-netipaddress -InterfaceAlias LAN1 -Ipaddress 192.168.1.254 -PrefixLength 24</li>
    <li>new-netipaddress -InterfaceAlias LAN4 -Ipaddress 192.168.4.253 -PrefixLength 24 -DefaultGateway 192.168.4.254</li>
    <li>new-netipaddress -InterfaceAlias LAN6 -Ipaddress 192.168.6.254 -PrefixLength 24</li>
  </ul>

  <img src="https://i.imgur.com/uctHQJe.png"/>
  <img src="https://i.imgur.com/uctHQJe.png"/>
  <p>Ref 29: Set a default route for unknown destinations</p>
   <ul>
    <li>netsh interface ipv4 show interfaces</li> <p>Shows the Name and index </p>
    <li>netsh interface ipv4 add route 0.0.0.0/0 "LAN1" 192.168.4.254</li> <p>Set default route</p>
     <li>netsh interface ipv4 add route 0.0.0.0/0 "LAN6" 192.168.4.254</li> <p>Set default route</p>
    <li>route print</li> <p>Verify that the default route has been set correctly </p>
  </ul> 
  <p>Disable IP Version 6 on the Interfaces</p>
   <ul>
    <li>disable-NetAdapterBinding -Name LAN1 -ComponentID ms_tcpip6</li>
    <li>disable-NetAdapterBinding -Name LAN4 -ComponentID ms_tcpip6</li>
     <li>disable-NetAdapterBinding -Name LAN6 -ComponentID ms_tcpip6</li>
    <li>route print</li> <p>Verify that the default route has been set correctly </p>
  </ul> 
</p>

### Install The Router on the LANR1-4-6
<p align="center">
<img src="https://i.imgur.com/3KStiYR.png"/>
  <p>Ref 30: Add roles and Features to setup this Core server as a router</p>
<img src="https://i.imgur.com/UuF8qJ6.png"/>
<p>Ref 31: Choose Routing</p>
<img src="https://i.imgur.com/KhHxexz.png"/>
<p>Ref 32: Add REmote amangeemnt tools to the WDS01 Management and Devployment Server</p>
<img src="https://i.imgur.com/eAah4hk.png"/>
<p>Ref 33: Setup routing on the LANR1-4-6 Server. Custom Configuration and then LAN routing</p>
<img src="https://i.imgur.com/fDBw9wb.png"/>
<p>Ref 34: Setup Routing using Static routes, So packets can get through the router and onto the other side</p>
<img src=""/>
<p>Ref 35: </p>
<img src=""/>
<p>Ref 36: </p>
<img src=""/>
<p>Ref 37: </p>
<img src=""/>
<p>Ref 38: </p>
</p>

### Install Snort - An Intrusion detection system (IDS) and Intrusion Prevention System (IPS)
<p align="center">
<img src=""/>
<img src=""/>
<img src=""/>
<p>Ref 2: </p>
</p>
<p></p>
<p></p>
<p></p>






