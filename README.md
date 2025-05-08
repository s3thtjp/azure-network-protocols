<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/19RzUHa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Accessing the Azure Portal to begin creating virtual machines in Azure, you'll need to:

Navigate to portal.azure.com in your web browser. Sign in with your Microsoft account credentials (work/school account or personal Microsoft account).
After authentication, you'll be directed to the Azure dashboard.
Ensure your subscription is active and has sufficient credits/budget for running VMs.

</p>
<br />

<p>
<img src="https://i.imgur.com/sDzlzI2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Creating a Resource Group
Resource groups in Azure act as logical containers for related resources:

From the Azure dashboard, click on "Resource groups" in the left navigation menu.
Click the "+ Create" button to start creating a new resource group.
Select your subscription from the dropdown menu.
Enter a descriptive name for your resource group (e.g., "OSLab-ResourceGroup").
Select an appropriate region (choose one closest to your physical location for best performance).
Add any relevant tags for organization/billing purposes (optional).
Click "Review + create" and then "Create" after validation passes.
</p>
<br />

<p>
<img src="https://i.imgur.com/IW76Hrl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now you can create your first VM within the resource group:

Return to the Azure dashboard and click "Virtual machines" in the left navigation menu.
Click "+ Create" and select "Azure virtual machine".
In the Basics tab:

Verify the correct subscription and resource group are selected.
Enter a name for your VM (e.g., "WindowsVM" or "linux-vm").
Select the region (should match your resource group region).
Choose availability options (Standard is sufficient for lab purposes).
Select the image (e.g., Windows 10 Pro for purposes of this lab).
Choose the VM size (select one with 2 vCPUs as specified)
Set username and password credentials (as specified: labuser/whatever password).
Note these credentials as you'll need them to access the VM later.
</p>

<p>
<img src="https://i.imgur.com/XDQi1Cy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After successfully creating your Windows 10 Pro VM:

Navigate back to the Azure dashboard.
Click on "Virtual machines" in the left navigation menu.
Click the "+ Create" button and select "Azure virtual machine".

Configuring the Basic Settings for Ubuntu Server
In the Basics tab, set up the following configurations:

Subscription: Select the same subscription used for your Windows VM.
Resource group: Select the existing resource group that contains your Windows VM.
Virtual machine name: Enter a descriptive name (e.g., "UbuntuVM" or "ubuntu-server").
Region: Select the same region as your Windows VM for optimal network performance.
Availability options: Standard availability is sufficient for lab environments.
Security type: Standard security works for most scenarios.
Image: Search for and select "Ubuntu Server 22.04 LTS".
VM size: Select a size with adequate resources (similar to your Windows VM).
Authentication type: Choose password.

using password: Create username and secure password.

Inbound port rules: Allow SSH (port 22) for remote administration.

Ensuring Network Compatibility with Windows VM.
The networking configuration is critical for communication between your VMs:

Navigate to the Networking tab.
Under "Virtual network", select the same virtual network used by your Windows VM.
This ensures both VMs can communicate with each other on the same network.
Verify subnet selection (use the same subnet as your Windows VM).
Configure Network Security Group to allow necessary traffic:

Ensure SSH (port 22) is allowed for remote management.
Add any additional ports needed for your specific applications.

Review advanced networking settings if you need specific IP configurations.

Before finalizing the deployment:

Click "Review + create".
Azure will validate your configuration.
Verify all settings are correct, particularly:

Confirm the same resource group as your Windows VM.
Confirm the same virtual network as your Windows VM.
Verify region is consistent with your Windows VM.

After validation passes, click "Create" to deploy the Ubuntu Server VM.
The deployment process will take several minutes to complete.

</p>
<br />

<p>
<img src="https://i.imgur.com/vtOEjma.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Locate your VM's public IP address: 
  
Go to the Azure Portal.
Navigate to "Virtual Machines".
Select your Windows 10 VM.
Note the public IP address displayed on the Overview page.

Launch Remote Desktop Connection:

On your local computer, press Win+R to open Run.
Type "mstsc" and press Enter.
The Remote Desktop Connection window will appear.

Configure the connection:

Enter the public IP address of your VM in the "Computer" field.
Click "Show Options" to expand additional settings.
Under the "User name" field, enter your VM credentials (e.g., "labuser").
You can save these connection settings for future use.

Connect to the VM:

Click "Connect".
When prompted, enter your password (e.g., "WhateverPassword1!").
You may receive a certificate warning - select "Yes" to proceed.

Begin working in your Windows 10 environment:
After successful authentication, the Windows 10 desktop will load.
You now have full access to your virtual machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/vltSAV5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Download Wireshark:

