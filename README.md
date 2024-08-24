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

- Step 1: Setup necessary Azure Reasources
- Step 2: Install Active Directory
- Step 3: Create an Admin and End-User Account inside AD
- Step 4: Route Client-1 to to your Domain Controller
- Step 5: Test Connections on non-admin account using Remote Desktop
- Step 6: Change your end-user Virtual Machine's domain to log into any accounts on the Domain Server

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/kSVHYCo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we created two virtual machines: 'DC-1,' which operates on Windows Server, and 'Client-1,' running on Windows 10. When setting up the second virtual machine, ensure that it joins the same virtual network as DC-1 to enable communication between the two. Make sure to also set the Private IP of DC-1 to static.
</p>
<br />

<p>
<img src="https://i.imgur.com/env9vMQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To enable communication between the two machines, DC-1's firewall must allow ICMPv4 traffic. To configure this, we opened 'Windows Defender Firewall with Advanced Security,' located the rule for ICMP Echo Requests, and enabled the protocol. To verify success, I had Client-1 ping DC-1's private IP address and confirmed that replies were received.
</p>
<br />

<p>
<img src="https://i.imgur.com/jOErij6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we'll install Active Directory on DC-1. Start by navigating to the Server Manager Dashboard and selecting 'Add roles and features.' In the new window, ensure that 'Active Directory Domain Services' is selected, then proceed with the installation. Once Active Directory is installed, return to Server Manager, click the flag icon in the top right corner, and select 'Promote this server to a domain controller.' Create a new forest and name it as desired; in this case, we chose 'Domain.com.' Continue with the installation. During the process, the server will restart, and DC-1 will be configured as a domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/ngsK4K6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back into DC-1 using your fully qualified domain name (FQDN), which in my case is 'Domain.com\labshogan.' With Active Directory successfully installed, you can now open 'Active Directory Users and Computers' from the Tools menu. Here, we'll create organizational units named '_EMPLOYEES' and '_ADMINS. It's common practice to create an administrator user to handle specific tasks. To do this, right-click your newly created '_ADMINS' unit and create a user. Then, go to the properties of the new user, and under the 'Members of' tab, add them to the 'Domain Admins' group. With that done, logout and reconnect to DC-1 using your new Admin Account Credentials.
</p>
<br />

<p>
<img src="https://i.imgur.com/2I1aNDf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Our goal now is to join Client-1 to DC-1's DNS server. To achieve this, navigate to Client-1 in Microsoft Azure, go to the DNS server settings under Network, and change Client-1's DNS server to DC-1's private IP. Save the changes and restart Client-1's virtual machine. After logging back into Client-1, confirm that its DNS server has been changed to DC-1's by entering the command 'ipconfig /all' in the command line and verifying the DNS server settings. After confirming the DNS change, navigate to 'About this PC' and click on 'Rename this PC (Advanced).' Here, change the domain to your own, in my case, 'Domain.com.' Completing this step will prompt a restart. After the restart, you can log back into Client-1's virtual machine using your admin credentials.
</p>
<br />
