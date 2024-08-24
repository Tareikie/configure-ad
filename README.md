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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back into DC-1 using your fully qualified domain name (FQDN), which in my case is 'Domain.com\labshogan.' With Active Directory successfully installed, you can now open 'Active Directory Users and Computers' from the Tools menu. Here, we'll create organizational units named '_EMPLOYEES' and '_ADMINS. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
