# Network-Architecture-and-Cyber-Security-Lab

## Objective

This Real-World Network Architecture and CyberSecurity Lab aims to establish a controlled environment simulating and detecting cyber attacks, setup up and secure Routers, Switches using security best practices, User provisioning and deprovisioning, as well as other system administration responsibilities. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real world attack scenarios, perform system and network documentation. 

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
  <p>Ref 1: Network Diagram</p>
  <img src="https://i.imgur.com/AGCxfPS.png"/>
  <p>Ref 2: Hyper-V Manager - Hosting all of the Virtual Machines used in this Project</p>
  <img src="https://i.imgur.com/PImBLSe.png"/>
</p>
<p>The Final Network Architecture including (Security Operations Center, Attack Network, System Administration, Virtual Private Networks, Office & Corporate Envrironments, and the Intermediary Devices Cisco Router Csr1000v and Windows Routing)</p>


### Configuring the VPN Server IP Address on LAN 4
<p align="center">
  <p>Ref 3: Windows VPN Server on LAN 4 to setup the PFsense-FW3</p>
  <img src="https://i.imgur.com/vVH1zwR.png"/>
</p>
<p>We ned an IP Address to communicate to other end-point devices. IN this case its the firewall. The default gateway is the Pfsense Firewall. The is directlt connected to the PFsense, so it is faster to configure it using this server than configuring the WDS01 and routers just to get to the Firewall to get internet.</p>


-

# Setup Pfsense-FW1 to get Internet Access on the Internal LAN
<p align="center">
  <p>Ref 4: Pfsense Firewall IP address setup</p>
  <img src="https://i.imgur.com/DlwV84Y.png"/>
</p>
<p>This allows up to get access to the Pfsense web interface to further do firewall configurations, rules and download packages.</p> 
<p>Our VPN server is directly connected to LAN 4, as well as the LAN interface side of the Pfsense-FW3. The WAN interface side of the Pfsense-FW3 is automatically getting a IP Address from the Internet Service Provider and using NAT to translate internal IP addresses into a single address for connecting out onto the internet.</p>

- 

## Pfsense-FW1 Initial Configurations Web Interface
<p align="center">
  <p>Ref 5: Pfsense Web Interface on HTTP</p> 
  <img src="https://i.imgur.com/ChTG5rB.png"/>
  <p>Ref 6: Pfsense Web Interface for firewall configurations - Setting DNS, and Domain</p> 
  <img src="https://i.imgur.com/U5yhbFY.png"/>
  <p>Ref 7: Setting the Timezone for my current location</p>
  <img src="https://i.imgur.com/NBdm7o1.png"/>
  <p>Ref 8: Updating Pfsense to its latest version to mitigate vulnerability in the software</p>
  <img src="https://i.imgur.com/R5UVnDa.png"/>
  <p>Ref 9: Change the default PFsense web interface to use HTTPS instead of HTTP</p>
  <img src="https://i.imgur.com/Jnlm3c0.png"/>
  </p>

- 

## Pfsense-FW1 Setting up TCP & UDP Aliases and Firewall Rules to be able to access the internet on the LAN interface
<p align="center">
  <p>Ref 10: Creating a TCP group of Ports called an Alias to use for convenience instead of having single Port rules.</p>
  <img src="https://i.imgur.com/j6KCKA0.png"/>
  <p>Ref 11: Creating a UDP group Alias.</p>
  <img src="https://i.imgur.com/cHjPxcT.png"/>
  <p>Ref 12: Using the TCP Aliase in a firewall Rule to Allow Traffic on these ports</p>
  <img src="https://i.imgur.com/Kc23syW.png"/>
  <p>Ref 13: Using the UDP Aliase in a firewall Rule to Allow Traffic on these ports</p>
  <img src="https://i.imgur.com/kjbqntR.png"/>
  <p>Ref 14: Creating a Rule to Allow ICMP Traffic (Echo Request, Echo Reply, Destination Unreachable, Time Exceeded and Parameter Problem on the LAN Interface ) For pinging</p>
  <img src="https://i.imgur.com/BtdBC6y.png"/>
  <p>Ref 15: Reject ANY traffic that is not on the Allow Rules</p>
  <img src="https://i.imgur.com/4wFJqW9.png"/>
