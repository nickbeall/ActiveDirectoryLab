<h1>Active Directory Home Lab</h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)-->

<h2>Description</h2>
In this lab I set up an active directory using Oracle VirtualBox. I have two VMs, one running Windows Server 2019, acting as our domain controller, and the other running Windows 10 Enterprise, acting as our client. A PowerShell script is used to add 1000 accounts to the Active Directory.  
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10 Enterprise</b>

<h2>Lab Walk-Through:</h2>


<h4 align="center">Install VirtualBox & Download Windows ISOs:</h4> 

Download & install Oracle VirtualBox and the VirtualBox Extension Pack. Also download the [Windows 10 Enterprise ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise) and the [Windows Server 2019 ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019).  <br/>
<img src="https://i.imgur.com/KNRP7UN.png" height="80%" width="80%" alt="Download Pt1"/><br/>
<img src="https://i.imgur.com/d8LVOYa.png" height="80%" width="80%" alt="Download Pt2"/><br/>
<img src="https://i.imgur.com/nPrNjm0.png" height="80%" width="80%" alt="Download Pt3"/><br/>
<br />
<br />


<hr>

<h4 align="center">Setting up Domain Controller Virtual Machine:</h4> 
In Oracle VirtualBox click new. Name it DC (for Domain Controller) and set version to Other Windows 64 bit.  <br/>
<img src="https://i.imgur.com/fkslFNp.png" height="80%" width="80%" alt="DC Setup  Pt1"/><br/>
<img src="https://i.imgur.com/Q6ARG1I.png" height="80%" width="80%" alt="DC Setup  Pt2"/><br/>
Set RAM to 2048 MB and Processor to 4 cores. Give it 20GB of drive space. These settings can be adjusted to what you feel comfortable allocating based on the PC you are using. Click Finsh to create the VM.  <br/>
<img src="https://i.imgur.com/sZ8Tu4c.png" height="80%" width="80%" alt="DC Setup  Pt3"/><br/>
<img src="https://i.imgur.com/K2KgPnc.png" height="80%" width="80%" alt="DC Setup  Pt4"/><br/>
Open the settings for our new VM, go to advanced and set "Shared Clipboard" and "Drag'n'Drop" both to Bidirectional. Click "Network" on the left and navigate to Adapter 2. Check Enable Network Adapter and attach it to the Internal Network.  <br/>
<img src="https://i.imgur.com/6LgENSb.png" height="80%" width="80%" alt="DC Setup  Pt5"/><br/>
<img src="https://i.imgur.com/0d9LUAw.png" height="80%" width="80%" alt="DC Setup  Pt6"/><br/>
Close the settings and start up the VM. Load the Server 2019 ISO and click "Mount and Retry". Click Next and Install Now.  <br/>
<img src="https://i.imgur.com/WYOHCjt.png" height="80%" width="80%" alt="DC Setup  Pt7"/><br/>
<img src="https://i.imgur.com/M5mipwR.png" height="80%" width="80%" alt="DC Setup  Pt8"/><br/>
Select either of the Desktop Experience versions when prompted. Accept the Licenses and select Custom Install. Select the only drive that should be visible and click next to begin the setup.   <br/>
<img src="https://i.imgur.com/cNJ2AtE.png" height="80%" width="80%" alt="DC Setup  Pt9"/><br/>
<img src="https://i.imgur.com/ANRUkKQ.png" height="80%" width="80%" alt="DC Setup  Pt10"/><br/>
Let the VM restart as needed during the install. If you see the below screen do **NOT** press any keys.   <br/>
<img src="https://i.imgur.com/kF5OVJ4.png" height="80%" width="80%" alt="DC Setup  Pt11"/><br/>
For example purposes we will give the Administrator account a password of Password1. Once on the login screen, you can input Ctrl+Alt+Del by going to Input>Keyboard>Insert Ctrl+Alt+Del. Input your password to log in.  <br/>
<img src="https://i.imgur.com/PsEwGAT.png" height="80%" width="80%" alt="DC Setup  Pt12"/><br/>
<img src="https://i.imgur.com/64JEZf8.png" height="80%" width="80%" alt="DC Setup  Pt13"/><br/>
Now that we are logged in, in the VirtualBox menu, go to Devices>Insert Guest Additions CD Image... Open Explorer and navigate to the CD Drive. Launch the amd64 version of the software and click through to install.   <br/>
<img src="https://i.imgur.com/Lc41Ien.png" height="80%" width="80%" alt="DC Setup  Pt14"/><br/>
<img src="https://i.imgur.com/yz5sDQx.png" height="80%" width="80%" alt="DC Setup  Pt15"/><br/>
Navigate to Network settings and click change adapter options.   <br/>
<img src="https://i.imgur.com/uzR5WEe.png" height="80%" width="80%" alt="DC Setup  Pt16"/><br/>
<img src="https://i.imgur.com/bAnKJWn.png" height="80%" width="80%" alt="DC Setup  Pt17"/><br/>
Rename the adapter connected to the internet _INTERNET_ and the adapter connected internally to X_INTERNAL_X. These names are arbatrary and can be changed as long as you know which one is internal vs external. You can check which is internal by checking for a 169.x.x.x IP address.   <br/>
<img src="https://i.imgur.com/ZIyyzpW.png" height="80%" width="80%" alt="DC Setup  Pt18"/><br/>
<img src="https://i.imgur.com/xWbDUaL.png" height="80%" width="80%" alt="DC Setup  Pt19"/><br/>
On the internal NIC, right click and go to Properties. Open the IPv4 settings and give it the following IP Address, Subnet mask and DNS. See below image if needed.    <br/>

