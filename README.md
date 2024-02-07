<h1>Active Directory Home Lab</h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)-->

<h2>Description</h2>
In this lab I set up an active directory using Oracle VirtualBox. I have two VMs, one running Windows Server 2019 and the other acting as a client running Windows 10 Enterprise. A PowerShell script is used to add 1000 accounts to the Active Directory.  
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10 Enterprise</b>

<h2>Lab Walk-Through:</h2>


<h4 align="center">Install VirtualBox:</h4> 
<p align="center">
 Search "Virtual Machine" in the search bar to visit the Virtual Machine page. Click "Create" in the top left and select "Azure Virtual Machine".
<img src="https://i.imgur.com/Zi6VTdQ.png" height="80%" width="80%" alt="Creating Virtual Machine"/>
<br />
<br />
</p>

<hr>

<h4 align="center">Setting up Domain Controller Virtual Machine:</h4> 
<p align="center">
 Once in the VM settings, create a new Resource group named "HoneypotLab". Name the VM "honeypot". Set the region to "West US 3". Set the Image to "Windows 10 Pro". <br/>
<img src="https://i.imgur.com/AwE05eP.png" height="80%" width="80%" alt="VM Configuration Pt1"/><br/>
 Set a username and password. We will need these in a moment to access our VM. Set inbound ports to "RDP (3389)".<br/>
 <img src="https://i.imgur.com/9KM0Z9c.png" height="80%" width="80%" alt="VM Configuration Pt2"/><br/>
 Click next until you reach the Network page. Set NIC network security group to "Advanced". Click "Create new" under "Configure network security group".<br/>
 <img src="https://i.imgur.com/SWdJGzy.png" height="80%" width="80%" alt="VM Configuration Pt3"/><br/>
 Delete the inbound rule and create and new one with the below settings. <br/>
 <img src="https://i.imgur.com/ja39a3Z.png" alt="VM Configuration Pt4"/><br/>
 Click "Review+Create" and "Create" on the page following that. This will begin the process of deploying your Virtual Machine. <br />
 <img src="https://i.imgur.com/npijgic.png" height="80%" width="80%" alt="VM Configuration Pt5"/><br/>
<br />
<br />
</p>

<hr>

<h4 align="center">Set Up Log Analytics Workspace:</h4> 
<p align="center">
Navigate to the Log Analytics Workspaces page. Click "Create" in the top left. <br/>
<img src="https://i.imgur.com/amVBUHV.png" height="80%" width="80%" alt="LAW Creation Pt1"/><br/>
 Set resource group to "HoneypotLab". Name the new Log Analytics Workspace "law-honeypot1". Set region to "West US 3". Click "Review+Create". <br/>
 <img src="https://i.imgur.com/wFGAw3Z.png" height="80%" width="80%" alt="LAW Creation Pt2"/><br/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Configure Microsoft Defender:</h4> 
<p align="center">
Navigate to Microsoft Defender for Cloud. <br/>
<img src="https://i.imgur.com/bgwDo8F.png" height="80%" width="80%" alt="Defender Config Pt1"/><br/>
 Click "Environment Settings" in the left menu.  <br/>
 <img src="https://i.imgur.com/W1Ltio1.png" height="80%" width="80%" alt="Defender Config Pt2"/><br/>
 Expand your Azure Subscription to find the Log Analytics Workspace we created and open it.  <br/>
 <img src="https://i.imgur.com/9IMgjI4.png" height="80%" width="80%" alt="Defender Config Pt3"/><br/>
 Turn servers on and leave SQL servers off. Click save in the top left. Select "Data Collection" in the left menu and set to "All Events". Click Save in the top left.  <br/>
 <img src="https://i.imgur.com/8vxnYT2.png" height="80%" width="80%" alt="Defender Config Pt4"/>
 <img src="https://i.imgur.com/ZVubHVU.png" height="80%" width="80%" alt="Defender Config Pt5"/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Connect Log Analytics Workspace to the Virtual Machine:</h4> 
