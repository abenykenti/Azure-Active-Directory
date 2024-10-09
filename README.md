# Azure Active Directory
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

This lab outlines a hands-on project for implementing an on-premises Active Directory (AD) environment using Azure Virtual Machines (VMs). The goal is to create a resource group in Azure containing two VMs, both within the same virtual network. One VM will serve as the Domain Controller (DC), providing Active Directory services, and the other VM will be a Client machine that joins the domain. The project involves setting up centralized credential management via AD and ensuring that network traffic is routed through the Domain Controller, allowing monitoring and detection of suspicious activity.

---

<details>
<summary><h2>Project Diagram</h2></summary>

![image](https://github.com/user-attachments/assets/7ed42b43-6042-49c4-94da-f567aceaa7d0)

</details>

---

<details>
<summary><h2>Environments and Technologies Used</h2></summary>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

</details>

---

<details>
<summary><h2>Operating Systems Used</h2></summary>

- Windows Server 2022
- Windows 10 (21H2)

</details>

---

<details>
<summary><h2>Key Components</h2></summary>

**Domain Controller (DC) VM:**
- Runs Active Directory Domain Services (AD DS).
- Uses a static IP address for consistent DNS services.
- Acts as a DNS server for the virtual network.
- Provides centralized credential management for devices in the domain.

**Client Machine VM:**
- Joins the domain managed by the DC.
- Configures DNS settings to use the DC’s IP address as the primary DNS server.

**PowerShell Script:**
- Generates 10,000 users in Active Directory to simulate a production environment.

**Traffic Routing and Monitoring:**
- The AD system monitors network traffic.
- All internet traffic from devices (clients) is routed through the Domain Controller.
- Administrators monitor network activity and can identify suspicious logs.

</details>

---

<details>
<summary><h2>Deployment and Configuration Steps</h2></summary>

### Set Up Azure Resources:
- Create a Resource Group to house the VMs and the virtual network.

  ![image](https://github.com/user-attachments/assets/137cae6f-a387-4dc6-838f-ce5711cd5afa)
  
- Set up a Virtual Network (VNet) that the VMs will use to communicate.

  ![image](https://github.com/user-attachments/assets/b048c013-bff5-48c5-834a-4232f139f57a)

### Create the Domain Controller (DC) VM:
- In Azure, deploy a Windows Server VM that will function as your DC.
  
  ![image](https://github.com/user-attachments/assets/dca8d1f8-21d9-4b3a-b1ae-2f87e7e0ab55)

- Assign a static IP address to the VM for DNS consistency.
  
  ![image](https://github.com/user-attachments/assets/848f0dc4-8986-4d10-a71e-34990d6d15ea)

- Install Active Directory Domain Services (AD DS) and promote the VM to a Domain Controller.

  ![image](https://github.com/user-attachments/assets/aceef685-94a8-4b26-9916-920e0e091eeb)

- Setup a new forest as `mydomain.com` (or any domain name of your choice).

  ![image](https://github.com/user-attachments/assets/8c015f29-c0b9-445a-8ea1-0ed52e1b06e1)

- Create Organizational Units (OUs) like "_EMPLOYEES" and "_ADMINS" and add users.

  ![image](https://github.com/user-attachments/assets/e4c1fc2f-f5ff-4a0e-8134-483956292187)

- Assign user roles and admin privileges.

  ![image](https://github.com/user-attachments/assets/c45186b8-cf82-4e62-ad0f-28fe28244d66)

### Create the Client Machine VM:
- Deploy another Windows VM for the client.

  ![image](https://github.com/user-attachments/assets/98460eff-ab81-4b22-9283-23d70c7e1cd9)

- Configure DNS settings on the client to point to the DC’s IP address.

  ![image](https://github.com/user-attachments/assets/e0bee256-1bbc-48cd-a08f-912244d2e335)

- Join the Client VM to the domain and verify using ADUC.

  ![image](https://github.com/user-attachments/assets/2a5fd275-8d20-4025-988c-02acd244eed7)

- Create a new OU named "_CLIENTS" and move Client-1 into it.

  ![image](https://github.com/user-attachments/assets/914d0c41-bfec-4746-8e7e-33fd3df7b866)

- Set up Remote Desktop for non-administrative users.

  ![image](https://github.com/user-attachments/assets/d7d6e247-0e04-4a81-aaf2-bf1b361177a2)

</details>

