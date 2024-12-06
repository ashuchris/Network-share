<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Network Files Share And Security Group Permissions </h1>
In this tutorial, we are going to learn how to share folders in active directory and assign permissions to the folders. We are also going to create a security group and demonstrate its importance<br />

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

<p>
 right click and click on Create, then New, then group
</p>
<p>
<img src="https://i.imgur.com/0I4rh4A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Name the group HR and take OK. We have just created the HR security group.
</p>
<p>
<img src="https://i.imgur.com/EM11cIM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Now go back to our folders in the server and let us give the HR folder permissions. We want to assign the HR security group read and write permissions to the HR folder and share it on the network.
</p>
<p>
<img src="https://i.imgur.com/vn8lDMv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 Trying to access the HR folder with any domain user would fail. Why? Because we only created a security group we did not assign a user to that security group or assign a group to that security group. So let's assign a user to that security group. Right-click on the group we created, click on properties, click on members, and click on Add.
</p>
<p>
<img src="https://i.imgur.com/Wa4M5xl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 You can select any user from the _EMPLOYEE OU we created before. I do have a user called Joe. Type in the name and click on check name and click on ok. We have added Joe to the security group. Click on Apply and OK
</p>
<p>
<img src="https://i.imgur.com/OxDL7JJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 To access the HR folder, log in as the user you choose into the Windows VM. I have logged in as Joe. Try to access the HR folder now. It should work for Joe since he is now a part of the security group with permissions for HR folder access.
</p
<p>
<img src="https://i.imgur.com/nI5yOFL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
 But wait what if we want all domain users to access the HR folder and not just Joe? Then we would add the domain users group as members of the HR security group so they get the security group permissions. So we can add groups to groups like this.Go back to the Security group we created and add "domain users". Now all domain users can access the HR folder.
</p
<p>
<img src="https://i.imgur.com/pZ0XZ0J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h2>That is how we share files over the network and setup security groups and permisions</h2>

