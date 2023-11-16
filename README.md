# Building-an-At-Home-SOC-Lab

<h2>Description</h2>
In this lab, I created an at-home SOC lab environment using VirtualBox. This SOC lab contains pfSense, Active Directory, a Windows Workstation, Sysmon, and CrowdSec.
<br />

<h2>Skills Used</h2>

- <b>Virtual Machine creation</b>
- <b>Linux Command Line</b>
- <b>PowerShell</b> 
- <b>Windows Cmd</b>
- <b>Active Directory</b>
- <b>pfSense</b> 

<h2>VMs Environments Created</h2>

- <b>Linux VM</b>
- <b>Windows 2019 VM</b>
- <b>Windows 10 VM</b>

<h2>Setting up pfSense:</h2>

The first virtual machine I created was a pfSense firewall machine. This would be a dedicated VM only for firewall purposes.
I downloaded the latest pfSense .iso file and compared SHA-256 hashes to ensure the file wasn’t tampered with.
I ran the “certutil -hashfile [file location] SHA256” command and compared hashes from what I received from the command line and the hash I downloaded in the .iso link.
<br />

As you can see below, the hashes are a perfect match.<br />

<p align="center">
Hash Check: <br/>
<img src="https://i.imgur.com/8CL9kIr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
After configuring and creating the VM, I activated 3 Network Adapters. One for the external network (WAN), the internal network (LAN), and the Demilitarized Zone (DMZ). Then, I launched the VM.
<p align="center">
pfSense Downloaded:<br/>
<img src="https://i.imgur.com/8CL9kIr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
Once I could install pfSense onto the VM, I had to link the 3 Network Adapters to which type of network they would represent on pfSense (WAN, LAN, etc.). 
Lastly, I added a static IP address for the LAN adapter. This made it easy to remember to use throughout this project. Then, I enabled DHCP for the WAN.
<p align="center">
pfSense Configured:<br/>
<img src="https://i.imgur.com/hmqLxtY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Setting up Active Directory:</h2>
Firstly, I downloaded the Windows Server .iso file and configured it into a new virtual machine on VirtualBox. Then, I started up the VM. 
Once installed, I connected to the Admin account. 
From the Server Manager Dashboard, I went to the "Open Network & Internet Settings."
<br />
<br />
<p align="center">
Dashboard:<br/>
<img src="https://i.imgur.com/e0EWtg2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
Then, I went to the Desktop Adapter Ethernet Properties, assigned a static IPv4 address, and used the LAN IP address from the pfSense virtual machine as the Default gateway. 
<br />
<br />
<p align="center">
Dashboard:<br/>
<img src="https://i.imgur.com/YP1Ngrl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
After that, I renamed my PC to something easier to use/remember. Once I renamed the PC, I had to restart the VM. From there, I installed Active Directory Domain Services and promoted the Windows Workstation to the domain controller. 
Then, I created a new AD Forest and rebooted the VM.
<br />
<br />
Finally, I downloaded BadBlood onto the AD. BadBlood is a software that fills Active Directory with OS structure and thousands of objects to simulate a real-world environment. 
However, because the virtual network didn’t have wireless access, I had to plug in a USB drive with the software downloaded and transfer it into the VM.
From there, I opened up Powershell as an administrator, went to the folder containing BadBlood (cd command), launched the program, and watched it install.
<br />
<br />
<p align="center">
Terminal BadBlood Installation:<br/>
<img src="https://i.imgur.com/J0CivQk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://i.imgur.com/XLnLy2t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
After the installation, 2500 users, 500 groups, OU, and 100 computers were configured into my Active Directory VM.
<br />
<br />
<h2>Setting up Windows 2019 Workstation:</h2>
I began by downloading a Windows 10 .iso file and used it to create another virtual machine on VirtualBox.
Then, I configured a Network Adapter for the VM and booted the VM.
From there, I configured the VM with the Windows Workstation .iso file.
<br />
<br />
<p align="center">
Installing the Workstation:<br/>
<img src="https://i.imgur.com/B3kAPaw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p align="left"><br />
<br />
Once the Workstation was loaded, I went to the network adapter and changed its IPv4 properties to connect with the pfSense VM created previously and statically added the DNS server to the IPv4 address of the Active Directory VM.
<br />
<p align="center">
IPv4 Network Properties:<br/>
<img src="https://i.imgur.com/qeUMpZB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="left"><br />
Then, I decided to confirm the connection between the Workstation VM and the pfSense VM by using the ping command, which returned successfully.
After testing the connection, I renamed the Workstation to something simpler and restarted the VM.
<br/>
<p align="center">
Ping Test:<br/>
<img src="https://i.imgur.com/hSiBjfk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="left"><br />
I then connected the Workstation to the AD Domain created in the Active Directory VM. I did this by going to “Advanced system settings” (System Properties), making the Workstation a member of the Domain "soc.lab", and finally logging into the Administrator account. 
<p align="center">
System Properties:<br/>
<img src="https://i.imgur.com/Wv8ie21.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 <br />
  <br />
  <br />
Here's the successful login screenshot:
<img src="https://i.imgur.com/WN4d8Ml.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<p align="left"><br />

<h2>Setting up Sysmon:</h2>
Next, I decided to download Sysmon into the Windows machines.
Once downloaded and extracted, I opened PowerShell and installed it into the VMs using the “sysmon.exe -accepteula” command.
<p align="center">
Powershell:<br/>
<img src="https://i.imgur.com/Cptc9w2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
<p align="left"><br />
<h2>Setting up CrowdSec:</h2>
The first step I did was to download the CrowdSec .msi file. This was a little tricky because my virtual machines don’t have access to the internet.
So, I had to download the .msi file onto a USB stick and transfer it over to the VMs.
From there, I launched the CrowdSec setup wizard on both the server (Active Directory VM) and the Windows Workstation. 
<p align="center">
 <br />
CrowdSec Wizard Installation:<br/>
<img src="https://i.imgur.com/PWEtT0q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 





<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