</p>


# Install PFBlockerNG  
<p align="center">
  <p>Ref 16: Install PFBlockerNG Package</p>
  <img src="https://i.imgur.com/rPFW2W6.png"/>
  
  <p>Ref 17: The DNS Url and IP Address Block list created by PFBlockerNG</p>
  <!--  <img src="blob:https://imgur.com/a6a816d3-ad6a-4b03-9aed-a91a0399524f"/> -->
  <img src="https://i.imgur.com/ogXgVfw.png"/>
  <p>PFBlocker assigns many Ip Address Url lists such as IBlock Lists into a single Alias and choosing a Rule action to block Counrties, DNS and IP Block list Ranges. </p>
  <p>It aggregates several IP and DNS block lists into a single Alias that can be checked. </p>
  <p>This Stops traffic before the DNS Name resolution is even complete. Reducing the processing.</p>
</p>



# Install Snort - An Intrusion detection system (IDS) and Intrusion Prevention System (IPS)
<p align="center">
  <p>Ref 18: Installed Snort</p>
  <img src="https://i.imgur.com/SlOIRHd.png"/>
  <p>Ref 19: Snort Running on Both Interfaces WAN & LAN</p>
  <img src="https://i.imgur.com/tl4391S.png"/>
  <p>Ref 20: LAN Configuration of Snort</p>
  <img src="https://i.imgur.com/QPCjuUf.png"/>
  <p>Ref 21: WAN Configuration in snort</p>
  <img src="https://i.imgur.com/aZMimrp.png"/>
  <p>Ref 22: Snort Global Configurations 1</p>
  <img src="https://i.imgur.com/VTfsMOQ.png"/>
  <p>Ref 23: Snort Global Configurations 2</p>
  <img src="https://i.imgur.com/59Fd0pa.png"/>
  <p>Ref 24: Snort Global Configurations 3</p>
  <img src="https://i.imgur.com/kfnom77.png"/>
  <p>Ref 25: Create a Passlist on snort to allow your internal network to flow threw and not get blocked</p>
  <img src="https://i.imgur.com/Yf7dP28.png"/>
  <p>Ref 26: Snort Pass List</p>
  <img src="https://i.imgur.com/vmdDGJz.png"/>
  <p>Ref 27: If you realize you don't have internet or you can't ping the firewall, you were maybe blocked.</p>
  <img src="https://i.imgur.com/YuGSgbV.png"/>
  <p>Remove yourself from the block list by just clicking the "x" on the right side. Now you should be able to ping and have internel access.</p>
  <p>Ref 28: Include the Pass list on the snort LAN interface</p>
  <img src="https://i.imgur.com/SRVUHvv.png"/>
  <p>Snort does signature based and Protocol Based Detection</p>
  <p>Snort shows alerts and Blocks suspected IP Addresses</p>
</p>






# Setup LANR1-4-6 (Windows Core Server as a LAN Router)
<p align="center">
  <p>sconfig</p>
  <p>Change the Computer Name</p>
  <p>Update the timezone if necessary</p>

  <p>Ref 29: Allow Remote Management and update the IP Adrdesses of Each INterface</p>
  <img src="https://i.imgur.com/wtbEs0G.png"/>
  <ul>
    <li>winrm Quickconfig</li>
    <li>set-netfirewallrule -Profile Public,Private,Domain -DisplayGroup "Windows Remote Management" -Enabled True</li>
  </ul>
</p> 

<p align="center">
  <p>Ref 30: Rename Net Adapter Name</p>
  <img src="https://i.imgur.com/rQxMlxQ.png"/>
  <img src="https://i.imgur.com/d5mP42q.png"/>
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
</p>

<p align="center">
  <p>Ref 31: Setting up default routes for unknown destinations for LAN 1 and LAN 6</p>
  <img src="https://i.imgur.com/uctHQJe.png"/>
  <img src="https://i.imgur.com/uctHQJe.png"/>
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
<br>

