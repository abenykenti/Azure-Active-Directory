# Azure-Active-Directory
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This lab outlines a hands-on project for implementing an on-premises Active Directory (AD) environment using Azure Virtual Machines (VMs). The goal is to create a resource group in Azure containing two VMs, both within the same virtual network. One VM will serve as the Domain Controller (DC), providing Active Directory services, and the other VM will be a Client machine that joins the domain. The project involves setting up centralized credential management via AD and ensuring that network traffic is routed through the Domain Controller, allowing monitoring and detection of suspicious activity.
<br /><br />

<h2>Project Diagram</h2>

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
 - Generates 10,000 users in Active Directory to simulate a production environment.

Traffic Routing and Monitoring:
 - The AD system monitors network traffic.
 - All internet traffic from devices (clients) is routed through the Domain Controller.
 - Administrators monitor network activity and can identify suspicious logs.

<h2>Deployment and Configuration Steps</h2>

<p>

Set Up Azure Resources:
- Create a Resource Group to house the VMs and the virtual network.

  ![image](https://github.com/user-attachments/assets/137cae6f-a387-4dc6-838f-ce5711cd5afa)

- Set up a Virtual Network (VNet) that the VMs will use to communicate.

  ![image](https://github.com/user-attachments/assets/b048c013-bff5-48c5-834a-4232f139f57a)

  ![image](https://github.com/user-attachments/assets/c34b05a9-b826-494f-91d8-8254fd077c8f)

Create the Domain Controller (DC) VM:

- In Azure, deploy a Windows Server VM that will function as your DC.
  ![image](https://github.com/user-attachments/assets/dca8d1f8-21d9-4b3a-b1ae-2f87e7e0ab55)

  ![image](https://github.com/user-attachments/assets/db321eb1-f00c-4e5f-8bf9-4c590b05badd)

  ![image](https://github.com/user-attachments/assets/96f2c7ce-2d79-4300-ad31-e5db9b4c1249)

- Assign a static IP address to the VM for DNS consistency.
  ![image](https://github.com/user-attachments/assets/848f0dc4-8986-4d10-a71e-34990d6d15ea)

  ![image](https://github.com/user-attachments/assets/95ee63b1-7448-473a-a9b1-c24634ec37a6)

- Install Active Directory Domain Services (AD DS) and promote the VM to a Domain Controller.
  - RDP/login into DC-1 and install Active Directory Domain Services

  ![image](https://github.com/user-attachments/assets/bdc34ab6-b628-4ba7-afa3-0c34a1f70ebb)

  ![image](https://github.com/user-attachments/assets/d6caccf7-23ad-444e-a354-fadb32da4628)

  ![image](https://github.com/user-attachments/assets/aceef685-94a8-4b26-9916-920e0e091eeb)

  ![image](https://github.com/user-attachments/assets/17687740-0880-4d7c-93b5-4bee2febc094)

  ![image](https://github.com/user-attachments/assets/98540afe-388e-44c6-a807-37f7cfbcceb6)

  ![image](https://github.com/user-attachments/assets/12429596-7669-43ef-99de-b7f96141020a)

  
  ![image](https://github.com/user-attachments/assets/57d6e055-f8d3-4dc8-978d-f964168c2845)

  ![image](https://github.com/user-attachments/assets/50134a9c-963c-4903-8e4e-4c93e331012a)


  
- Configure the VM as a DNS server. When using Wizard to install Active Directory checks are done to see if the server meets the necessary requirements to become a Domain Controller. The Wizard checks operating system version, network configuration and hardware specification. This is a demonstration of me Using Wizard to install Active Directory.

   ![image]()
   ![image]()
   ![image]()
   ![image]()

Create the Client Machine VM:
- Deploy another Windows VM for the client.
  
 ![image](https://github.com/user-attachments/assets/98460eff-ab81-4b22-9283-23d70c7e1cd9)
 ![image](https://github.com/user-attachments/assets/1cf36e37-6282-4780-a9e3-05cdb23c5c36)

Join this VM to the domain controlled by the DC.
- Configure the client’s DNS settings to point to the DC’s static IP.

  ![image](https://github.com/user-attachments/assets/e0bee256-1bbc-48cd-a08f-912244d2e335)
  ![image](https://github.com/user-attachments/assets/1f76ae64-3ba6-4710-83f3-cf73b13af076)
 ![image](https://github.com/user-attachments/assets/40b3d501-d14e-44ea-a6b3-e7ee5686f760)
 ![image](https://github.com/user-attachments/assets/6ce566fa-6b58-4586-b38b-7c4faa612a58)

- To activate the updated settings from the Azure Portal, restart Client-1
  
 ![image](https://github.com/user-attachments/assets/ecbf768e-f7f9-464c-a372-92bb2ac6d30a)

RDP/login into Client-1 and attempt to ping DC-1’s private IP address
 - Ensure the ping succeeds

  ![image](https://github.com/user-attachments/assets/301aed2e-ba45-4712-ae3b-e1f009067966)
  ![image](https://github.com/user-attachments/assets/1054bccf-bbd7-4dc6-ae8c-5c574aaa06a7)
 - Ensure the ping succeeds
  ![image](https://github.com/user-attachments/assets/f71ca7f2-60e7-4c50-8688-0f0315a05caf)
 - From Client-1, open PowerShell and run ipconfig /all
	• The output for the DNS settings should show DC-1’s private IP 
	Address
![image](https://github.com/user-attachments/assets/146d3f33-2a50-4798-9287-1a9d5a4b97a1)






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
