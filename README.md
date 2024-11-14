![image](https://github.com/user-attachments/assets/cc9758d6-c6cc-4276-8945-bae756a94f93)<p align="center">
<img src="https://i.imgur.com/ouRvZVR.png" alt="logo"/>
</p>

<h1>Configuring Active Directory in Azure</h1>
This lab builds upon the previous Active Directory setup by configuring it further to allow a client VM to join the domain and create user accounts. These configurations lay the groundwork for future domain management and user access labs.
.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop Connection
- Active Directory Domain Services
- PowerShell

<h2>Environments and Technologies Used</h2>

- Windows Server 2022
- Windows 10 Pro 

<h2>Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/czmxq5V.png" height="80%" width="80%" alt="created-new-admin"/>
</p>

<p>
<img src="https://i.imgur.com/UYoiYoR.png" height="80%" width="80%" alt="creating-member-admin-member"/>
</p>

<p>
With Active Directory Users and Computers open on the domain controller, I created two Organizational Units (OUs) named _EMPLOYEES and _ADMINS under the domain “mydomain.com.” This naming convention is helpful for future PowerShell scripting. I then created a new user, Jane Doe, in the _ADMINS OU and assigned her administrative privileges by adding her to the Domain Admins security group. From then on, I switched to Jane’s account for administrative tasks.
</p>

<p>
<img src="" height="80%" width="80%" alt="place-holder"/>
</p>

<p>
Before the client can join the domain, I configured its DNS to point to the domain controller’s private IP address. I accessed the Networking tab of the client VM’s Network Interface in the Azure portal and set the DNS server to the domain controller’s IP. After saving the changes, I restarted the client VM to ensure the new DNS settings were applied.
</p>

<p>
<img src="https://i.imgur.com/VOzDzZ2.png" height="80%" width="80%" alt="place-holder"/>
</p>

<p></p>
<img src="https://i.imgur.com/SzGoCBB.png" height="80%" width="80%" alt="place-holder"/>

<p>
<img src="https://i.imgur.com/HRR0Sg9.png" height="80%" width="80%" alt="client-1"/>
</p>

<p>
On the client VM, I went to System settings, selected “Rename this PC (advanced),” and clicked “Change.” I entered the domain name and Jane’s credentials in mydomain.com\jane_admin. After joining the domain, the client appeared in the Active Directory Users and Computers panel under Computers.
</p>

<p>
<img src="https://i.imgur.com/SisjeLd.png" height="80%" width="80%" alt="allow-domain-users"/>
</p>

<p>
To allow non-admin domain users to access the client VM via Remote Desktop, I logged in as an administrator (Jane) and opened System Properties. Under Remote Desktop settings, I selected the option to allow “Domain Users” to access the client remotely. Although Group Policy could achieve this on a larger scale, this manual setting was sufficient for the lab.
</p>

<p>
<img src="https://i.imgur.com/5QFGcaC.png" height="80%" width="80%" alt="powershell-script"/>
</p>

<p>
<img src="https://i.imgur.com/GQl7kaP.png" height="80%" width="80%" alt="generating-users"/>
</p>

<p>
I used a PowerShell script to generate multiple users at once to streamline user creation. The script is available here and is run in PowerShell ISE on the domain controller. Once executed, the script added the specified users to Active Directory.
</p>

<p>
<img src="https://i.imgur.com/W7WtEMe.png" height="80%" width="80%" alt="generated-user-login"/>
</p>

<p>
After creating the users, I verified the setup by logging into the client VM with one of the new users. I selected a user (e.g., mydomain.com\tek.hive) and confirmed a successful login under the domain context.
</p>

<h2>Lessons Learned</h2>

<p>
  This lab provided hands-on experience configuring Active Directory, joining clients to the domain, and managing user permissions. The process has clarified the fundamental steps for AD administration, from DNS configuration to user creation. This experience will be a foundation for more advanced topics, such as DNS settings and file permissions, in future labs.
</p>