# Install The Remote Access (Routing) Roles and Feature on the LANR1-4-6
<p align="center">
  <p>Ref 32: Add roles and Features to setup this Core server as a router</p>
  <img src="https://i.imgur.com/3KStiYR.png"/>
  <p>Ref 33: Choose The Role for "Routing"</p>
  <img src="https://i.imgur.com/UuF8qJ6.png"/>

# Add the Administration Roles and Features to WDS01 Mangement Server
  <p>Ref 34: Add Remote management tools to the WDS01 Management and Deployment Server</p>
  <img src="https://i.imgur.com/KhHxexz.png"/>

# Access and Finish Setting up The Remote Access (Routing) Roles and Feature on the LANR1-4-6
  <p>Ref 35: Setup routing on the LANR1-4-6 Server. Choose "Custom Configuration" and then "LAN Routing"</p>
  <img src="https://i.imgur.com/eAah4hk.png"/>
  <p>Ref 36: Setup Static Routes, So packets can get through the router and onto the other side</p>
  <img src="https://i.imgur.com/fDBw9wb.png"/>
</p>

# Cisco Router CSR1000v
### Setup Cisco Router - IP Addresses, Passwords, usernames, SSH, ACLs
<p align="center">
  <p>Ref 37: Setup the IP Addresses for (GigabitEthernet1) LAN1 and (GigabitEthernet2) LAN 5 Interfaces on the Router</p> 
  <img src="https://i.imgur.com/9UsbIUx.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 38: Setup Passwords for enable mode</p>
  <img src="https://i.imgur.com/IVVKL3w.png"/>
  <p>Also encrypt the plain text passwords on running-config using "service password-encryption"</p>
</p>

<p align="center">
  <p>Ref 39: Setup Line VTY (Virtual Teletype) </p>
  <img src="https://i.imgur.com/3lkZmqD.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 40: Created usernames and passwords</p>
  <img src="https://i.imgur.com/eQuUaji.png"/>
  <p> for those users using the password policy for string passwords and over 20 characters and only allow username and password to login</p>
</p>

<p align="center">
  <p>Ref 41: Setup SSH on the Router</p>
  <img src="https://i.imgur.com/09DQ8ep.png"/>
  <p>SSH allows for encryted traffic in both directions for confidentiality</p>
</p>

<p align="center">
  <p>Ref 42: Setup Static Routes</p>
  <img src="https://i.imgur.com/52QHTjL.png"/>
  <p>Allows for communication with the other Networks in our infrastructure.</p>
</p>

<p align="center">
  <p>Ref 43: Cisco Routing table with A Static Route for unknown destinations "Last Resort"</p>
  <img src="https://i.imgur.com/FXIZFq6.png"/>
</p>

<p align="center">
  <p>Ref 44: Setup ACLs</p>
  <img src="https://i.imgur.com/b2NRtpo.png"/>
  <p> This was setup for the furture in case of malicious IP on the network that needs to be blocked. To mitigate risk.</p>
</p>


# Setup Pfsense-FW2


<p align="center">
  <p>Ref 45: Pfsense copyright Acceptance to accept</p>
  <img src="https://i.imgur.com/Flk62PP.png"/>
  <p>Ref 46: Installation of Pfsense</p>
  <img src="https://i.imgur.com/QTOKHDh.png"/>
</p>

<p align="center">
  <p>Ref 47: Choose Manual Disk Setup (experts) </p>
  <img src="https://i.imgur.com/OnTuIOV.png"/>
  <p>This method is the only one that works so far while using Pfsense.</p>
</p>


<p align="center">
  <p>Ref 48: Auto Disk setup</p>
  <img src="https://i.imgur.com/ogc87Fx.png"/>
  <p>This created three partitions (da0p1 da0p2, da0p3)</p>
</p>

<p align="center">
  <p>Ref 49: Commit these changes</p>
  <img src="https://i.imgur.com/Qa66xrZ.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 50: Extracting the files and installing them on the disk.</p>
  <img src="https://i.imgur.com/izkp3AJ.png"/>
</p>

