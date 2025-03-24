# Small-Office-Network

![image](https://github.com/user-attachments/assets/3ce00251-40a6-4e38-a17a-42df0e5d8261)

This Lab focuses on demonstrating the fundamental concepts to set up a a basic netowrk for a small office. It covers the essential elements of networking, such as hardware configuration and netowrk setup. The goal is to establish a functional network tailored to the requirements of the lab from Jeremy's IT Lab.

<h1>Environments and Technologies Used</h1>

**Technology and Service**
- Cisco Packet Tracer

**Program File**
- [Jeremy's IT Lab CCNA Mega Lab](https://jitl.jp/mega-lab)

<h2>High-Level Deployment and Configuration Steps</h2>

**Part 1: Initial Setup**
- Configure each router and switches with the appropriate hostname
  - R1, CSW1, CSW2, DSW-A1, DSW-A2, DSW-B1, DSW-B2, ASW-A1, ASW-A2, ASW-A3, ASW-B1, ASW-B2, ASW-B3
- Enable secret "jeremysitlab" on each routers and switches. Using type 9 hashing if routers or switches offer it, otherwise using type 5. 
- Created user accounts "cisco" and enable secret "ccna" on each routers and switches. Using type 9 hashing if routers or switches offer it, otherwise using type 5.
- Configure the conslole line to require login with login with a local account with 30 minute inactivity timeout. Also enabling synchronous logging.
- Verify configuration by running a "show run" command to view the configuration made.


**Part 2: Vlans, Layer-2 EtherChannel**

- In Office A, configure a Layer-2 EtherChannel with PortChannel1 between DSW-A1 and DSW-A2 using PAgP.
- In Office B, configure a Layer-2 EtherChannel with PortChannel1 between DSW-B1 and DSW-B2 using LACP.
- 





