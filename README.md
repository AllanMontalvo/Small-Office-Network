# Small-Office-Network-Deployment

![image](https://github.com/user-attachments/assets/3ce00251-40a6-4e38-a17a-42df0e5d8261)

This Lab focuses on demonstrating the fundamental concepts to set up and deploy a basic network for a small office. It covers the essential elements of networking, such as hardware configuration and network setup. The goal is to establish a functional network tailored to the requirements of the lab from Jeremy's IT Lab.

<h1>Environments and Technologies Used</h1>

**Technology and Service**
- Cisco Packet Tracer

**Program File**
- [Jeremy's IT Lab CCNA Mega Lab](https://jitl.jp/mega-lab)

**Source Command List**
- [Small Office Network Deployment Source Command](https://github.com/AllanMontalvo/Small-Office-Network-Source-Command/blob/main/README.md)

<h2>High-Level Deployment and Configuration Steps</h2>

**Part 1: Initial Setup**
- Configure each router and switches with the appropriate hostname
  - R1, CSW1, CSW2, DSW-A1, DSW-A2, DSW-B1, DSW-B2, ASW-A1, ASW-A2, ASW-A3, ASW-B1, ASW-B2, ASW-B3
- Enable secret "jeremysitlab" on each routers and switches. Using type 9 hashing if routers or switches offer it, otherwise using type 5. 
- Created user accounts "cisco" and enable secret "ccna" on each routers and switches. Using type 9 hashing if routers or switches offer it, otherwise using type 5.
- Configure the conslole line to require login with login with a local account with 30 minute inactivity timeout. Also enabling synchronous logging.
- Verify configuration by running a "show run" command to view the configuration made.

![Device name and Password](https://github.com/user-attachments/assets/b8eed00d-02be-4e78-864e-6c98bb53043e)
![Device name and Password 9](https://github.com/user-attachments/assets/1a6ad282-62c0-4969-9da6-00c2ec175612)
![Username and password](https://github.com/user-attachments/assets/aa30898a-84cd-4902-9be5-64c08810c445)
![Username and password 9](https://github.com/user-attachments/assets/7f48a677-9f1c-49dc-a67a-e7f83f22071a)
![Local logging](https://github.com/user-attachments/assets/8a84f43a-a356-43d0-a51d-5b9629ea0e76)




**Part 2: Vlans, Layer-2 EtherChannel**

- In Office A, configure a Layer-2 EtherChannel with PortChannel1 between DSW-A1 and DSW-A2 using PAgP.
- In Office B, configure a Layer-2 EtherChannel with PortChannel1 between DSW-B1 and DSW-B2 using LACP.
- Verify configuration with the command "show etherchannel summary".

![Etherchannel Summary DSW-A1](https://github.com/user-attachments/assets/9e60db1b-6029-47d6-97f9-6bb35bc2fbef)
![EtherChannel Summary DSW-B1](https://github.com/user-attachments/assets/246bac5c-58be-446d-af6d-1b3ed4bd5df0)

- Configure all links between Access and Distribution switches, including EtherChannel links as trunk links.
	- Setting Office A devices to allow VLAN 10, 20, 40, and 99 through trunk.
	- Setting Office B devices to allow VLAN 10, 20, 30, and 99 through trunk.
	- Set each trunk's native VLAN to be VLAN 1000
	- Disable DTP on all ports.
 - Verify trunk configuration by using command "show interface (interface port) switchport", except Port-Channel 1or "show run".
   
![Trunk Configuration DSW-A1](https://github.com/user-attachments/assets/4363724f-1f72-417b-b71f-b6cb50a5a93a)
![Trunk Configuration DSW-B1](https://github.com/user-attachments/assets/369c1bb2-8166-4b52-b2c4-c5b1f95b17cd)
![Trunk Conf DSW-A1](https://github.com/user-attachments/assets/f2966b37-46ab-43e9-97f0-8f17ec4a30c5)
![Trunk Conf DSW-B1](https://github.com/user-attachments/assets/71492f5e-b2d5-441a-81b9-402de8c7979f)

- Update one Distribution switch in each Office to to VTPv2 and configure domain name to JeremysITLab. Also 
	configure each Access switches to a VTP client.
- Verify configuration with the command "show vtp status".

![VTP](https://github.com/user-attachments/assets/3cb02c5c-5019-40c4-bf00-25aeb8661b1b)

- Created and named 4 VLANs for Office A on DSW-A1.
	- VLAN 10: PCs
	- VLAN 20: Phones
	- VLAN 40: Wi-Fi
	- VLAN 99: Management
- Created and named 4 VLANs for Office B on DSW-B1.
	- VLAN 10: PCs
	- VLAN 20: Phones
	- VLAN 40: Wi-Fi
	- VLAN 99: Management
- Verify configuration with the command "show vlan".

![Vlan DSW-A1](https://github.com/user-attachments/assets/905476c4-1229-4343-a67f-cce78cd14593)
![Vlan DSW-B1](https://github.com/user-attachments/assets/57af1b93-b567-4cb9-9104-4ccfcb74ea8e)

- Configure F0/1 on each Access switch as an access port and explicility disable DTP
	with the following.
	- ASW-A2, ASW-A3, ASW-B2 are to be configure with VLAN 10 for PCs and VLAN 20 for 
		phones.
	- ASW-B3 is to be configure with VLAN 30 for Servers.
	- ASW-A1 and ASW-B1 are to be configure with VLAN 99 for management and disable 
		FlexConnect for LWAP.
- Configure F0/2 on ASW-A1 as a trunk port for WLC1 to support VLANs 40 (Wi-Fi) and 99
	(Management), make VLAN 99 as the native VLAN, and disable DTP.
- Verify configuration with the command "show inter (interface port) switchport" or "show run".

![Access ASW-A1](https://github.com/user-attachments/assets/d173b6a1-728b-4721-9d35-3b2176185298)
![Access ASW-B2](https://github.com/user-attachments/assets/51608bba-3a8e-46ae-a136-e528de8789a9)
![Access ASW-B3](https://github.com/user-attachments/assets/04dcef9a-242e-4afc-9717-c12a31874a52)

- Shutdown all unused ports on Access and Distribution switches.
- Verify port shutdown with the command "show ip inter brief".
 
![IP shutdown](https://github.com/user-attachments/assets/257fc0cd-3e26-4f5e-808e-2fe61af4083a)



**Part 3 IP Address, Layer-3 EtherChannel**

- Enable and configure the following IP addresses onto R1's interfaces
	- G0/0/0: DHCP client
	- G0/1/0: DHCP client
	- G0/0: 10.0.0.33/30
	- G0/1: 10.0.0.37/30
	- Loopback0: 10.0.0.76/30
- Configure G1/0/2 and G1/0/3 on both CSW1 and CSW2 as a Layer-3 EtherChannel using PAnG.
	Enable IPv4 routing on these Layer-3 switches and configure the following IP addresses.
	- CSW1 PortChannel1: 10.0.0.41/30
	- CSW2 PortChannel1: 10.0.0.42/30
- Configure the following IP addresses on CSW1, enable IPv4 routing, and shutdown all 
	unused interfaces.
	- G1/0/1: 10.0.0.34/30
	- G1/1/1: 10.0.0.45/30
	- G1/1/2: 10.0.0.49/30
	- G1/1/3: 10.0.0.53/30
	- G1/1/4: 10.0.0.57/30
	- Loopback0: 10.0.0.77/32
- Configure the following IP addresses on CSW2, enable IPv4 routing, and shutdown all 
	unused interfaces.
	- G1/0/1: 10.0.0.38/30
	- G1/1/1: 10.0.0.61/30
	- G1/1/2: 10.0.0.65/30
	- G1/1/3: 10.0.0.69/30
	- G1/1/4: 10.0.0.73/30
	- Loopback0: 10.0.0.78/32
- Configure the following IP addresses on DSW-A1 and enable IPv4 routing.
	- G1/1/1: 10.0.0.46/30
	- G1/1/2: 10.0.0.62/30
	- Loopback0: 10.0.0.79/30
- Configure the following IP addresses on DSW-A2 and enable IPv4 routing.
	- G1/1/1: 10.0.0.50/30
	- G1/1/2: 10.0.0.66/30
	- Loopback0: 10.0.0.80/32
- Configure the following IP addresses on DSW-B1 and enable IPv4 routing.
	- G1/1/1: 10.0.0.54/30
	- G1/1/2: 10.0.0.70/30
	- Loopback0: 10.0.0.81/32
- Configure the following IP addresses on DSW-B2 and enable IPv4 routing.
	- G1/1/1: 10.0.0.58/30
	- G1/1/2: 10.0.0.74/30
	- Loopback0: 10.0.0.81/32
- Manually configure Server 1 with the following IP settings.
	- Default Gateway: 10.5.0.1
	- IPv4 Address: 10.5.0.4
	- Subnet Mask: 255.255.255.0
- Configure the IP addresses to the following Access switches on VLAN 99 and assigned the
	default gateway to 10.0.0.1.
	- ASW-A1: 10.0.0.4/28
	- ASW-A2: 10.0.0.5/28
	- ASW-A3: 10.0.0.6/28
	- ASW-B1: 10.0.0.20/28
	- ASW-B2: 10.0.0.21/28
	- ASW-B3: 10.0.0.22/28
 - Verify IP Address configuration with "show ip interface brief" command.

![IP Config R1](https://github.com/user-attachments/assets/584693bc-c0fa-4432-9e03-a72669c54f49)
![IP Config CSW1](https://github.com/user-attachments/assets/2a2d81a9-d993-4c9c-a49c-841c8c0ab638)
![IP Config DSW-A1](https://github.com/user-attachments/assets/bdde22f9-a6d8-4c21-aef2-4c0c6b9d8fc4)
![IP Config ASW-A1](https://github.com/user-attachments/assets/47d6ca1a-47bb-4fab-a45e-fd312309553d)


**Part 4 HSRP**

- Configure a HSRPv2 group 1 in Office A's VLAN 99 in DSW-A1 and DSW-A2 with a subnet 
	of /28. Also make DSW-A1 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.0.0.2
	- DSW-A2: 10.0.0.3
	- VIP: 10.0.0.1
	
- Configure a HSRPv2 group 2 in Office A's VLAN 10 in DSW-A1 and DSW-A2 with a subnet 
	of /24. Also make DSW-A1 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.1.0.2
	- DSW-A2: 10.1.0.3
	- VIP: 10.1.0.1
	
- Configure a HSRPv2 group 3 in Office A's VLAN 20 in DSW-A1 and DSW-A2 with a subnet 
	of /24. Also make DSW-A2 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.2.0.2
	- DSW-A2: 10.2.0.3
	- VIP: 10.2.0.1
	
- Configure a HSRPv2 group 4 in Office A's VLAN 40 in DSW-A1 and DSW-A2 with a subnet 
	of /24. Also make DSW-A2 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.6.0.2
	- DSW-A2: 10.6.0.3
	- VIP: 10.6.0.1
	
- Configure a HSRPv2 group 1 in Office B's VLAN 99 in DSW-B1 and DSW-B2 with a subnet 
	of /28. Also make DSW-B1 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.0.0.18
	- DSW-A2: 10.0.0.19
	- VIP: 10.0.0.17
	
- Configure a HSRPv2 group 2 in Office B's VLAN 10 in DSW-B1 and DSW-B2 with a subnet 
	of /24. Also make DSW-B1 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.3.0.2
	- DSW-A2: 10.3.0.3
	- VIP: 10.3.0.1
	
- Configure a HSRPv2 group 3 in Office B's VLAN 10 in DSW-B1 and DSW-B2 with a subnet 
	of /24. Also make DSW-B2 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.4.0.2
	- DSW-A2: 10.4.0.3
	- VIP: 10.4.0.1
	
- Configure a HSRPv2 group 4 in Office B's VLAN 10 in DSW-B1 and DSW-B2 with a subnet 
	of /24. Also make DSW-B2 the active router with a priority 105 and enable 
	preemption.
	- DSW-A1: 10.5.0.2
	- DSW-A2: 10.5.0.3
	- VIP: 10.5.0.1
 - Verify configuration with "show standby" command.
    
![HSRP DSW-1A](https://github.com/user-attachments/assets/f993223a-c436-489b-a866-e76700281e9c)
![HSRP DSW-2A](https://github.com/user-attachments/assets/5468b3e8-35ac-4875-8951-ecb4d22ec2a4)

	
**Part 5 Rapid Spanning Tree Protocol**

- Configure all Access and Distribution switches to Rapid-PVST+. 

- In Office A, set DSW-A1 as the Root Bridge for VLAN 10 and 99 and set DSW-A2 as 
	the Root Bridge for VLAN 20 and 40.

- In Office A, set DSW-A1 as the Backup Root Bridge for VLAN 20 and 40 and set DSW-A2
	as the Backup Root Bridge for VLAN 10 and 99.
	
- In Office B, set DSW-B1 as the Root Bridge for VLAN 10 and 99 and set DSW-B2 as 
	the Root Bridge for VLAN 20 and 40.

- In Office B, set DSW-B1 as the Backup Root Bridge for VLAN 20 and 40 and set DSW-B2
	as the Backup Root Bridge for VLAN 10 and 99.
-  Verify Spanning Tree configuration with "show spanning-tree active" command.

![Spanning Tree 1](https://github.com/user-attachments/assets/edd61574-f59f-48b7-a5fb-78944e0ed0dc)
![Spanning Tree 2](https://github.com/user-attachments/assets/ba6b99a9-abc4-40ca-9c3c-2ac37a7c4edd)

- In all Access switches, enable PortFast and DPDU Guard on interfaces with end host.
-Verify PortFast and DPDU Guard is enable with "show run" command and view interface F0/1 details.

![FastGuard](https://github.com/user-attachments/assets/16e3b4b5-719a-47c1-a7a3-6aaf7170eaa9)


**Part 6 Static and Dynamic Routing**

- Configuration of Router 1: 
	- Configure the Router-ID with loopback interface IP.
	- Ensure interface Loopback0 is set to passive and OSPF is enable. 
	- Configure all physical connections between OSPF neighbors with a network type 
		that will not select DR/BDR.
	- Configure two static routes to the internet with one route set as a backup in 
		case the primary route is disconnected.
	- Set R1 as the OSPF ASBR.

- Configuration of CSW1 and CSW2:
	- Configure the Router-ID with loopback interface IP and interface Loopback0 is set 
		to passive.
	- Configured OSPF to include only the exact IP addresses of connected OSPF neighbors,
		ensuring their participation in the OSPF routing process.
	- Configure all physical connections between OSPF neighbors with a network type 
		that will not select DR/BDR.

- Configuration of DSW-A1, DSW-A2, DSW-B1, and DSW-B2:
	- Configure the Router-ID with loopback interface IP and interface Loopback0 is set 
		to passive.
	- Set their VLANs as passive interfaces as well.
	- Configured OSPF to include only the exact IP addresses of connected OSPF neighbors,
		ensuring their participation in the OSPF routing process.
	- Configure all physical connections between OSPF neighbors with a network type 
		that will not select DR/BDR.
- Verify Dynamic and Static Route with "show ip route" command.

![IP Route R1](https://github.com/user-attachments/assets/c766078e-a68b-4a91-b8fd-6b7fa8897427)
![IP route CSW1](https://github.com/user-attachments/assets/da21ed27-4d8e-492a-8315-fa99d96da0ef)
![IP Route DSW-A1](https://github.com/user-attachments/assets/28989df2-a88f-4f16-ba1b-2e831140c9f4)

- Also verify OSPF neighbors with "show ip ospf neighbor" command.

![OSPF Neighbors](https://github.com/user-attachments/assets/61e072b3-eb85-4222-8f30-261643522827)

**Part 7 DHCP**

- Configure Router 1 as the DHCP server for all hosts in Office A and B with DHCP pool.
- Exclude the first 10 usable host addresses in each DHCP pool.
- Configure the following DCHP pools with the following information.
	- Pool: A-Mgmt
		- Network: 10.0.0.0/28
		- Default gateway: 10.0.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
		- WLC: 10.0.0.7
	- Pool: A-PC 
		- Network: 10.1.0.0/24
		- Default gateway: 10.1.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
	- Pool: A-Phone 
		- Network: 10.2.0.0/24
		- Default gateway: 10.2.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
	- Pool: B-Mgmt
		- Network: 10.0.0.16/28
		- Default gateway: 10.0.0.17
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
		- WLC: 10.0.0.7
	- Pool: B-PC 
		- Network: 10.3.0.0/24
		- Default gateway: 10.3.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
	- Pool: B-Phone 
		- Network: 10.4.0.0/24
		- Default gateway: 10.4.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
	- Pool: Wi-Fi 
		- Network: 10.6.0.0/24
		- Default gateway: 10.6.0.1
		- Domain name: jeremysitlab.com
		- DNS server: 10.5.0.4
- Verify DHCP Pool with "show ip dhcp pool" command.

![DHCP Pool 1](https://github.com/user-attachments/assets/0b19feda-866a-4b10-81f0-cb7b0f4a1d86)
![DHCP Pool 2](https://github.com/user-attachments/assets/d4f4ca42-4e35-4002-9cc4-fb9cac3d24fd)

- Configure Vlans in Distribution switches to relay-wired DHCP clients' broadcast message to 
	Router 1's Loopback0 IP address.
- Verify configuration of relay-wired DHCP of Vlans with "show ip inter vlan (number)" command and view the helper address section.

 ![DCHP relay-wired](https://github.com/user-attachments/assets/47db6494-4580-44f0-aff5-abb17ae2f6a2)


**Part 8 DNS**

- Configure the following DNS entries onto Server 1
	- google.com = 172.253.62.100
	- youtube.com = 152.250.31.93
	- jeremysitlab.com = 66.235.200.145
	- www.jeremysitlab.com = jeremysitlab.com
- Configure all routers and switches to use domain name jeremysitlab.com and use
	Server 1(10.5.0.4) as their default DNS server.
- Verify DNS configuration by pinging the websites on the pcs in command prompt with "ping (website)"
  	and see the ip address the pc is pinging.

  ![DNS ping](https://github.com/user-attachments/assets/3a800e72-988b-438b-a364-13f8bf767b16)

	
**Part 9 NTP**

- Configure Router 1 as a stratum 5 NTP server
- Configure Router 1 to synchronous its time with NTP server 216.239.35.0
- Configure Router 1 to generate authentication key number 1 and password "ccna".
- Configure all other switches to use Router 1's Loopback0 interface as their 
	NTP server using the authentication key and password.
- Verify NTP configuration with "show ntp status" command.

![NTP](https://github.com/user-attachments/assets/c5717b2b-a061-4f6e-bdff-17f9f6a80ece)

	
**Part 10 SNMP**

- Configure the SNMP community string SNMPSTRING on all routers and switches to allow
	GET messages but not SET messages.
- Verify SNMP community string with the command "show run | include snmp".

![SNMP message](https://github.com/user-attachments/assets/70a62cb2-ed47-430a-bdd8-5047f24270b5)


**Part 11 Syslog**

- Configure all routers and switches to log all messages to Server 1 (10.5.0.4) at all levels.
- Enable logging to the buffer with 8192 bytes of reserve memory for the buffer.
- Verify syslog setting with the command "show logging" command.

![Syslog](https://github.com/user-attachments/assets/2821270e-af98-4c6d-ad0e-fdd354ba5838)


**Part 12 FTP**

- Configure Router 1's default FTP credentials with username "cisco" and password "cisco".
- Verify FTP credenials configuration with command "show run | section ftp".

![FTP username and password](https://github.com/user-attachments/assets/60024bc4-d857-4a5f-8147-c645bcb45276)

- Copy IOS file "c2900-universalk9-mz.SPA.155-3.M4a.bin" from Server 1 to flash.
- Configure Router 1 to boot "c2900-universalk9-mz.SPA.155-3.M4a.bin" from flash and 
	reboot router.
- Once rebooted, delete file "c2900-universalk9-mz.SPA.151-4.M4.bin" from flash.
- Verify new IOS on router with "show version" command.

![IOS ver](https://github.com/user-attachments/assets/1681e205-24df-4fb3-95ed-3720de04f3f9)


**Part 13 SSH**

- Configure all routers and switches to use the largest module size (4096) for the 
	RSA key.
- Update SSH to version 2 in all routers and switches.
- Create an ACL 1 that will allow packets from Office A's PCs subnet.
- Configure VTY lines to allow only SSH connections, require local user account login,
	and synchronous logging.
- Verify configuration of VTY lines with command "show run | section line vty".

![SSH](https://github.com/user-attachments/assets/bb4a7785-620f-474e-989e-36a29e35f226)


**Part 14 NAT**

- Configure a static NAT on  Router 1 to enable end hosts on the Internet to access
	Server 1 via IP address 203.0.113.113
- verify configuration of static NAT with "show ip nat translation".
- Configure a standard ACL 2 with the appriate inside local address range on Router 1.
	- Office A PCs: 10.1.0.0/24
	- Office A Phones: 10.2.0.0/24
	- Office B PCs: 10.3.0.0/24
	- Office B Phones: 10.4.0.0/24
	- Wi-Fi: 10.6.0.0/24
- Configure a range of inside global addresses called POOL1 from 203.0.113.200-203.0.113.207
	with subnet mask of /29.
- Map ACL 2 to POOL1 and enable PAT.
- Verify pool with "show ip nat statistic" command.

![NAT](https://github.com/user-attachments/assets/512d25c5-5e22-4a87-b4ba-43da4c0779bd)


**Part 15 LLDP**

- Disable CDP on all routers and switches and enable LLDP
- Disable LLDP Tx on each Access switch's access port (F0/1).
- Veify LLDP usage with command "show lldp neighbor".

  ![LLDP](https://github.com/user-attachments/assets/681f647e-788f-48aa-9d3c-51ebf4e5a5c8)


**Part 16 ACLs**

- Configure an extended ACL called OfficeA_to_OfficeB on Distribution switches with the following on DSW-A1 and DSW-A2.
	- Allow ICMP messages from Office A PCs (10.1.0.0/24) to Office B PCs (10.3.0.0/24).
	- Deny any traffic from Office A PCs (10.1.0.0/24) to Office B PCs (10.3.0.0/24).
	- Allow all other traffic trough.
 - Verify extended ACL with "show ip access-list" command.

![ACL Extended ](https://github.com/user-attachments/assets/fe7b6109-13b7-4aec-b4f2-07f9f6a34a6e)


	
**Part 17 Port Security**

- Configure Port Security of interface F0/1 of ASW-A1, ASW-B1, and ASW-B3
	- Configure the maximune number of MAC addresses to be 1.
	- Configure for a restrict violation mode.
	- Configure to automatically save the secure MAC address they learn to 
		running-config with sticky MAC address.
- Configure Port Security of interface F0/1 of ASW-A2, ASW-A3, and ASW-B2
	- Configure the maximune number of MAC addresses to be 2.
	- Configure for a restrict violation mode.
	- Configure to automatically save the secure MAC address they learn to 
		running-config with sticky MAC address.
- Verify Port Security with the command "show port-security interface f0/1". 

![Port Security](https://github.com/user-attachments/assets/970736fe-68d2-4016-9520-d2cc07adfd20)


**Part 18 DHCP Snooping**

- Configure all Access switches in Office A and B with DCHP Snooping.
	- Enable dhcp snooping for VLANs 10, 20, 30, 40, and 99 in appropriate switches.
	- Enable trust on interfaces G0/1 and G0/2.
	- Disable insertion of DHCP Option 82.
	- Set a DHCP rate limit of 15 pps on all activce untrusted ports (F0/1).
	- Set a DCHP rate limit of 100 pps on interface F0/2 on switch ASW-A1.
 - Verify DHCP snooping configuration with command "show ip dhcp snooping".

 ![DHCP Snooping](https://github.com/user-attachments/assets/3bfd347f-0420-4d2a-8d01-1d18e9e06566)

	
**Part 19 DAI**

- Configure all Access switches in Office A and B with Dynamic ARP Inspection.
	- Enable DAI for VLANs 10, 20, 30, 40, and 99 in appropriate switches.
	- Enable validation checks Destination MAC, Source MAC, and IP.
- Verify DAI and validation checks with command "show ip arp inspection vlan (number)".
![DAI validation](https://github.com/user-attachments/assets/aa148b84-0779-4f33-b195-606ed695ca13)

- Enable trust on interfaces G0/1 and G0/2.
- Verify trusted interface with command "show ip arp inspection [g0/1 or g0/2]".
![DAI Trust](https://github.com/user-attachments/assets/e4b784ab-bde5-4269-ae92-c9d1e3db1b53)



**Part 20 IPv6**

- Configuration of Router 1
	- Enable IPv6 routing on Router 1.
	- Configure IPv6 address for interface G0/0/0: 2001:db8:a::2/64
	- Configure IPv6 address for interface G0/1/0: 2001:db8:b::2/64
	- Configure IPv6 address for interface G0/0 with EUI-64: 2001:db8:a1::/64
	- Configure IPv6 address for interface G0/1 with EUI-64: 2001:db8:a2::/64
	- Configure a recursive route with next hop 2001:db8:a::1.
	- Configure a floating recursive route with next hop 2001:db8:b::1 with AD of 2.
	
- Configuration CSW1 and CSW2:
	- Enable IPv6 routing on CSW1 and CSW2.
	- Configure IPv6 address for interface G1/0/1 on CSW1 with EUI-64: 2001:db8:a1::/64.
	- Configure IPv6 address for interface G1/0/1 on CSW2 with EUI-64: 2001:db8:a2::/64
	- Enable IPv6 on PortChannel1 on both CSW1 and CSW2 without using "ipv6 address"
		command.
- Verify IPv6 address configuration with command "show ipv6 interface brief".
		
![IPV6 R1](https://github.com/user-attachments/assets/484ad520-f64a-4730-91c5-ba952fd355a5)
![IPv6 CSW1](https://github.com/user-attachments/assets/f5bb7b0b-7150-429b-b9fe-e6ab756b1b1c)

	
		
**Part 21 Wireless**

- Access the GUI of WLC1 via 10.0.0.7 from a PC using username "admin" and
	password "adminPW12".
- Under Controller and selecting Interface, created a new interface with the following	
	information.
	- Name: Wi-Fi
	- VLAN: 40
	- Port Number: 1
	- IP Address: 10.6.0.4
	- Subnet: 255.255.255.0
	- Gateway: 10.6.0.1
	- DHCP Server: 10.0.0.76
- Under WLAN, created a new WLAN with the following information.
	- Profile Name: Wi-Fi
	- SSID: Wi-Fi
	- ID: 1
	- Status: Enable
	- Security: Enable WPA2 Policy with AES encryption, PSK of "cisco123"
 - Verify laptop connection to the office network by selecting a laptop, under the Config tab, choosing Wireless0,
   setting WPA2-PSK with passphrase "cisco123," and checking the assigned IP address.
- Please Note: The assign IP Address may not be within the desire IP range (10.6.0.0/24).

![Wireless verify](https://github.com/user-attachments/assets/051e2409-b0f2-4a50-9ec5-cc6afd7659e4)


<h3>Final Notes</h3>
In this project, I successfully implemetned VLANs, IP addressing, Layer-3 routing protocols, redundancy, spanning-tree protocol, security enhancements, network management and monitoring, as well as wireless configuration. Additionally, I verified and corrected configuration of devices using show commands to ensure proper setup. Given the large number of devices that needed to be configured without the use of network automation or SDN, I utilized a notepad to document commands and reused them when the same configuration was required on multiple devices. Through careful planning and execution of each task, I ensured the network is highly resilient and scalable, ready to support future growth.