<p align="center">
Navigate back to the Log Analytics Workspaces page. Click our Log Analytic Workspace. Click "Virtual Machines (deprecated)" in the left menu. Click "Connect" in the top left. <br/>
 <img src="https://i.imgur.com/VfHudgx.png" height="80%" width="80%" alt="Connect LAW to VM Pt1"/>
 <img src="https://i.imgur.com/0WKRbrl.png" height="80%" width="80%" alt="Connect LAW to VM Pt2"/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Set Up Sentinel:</h4> 
<p align="center">
In a new tab, visit portal.azure.com. Navigate to the Microsoft Sentinel page. Click "Create".<br/>
 <img src="https://i.imgur.com/CTd4JYP.png" height="80%" width="80%" alt="Sentinel Pt1"/><br/><br/>
 Select our Log Analytics Workspace and Click "ADD" in the bottom left. <br/>
 <img src="https://i.imgur.com/kNILkS8.png" height="80%" width="80%" alt="Sentinel Pt2"/><br/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Login to the Virtual Machine:</h4> 
<p align="center">
Navigate to the Virtual Machine page. Click our VM to view information. Copy the public IP address. <br/>
<img src="https://i.imgur.com/CJKv0zi.png" height="80%" width="80%" alt="VM Access Pt1"/><br/>
Open Remote Desktop Connection on your PC. Paste the IP address in and click connect. <br/>
<img src="https://i.imgur.com/8agC3gd.png" alt="VM Access Pt2"/><br/>
Select "More choices" and "use a different account". Use the username and password we select earlier when setting up the virtual machine. <br/>
<img src="https://i.imgur.com/kHzs6SZ.png" alt="VM Access Pt3"/><br/>
Accept the certificate warning. <br/>
<img src="https://i.imgur.com/pIx0XLl.png" alt="VM Access Pt4"/><br/>
Turn all settings off and click accept. <br/>
<img src="https://i.imgur.com/gaYW4h6.png" alt="VM Access Pt5"/><br/>
On your PC setup a perpetual ping of the VM in command prompt. <br/>
<img src="https://i.imgur.com/ZIBnkIC.png" alt="VM Access Pt6"/><br/>
Back on the Virtual Machine, open wf.msc. Click "Windows Defender Firewall Properties", turn off Firewall State in Domain, Private, and Public Profiles. You should now see the pings on your PC being returned.<br/>
<img src="https://i.imgur.com/jizfBkG.png" alt="VM Access Pt7"/><br/>
<img src="https://i.imgur.com/o0iDu6L.png" alt="VM Access Pt8"/><br/>
<img src="https://i.imgur.com/2iYlw7S.png" alt="VM Access Pt9"/><br/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Setting Up PowerShell Script:</h4> 
<p align="center">
Grab the PowerShell script in this repository that we will use for logging access attempts (LogExporter.ps1). This script is an edit of a script originally made by YouTuber Josh Madakor, the creator of this home lab. Paste it into PowerShell ISE on your Virtual Machine and save it to the Desktop. <br/>
 <img src="https://i.imgur.com/OK9UJwO.png" alt="PowerShell Setup Pt1"/><br/>
 <img src="https://i.imgur.com/n4l6tlW.png" alt="PowerShell Setup Pt2"/><br/>
 Visit ipgeolocation.io and sign up for an account. Once logged in, visi the dashboard to find your API key and paste it into the script. Start the script. <br/>
 <img src="https://i.imgur.com/ErSJke6.png" alt="PowerShell Setup Pt3"/><br/>
 <img src="https://i.imgur.com/z139bw1.png" alt="PowerShell Setup Pt4"/><br/>
  <br />
<br />
</p>

<hr>

