<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Azure Network Security Group (Firewall Resource)
- Wireshark (Protocol Analyzer)
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Remote Desktop
- Various Command-Line Tools

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
</p>
<p>
This tutorial is on Network Security Groups and Inspecting Network Protocols.We will need to create two VMs on Azure.
<li> Linux machine (Ubuntu) </li>
  <li> Windows 10 machine </li>
<br/>
Both will have two CPUs and they must be on the same VNET. On the Windows machine, download and install Wireshark. Find the wireshark link to download. https://www.wireshark.org/download.html Once installed, open Wireshark and filter for ICMP Traffic only. ICMP is a network layer protocol that relays messages concerning network connection issues.Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows VM. Ping uses ICMP protocol to test the connectivity between hosts. Observe ping requests and replies within Wireshark. When we filter Wirehsark to only capture ICMP packets and ping the private IP address of the linux machine we can visually see the packets on wireshark. 
</p>
<br />
<p>
<img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We can inspect each individual packet and see the actual data that is being sent in each ping. the picture below demonstrates just that. 
</p>
<br />
<p>
<img src="https://i.imgur.com/GLxSIG3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing ICMP Traffic</h2>
In the next portion of the lab we will perpetually ping (-t) the Linux machine
<br/>
<li> Open the Network Security Group on the Ubuntu VM is using and disable incoming (inbound)ICMP traffic </li>
<li> In the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity </li>
<li> Re-enable ICMP traffic for the Network Security Group on the Ubuntu VM is using command line Ping activity (should start working now)</li>
<li> Stop the ping activity </li> 
</p>
<br />
<img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h2>Observing SSH Traffic</h2>
Next we will use our Windows machine to SSH to the Linux machine. SSH has no GUI it just gives the user access to the machines CLI. We will set the WireShark filter to capture SSH packets only. When we ssh into the Linux machine with the command prompt "ssh labuser@10.0.0.5" we can see that WireShark starts to immediately capture SSH packets.
</p>
<br />
<img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing DHCP Traffic</h2>
Now we will use WireShark to filter for DHCP. DHCP is the Dynamic Host Configuration Protocol, which uses ports 67/68. It is used to assign IP addresses to hosts. We will request a new IP address with the command "ipconfig /renew". Once we enter the command WireShark will capture DHCP traffic.
</p>
<br />
<img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing DNS Traffic</h2>
Next we will filter DNS traffic. We will set WireShark to filter DNS traffic. We will initiate DNS traffic by using "nslookup www.google.com" in the command prompt. This command asks our DNS server what is google's IP address.
</p>
<br />
<img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing RDP Traffic</h2>
Finally we will filter for RDP traffic. When we enter tcp.port==3389 traffic is spammed non-stop because we are using Remote Desktop Protocol to connect to our Virtual Machine. This is due to RDP is constantly showing a live stream from once computer to another, therefor traffic is always being transmitted. 
</p>
<br />
<img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