<p align="center">
  <p>Ref 51: Installation of Pfsense is Complete</p>
  <img src="blob:https://imgur.com/8be6885e-692d-4b64-85a2-74abafdfd8ce"/>
  <p>After the installation is complete we will go to the shell.</p>
</p>

<p align="center">
  <p>Ref 52: Halt Pfsense</p>
  <img src="https://i.imgur.com/CCX6Z3l.png"/>
  <p>We need some tiem to remove the ISO before Pfsense Reboots, Otherwise we will get the screen to Install Pfsense again.</p>
  <p>Eject the Pfsense ISO disk at this time.</p>
  <p>After ISO is ejected. CLick any key to continue with the reboot.</p>
</p>

<p align="center">
  <p>Ref 53: Pfsense Initial Screen after reboot</p>
  <img src="https://i.imgur.com/t2yOlUV.png"/>
  <p>Only the default LAN ip address is setup. We will change this to our internal IP Addresses.</p>
</p>

<p align="center">
  <p>Ref 54: WAN interface IP Address setup</p>
  <img src="https://i.imgur.com/GbtZ4Yg.png"/>
  <p>This is pointing to the internet</p>
</p>

<p align="center">
  <p>Ref 55: Setup the LAN and WAN Ip Addresses</p>
  <img src="https://i.imgur.com/5W4GMNx.png"/>
  <p>Now we will have access to the Pfsense web interface from within the LAN network that is directly connected</p>
</p>


# Create a Windows Desktop Virtual Machine to finish configuring the PFsense-FW2
<p align="center">
  <p>Ref 56: </p>
  <img src="https://i.imgur.com/JD55gaF.png"/>
  <p>The configuration process will be the same as Pfsense-FW2 expect for the IPS/IDS system</p>
  <p>Then we will setup Active Directory, DHCP,DNS and WINS Server. then add a redundant DC02 controller for Availability purposes.</p>
</p>

## PFsense-FW2 WAN interface Rule Update
<p align="center">
  <p>Ref 57: Updating the Firewall TCP Alias to include Active directory ports on the LAN</p>
  <img src="https://i.imgur.com/Ep2UM28.png"/>
  <p>Updating the Firewall rule to allow Active Directory Services Inbound on TCP ports on the WAN interface</p>
</p>

<p align="center">
  <p>Ref 58: Updating the Firewall UDP Alias to include Active directory ports on the LAN</p>
  <img src="https://i.imgur.com/o19qfEz.png"/>
  <p>Updating the Firewall rule to allow Active Directory Services Inbound on TCP ports on the WAN interface</p>
</p>

<p align="center">
  <p>Ref 59: Created the Randomly allocated port used by Active Directory to use inside of TCP_Standard_Outbound</p>
  <img src="https://i.imgur.com/PvTqcKu.png"/>
</p>

The use of both a main firewall connected to the internet and an internal firewall within a network serves to enhance security through multiple layers of protection. Here’s a breakdown of their roles:

Main Firewall (Perimeter Firewall):

Purpose: Acts as the first line of defense between the external world (the internet) and your internal network.
Functions:
Traffic Filtering: Monitors and controls incoming and outgoing traffic based on predefined security rules, allowing or blocking traffic based on IP addresses, ports, and protocols.
Attack Prevention: Protects against external threats such as DDoS attacks, malware, and unauthorized access attempts.
VPN Termination: Often handles VPN connections for remote users or branch offices.
Network Address Translation (NAT): Hides internal IP addresses from external entities and translates them into public addresses.
Internal Firewall (Internal or Layer 2/3 Firewall):

Purpose: Provides additional security within the internal network, protecting different segments or departments from each other.
Functions:
Segmenting the Network: Divides the network into segments (e.g., by department, sensitivity level, or function) to limit the spread of threats within the network.
Access Control: Enforces policies for traffic between different internal segments, ensuring that only authorized users and devices can communicate across boundaries.
Monitoring and Logging: Tracks internal network activity and detects unusual patterns or potential threats that might not be visible to the perimeter firewall.
Threat Containment: Helps in isolating compromised systems or preventing lateral movement by attackers within the network.
Benefits of This Dual Firewall Approach:

