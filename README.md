<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create VMs and Install Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic (Quiz time!)

<h2>Actions and Observations</h2>

<img width="585" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/406a7255-e240-4776-b6d3-38f25fb62957">

<img width="1182" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/917d338a-53a8-45d3-9f6b-59c1f8136c8d">


Part 1 (Create our Resources)
- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
- While creating the VM, select the previously created Resource Group
- While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
- While creating the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher


<img width="642" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/6446148c-e9f4-4494-b1a6-26b5cab56733">



Part 2 (Observe ICMP Traffic)
- Use Remote Desktop to connect to your Windows 10 Virtual Machine
- Within your Windows 10 Virtual Machine, Install Wireshark
- Open Wireshark and filter for ICMP traffic only
- Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
- Observe ping requests and replies within WireShark
- From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
<img width="788" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/e7600f12-75ee-454f-8ffa-e6dc48ea8715">


- Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
- Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
<img width="803" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/21f637be-c324-482a-9da7-d9969e0fe477">


- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity

<img width="1184" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/73633049-c5e7-4343-ac2d-94b1d84fd119">


- Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
- In the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
- Stop the ping activity by typing 'Ctrl+c'

Part 3 (Observe SSH Traffic)
- In Wireshark, filter for SSH traffic only
- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
- Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
- Exit the SSH connection by typing ‘exit’ and pressing [Enter]

<img width="673" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/03799996-129f-4d0a-b3a7-68aea4838ee3">
<img width="849" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/a80f0314-5ff5-4307-9d8b-644983f27e54">




Part 4 (Observe DHCP Traffic)
- In Wireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark
<img width="680" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/1cdd3365-9455-4ddc-8f84-77b4d858cf24">


Part 5 (Observe DNS Traffic)
- In Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
- Observe the DNS traffic being shown in WireShark

<img width="846" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/163fe170-4c06-499a-b64b-81ec182dbcdd">


Part 6 (Observe RDP Traffic)
- In Wireshark, filter for RDP traffic only (tcp.port == 3389)
- <b>Quiz!</b> Observe the immediate spam of RDP traffic? Why do you think it’s spamming vs only showing traffic when you do an activity?
<img width="848" alt="image" src="https://github.com/jaydcollins/azure-network-protocols/assets/164976272/2c7eab8c-b16f-4ae1-8d55-9a65e5ab365d">


- Answer: Because the RDP protocol is constantly showing you a live stream from one computer to another, so traffic is continuously being transmitted.

<h2 align="center"> Great Job! We now know how to observe various forms of network traffic with Wireshark as well as some Network Security Groups basics. </h2>

