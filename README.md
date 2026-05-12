<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>

# On-premises Active Directory Deployed in the Cloud (Azure) 
*This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.*

### Executive Summary
This project involved the end-to-end deployment of a Windows-based **Active Directory** environment within **Microsoft Azure**. I provisioned a Domain Controller and a Client workstation, established a private network, and managed the full lifecycle of directory objects. This lab demonstrates my proficiency in **Identity and Access Management (IAM)**, network configuration, and administrative automation using PowerShell.


### Environments and Technologies Used
* **Microsoft Azure** (Virtual Machines, VNet, Private DNS)
* **Remote Desktop Protocol (RDP)**
* **Active Directory Domain Services (AD DS)**
* **Active Directory Users and Computers (ADUC)**
* **PowerShell ISE**

### Operating Systems Used
* Windows Server 2022 (Domain Controller)
* Windows 10 (Client Workstation)

## Deployment and Configuration Steps

**Step 1**: **AD DS Installation and Domain Creation**

I began by provisioning **DC-1** (Windows Server) and installing the **Active Directory Domain Services** role through Server Manager. I promoted the server to a **Domain Controller** and established a new forest named `mydomain.com`.

* Added a new forest

<img width="567" height="422" alt="image" src="https://github.com/user-attachments/assets/98a1294d-1d74-45c1-bbe6-723fa606db4a" />
<br/>

* Server Manager
  
<img width="553" height="304" alt="image" src="https://github.com/user-attachments/assets/9b43cc17-296a-4935-8cd6-e65bda5d1277" />
<br/>

* Added Roles

<img width="624" height="409" alt="image" src="https://github.com/user-attachments/assets/959cc7c6-21fe-4028-9d6a-9f7431b5fc5a" />
<br/>

* Confirmation

<img width="610" height="246" alt="image" src="https://github.com/user-attachments/assets/ca820f91-8e1b-40e8-b34b-cf5f47fc56f6" />

Following the restart, I created a dedicated Administrative User (**"jane_admin"**) and organized the directory by creating **Organizational Units (OUs)** for `_EMPLOYEES` and `_ADMINS`.


---

**Step 2**: **Network Integration & Joining the Domain**

To integrate the client workstation, I adjusted the **DNS settings** in the Azure Portal to point the Client-1 VM toward the private IP of DC-1.

I then successfully joined Client-1 to the `mydomain.com` domain. To maintain organizational standards, I created a `_CLIENTS` OU in **Active Directory Users and Computers (ADUC)** and moved the Client-1 computer object into it.

<img width="322" height="384" alt="image" src="https://github.com/user-attachments/assets/c660973c-f4ce-41e1-b9ea-fbfe8534ffa9" />
<br/>

<img width="865" height="122" alt="image" src="https://github.com/user-attachments/assets/e5a1ec49-66cc-4073-9d67-688cdfb3c2de" />


---

**Step 3**: **Configuring Remote Desktop Access**

To simulate a real enterprise environment where non-admin employees need to access workstations remotely, I modified the **Remote Desktop settings** on Client-1. I added the **"Domain Users"** security group to the allowed RDP list, ensuring that any user created within the domain could log in to the workstation.


<img width="546" height="388" alt="image" src="https://github.com/user-attachments/assets/211256fd-e97a-4893-bce4-76f443011a39" />
<br/>

<img width="418" height="257" alt="image" src="https://github.com/user-attachments/assets/d3214641-a324-4072-bfce-abc5a1b32594" />


---

**Step 4**: **Bulk User Creation & PowerShell Automation**

To populate the directory at scale, I used a **PowerShell** script to bulk-create over 1,000 simulated user accounts. I executed this script within **PowerShell ISE** on DC-1, which automatically generated unique usernames and passwords and placed them into the `_EMPLOYEES` OU.

I verified the success of the automation by logging into **Client-1** using one of the newly generated accounts, confirming that domain-wide authentication and folder redirection were functioning correctly.

<img width="768" height="568" alt="image" src="https://github.com/user-attachments/assets/1a888595-c5bd-41e1-a90a-aa5fbc048120" />
<br/>


<img width="623" height="324" alt="image" src="https://github.com/user-attachments/assets/cf4cc37e-9216-4f13-b8ab-1d8e70480e0a" />


---

### Key Skills Demonstrated

* **Domain Controller Promotion**: Building the root of trust for an enterprise network.
* **Organizational Unit (OU) Design**: Structuring a directory for efficient Group Policy application.
* **Network Administration**: Configuring private DNS and Virtual Networks in a cloud environment.
* **Administrative Automation**: Using PowerShell to eliminate manual entry and reduce human error.
* **Security Group Management**: Applying the Principle of Least Privilege for RDP access.

