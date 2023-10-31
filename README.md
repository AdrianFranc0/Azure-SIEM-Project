<h1>Azure Sentinal SIEM Project</h1>


<h2>Description</h2>
Project consists of using a honey pot VM to attract attackers, with IP Geolocation we will trace the IP addresses from the attacker failed attempt logs. We will also set up Azure SIEM to monitor/manage the data and attacks to the honey pot from different reigons. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell ISE</b> 
- <b>Azure Sentinal SIEM</b>
- <b>IP Geolocation</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Azure Windows VM</b> 

<h2>Program walk-through:</h2>

<p align="center">
Project overview : <br/>
<img src="https://i.imgur.com/EoEEJj6.jpg" height="80%" width="80%" alt="Project overview"/>
<br />
<br />
Go to Azure portal after setting up account:  <br/>
<img src="https://i.imgur.com/lbQQkR7.png" height="80%" width="80%" alt="Go to Azure portal after setting up account"/>
<br />
<br />
Set up a VM on Azure: <br/>
<img src="https://i.imgur.com/EyuGeap.png" height="80%" width="80%" alt="Set up a VM on Azure"/>
<br />
<br />
Now create log analytics workspace:  <br/>
<img src="https://i.imgur.com/CHYdpF5.png" height="80%" width="80%" alt="Now create log analytics workspace"/>
<br />
<br />
Use these settings for Log Analytics Workspace:  <br/>
<img src="https://i.imgur.com/x2LiwZ1.png" height="80%" width="80%" alt="Use these settings for Log Analytics Workspace"/>
<br />
<br />
navigate to "Microsoft Defender For Cloud" and use these settings  :  <br/>
<img src="https://i.imgur.com/if1RKyP.png"80%" width="80%" <br/>
<img src="https://i.imgur.com/G8tYaWP.png" height="80%" width="80%" <br/> 
<img src="https://i.imgur.com/O0DMP1O.png height="80%" width="80%" alt="navigate to "Microsoft Defender For Cloud"/>
<br />
<br />
Connect to the Virtual Machine:  <br/>
<img src="https://i.imgur.com/KBjvqZp.png" height="80%" width="80%" alt="go to "Connect to the Virtual Machine"/>
<br />
<br />
add honeypot VM to "Workspace":  <br/>
<img src="https://i.imgur.com/28newlD.png)" height="80%" width="80%" alt="add honeypot VM to "Workspace""/>
<br />
<br />
Open remote desktop connection on windows to access the VM with the IP provided :  <br/>
<img src="https://i.imgur.com/b479vvy.png" height="80%" width="80%" alt="Open remote desktop connection on windows to access the VM with the IP provided"/>
<br />
<br />
In the VM open "Event viewer":  <br/>
<img src="https://i.imgur.com/8pu8l0S.png" height="80%" width="80%" alt="In the VM open "Event viewer"/>
<br />
<br />
On security viewer look for failed attempt audits, (if there is none, open "remote desktop connection" and get the password wrong on purpose to get a failed attempt):  <br/>
<img src="https://i.imgur.com/FHjdjQx.png" height="80%" width="80%" alt="On security viewer look for failed attempt audits, (if there is none, open "remote desktop connection" and get the password wrong on purpose to get a failed attempt)"/>
<br />
<br />
Double click on the failed attempt and as you can see the log includes the IP address of where the failed attempt came from, use (IP Geolocation to look the IP up):  <br/>
<img src="https://i.imgur.com/bEbQD5k.png" height="80%" width="80%" alt="Double click on the failed attempt and as you can see the log includes the IP address of where the failed attempt came from"/>
<br />
<br />
on the (VM) open up "wf.msc" and turn off the firewall:  <br/>
<img src="https://i.imgur.com/FIPgJhO.png" height="80%" width="80%" <br>
<img src="https://i.imgur.com/gE1tV87.png" height="80%" width="80%" alt="on the (VM) open up "wf.msc" and turn off the firewall"/>
<br />
<br />
Open up "Powershell ISE" and use this script from Josh Madakor:  <br/>
<img src="https://i.imgur.com/74vjDMx.png" height="80%" width="80%" alt="Open up "Powershell ISE"/>
(https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1)
<br />
<br />
Through "prgram Data" access "Failed rdp notepad" to see the logs/data from security viewer :  <br/>
<img src="https://i.imgur.com/4UWrBE7.png" height="80%" width="80%" alt="Open up "Through "prgram Data" access "Failed rdp notepad""/>
<br />
<br />
(Not on desktop) on Azure navigate to Log Analytics Workspace and enter your Honey pot, enter "Tables":  <br/>
<img src="https://i.imgur.com/1vGFErf.png" height="80%" width="80%" <br/>
<img src="https://i.imgur.com/9YvxqjR.png" height="80%" width="80%" alt="(Not on desktop) on Azure navigate to Log Analytics Workspace and enter your Honey pot, enter "Tables""/>
<br />
<br />
Now on log, type this command and click on run. As you can see, the logs of the VM is there:  <br/>
<img src="https://i.imgur.com/paLVUhJ.png" height="80%" width="80%" alt="Open up "Powershell ISE"/>
<br />
<br />
Open up a query and use this script and click run, this script exports the failed attempt logs from the VM and categorizes them by country/longitude etc.:  <br/>
<img src="https://i.imgur.com/ExEI62J.png" height="80%" width="80%" alt="Open up "Powershell ISE"/>
<br />
<br />
Now use this script on "workbook" and (create) a workbook:  <br/>
<img src="https://i.imgur.com/ANPLTWt.png" height="80%" width="80%" alt="Open up "Powershell ISE"/>
<br />
<br />
On workbook create template and add map and use these configurations:  <br/>
<img src="https://i.imgur.com/VIg4RDB.png" height="80%" width="80%" <br/>
<img src="https://i.imgur.com/R3XaCf6.png" height="80%" width="80%" <br/>
<img src="https://i.imgur.com/1c6PmeY.png" height="80%" width="80%" alt="On workbook create template and add map and use these configurations"/>
<br />
<br />
This is the finished SIEM map,it will update and in the VM it displays a live log feed in the power shell:  <br/>
<img src="https://i.imgur.com/ULEqVnv.png"  height="80%" width="80%" <br/>
<img src="https://i.imgur.com/1mM3L3x.png" height="80%" width="80%" 
<br />
<br />


 That is the end of my project, thank you for checking this out! :)
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
