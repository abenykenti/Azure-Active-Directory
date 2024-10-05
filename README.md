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

  
- AD is installed but not configured. When using Wizard to install Active Directory checks are done to see if the server meets the necessary requirements to become a Domain Controller. The Wizard checks operating system version, network configuration and hardware specification. 

- Setup a new forest as mydomain.com (can be anything)
  ![image](https://github.com/user-attachments/assets/8c015f29-c0b9-445a-8ea1-0ed52e1b06e1)

  ![image](https://github.com/user-attachments/assets/2a8ca9a5-ab30-433a-943c-fae1af173488)

  ![image](https://github.com/user-attachments/assets/5d7f0f78-423c-4f19-8ff8-927b229fd468)

  ![image](https://github.com/user-attachments/assets/da8ff662-3a77-455d-931d-96a015166e79)

  ![image](https://github.com/user-attachments/assets/80a4489d-dcbb-4119-8a16-0ef5071510b8)

  ![image](https://github.com/user-attachments/assets/07014171-246e-470b-bc88-8800de4ea580)

  ![image](https://github.com/user-attachments/assets/fd9730a8-08aa-40e5-957e-6f3d090959a8)

  ![image](https://github.com/user-attachments/assets/398a6570-af90-4f99-b966-90b40b56bdbd)

  ![image](https://github.com/user-attachments/assets/7de3820d-43d4-4dfc-862e-9cf1c808fe5b)

- Create Employees and Admins within the domain
  - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”

  ![image](https://github.com/user-attachments/assets/6e872265-d359-4aff-9e87-60c2a904b025)

  ![image](https://github.com/user-attachments/assets/e4c1fc2f-f5ff-4a0e-8134-483956292187)

  - Create a new OU named “_ADMINS”

   ![image](https://github.com/user-attachments/assets/77d4a286-9d48-474b-986d-cdb023181a88)

 - Create a new employee e.g named “Jane Doe”  with the username of “jane_admin” 

   ![image](https://github.com/user-attachments/assets/d11e6092-22c9-4c97-a752-266cbbd8f5fa)

   ![image](https://github.com/user-attachments/assets/cd49b67e-dec2-400b-9d1a-882cc81f9e43)

   ![image](https://github.com/user-attachments/assets/eee47533-49f1-4d17-9e5b-2624aad56d51)

   ![image](https://github.com/user-attachments/assets/42da13ff-e9e0-4235-85ad-bfb22bc76bb5)

 
- Add jane_admin to the “Domain Admins” Security Group to become an Admin.
  
   ![image](https://github.com/user-attachments/assets/6c88bdcb-e602-4bd5-b949-39a4a0fe2f48)

   ![image](https://github.com/user-attachments/assets/c4cf1d4d-3615-4d12-b846-b5c756fb37af)

   ![image](https://github.com/user-attachments/assets/c45186b8-cf82-4e62-ad0f-28fe28244d66)
- Log out/close the connection to DC-1 and log back in as “mydomain.com\jane_admin”. User jane_admin is now your admin account.
   ![image](https://github.com/user-attachments/assets/e27ae859-3d37-4001-9998-751de5400ee6)


Create the Client Machine VM:
- Deploy another Windows VM for the client.
  
  ![image](https://github.com/user-attachments/assets/98460eff-ab81-4b22-9283-23d70c7e1cd9)
  ![image](https://github.com/user-attachments/assets/1cf36e37-6282-4780-a9e3-05cdb23c5c36)


- Configure the client’s DNS settings to point to the DC’s static IP.

  ![image](https://github.com/user-attachments/assets/e0bee256-1bbc-48cd-a08f-912244d2e335)
  ![image](https://github.com/user-attachments/assets/1f76ae64-3ba6-4710-83f3-cf73b13af076)
  ![image](https://github.com/user-attachments/assets/40b3d501-d14e-44ea-a6b3-e7ee5686f760)
  ![image](https://github.com/user-attachments/assets/6ce566fa-6b58-4586-b38b-7c4faa612a58)

- To activate the updated settings from the Azure Portal, restart Client-1
  
   ![image](https://github.com/user-attachments/assets/ecbf768e-f7f9-464c-a372-92bb2ac6d30a)

- RDP/login into Client-1 and attempt to ping DC-1’s private IP address

    ![image](https://github.com/user-attachments/assets/301aed2e-ba45-4712-ae3b-e1f009067966)
    ![image](https://github.com/user-attachments/assets/1054bccf-bbd7-4dc6-ae8c-5c574aaa06a7)
   
 - Ensure the ping succeeds
    ![image](https://github.com/user-attachments/assets/f71ca7f2-60e7-4c50-8688-0f0315a05caf)
   
 - From Client-1, open PowerShell and run ipconfig /all
   - The output for the DNS settings should show DC-1’s private IP Address
     
    ![image](https://github.com/user-attachments/assets/c054c219-9648-4337-8eb1-7b097a34b58e)
- Join this VM to the domain controlled by the DC.
  - Login to Client-1 as the original local admin and join it to the domain (computer will restart at the end of process)
 
    ![image](https://github.com/user-attachments/assets/1c2e587d-0223-40c6-beb2-fe572f81731e)

    ![image](https://github.com/user-attachments/assets/3bc8493f-6637-412e-9f0f-88d474903065)

    ![image](https://github.com/user-attachments/assets/93c74962-17e5-4fd3-a540-1e421ffbf590)

    ![image](https://github.com/user-attachments/assets/2a5fd275-8d20-4025-988c-02acd244eed7)

    ![image](https://github.com/user-attachments/assets/4dbe4e57-5a6e-442a-8001-ac6eee697ecb)

    ![image](https://github.com/user-attachments/assets/905685e1-06f4-46b1-8478-84fef0b20c7f)

    ![image](https://github.com/user-attachments/assets/c075364e-f671-4d41-a256-2c5807e8f6a2)

 - Login to the Domain Controller and verify Client-1 shows up in ADUC

    ![image](https://github.com/user-attachments/assets/88ad6632-1c73-41b4-b087-3b2b3edca35e)


   ![image](https://github.com/user-attachments/assets/34be90d7-2437-43d5-b216-808e7797e6c7)

   ![image](https://github.com/user-attachments/assets/45200214-6cc9-4063-9e2f-a3f9b7d16bb1)


 - Create a new OU named “_CLIENTS” and drag Client-1 into there
    ![image](https://github.com/user-attachments/assets/914d0c41-bfec-4746-8e7e-33fd3df7b866)

- Setup Remote Desktop for non-administrative users on Client-1
  - Log into Client-1 as mydomain.com\jane_admin!
   ![image](https://github.com/user-attachments/assets/f61a2879-386f-453d-a2f0-98c2597dcb44)


Open system properties
   ![image](https://github.com/user-attachments/assets/76f89c32-8904-4cc6-9e5c-f486f7baefe0)

   ![image](https://github.com/user-attachments/assets/76f89c32-8904-4cc6-9e5c-f486f7baefe0)

   ![image](https://github.com/user-attachments/assets/b2c9710a-23d7-42ea-9541-d6de01df6631)


- Allow “domain users” access to remote desktop
 - You can now log into Client-1 as a normal, non-administrative user now
 - 
   ![image](https://github.com/user-attachments/assets/85735c51-f48e-47a1-b44e-9e1939b7d9c1)

   ![image](https://github.com/user-attachments/assets/4a976fdf-5564-41cc-9ae0-3aae8e500379)

   ![image](https://github.com/user-attachments/assets/32e5d9b8-f0d5-42df-a3d2-5d1c844f6c38)

   ![image](https://github.com/user-attachments/assets/34884699-1386-4a16-89c0-7ee057fc42d2)

PowerShell Script for User Creation:
Power Shell ISE Stands for Power Shell Integrated Scripting Environment. It is a scripting tool provided by Microsoft to write and edit Power Shell scripts. It provide a great environment for writing, editing and debugging capabilities. Create 1,000 user accounts in Active Directory and attempt to log into client-1 with one of the users

 - Login to DC-1 as jane_admin

    ![image](https://github.com/user-attachments/assets/6ff9443a-96f8-425d-92da-c74ad67d514b)

Open PowerShell_ise as an administrator
    ![image](https://github.com/user-attachments/assets/bee2133b-0468-48f8-8c5d-407219885b23)



   ![image](https://github.com/user-attachments/assets/5021d41e-cb30-46d5-9d0f-991fea650276)

   ![image](https://github.com/user-attachments/assets/af73f7eb-6166-4927-afff-272f6429d6bb)

   ![image](https://github.com/user-attachments/assets/8df10b10-040f-43ca-8fb4-7320eff0a1b9)

 
Ensure all users are created in a specific Organizational Unit (OU) for easier management. e.g When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)

   ![image](https://github.com/user-attachments/assets/13e7eedd-acc2-427e-8b93-a4a3b9bcdc41)

   ![image](https://github.com/user-attachments/assets/d0a1be7d-3c32-4142-9bf7-269aec6810c4)

   ![image](https://github.com/user-attachments/assets/c650dd44-c3db-460d-956d-4be77453c75d)

  
The end! You have completed the project!

</p>
<br />

<p>


</p>
<p>
<h2>Conclusion:</h2>
Active Directory is key for helping organizations manage network traffic and protect against unauthorized access. This project walks through a full Active Directory setup, covering traffic routing, managing user credentials, and monitoring network activity. It demonstrates essential skills for anyone looking to get hands-on experience with network and security management.
</p>
<br />