Defense in Depth: By having multiple layers of security, you reduce the risk of a single point of failure. Even if an attacker bypasses the perimeter firewall, the internal firewall can still offer protection.
Granular Control: Internal firewalls allow for more precise control of traffic between different segments of your network, which is useful for implementing strict security policies and minimizing risks.
Reduced Impact of Breaches: In the event of a security breach, internal firewalls can limit the scope of damage by preventing attackers from easily moving within the network.
Compliance and Best Practices: Many regulatory frameworks and security best practices recommend or require the use of multiple layers of firewalls and network segmentation.
In summary, the main firewall secures the boundary between the external internet and your internal network, while the internal firewall enhances security within the network, providing additional control and segmentation. This layered approach helps in building a more resilient and secure network infrastructure.

# Active Directory Domain Services
<p align="center">
  <p>Ref 60: DC01 IP Address configuration </p>
  <img src="https://i.imgur.com/K80njvT.png"/>
</p>

<p align="center">
  <p>Ref 61: DC01 remove ipv6 binding and allow remote management from the firewall</p>
  <img src="https://i.imgur.com/YSCkv9i.png"/>
</p>

<p align="center">
  <p>Ref 62: Added DC01 to Server Manager</p>
  <img src="https://i.imgur.com/6ZNUMp5.png"/>
</p>


<p align="center">
  <p>Ref 63: Install Active Directory DS  and DNS Roles</p>
  <img src="https://i.imgur.com/fa5C91p.png"/>
</p>


<p align="center">
  <p>Ref 64: Created a new forest</p>
  <img src="https://i.imgur.com/oPqWsit.png"/>
  <p>Promote ot Domain Controller</p>
</p>


<p align="center">
  <p>Ref 65: Removing ipv6 and updating DNS</p>
  <img src="https://i.imgur.com/4LvayDO.png"/>
  <p>After successful Installation of ADDS update the ip configuration removing ipv6 and updating DNS</p>
</p>

<p align="center">
  <p>Ref 66: Join the Domain from the WDS01 VM</p>
  <img src="https://i.imgur.com/ibUkgC9.png"/>
</p>


## DNS Configuration
<p align="center">
  <p>Ref 67: Setup DNS Server REverse Lookup Zones</p>
  <img src="https://i.imgur.com/Mpbu533.png"/>
</p>

## Install DHCP and WINS ROles and Features
<p align="center">
  <p>Ref 68: Added DHCP and WINS to DC02</p>
  <img src="https://i.imgur.com/eRz3rrt.png"/>
</p>

## DCHP Configuration 
<p align="center">
  <p>Ref 69: Adding DHCP Scopes for issuing IP Addresses and IP Configurations</p>
  <img src="https://i.imgur.com/35jBbbS.png"/>
</p>

<p align="center">
  <p>Ref 70: DC01 Added IP Address Ranges for all Subnets</p>
  <img src="https://i.imgur.com/mzzNrEL.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 71: Added the Domain namd and DNS Ip Addresses</p>
  <img src="https://i.imgur.com/Z9785cH.png"/>
  <p></p>
</p>

## DC01 Setup WINS Server (Windows Internet Name Service)
<p align="center">
  <p>Ref 72: WINS Server setup</p>
  <img src="https://i.imgur.com/Mxu44Tw.png"/>
  <p></p>
</p>

# DC02 Redundant Domain Controller
<p align="center">
  <p>Ref 73: Added DC02 to Server Manager</p>
  <img src="https://i.imgur.com/k6x3YQv.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 74: Promoting DC02 as a Domain Controller</p>
  <img src="https://i.imgur.com/7PfMCZ1.png"/>
  <p>Installed Active Directory Domain Srevices and DNS Roles at the same times.</p>
</p>

<p align="center">
  <p>Ref 75: DC02 will replicate resources from DC01</p>
  <img src="https://i.imgur.com/zekf4Xx.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 76: Update the forwarders</p>
  <img src="https://i.imgur.com/QdkPSUQ.png"/>
</p>

<p align="center">
  <p>Ref 77: DC02 DNS Zones were Replicated automatically from DC01</p>
  <img src="https://i.imgur.com/aSaZ4Nj.png"/>
  <p></p>