Open a web browser within your VM.
Navigate to wireshark.org/download.html.
Select the Windows Installer (64-bit) option.
Save the executable file to a convenient location (e.g., Downloads folder).

Run the Installer:

Locate and double-click the downloaded file.
If prompted by User Account Control, click "Yes".
When the installer launches, follow these steps:

Accept the license agreement.
Keep all components selected (default).
Accept default installation location.
Allow the installation of WinPcap/Npcap packet capture drivers.

Complete Installation:

Wait for the installation to complete.
Check the option to launch Wireshark when finished.
Click "Finish".


Initial Configuration:

When Wireshark opens for the first time, it will display available network interfaces.
The interface connected to your network will typically show some activity.
Click on your main network interface to begin capturing packets.

  <p>
<img src="https://i.imgur.com/RX371Z4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Launch Wireshark:

Locate Wireshark in the Start menu or desktop.
Double-click to open the application.

Select Network Interface:

In the Wireshark main window, you'll see a list of available network interfaces.
Identify your active network connection (usually labeled as Ethernet or Wi-Fi).
Double-click on the appropriate interface or select it and click the blue shark fin icon.

Begin Capture:

Packets will immediately start appearing in the main window.
Each line represents a single packet traveling through your network.
The packet list shows source, destination, protocol, and other information.

Monitor Traffic:

The live capture displays packets color-coded by protocol type.
TCP connections appear in light purple.
UDP traffic in light blue.
DNS queries in light green.
HTTP traffic in light blue.

Stop Capture:

Click the red square button in the toolbar when finished.
You can save the capture file for later analysis if needed.
</p>
<br />

<p>
<img src="https://i.imgur.com/0iIPkf5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Start with Active Capture:

Ensure Wireshark is open and actively capturing packets.
Alternatively, open a previously saved capture file.

Apply the ICMP Filter:

Locate the filter bar at the top of the Wireshark window.
Type icmp in the filter field.
Click the blue arrow button or press Enter to apply the filter.

Verify the Filter:

The display will now show only ICMP packets.
The status bar will indicate "ICMP" as the active filter.
If no packets appear, there may not be any ICMP traffic yet.
</p>
<br />

<p>
<img src="https://i.imgur.com/L3inWE7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Retrieve the Ubuntu VM's Private IP:
  
Check Azure portal for the private IP address.

Open PowerShell on your Windows 10 VM:

Right-click Start button → select Windows PowerShell.
Or press Win+X and select Windows PowerShell.

Perform the Ping Test using PowerShell:

In your PowerShell window:
Execute the ping command: ping [Ubuntu-VM-Private-IP]
Example: ping 10.0.0.5
A successful ping will show replies with time statistics.

Observe ICMP Traffic in Wireshark:

Watch as the ICMP packets appear in pairs in the Wireshark window:

Echo requests from your Windows VM (source) to Ubuntu VM (destination).
Echo replies from Ubuntu VM (source) back to Windows VM (destination).

Each request/reply pair corresponds to one ping iteration.

Analyze Packet Details:

Click on any ICMP packet to examine:

Protocol hierarchy (IP → ICMP).
Echo request/reply message type.
Sequence numbers that match between requests and replies.
Timestamp information showing round-trip time.

Verify Connection Between VMs:

Successful pings confirm network connectivity between your VMs.
Check for consistent response times and no packet loss.

  <p>
<img src="https://i.imgur.com/KAAR8lo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Start Continuous Ping:

Use the PowerShell continuous ping command:
ping  [Ubuntu-VM-Private-IP] -t.
Example: ping 10.0.0.5 -t.
This will send ICMP echo requests indefinitely until stopped.
</p>
<br />

<p>
<img src="https://i.imgur.com/QEmvmbQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Modify the Ubuntu VM's Network Security Group:

Access the Azure Portal.
Navigate to Network Security Groups.
Select the NSG associated with your Ubuntu VM.
Click "Inbound security rules".
Add a new rule:

Priority: 290 (lower than 300).
Protocol: ICMPv4.
Action: Deny.
Destination port ranges: *.

Click "Save" to apply the rule.
</p>
<br />

<p>
<img src="https://i.imgur.com/UWdYV2t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe Blocked Traffic:

Return to your Windows 10 VM.
Watch the PowerShell window as "Request timed out" messages appear.
In Wireshark, notice:

Echo requests continue to be sent.
No echo replies are being received.
Only one-way traffic is visible.

  <p>
<img src="https://i.imgur.com/v1gSLxh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Remove the Blocking Rule:

Return to the Azure Portal.
Navigate to the same Network Security Group.
Find your "Block-ICMP" rule.
Select the rule and click "Delete".
Confirm the deletion.
</p>
<br />

