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

<br />
<br />
<h2>Setting up Sysmon:</h2>

<br />
<br />
<h2>Setting up CrowdSec:</h2>






<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