</p>

## WINS SERVER for DC02
<p align="center">
  <p>Ref 78: Replicate from DC01 for names and computers</p>
  <img src="https://i.imgur.com/U2iUEIm.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 79: Recored names of connected computers</p>
  <img src="https://i.imgur.com/EC6u97g.png"/>
  <p></p>
</p>



<p align="center">
  <p>Ref 80: Active Registrations then click find now - this will be replicated between DC01 and DC02</p>
  <img src="https://i.imgur.com/X1M65TX.png"/>
</p>


<p align="center">
  <p>Ref 81: Showing that we successfully setup two domain controllers for avalability purposes</p>
  <img src="https://i.imgur.com/Wc6D2SG.png"/>
  <p></p>
</p>

## DHCP Final Setup
<p align="center">
  <p>Ref 82: Splitting the Scopes of DC01 so that it is a shared resoponsibility between DC01 and DC02 50/50</p>
  <img src="https://i.imgur.com/nKNfs7o.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 83: Setting the Percentage split to 50/50 </p>
  <img src="https://i.imgur.com/C4mIdLD.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 84: After the Scopes are Split on DC01 DHCP Server - We need to activate all the scopes on DC02 DHCP Server to have Redundant DHCP</p>
  <img src="blob:https://imgur.com/48d54769-11d6-4e24-ab5f-91e074c38669"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 85: DC02 - Restart the DHCP service and now our scopes are split and activated</p>
  <img src="https://i.imgur.com/9CBx7ha.png"/>
  <p>The Green check shows it is running and Activated</p>
</p>

# LANR1-4-6
<p align="center">
  <p>Ref 86: Make sure the DHCP Relay Agent now has our DC01 and DC02 ip addresses so that if computers need to get IP configurations, The router will send ttheir request to those Servers.</p>
  <img src="https://i.imgur.com/qvRpXn5.png"/>
  <p></p>
</p>

## WDS01 Server - GUI
<p align="center">
  <p>Ref 87: Added a mapped drive to the DC01 and DC02 secret shared Folders
\\DC01.giovanni.cspec\C$</p>
  <img src="https://i.imgur.com/DTPGjDg.png"/>
</p>



# SOC Analyst PC - Installing Splunk Enterprise
### This is used to monitor the computer logs and investigate suspicious activities.
<p align="center">
  <p>Ref 88: Download the Splunk Enterprise Free trial from their website</p>
  <img src="https://i.imgur.com/831EIiq.png"/>
  <p>Splunk: https://www.splunk.com/en_us/download/splunk-enterprise.html</p>
</p>


<p align="center">
  <p>Ref 89: Splunk downloaded and installed on the SOC Analyst COmputer on LAN 2</p>
  <img src="https://i.imgur.com/MBd6FEJ.png"/>
</p>


<p align="center">
  <p>Ref 90: Setop the Receiving Port of 9997</p>
  <img src="https://i.imgur.com/5c78aEu.png"/>
  <p>This allows for computers to send logs to this computer using their port of 8089 and we will receive it on port 9997</p>
</p>


<p align="center">
  <p>Ref 91: Settup port 9997 for recieving Logs</p>
  <img src="https://i.imgur.com/COU6J0c.png"/>
  <p></p>
</p>

# Adding Index
<p align="center">
  <p>Ref 92: Lets create an index to store our logs</p>
  <img src="https://i.imgur.com/98ISH5h.png"/>
  <p>This is like a bucket for logs</p>
</p>

<p align="center">
  <p>Ref 93: Create an index called endpoint</p>
  <img src="https://i.imgur.com/JJqOWBA.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 94: the "endpoint" index was successfully created</p>
  <img src="https://i.imgur.com/iFqpcd7.png"/>
  <p></p>
</p>


## Open Advanced Firewall Configuration to allow Splunk in and out of the network
<p align="center">
  <p>Ref 95: Create a "New Rule" and Select Program</p>
  <img src="https://i.imgur.com/fTnvESC.png"/>
  <p>This should be done on both the Splunk Server and the Client VMs, so logs are not denied or dropped</p>
