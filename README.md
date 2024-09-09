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
  <p>Ref 1: Network Diagram</p>
  <img src="https://i.imgur.com/IMgwPno.png"/>
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

# Setup Pfsense-FW3 to get Internet Access on the Internal LAN
<p align="center">
  <p>Ref 4: Pfsense Firewall IP address setup</p>
  <img src="https://i.imgur.com/DlwV84Y.png"/>
</p>
<p>This allows up to get access to the Pfsense web interface to further do firewall configurations, rules and download packages.</p> 
<p>Our VPN server is directly connected to LAN 4, as well as the LAN interface side of the Pfsense-FW3. The WAN interface side of the Pfsense-FW3 is automatically getting a IP Address from the Internet Service Provider and using NAT to translate internal IP addresses into a single address for connecting out onto the internet.</p>

- 

## Pfsense-FW3 Initial Configurations Web Interface
<p align="center">
  <p>Ref 4: Pfsense Web Interface on HTTP</p> 
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

## Pfsense-FW3 Setting up TCP & UDP Aliases and Firewall Rules to be able to access the internet on the LAN interface
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

  <p>Ref 28: Allow Remote Management and update the IP Adrdesses of Each INterface</p>
  <img src="https://i.imgur.com/wtbEs0G.png"/>
  <ul>
    <li>winrm Quickconfig</li>
    <li>set-netfirewallrule -Profile Public,Private,Domain -DisplayGroup "Windows Remote Management" -Enabled True</li>
  </ul>
</p> 

<p align="center">
  <p>Ref 29: Rename Net Adapter Name</p>
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
  <p>Ref 30: Setting up default routes for unknown destinations for LAN 1 and LAN 6</p>
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
  <p>Ref 31: Add roles and Features to setup this Core server as a router</p>
  <img src="https://i.imgur.com/3KStiYR.png"/>
  <p>Ref 32: Choose The Role for "Routing"</p>
  <img src="https://i.imgur.com/UuF8qJ6.png"/>

# Add the Administration Roles and Features to WDS01 Mangement Server
  <p>Ref 33: Add Remote management tools to the WDS01 Management and Deployment Server</p>
  <img src="https://i.imgur.com/KhHxexz.png"/>

# Access and Finish Setting up The Remote Access (Routing) Roles and Feature on the LANR1-4-6
  <p>Ref 34: Setup routing on the LANR1-4-6 Server. Choose "Custom Configuration" and then "LAN Routing"</p>
  <img src="https://i.imgur.com/eAah4hk.png"/>
  <p>Ref 35: Setup Static Routes, So packets can get through the router and onto the other side</p>
  <img src="https://i.imgur.com/fDBw9wb.png"/>
</p>


# Setup PFsense-FW1
### Setup this up the same way as Pfsense-FW3 

<p align="center">
  <p>Ref 36: Create an Alias of IP Addresses</p> 
  <img src="https://i.imgur.com/iJOa2Mk.png"/>
</p>

<p align="center">
  <p>Ref 37: Created the Alias "Internal Network"</p> 
  <img src="https://i.imgur.com/OFEMUfZ.png"/>
  <p>This allows communication from internam network</p>
</p>

<p align="center">
  <p>Ref 38: Allow TCP, UDP and ICMP</p> 
  <img src="https://i.imgur.com/pR7yhha.png"/>
  <p>Allow TCP and UDP to enter the WAN interface from any source and any destination</p>
  <p>Allow ICMP from only the internal networks</p>
</p>



# Cisco Router CSR1000v
### Setup Cisco Router - IP Addresses, Passwords, usernames, SSH, ACLs
<p align="center">
  <p>Ref 39: Setup the IP Addresses for (GigabitEthernet1) LAN1 and (GigabitEthernet2) LAN 5 Interfaces on the Router</p> 
  <img src="https://i.imgur.com/9UsbIUx.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 40: Setup Passwords for enable mode</p>
  <img src="https://i.imgur.com/IVVKL3w.png"/>
  <p>Also encrypt the plain text passwords on running-config using "service password-encryption"</p>
</p>

<p align="center">
  <p>Ref 41: Setup Line VTY (Virtual Teletype) </p>
  <img src="https://i.imgur.com/3lkZmqD.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 42: Created usernames and passwords</p>
  <img src="https://i.imgur.com/eQuUaji.png"/>
  <p> for those users using the password policy for string passwords and over 20 characters and only allow username and password to login</p>
