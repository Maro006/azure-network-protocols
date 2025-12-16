<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This project demonstrates how Network Security Groups (NSGs) control and filter network traffic between Azure Virtual Machines within a simulated cloud network environment. Using the Azure Portal, I deployed two Windows Server virtual machines inside a virtual network and configured NSGs to allow, deny, and inspect traffic flows between them. The project highlights how security rules impact connectivity, how to test traffic using built-in Windows tools (PowerShell, ping, RDP), and how to validate traffic flow using Azure Network Watcher. <br />



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

- Create Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

  - you’ll start by creating two VMs on Azure — one Linux and one Windows 10 machine, both with two CPUs and on the same VNET. Then, on the Windows machine, you’ll need to download Wireshark (a network protocol analyzer), which can be found at the link provided. After installing Wireshark, you’ll filter it to only capture ICMP traffic, which is a protocol used to relay messages about network connection issues and is also used by ping to test connectivity between hosts. By filtering Wireshark to capture only ICMP packets and pinging the private IP address of the Linux machine, you’ll be able to visualize the packets in Wireshark.
  - After that we will retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:

<img width="1400" height="758" alt="image" src="https://github.com/user-attachments/assets/89ee1e07-f630-4b67-bff9-00327abbb5c9" />

<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/7429eb33-6fbc-4473-9a5e-cc9e1f70136a" />


  - Attempt to ping google.com and see results
<img width="1400" height="835" alt="image" src="https://github.com/user-attachments/assets/fd549c18-fed4-4a27-88e9-94988564e770" />


  - Now we initiated perpetual ping from Windows VM to Ubuntu VM
<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/d5548c31-aa33-4369-b093-6f78122a099e" />


  - After disabling inbound ICMP traffic, we will no longer receive echo replies from the Linux machine. To block ICMP traffic, we will create a new Network Security Group on the Linux machine and set it to block ICMP. If we want to allow the traffic, we can enable ICMP on the Linux Network Security Groups page in Azure.

<img width="1400" height="759" alt="image" src="https://github.com/user-attachments/assets/0ba8b95a-ccd0-4925-ab84-cde7f8543579" />

<img width="1400" height="834" alt="image" src="https://github.com/user-attachments/assets/baff0901-3d60-4e87-94fa-bf4215ec4035" />


<h3>SSH traffic</h3> 

  - Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.
  - Exit the SSH connection by typing ‘exit’ and pressing [return]:
<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/f0fe14da-bcf7-4e8a-aa35-e27b19a41818" />


<h3>DHCP Traffic</h3> 

  - Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
<img width="1400" height="832" alt="image" src="https://github.com/user-attachments/assets/23cea943-33c1-45e3-a487-453639d3ee4b" />


<h3>DNS traffic</h3>

  - From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:
<img width="1400" height="833" alt="image" src="https://github.com/user-attachments/assets/ea54782d-497f-4ccb-a4e9-871c77997843" />


<h3>RDP traffic</h3>

  - To filter for RDP traffic only use command (tcp.port == 3389)
<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/c4e4bb60-a12a-4bde-9016-18c06cdb1858" />


  - Finally, clean up your Azure environment so that you don’t incur unnecessary charges. Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.





