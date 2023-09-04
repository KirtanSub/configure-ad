<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Active Directory in the Cloud (Azure)</h1>
This tutorial explores the uses of Active Directory within Microsoft Azure using virtual machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>
</p>
<p>

Welcome back to another lab in Azure, where we will explore the basics of active directory. We will start off by creating two virtual machines as usual, one will be a domain controller (the VM that houses active directory) which will use the windows server 2022, and the other will be the client VM (which will use the windows 10 OS). We will also need to make sure that the Windows Server IP address is static and not dynamic, as our server is offering active directory services to the client. Also ensure that both VMs are in the same Vnet.

<img src="https://i.imgur.com/b072hLc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tZZUpmO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GJF7yR3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/70Y5c4y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
</p>
<p>

Go ahead and now login to client-1 via Microsoft Remote Desktop, and ping the domain controller's private IP address with a perpetual ping (-t). It should say request timed out, this is because we need to enable ICMPv4 on the domain controller's firewall. After we have done this, go back to client-1 and you will see that the ping succeeded.

<img src="https://i.imgur.com/2DM2G7R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LYxeMG1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />

<p>
</p>
<p>

We can now install active directory. Go back and log-on to DC-1 and install Active Directory Domain Services, then go and set-up a new forest as mydomain.com (you can set-up anything as long as you can remember what it is). Afterward, restart and log back into DC-1 as mydomain.com\labuser.

<img src="https://i.imgur.com/Pi4FxFO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/kBCdNPE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<br />



<p>
</p>

Now, in Active Directory Users and Computers, create an organizational unit called "_EMPLOYEES", and after this create another organizational unit called "_ADMINS". Then create a new employee called "Jane Doe" (you can name this employee any name you wish to). After this, go ahead and add jane_admin to the "Domain Admins" security group, and then logout of DC-1 as yourself, and log back in as "mydomain.com\jane_admin", and use jane_admin as your account from this point forward. 


<img src="https://i.imgur.com/MeCobQo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/oNIERfW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/hJ5WDnj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/0iPMKfD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tBJumqF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />


<p>
</p>
<p>

Now, we will have to set Client-1's DNS settings to the Domain Controller's private IP address. After you do this, go back and re-start client-1 and then log back in as the original local admin (labuser, the credentials you used to log in back in the beginning) the computer itself will restart. After this, log in to the Domain Controller and verify that Client-1 shows into the active directory users and computers inside the "Computers" container. Finally, create a new organizational unit called "_CLIENTS", and drag client-1 in there. 

<img src="https://i.imgur.com/BWCk3Cq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/fZ2FXHA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xBSqvqh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/MWcXKPu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<br />


<p>
</p>
<p>

After this, log back into client-1 as jane_admin and open up system properties, click remote desktop and allow domain users to access remote desktop. This will allow users to login to client-1 as a normal, non-administrative user now. 

<img src="https://i.imgur.com/wIBdvYt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<br />


<p>
</p>
<p>

We will now create lots of additional users. Go back to Domain Controller-1 (DC-1) and login as jane_admin, and open powershell_ise as an administrator. Then, create a new file and paste the contents of this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it. Go ahead and run the script and observe the accounts being created. When finished, observe the accounts in another organizational unit, and then attempt to login to Client-1 with one of the accounts (do be sure to take note of the password in the script).

<img src="https://i.imgur.com/txgin1h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/JuQlIJu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qJGC1yy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/c0HaJAw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
