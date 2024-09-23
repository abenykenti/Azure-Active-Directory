# Azure-Active-Directory
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This lab outlines a hands-on project for implementing an on-premises Active Directory (AD) environment using Azure Virtual Machines (VMs). The goal is to create a resource group in Azure containing two VMs, both within the same virtual network. One VM will serve as the Domain Controller (DC), providing Active Directory services, and the other VM will be a Client machine that joins the domain. The project involves setting up centralized credential management via AD and ensuring that network traffic is routed through the Domain Controller, allowing monitoring and detection of suspicious activity.
<br /><br />

![image](https://github.com/user-attachments/assets/7ed42b43-6042-49c4-94da-f567aceaa7d0)




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Key Components:</h2>

Domain Controller (DC) VM:
 - Runs Active Directory Domain Services (AD DS).
 - Uses a static IP address for consistent DNS services.
 - Acts as a DNS server for the virtual network.
 - Provides centralized credential management for devices in the domain.

Client Machine VM:
 - Joins the domain managed by the DC.
 - Configures DNS settings to use the DC’s IP address as the primary DNS server.

PowerShell Script:
 - Generates 1,000 users in Active Directory to simulate a production environment.

Traffic Routing and Monitoring:
 - The AD system monitors network traffic.
 - All internet traffic from devices (clients) is routed through the Domain Controller.
 - Administrators monitor network activity and can identify suspicious logs.

<h2>Deployment and Configuration Steps</h2>

<p>

![image]()

Set Up Azure Resources:
Create a Resource Group to house the VMs and the virtual network.
Set up a Virtual Network (VNet) that the VMs will use to communicate.
![image]()

Create the Domain Controller (DC) VM:
In Azure, deploy a Windows Server VM that will function as your DC.
Assign a static IP address to the VM for DNS consistency.
Install Active Directory Domain Services (AD DS) and promote the VM to a Domain Controller.
Configure the VM as a DNS server. When using Wizard to install Active Directory checks are done to see if the server meets the necessary requirements to become a Domain Controller. The Wizard checks operating system version, network configuration and hardware specification. This is a demonstration of me Using Wizard to install Active Directory.
![image]()

Create the Client Machine VM:
Deploy another Windows VM for the client.
Join this VM to the domain controlled by the DC.
Configure the client’s DNS settings to point to the DC’s static IP.
![image]()

PowerShell Script for User Creation:
Power Shell ISE Stands for Power Shell Integrated Scripting Environment. It is a scripting tool provided by Microsoft to write and edit Power Shell scripts. It provide a great environment for writing, editing and debugging capabilities. This is an example of me creating users in Active Directory Domain Controller using Power Shell ISE. Write and run a PowerShell script to create 1,000 user accounts in Active Directory. Example script:
powershell

Ensure all users are created in a specific Organizational Unit (OU) for easier management.
![image]()

Configure Network Traffic Routing:
Set up policies on the DC to route all internet traffic from the client machines through the Domain Controller.
This can be done using Group Policy settings for DNS forwarding, firewall rules, and network traffic rules.


</p>
<br />

<p>

![image]()

</p>
<p>
When using Wizard to install Active Directory checks are done to see if the server meets the necessary requirements to become a Domain Controller. The Wizard checks operating system version, network configuration and hardware specification. This is a demonstration of me Using Wizard to install Active Directory.
</p>
<br />

<p>

![image]()

</p>
<p>
<h2>Conclusion:</h2>
Active Directory is key for helping organizations manage network traffic and protect against unauthorized access. This project walks through a full Active Directory setup, covering traffic routing, managing user credentials, and monitoring network activity. It demonstrates essential skills for anyone looking to get hands-on experience with network and security management.
</p>
<br />