<h4 align="center">Create The Custom Log:</h4> 
<p align="center">
Navigate back to the Log Analysis Workspace page. Select your Log Analysis Workspace. In the left menu select "Tables", click "Create" and "New Custom Log (MMA Based)". <br/>
 <img src="https://i.imgur.com/1tEbigo.png" height="80%" width="80%" alt="Custom Log Pt1"/><br/>
 On the Virtual Machine, open the log file found at C:\ProgramData\failed_rdp.log. Copy the text and paste it into a new text document on your PC and save it to the Desktop. <br/>
 <img src="https://i.imgur.com/VvC2a2X.png" alt="Custom Log Pt2"/><br/>
 <img src="https://i.imgur.com/5fwYE0R.png" alt="Custom Log Pt3"/><br/>
 Upload the custom log you just made on your PC as a sample. Click "Next" until you reach Collection Paths. <br/>
 <img src="https://i.imgur.com/Q6lWTDP.png" height="80%" width="80%" alt="Custom Log Pt4"/><br/>
 Select "Windows" for the type and set the path to "C:\ProgramData\failed_rdp.log". Click "Next". Name the custom log "FAILED_RDP_WITH_GEO".<br/>
 <img src="https://i.imgur.com/kA6zwr8.png" alt="Custom Log Pt5"/><br/>
 Navigate to Logs in the left menu and confirm that your custom log and the VM are connected. This can take some time to happen, upwards of 30 minutes. You can confirm by pasting the following into the query and selecting "Run". <br/>

 
 ```
FAILED_RDP_WITH_GEO_CL
| extend CSVFields  = split(RawData, ',') 
| extend timestamp_CF  = todatetime(CSVFields[8]) 
| extend label_CF    = tostring(CSVFields[7])
| extend country_CF = tostring(CSVFields[6])
| extend state_CF = tostring(CSVFields[5])
| extend source_CF = tostring(CSVFields[4])
| extend user_CF = tostring(CSVFields[3])
| extend dest_CF = tostring(CSVFields[2])
| extend longitude_CF = tostring(CSVFields[1])
| extend latitude_CF = tostring(CSVFields[0])
| summarize event_count=count() by source_CF, tostring(latitude_CF), tostring(longitude_CF), country_CF, label_CF, dest_CF
```
<br />
<br />
  </p>

 <hr>

<h4 align="center">Setting Up Map in Sentinel:</h4> 
<p align="center">
Navigate back to Microsoft Sentinel and click your Log Analysis Workspace. Click "Workbook", add a new one, and click "edit". Remove the default widgets by clicking the three dots.<br/>
<img src="https://i.imgur.com/6vShvjk.png" height="80%" width="80%" alt="Sentinel Map Pt1"/><br/>
Click "Add" and select "Add query". <br/>
<img src="https://i.imgur.com/leYA0t3.png" height="80%" width="80%" alt="Sentinel Map Pt2"/><br/>
Paste the following code into the query. <br/>

```
FAILED_RDP_WITH_GEO_CL
| extend CSVFields  = split(RawData, ',') 
| extend timestamp_CF  = todatetime(CSVFields[8]) 
| extend label_CF    = tostring(CSVFields[7])
| extend country_CF = tostring(CSVFields[6])
| extend state_CF = tostring(CSVFields[5])
| extend source_CF = tostring(CSVFields[4])
| extend user_CF = tostring(CSVFields[3])
| extend dest_CF = tostring(CSVFields[2])
| extend longitude_CF = tostring(CSVFields[1])
| extend latitude_CF = tostring(CSVFields[0])
| summarize event_count=count() by source_CF, tostring(latitude_CF), tostring(longitude_CF), country_CF, label_CF, dest_CF
| where dest_CF != "destinationhost:samplehost"
```
Set Visualization to "Map". Set latitude to latitude_CF. Set longitude to longitude_CF. Set Metric Label to label_CF. Save the query named "Failed RDP World Map" in the HoneypotLab Resource Group on West US3.<br/>
<img src="https://i.imgur.com/T8BRidq.png" height="80%" width="80%" alt="Sentinel Map Pt3"/><br/>
<img src="https://i.imgur.com/CtGw1yU.png" height="80%" width="80%" alt="Sentinel Map Pt4"/><br/>
After running for a little while your map should be populated with where attempted attacks are located. Enjoy!
<img src="https://i.imgur.com/fLaCqXS.png" height="80%" width="80%" alt="Sentinel Map Pt5"/><br/>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
