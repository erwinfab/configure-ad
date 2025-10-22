<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Install Active Directory Domain Services on the DC-1 server and promote it as a new forest controller.
- Step 2: Create a dedicated Domain Admin user ("jane_admin") and organize Active Directory by creating new Organizational Units (OUs).
- Step 3: Join the Client-1 workstation to the new domain (mydomain.com) and verify its registration on the domain controller.
- Step 4: Enable Remote Desktop for non-administrative users on Client-1 and use a PowerShell script on DC-1 to bulk-create domain users.

<h2>Deployment and Configuration Steps</h2>

<p>
updating image...
</p>
<p>
<h2>Step 1: Install Active Directory and Create Admin User</h2>
First, log in to your DC-1 virtual machine and install the Active Directory Domain Services (ADDS) role. After the role is installed, promote the server to a new domain controller, choosing the option to set up a new forest named mydomain.com. Once the server restarts, log back in as the new domain administrator (mydomain.com\labuser). Open Active Directory Users and Computers (ADUC) and create two Organizational Units (OUs): _EMPLOYEES and _ADMINS. Create a new user named "Jane Doe" (username jane_admin) inside the _ADMINS OU. Finally, add this jane_admin user to the "Domain Admins" security group, log out, and log back in as mydomain.com\jane_admin for all future administrative work.
</p>
<br />

<p>
updating image...
</p>
<p>
<h2>Step 2: Join Client-1 to the Domain</h2>
Next, log in to the Client-1 VM as the local administrator (labuser). (Note: In a real lab, you would first set Client-1's DNS settings in the Azure Portal to point to DC-1's private IP address and restart, but this is marked as already done ). From the System Properties window, join Client-1 to the mydomain.com domain. After Client-1 restarts, log back into your DC-1 server and open ADUC. Verify that Client-1 now appears in the "Computers" container. Create a new OU named _CLIENTS and drag the Client-1 computer object into it for organization.
</p>
<br />

<p>
updating image...
</p>
<p>
<h2>Step 3: Enable Remote Desktop for Domain Users</h2>
Log in to Client-1, this time using your new domain admin account (mydomain.com\jane_admin). Open System Properties and navigate to the "Remote Desktop" tab. Click the "Select users" button and add the "Domain Users" group to the list, allowing any user in your domain to log in to this machine via RDP.
</p>
<br />

<p>
updating image...
</p>
<p>
<h2>Step 4: Bulk-Create Users and Test Login</h2>
Log back into DC-1 as jane_admin. Open PowerShell ISE as an administrator, create a new file, and paste in the contents of the provided user-creation script. Run the script and observe as it automatically creates numerous new user accounts. Once finished, open ADUC to confirm that all the new accounts appear in the _EMPLOYEES OU. To verify everything is working, log out of Client-1 and attempt to log back in as one of the newly created users. Remember to stop (but not delete) your VMs in the Azure portal when you are done to save costs.
</p>
<br />