```
IP: 172.16.0.1
Subnet: 255.255.255.0
DNS: 127.0.0.1
```

<img src="https://i.imgur.com/zw1V3za.png" height="80%" width="80%" alt="DC Setup  Pt20"/><br/>
Right click the Start icon and go to System. Click Rename this PC and name it "DC". Restart the PC. <br/>
<img src="https://i.imgur.com/ikFZGLI.png" height="80%" width="80%" alt="DC Setup  Pt21"/><br/>
Once logged back in, open Server Manager and click "Add roles and features". Click through the first two screens. On the third screen ensure that our domain controller is selected.  <br/>
<img src="https://i.imgur.com/kcIERvZ.png" height="80%" width="80%" alt="DC Setup  Pt22"/><br/>
<img src="https://i.imgur.com/rD9HufN.png" height="80%" width="80%" alt="DC Setup  Pt23"/><br/>
Check the box next to Active Directory Domain Services and click Add Features in the pop up. Click next through remaining screens to finish adding the feature.  <br/>
<img src="https://i.imgur.com/Uhx8d1P.png" height="80%" width="80%" alt="DC Setup  Pt24"/><br/>
<img src="https://i.imgur.com/pSrQb0H.png" height="80%" width="80%" alt="DC Setup  Pt25"/><br/>
Click the flag in the top right with the yellow alert and click Promote this server to a domain contrroller. Click Add new forest and set the domain to mydomain.com. Click Next and set the password to Password1 for example purposes. Click Next until you can click Install. Installing will restart the PC.  <br/>
<img src="https://i.imgur.com/DMKoyQz.png" height="80%" width="80%" alt="DC Setup  Pt26"/><br/>
<img src="https://i.imgur.com/wSkzVbZ.png" height="80%" width="80%" alt="DC Setup  Pt27"/><br/>
Once logged back in, click start and open Active Directory Users and Computers. Right click our domain the left, select New>Organizational Unit. Name it _ADMINS  <br/>
<img src="https://i.imgur.com/6qLfCGx.png" height="80%" width="80%" alt="DC Setup  Pt28"/><br/>
Right click _ADMINS and select New>User. Give the user a name of your choosing and a user name of a- followed by the first initial and last name. Ex: a-nbeall. For lab purposes, uncheck user must change password and check password never expires.  <br/>
<img src="https://i.imgur.com/rkMcoq4.png" height="80%" width="80%" alt="DC Setup  Pt29"/><br/>
<img src="https://i.imgur.com/G1p6s4s.png" height="80%" width="80%" alt="DC Setup  Pt30"/><br/>
<img src="https://i.imgur.com/BQ7mdvI.png" height="80%" width="80%" alt="DC Setup  Pt31"/><br/>
Right click the user and go to Properties>Member Of, Click Add and type in Domain Admins and click Check Names. Logout of the Administrator account, and log in with the account you just made.  <br/>
<img src="https://i.imgur.com/Q0AO0sz.png" height="80%" width="80%" alt="DC Setup  Pt32"/><br/>
<img src="https://i.imgur.com/Zq174Vs.png" height="80%" width="80%" alt="DC Setup  Pt33"/><br/>
<img src="https://i.imgur.com/7QIJfKp.png" height="80%" width="80%" alt="DC Setup  Pt34"/><br/>
In Server Manager, click Add Roles and Features. Click next through the first 3 pages again, ensuring our domain controller is selected on page 3. Check the box next to Remote Access. Check the box next to Routing on the following screen.    <br/>
<img src="https://i.imgur.com/gUOUTFd.png" height="80%" width="80%" alt="DC Setup  Pt35"/><br/>
<img src="https://i.imgur.com/8osvwEe.png" height="80%" width="80%" alt="DC Setup  Pt36"/><br/>
Click Tools in the top right of Server Manager. Select Routing and Remote Access.     <br/>
<img src="https://i.imgur.com/SlxVydm.png" height="80%" width="80%" alt="DC Setup  Pt37"/><br/>
Right click DC and select "Configure and Enable Routing for Remote Access". Select NAT and click Next. Select your Internet Interface. The DC should now have a green dot.    <br/>
<img src="https://i.imgur.com/Us5dLnO.png" height="80%" width="80%" alt="DC Setup  Pt38"/><br/>
<img src="https://i.imgur.com/tAhQM7Q.png" height="80%" width="80%" alt="DC Setup  Pt39"/><br/>
<img src="https://i.imgur.com/9v5JJYi.png" height="80%" width="80%" alt="DC Setup  Pt40"/><br/>
In Server Manager, click Add Roles and Features. Click next through the first 3 pages again, ensuring our domain controller is selected on page 3. Check the box next to Remote Access. Check the box next to Routing on the following screen. Click DHCP Server to add and install.     <br/>
<img src="https://i.imgur.com/O6649kD.png" height="80%" width="80%" alt="DC Setup  Pt41"/><br/>
Select Tools in the top right, and go to DHCP. Expand the domain controller. Right click IPv4 and click "Add New Scope". <br/>
<img src="https://i.imgur.com/g0qgWT4.png" height="80%" width="80%" alt="DC Setup  Pt42"/><br/>
<img src="https://i.imgur.com/B57OXYl.png" height="80%" width="80%" alt="DC Setup  Pt43"/><br/>
Set the name to the IP range we will use. For this lab that will be 172.16.0.100-200. Set your starting IP to 172.16.0.100 and end IP to 172.16.0.200. Length set to 24 and Subnet mask to 255.255.255.0. Add 172.16.0.1 as the Router (Default Gateway).  <br/>
<img src="https://i.imgur.com/jFBhrDe.png" height="80%" width="80%" alt="DC Setup  Pt44"/><br/>
<img src="https://i.imgur.com/LiwRyIv.png" height="80%" width="80%" alt="DC Setup  Pt45"/><br/>
<img src="https://i.imgur.com/EnEs3ju.png" height="80%" width="80%" alt="DC Setup  Pt46"/><br/>
On Server Manager click Configure this local server. Turn off IE Enhanced Security Configuration. This is only for lab purposes.  <br/>
<img src="https://i.imgur.com/f1ZKfky.png" height="80%" width="80%" alt="DC Setup  Pt47"/><br/>
<br />
<br />

<hr>

<h4 align="center">Add Users with PowerShell Script:</h4> 

You can download the PowerShell script [here](https://shorturl.at/rtBHW). Open the txt file and add your name at the top. <br/>
<img src="https://i.imgur.com/PEcn9GR.png" height="80%" width="80%" alt="User Creation Pt1"/><br/>
Launch PowerShell ISE as Admin. Open the 1_CREATE_USERS script in PowerShell ISE.  <br/>
<img src="https://i.imgur.com/ZAPnzZh.png" height="80%" width="80%" alt="User Creation Pt2"/><br/>
In the bottom portion of PowerShell type the following scripts. If prompted hit Yes to All.  <br/>

```
Set-ExecutionPolicy
```

```
cd C:\users\a-nbeall\Desktop\AD_PS-master\AD_PS-master\
```

**Substitute the username you made for a-nbeall** <br/>
Run the Script. <br/>
<br />
<br />

<hr>

<h4 align="center">Set Up Client PC Virtual Machine:</h4> 
On VirtualBox click New, name it CLIENT1. Give it 4096 GB of RAM and 4 core of CPU. Again, these can be adjusted to what you feel comfortable giving. <br/>
<img src="https://i.imgur.com/z17aEOT.png" height="80%" width="80%" alt="Client VM Pt1"/><br/>
Set "Shared Clipboard" and "Drag'n'Drop" both to Bidirectional in the settings. Under Network, set Adapter 1 to Internal Network. <br/>
<img src="https://i.imgur.com/K06nUZA.png" height="80%" width="80%" alt="Client VM Pt2"/><br/>
<img src="https://i.imgur.com/eg6C4zU.png" height="80%" width="80%" alt="Client VM Pt3"/><br/>
Start the CLIENT1 virtual machine and load the Windows 10 Enterprise ISO. Again, do custom install. When asked to log in, select "Domain join instead" in the bottom left. Name the account user for now. Click next on password to bypass that.  <br/>
<img src="https://i.imgur.com/I325VKH.png" height="80%" width="80%" alt="Client VM Pt4"/><br/>
<img src="https://i.imgur.com/YY4MbvD.png" height="80%" width="80%" alt="Client VM Pt5"/><br/>
Open Command Prompt to confirm we are getting an IP address. Ping www.google.com to that our setup is functional.  <br/>
<img src="https://i.imgur.com/BYOU3Zc.png" height="80%" width="80%" alt="Client VM Pt6"/><br/>

```ipconfig```

```ping www.google.com```

Right click Start and go to System. Scroll down and click "Rename this PC (advanced)". Click Change on the bottom right. Set the computer name to CLIENT1 and domain to mydomain.com. Log in with a user we made earlier and restart the PC. <br/>
<img src="https://i.imgur.com/hLjZhQu.png" height="80%" width="80%" alt="Client VM Pt7"/><br/>
<img src="https://i.imgur.com/MuOFbj5.png" height="80%" width="80%" alt="Client VM Pt8"/><br/>
<img src="https://i.imgur.com/tdhqdzF.png" height="80%" width="80%" alt="Client VM Pt9"/><br/>

On the domain controller PC you should now see the PC under Computers in Active Directory and the IP leased under Address Leases.  <br/>
<img src="https://i.imgur.com/ECFLNYI.png" height="80%" width="80%" alt="Client VM Pt10"/><br/>
<img src="https://i.imgur.com/KHiZVz5.png" height="80%" width="80%" alt="Client VM Pt11"/><br/>
<br />
<br />



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
