<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Network Files Share And Security Group Permissions </h1>
In this tutorial, we are going to learn how to share folders in active directory and assign permissions to the folders. We are also going to create a security group and demonstrate its importance<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Network Share
- File Permissions
- Active Directory Groups

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)
- Windows Server 2022

<h2>Tutorial Walkthrough</h2>

<p>
 RDP into your Windows server VM and go to your C: drive. Let's create some folders we are to share. Create the following folders: "read-access", "write-access", "no-access" and "HR".
  It is important to note that just because we name these folders this way does not mean they are automatically assigned permissions based on their names. It is just for ease of understanding purposes. 
</p>
<p>
<img src="https://i.imgur.com/IXBh7eh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Now it's time to share the folders through the network. Right-click on the folder and click on properties then click on share
</p>
<p>
<img src="https://i.imgur.com/VU7dUmF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Search for "Domain users" and click on "Add" and then share. For this folder make sure to give the Domain users "read" permissions
</p>
<p>
<img src="https://i.imgur.com/8NjWiDd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 On the "write-access" folder share it the same way. This time give the write-access folder "read and write" permissions for the domain users.
</p>
<p>
<img src="https://i.imgur.com/vTXT0gY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 On the "no-access" folder share it the same way. This time give the no-access folder "read and write" permissions for the "Domain Admins". NOT "Domain Users".
  For now, do not touch the HR folder.
</p>
<p>
<img src="https://i.imgur.com/LpsXfAa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Now RDP into the Windows 10 client. Let us see the folders that we shared. Open file explorer and type in "\\(the name of your server)" for example mine is "\\active-server"
</p>
<p>
<img src="https://i.imgur.com/2cZn2hE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Open the "read-access" folder. Attempt to create a new folder in it. We should have an error because we are logged in with a domain user account and remember we assigned permissions for domain users to only read the "read-access" folder and not write into it or modify it. We do NOT have write permissions.
</p>
<p>
<img src="https://i.imgur.com/VHbu85V.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Let's do the same with the "write-access" folder. We observe we can open it and we can create a new file or folder in it. This is because in this folder we gave the read and write permissions for domain users.
</p>
<p>
<img src="https://i.imgur.com/twoQmkJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Let's do the same with the "no-access" folder. We observe we can not open the folder because we are domain users. We gave Domain Admins permission to read and write on this folder and not domain users.
</p>
<p>
<img src="https://i.imgur.com/y366kib.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h2>Let's Create A Security Group And Assign Permissions To It</h2>

<p>
 Let's go back to our server and into active directory users and computers. To keep things organised create an OU called HR
</p>
<p>
<img src="https://i.imgur.com/CLALvVg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />



