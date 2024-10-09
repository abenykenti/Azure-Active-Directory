# Azure-Active-Directory
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This lab outlines a hands-on project for implementing an on-premises Active Directory (AD) environment using Azure Virtual Machines (VMs). The goal is to create a resource group in Azure containing two VMs, both within the same virtual network. One VM will serve as the Domain Controller (DC), providing Active Directory services, and the other VM will be a Client machine that joins the domain. The project involves setting up centralized credential management via AD and ensuring that network traffic is routed through the Domain Controller, allowing monitoring and detection of suspicious activity.

<details>
  <summary>Project Diagram</summary>

![image](https://github.com/user-attachments/assets/7ed42b43-6042-49c4-94da-f567aceaa7d0)
</details>

<details>
  <summary>Environments and Technologies Used</summary>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
</details>

<details>
  <summary>Operating Systems Used</summary>

- Windows Server 2022
- Windows 10 (21H2)
</details>

## Key Components

<details>
  <summary>Domain Controller (DC) VM</summary>
  
  - Runs Active Directory Domain Services (AD DS).
  - Uses a static IP address for consistent DNS services.
  - Acts as a DNS server for the virtual network.
  - Provides centralized credential management for devices in the domain.
</details>

<details>
  <summary>Client Machine VM</summary>

  - Joins the domain managed by the DC.
  - Configures DNS settings to use the DC’s IP address as the primary DNS server.
</details>

<details>
  <summary>PowerShell Script</summary>

  - Generates 10,000 users in Active Directory to simulate a production environment.
</details>

<details>
  <summary>Traffic Routing and Monitoring</summary>

  - The AD system monitors network traffic.
  - All internet traffic from devices (clients) is routed through the Domain Controller.
  - Administrators monitor network activity and can identify suspicious logs.
</details>

## Deployment and Configuration Steps

<details>
  <summary>Set Up Azure Resources</summary>
  
  - Create a Resource Group to house the VMs and the virtual network.
  - Set up a Virtual Network (VNet) that the VMs will use to communicate.

  ![image](https://github.com/user-attachments/assets/b048c013-bff5-48c5-834a-4232f139f57a)
</details>

<details>
  <summary>Create the Domain Controller (DC) VM</summary>
  
  - Deploy a Windows Server VM that will function as your DC.
  - Assign a static IP address to the VM for DNS consistency.
  - Install Active Directory Domain Services (AD DS) and promote the VM to a Domain Controller.
  - Setup a new forest as `mydomain.com`.
  
  ![image](https://github.com/user-attachments/assets/8c015f29-c0b9-445a-8ea1-0ed52e1b06e1)
</details>

<details>
  <summary>Create Employees and Admins within the Domain</summary>
  
  - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”.
  - Create a new employee named “Jane Doe” with the username “jane_admin”.
  - Add `jane_admin` to the “Domain Admins” Security Group.
  
  ![image](https://github.com/user-attachments/assets/6e872265-d359-4aff-9e87-60c2a904b025)
</details>

<details>
  <summary>Create the Client Machine VM</summary>
  
  - Deploy another Windows VM for the client.
  - Configure the client’s DNS settings to point to the DC’s static IP.
  - Join this VM to the domain controlled by the DC.
  - Login to the Domain Controller and verify Client-1 shows up in ADUC.
  
  ![image](https://github.com/user-attachments/assets/f71ca7f2-60e7-4c50-8688-0f0315a05caf)
</details>

<details>
  <summary>PowerShell Script to Generate 10,000 Users</summary>
  
```powershell
# Connect to Active Directory
Import-Module ActiveDirectory

# Define the Organizational Unit (OU) where users will be created
$OU = "OU=_EMPLOYEES,DC=mydomain,DC=com"

# Loop to create 10,000 users
for ($i=1; $i -le 10000; $i++) {
    $Username = "User" + $i
    $Password = "P@ssw0rd" + $i
    New-ADUser -Name $Username -AccountPassword (ConvertTo-SecureString $Password -AsPlainText -Force) -Path $OU -Enabled $true
}

Write-Host "10,000 users created successfully!"


## Conclusion

This project demonstrated the deployment of a simulated on-premises Active Directory environment in the cloud using Azure VMs. Key highlights include:

- Creating users in bulk using PowerShell
- Managing credentials and organizational units
- Routing all network traffic through a centralized Domain Controller, allowing for monitoring of network activities.

The end!