</p>

<p align="center">
  <p>Ref 43: Setup SSH on the Router</p>
  <img src="https://i.imgur.com/09DQ8ep.png"/>
  <p>SSH allows for encryted traffic in both directions for confidentiality</p>
</p>

<p align="center">
  <p>Ref 44: Setup Static Routes</p>
  <img src="https://i.imgur.com/52QHTjL.png"/>
  <p>Allows for communication with the other Networks in our infrastructure.</p>
</p>

<p align="center">
  <p>Ref 45: Cisco Routing table with A Static Route for unknown destinations "Last Resort"</p>
  <img src="https://i.imgur.com/FXIZFq6.png"/>
</p>

<p align="center">
  <p>Ref 46: Setup ACLs</p>
  <img src="https://i.imgur.com/b2NRtpo.png"/>
  <p> This was setup for the furture in case of malicious IP on the network that needs to be blocked. To mitigate risk.</p>
</p>


# Setup Pfsense-FW2


<p align="center">
  <p>Ref 47: Pfsense copyright Acceptance to accept</p>
  <img src="https://i.imgur.com/Flk62PP.png"/>
  <p>Ref 48: Installation of Pfsense</p>
  <img src="https://i.imgur.com/QTOKHDh.png"/>
</p>

<p align="center">
  <p>Ref 48: Choose Manual Disk Setup (experts) </p>
  <img src="https://i.imgur.com/OnTuIOV.png"/>
  <p>This method is the only one that works so far while using Pfsense.</p>
</p>


<p align="center">
  <p>Ref 48: Auto Disk setup</p>
  <img src="https://i.imgur.com/ogc87Fx.png"/>
  <p>This created three partitions (da0p1 da0p2, da0p3)</p>
</p>

<p align="center">
  <p>Ref 48: Commit these changes</p>
  <img src="https://i.imgur.com/Qa66xrZ.png"/>
  <p></p>
</p>

<p align="center">
  <p>Ref 48: Extracting the files and installing them on the disk.</p>
  <img src="https://i.imgur.com/izkp3AJ.png"/>
</p>

<p align="center">
  <p>Ref 48: Installation of Pfsense is Complete</p>
  <img src="blob:https://imgur.com/8be6885e-692d-4b64-85a2-74abafdfd8ce"/>
  <p>After the installation is complete we will go to the shell.</p>
</p>

<p align="center">
  <p>Ref 48: Halt Pfsense</p>
  <img src="https://i.imgur.com/CCX6Z3l.png"/>
  <p>We need some tiem to remove the ISO before Pfsense Reboots, Otherwise we will get the screen to Install Pfsense again.</p>
  <p>Eject the Pfsense ISO disk at this time.</p>
  <p>After ISO is ejected. CLick any key to continue with the reboot.</p>
</p>

<p align="center">
  <p>Ref 48: Pfsense Initial Screen after reboot</p>
  <img src="https://i.imgur.com/t2yOlUV.png"/>
  <p>Only the default LAN ip address is setup. We will change this to our internal IP Addresses.</p>
</p>

<p align="center">
  <p>Ref 48: WAN interface IP Address setup</p>
  <img src="https://i.imgur.com/GbtZ4Yg.png"/>
  <p>This is pointing to the internet</p>
</p>

<p align="center">
  <p>Ref 48: Setup noth LAN and WAN Ip Addresses</p>
  <img src="https://i.imgur.com/5W4GMNx.png"/>
  <p>Now we will have access to the Pfsense web interface from within the LAN network that is directly connected</p>
</p>

## Create a Windows Desktop Virtual Machine to finish configuring the PFsense-FW2
<p align="center">
  <p>Ref 48: </p>
  <img src=""/>
  <p>The configuration process will be the same as Pfsense-FW2 expect for the IPS/IDS system</p>
  <p></p>
  <p></p>
</p>

Setup Firewall for LAN 6-3
Set-up DC01 (DHCP,WINS,DNS)
Set-up DC02 (DHCP,WINS,DNS)
Join the domain
Seup Splunk on SOC Analyst PC
Setup VPN
Setup Firewall IDS/IPS on Pfsense-FW1 (S)





