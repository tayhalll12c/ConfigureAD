<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This demonstration outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Datacenter and Client (Windows 10 Virtual Machine)
- Run Datacenter VM
- Install Active Directory Domain Services
- Promote Datacenter VM to Domain Controller through the creation of a domain
- Create an admin user 
- Link Client to Datacenter's domain 
- Create employee login credentials that can be managed in Datacenter 

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/aqRvHFG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Azure, create a new Virtual Machine, title it after a Domain Controller (in this case, DC) and select Windows Datacenter. 
</p>
<br />

<p>
<img src="https://i.imgur.com/0NZnuNR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
At least 2 CPUs are recommended for size. Set a username and password, and deploy the VM. 
</p>
<br />

<p>
<img src="https://i.imgur.com/5iGPvVK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to IP configurations for DC-1, and click the underlined box in the center of the screen.  
</p>
<br />

<p>
<img src="https://i.imgur.com/qr9QimN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Change IP configurations to "static" and save.  
</p>
<br />

<p>
<img src="https://i.imgur.com/PF4lgqw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a "client" virtual machine in the same resource group. This VM will also have 2 CPUs.    
</p>
<br />

<p>
<img src="https://i.imgur.com/u9DpTHv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here, we are checking topology to ensure that both VMs are truly linked.    
</p>
<br />

<p>
<img src="https://i.imgur.com/dWBFgoM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use Remote Desktop Connection after copying the public IP of DC-1, and enter credentials to run it. Let's also run Client-1.     
</p>
<br />

<p>
<img src="https://i.imgur.com/axn6bIM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Let's attempt to ping DC-1 from Client-1 using its private IP. As you can see, the attempt failed.     
</p>
<br />

<p>
<img src="https://i.imgur.com/3PgHUgF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will resolve this by navigating to advanced settings in the Firewall configurations of DC-1.      
</p>
<br />

<p>
<img src="https://i.imgur.com/4NWrrAs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to inbound rules, sort by protocol (click the word 'protocol') and right-click the two follwing ICMPv4 rules to enable them.      
</p>
<br />

<p>
<img src="https://i.imgur.com/2EaIfbk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 is now successfully able to ping DC-1.       
</p>
<br />

<p>
<img src="https://i.imgur.com/azWU570.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the sever manager of DC-1, click 'Add roles and features'.        
</p>
<br />

<p>
<img src="https://i.imgur.com/4XdLOGS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Keep clicking 'Next' until 'Server Roles' is reached. Then, select 'Active Directory Domain Services', and keep clicking 'Next' until the installation screen appears. Wait for installation to finish.         
</p>
<br />

<p>
<img src="https://i.imgur.com/OWBjQDq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click the flag, and then click 'Promote this server to a domain controller'.          
</p>
<br />

<p>
<img src="https://i.imgur.com/bCCINFc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in a root domain name, and then click 'Next'.           
</p>
<br />

<p>
<img src="https://i.imgur.com/qTqecAG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in a password, and then click 'Next'. Then, keep clicking 'Next' until 'Installation' is reached. Allow the installation and restart of the DC-1 virtual machine.            
</p>
<br />

<p>
<img src="https://i.imgur.com/zpuHDEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
In remote desktop, sign back in to DC-1, and add the new domain name in front of the username that was used to create the virtual machine in Azure.  
</p>
<br />

<p>
<img src="https://i.imgur.com/a9usS0d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After logging back in to DC-1, navigate to 'Active Directory Users and Computers' in the start menu folder titled 'Windows Administrative Tools'. Then, under your domain name, create three new organizational units: "_CLIENTS", "_EMPLOYEES", and "_ADMINS".  
</p>
<br />

<p>
<img src="https://i.imgur.com/BQR9HFe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside the "_ADMINS" unit, create a new user. Since this user is intended to be an admin, the login username will reflect that.   
</p>
<br />

<p>
<img src="https://i.imgur.com/JXfIr1C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set a password. In this case, the password has been set to remain static. Then, finish creating the user.    
</p>
<br />

<p>
<img src="https://i.imgur.com/92huwvn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to the properties of the user, then to the 'Member Of' tab, then click 'Add...'. Type in 'Domain Admins' into the box, click 'Check Names', then click 'OK'.     
</p>
<br />

<p>
<img src="https://i.imgur.com/luBnDfH.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log out of DC-1, then log back in with the new admin username.    
</p>
<br />

<p>
<img src="https://i.imgur.com/k9igG12.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Azure, change the DNS of Client-1 to the private IP address of DC-1, (10.0.0.4 in this case) and then save.      
</p>
<br />

<p>
<img src="https://i.imgur.com/MZPsxgx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Restart Client-1 in Azure.      
</p>
<br />

<p>
<img src="https://i.imgur.com/jF5ZynI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the restart is complete, log back in to Client-1. Then, in settings, navigate to 'Rename this PC (advanced)'.     
</p>
<br />

<p>
<img src="https://i.imgur.com/i0kDDDS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click 'Change...', type in the domain name of DC-1, and then click 'OK'.     
</p>
<br />

<p>
<img src="https://i.imgur.com/y7H3joW.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in the domain admin username and password, click 'OK', log out of Client-1, then log back in with the domain admin username and password     
</p>
<br />

<p>
<img src="https://i.imgur.com/PQEwTUU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In 'Active Directory Users and Computers' of DC-1, navigate to the 'Computers' folder, and move Client-1 to the "_CLIENTS" organizational unit.    
</p>
<br />

<p>
<img src="https://i.imgur.com/bWtYLu2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Client-1, go to settings, Remote Desktop, and click 'Select users that can remotely access this PC'.     
</p>
<br />

<p>
<img src="https://i.imgur.com/kXVb8RS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in "domain users" and add.      
</p>
<br />

<p>
<img src="https://i.imgur.com/tEEZUGv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1, right-click Powershell ISE, and run it as an administrator.       
</p>
<br />

<p>
<img src="https://i.imgur.com/vASlRFF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click the blank paper icon to create a new script. In this case, a script has been pasted that will automatically add random employee login credentials into the "_EMPLOYEES" organizational unit. CLick the green play button to run the script.        
</p>
<br />

<p>
<img src="https://i.imgur.com/MWZRpNi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
All employees have "Password1" set as their login password. Choose a random user, log out of Client-1, and log back in with the employee credentials. Since DC-1 and Client-1 have become linked via DNS, the login should be successful.            
</p>
<br />
