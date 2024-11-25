<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resource Group in Azure
- Create a Windows 10 Virtual Machine (VM)
- Create a Linux (Ubuntu) VM
- Observe ICMP Traffic
- Observe SSH, DHCP, DNS, RDP Traffic

<h2>Actions and Observations</h2>


![image](https://github.com/user-attachments/assets/cc589312-45a2-458a-bcc3-22dfdee93f49)

![image](https://github.com/user-attachments/assets/13e4fb12-ec48-45b2-a103-380ee7130227)

![image](https://github.com/user-attachments/assets/4d07525e-883c-4b05-b003-52675b08cd33)

![image](https://github.com/user-attachments/assets/f0a85f29-2b57-474e-848e-dfd57cff960f)


Part 1: Setting Up Resource Groups

Create a Resource Group:
- Begin by creating a new Resource Group to organize your resources.

Set Up a Windows 10 Virtual Machine (VM):
  - Create a Windows 10 VM.
  - During setup, select the previously created Resource Group.
  - Allow the system to automatically create a new Virtual Network (VNet) and Subnet for this VM.

Set Up a Linux (Ubuntu) Virtual Machine (VM):
  - Create a Linux (Ubuntu) VM.
  - During setup, select the same Resource Group and the VNet created with the Windows 10 VM.
  
Verify the Virtual Network:
  - Use Network Watcher to review and confirm the configuration of your Virtual Network and Subnet.

Part 2: Wireshark 
Download and Install WireShark.
  - Open Wireshark and apply a filter to display ICMP traffic only. This traffic shows the relay requests and responses, commonly known as "ping." You'll be able to observe the number of packets sent and received. What's great is that Wireshark allows you to inspect the detailed data within each packet.

![image](https://github.com/user-attachments/assets/00ed1899-d98c-4bcc-b443-4d66aac8c92f)

![image](https://github.com/user-attachments/assets/f51cd893-d9d5-4401-9a64-cbc33c671d9f)


![image](https://github.com/user-attachments/assets/7df60711-4f2d-4fa1-b926-32b6f8f74d8d)

Part 3: Different Kinds of Traffic 

Let’s analyze a different type of traffic: **SSH**.  

1. In Wireshark, apply a filter for **SSH traffic only**.  
2. From the Windows 10 VM, initiate an SSH connection to the Ubuntu VM using the following command:  
   ```bash
   ssh username@ipaddress
   ```  
   - For example:  
     ```bash
     ssh labuser@10.0.0.4
     ```  
3. Once the connection is established, Wireshark will immediately display the SSH packets exchanged between the two VMs.  

This allows you to observe secure communication traffic in real-time.

![image](https://github.com/user-attachments/assets/b13a592d-f798-470b-8735-4df8aa99bf8d)

**Observe DHCP Traffic**  

**DHCP (Dynamic Host Configuration Protocol)** operates on **ports 67 and 68** and assigns IP addresses to network devices. To analyze DHCP traffic in Wireshark, follow these steps:  

1. **Filter for DHCP Traffic**:  
   - Open Wireshark and apply a filter for **DHCP**.  

2. **Request a New IP Address**:  
   - On the Windows 10 VM, open **Command Prompt** and run the command:  
     `IPCONFIG /RENEW`  
   - This forces the system to request a new IP address from the DHCP server.  

3. **Inspect DHCP Traffic**:  
   - Look for the DHCP traffic in Wireshark to observe the communication between the VM and the DHCP server, including the request and assignment of the new IP address.  

This process helps you understand how DHCP dynamically assigns IP addresses and how the protocol operates.

![image](https://github.com/user-attachments/assets/efe2cf76-e0ea-44af-b6aa-564be15d2b4b)

**Analyze DNS Traffic**  
1. Set a filter for **DNS traffic** in Wireshark.  
2. Open the **Command Prompt (CMD)** and use the command:  
   ```bash
   nslookup google.com
   ```  
   (You can replace "google.com" with any website to retrieve its IP address.)  
3. In Wireshark, observe the DNS requests and responses captured during the lookup process.  
4. Examine the details of the DNS traffic to understand how the domain name resolution occurs.
   ![image](https://github.com/user-attachments/assets/662af743-1ffa-4b2a-a32d-a1958d591a9f)

**Monitor RDP Traffic**  

To observe **RDP (Remote Desktop Protocol)** traffic in Wireshark, apply a filter by entering:  
`tcp.port == 3389`  

This filter displays a live stream of packets transmitted between the two computers during the RDP session. It's incredible to watch the constant flow of data in real-time.

![image](https://github.com/user-attachments/assets/1aad716b-dbfe-46ed-a958-804631bb49ac)