<p>
<img src="https://i.imgur.com/omBNAOb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Verify Restored Connectivity:

Return to the Windows 10 VM.
Observe in PowerShell that ping replies resume.
Watch Wireshark as two-way ICMP traffic (requests and replies) returns.
Note the timestamp when connectivity resumed.
</p>
<br />

<p>
<img src="https://i.imgur.com/O2GIKSP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Stop the Continuous Ping:

In PowerShell, press Ctrl+C to terminate the ping command.
The console will display a summary of packets sent, received, and lost.

  <p>
<img src="https://i.imgur.com/DhN4AHG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Prepare Wireshark for SSH Capture:
  
Start a new packet capture on your main network interface.
Apply an SSH filter by typing ssh or tcp.port==22 in the filter bar.
Click the blue arrow or press Enter to activate the filter.
Confirm the filter appears in green, indicating it's active.
</p>
<br />

<p>
<img src="https://i.imgur.com/f2ZxXQ2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Initiate SSH Connection to Ubuntu VM:

Open PowerShell as administrator.
Use the SSH command with your Ubuntu VM's private IP:
ssh labuser@10.0.0.5.
If prompted about host authenticity, type yes to continue.
Enter your password when prompted (not visible as you type).
</p>
<br />

<p>
<img src="https://i.imgur.com/AxL1OO7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Interact with the SSH Session:

Run various Linux commands to generate traffic:

whoami (shows current user).
pwd (shows current directory).
ls -la (lists files with details).

Watch Wireshark as each command generates bursts of packets.
Note how even short commands create multiple packets due to SSH protocol overhead.

<br />


<p>
<img src="https://i.imgur.com/fnmWiZt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Terminate the SSH Session:

Type exit and press Enter to close the connection.
In Wireshark, observe the SSH termination packets:

SSH disconnect messages.
TCP connection termination sequence (FIN, ACK).
</p>
<br />

<p>
<img src="https://i.imgur.com/6hYTVXl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Configure Wireshark for DHCP Capture:

Start a new packet capture on your main network interface.
Type dhcp in the filter field.
Click the blue arrow or press Enter to activate the filter.
Verify the filter turns green, indicating it's active.
The filter includes BOOTP because DHCP is built on the BOOTP protocol.
</p>
<br />

<p>
<img src="https://i.imgur.com/ikmFQtr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Initiate DHCP Renewal Process:

Launch PowerShell as Administrator.

Right-click on Start → Windows PowerShell (Admin).
Accept the UAC prompt if it appears.


Execute the IP address renewal command:
ipconfig /renew.

Watch as PowerShell shows "Windows IP Configuration" and begins the renewal process.

<p>
<img src="https://i.imgur.com/dP1WUO5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Configure Wireshark for DNS Filtering:

Open Wireshark and start capturing on your main network interface.
Enter dns in the filter bar and apply it.
Confirm the filter shows green, indicating it's active.
The display will now show only DNS protocol packets.
</p>
<br />

<p>
<img src="https://i.imgur.com/hilDiXZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Execute DNS Lookups for Google and Disney:

In PowerShell, run:
nslookup google.com

Watch Wireshark as DNS query and response packets appear.
Then run:
nslookup disney.com

Observe the second set of DNS transactions.
</p>
<br />

<p>
<img src="https://i.imgur.com/lEVmgj6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Configure Wireshark for RDP Filtering:

Open Wireshark with an active capture on your main network interface.
Enter tcp.port == 3389 in the filter bar.
Click the blue arrow or press Enter to apply the filter.
Verify the filter appears green, indicating it's active.

Observe Active RDP Traffic:

The display will immediately fill with RDP packet data.
These packets represent the ongoing Remote Desktop connection between your local computer and the Windows 10 VM.
Note the high volume of traffic—RDP continuously streams screen updates and input data.

Analyze RDP Protocol Characteristics:

Examine the packet list to observe:

Consistent flow of packets in both directions.
Regular packet timing patterns.
Varying packet sizes depending on screen activity.

Select individual packets to see details:

TCP headers showing source and destination ports (3389 for RDP).
Encrypted payload data (RDP uses TLS encryption).
Session information in the connection establishment packets.

Generate Additional RDP Traffic:

Move your mouse or type in the VM.
Watch Wireshark display increased packet activity.
Observe how changing windows or complex screen updates generate larger bursts of packets.

Identify RDP Session Components:

Connection establishment packets (beginning of the session).
Continuous data exchange packets (during active use).
Keepalive packets (during periods of inactivity).
The RDP protocol efficiently compresses and encrypts all data.

<br />