</p>

<p align="center">
  <p>Ref 96: Locate Splunk within Program Files </p>
  <img src="https://i.imgur.com/IL56K0U.png"/>
</p>


<p align="center">
  <p>Ref 97: Choose Splunk</p>
  <img src="https://i.imgur.com/pKlhIoo.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 98: Select the Bin (Binary) Folder</p>
  <img src="https://i.imgur.com/hoKzEpl.png"/>
  <p>this is where the executable files live</p>
</p>

<p align="center">
  <p>Ref 99: Choose "Splunkd.exe" </p>
  <img src="https://i.imgur.com/I7ixGP2.png"/>
</p>


<p align="center">
  <p>Ref 100: Confirmation that its this program</p>
  <img src="https://i.imgur.com/V6sbHdo.png"/>
</p>

<p align="center">
  <p>Ref 101: Allow the Connection</p>
  <img src="https://i.imgur.com/MwhqyVs.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 102: Apply to all Profiles</p>
  <img src="https://i.imgur.com/XIO8It7.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 103: Give it a Name "Splunkd Allow Inbound"</p>
  <img src="https://i.imgur.com/KUnF02P.png"/>
  <p>For Splunk ports to allow, You can Allow additionally Port 8089</p>
</p>


# Setup Splunk Universal Forwarders 
### We will collect our windows logs from PC04 on LAN 3
<p align="center">
  <p>Ref 104: Download SPlunk Universal Forwarder</p>
  <img src="https://i.imgur.com/VPYMNX8.png"/>
  <p>Splunk Universal Forwarder: https://www.splunk.com/en_us/download/universal-forwarder.html</p>
</p>

<p align="center">
  <p>Ref 105: The Download is complete on the PC4 Computer</p>
  <img src="https://i.imgur.com/L5TjD12.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 106: Run the Setup</p>
  <img src="https://i.imgur.com/slGo5H9.png"/>
  <p>Then Click "Next"</p>
</p>

<p align="center">
  <p>Ref 107: Add username and Password</p>
  <img src="https://i.imgur.com/mnscRmz.png"/>
  <p>Leave the Generate Random Password checked</p>
</p>


<p align="center">
  <p>Ref 108: Set the Deployment Server to IP Address of the SOC Analyst computer</p>
  <img src="https://i.imgur.com/exvhBwX.png"/>
  <p>We did not setup a deployment server, But we can Put it for in the future we want to create one.</p>
</p>


<p align="center">
  <p>Ref 109: Set the Receiving Indexer</p>
  <img src="https://i.imgur.com/8NFwDUZ.png"/>
  <p>This is also going to be our Splunk Server</p>
</p>

# Download Sysmon
<p align="center">
  <p>Ref 110: </p>
  <img src="https://i.imgur.com/L4kOYYj.png"/>
  <p>Sysmon: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon</p>
</p>

# Download Sysmon Config File
<p align="center">
  <p>Ref 111: Select sysmonconfig.xml</p>
  <img src="https://i.imgur.com/KC4xRTF.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 112: </p>
  <img src="https://i.imgur.com/FbtfWm7.png"/>
</p>


<p align="center">
  <p>Ref 113: </p>
  <img src="https://i.imgur.com/rVdUEYW.png"/>
  <p>Sysmon Config: https://github.com/olafhartong/sysmon-modular</p>
  <p>Sysmon Config Raw: https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml</p>
</p>

<p align="center">
  <p>Ref 114: Right click and Save as</p>
  <img src="https://i.imgur.com/6vGFemJ.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 115: Save it as xml</p>
  <img src="https://i.imgur.com/Z8YMvTT.png"/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src="https://i.imgur.com/Wmu4U79.png"/>
  <p>Extract All of sysmon contents</p>
  <p>Copy the Address for later on on Powershell</p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 115: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 116: </p>
  <img src=""/>
  <p></p>
</p>

<p align="center">
  <p>Ref 117: </p>
  <img src=""/>
  <p></p>
</p>


<p align="center">
  <p>Ref 118: </p>
  <img src=""/>
  <p></p>
</p>




