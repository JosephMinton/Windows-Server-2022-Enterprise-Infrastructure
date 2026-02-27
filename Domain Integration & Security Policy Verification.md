# Enterprise Active Directory Security Governance Lab
<h1>Domain Integration & Security Policy Verification</h1>

<h2>Description</h2>
This lab is Part III of a multi-part Active Directory home lab series. This phase focuses on the integration of a Windows 11 client machine into the domain environment, ensuring proper DNS resolution, and verifying that the security policies (GPOs) configured in Part II are successfully enforced on end-user workstations.
<br />

<h2>Objective</h2>

<p>Successfully bridge the gap between server configuration and client-side enforcement to simulate a production Enterprise environment.</p>
<ul>
<li><strong>Establish Network Connectivity: Configure static IP and DNS settings on the Domain Controller to act as the primary name resolver.</li>
<li><strong>Perform a Domain Join: Connect a Windows 11 Pro/Enterprise client to the active domain.</li>
<li><strong>Validate GPO Inheritance: Move the client machine into the correct Organizational Unit (OU) to receive targeted policies.</li>
<li><strong>Force Policy Updates: Demonstrate the use of command-line utilities to trigger immediate security enforcement.</li>
</ul>

<h2>Languages and Utilities Used</h2>

- <b>VMware Workstation</b> 
- <b>Windows Server 2022 (Domain Controller)</b>
- <b>Windows 11 Pro/Enterprise (Client VM)</b>
- <b>Command Prompt (CMD)</b>
- <b>PowerShell</b>

<h1>I. Server Side Static IP & DNS Configuration</h1><br/>
 <p>Establishing a reliable anchor for the network by assigning a static IP to the Domain Controller. Servers must have static IPs to prevent client disconnection if a DHCP lease changes.</p>

<p>Action Taken Because the Settings app and Control Panel were inaccessible due to GPO restrictions implemented in Part II, I utilized PowerShell to configure the network interface.</p>
<ul>
<li><strong>Discovery: Identified the network adapter index (ifIndex 6) using Get-NetAdapter.</li>
<li><strong>Final Configuration: Successfully applied the static IP, Default Gateway, and DNS servers.</li>
<li><strong>DNS Resolution: Pointed the Primary DNS to the loopback address (127.0.0.1) so the server resolves domain queries through itself.</li>
</ul>
<img src="https://i.imgur.com/f8ZVEUP.png"/>
<br />
<img src="https://i.imgur.com/eqwjvWs.png"/>
<br />
<h2>What Went Wrong: Technical Troubleshooting Log</h2>
<p>During the initial setup, a configuration error occurred while manually inputting network parameters. This section details the identification and resolution of that issue.

Problem Encountered An incorrect IP address was initially assigned, and the Default Gateway was omitted during the first New-NetIPAddress attempt. This resulted in an "ambiguous" state where the adapter had multiple IP assignments and no routing path to the internet.</p>
<img src="https://i.imgur.com/hsZYLDe.png"/>
<br />
 <br><br>
<p>Remediation Workflow Instead of using the non-functional GUI, I resolved the conflict via the following PowerShell sequence:</p>
<p>1. Identify the incorrect assignment
ipconfig /all 

2. Remove the incorrect IP to clear the interface conflict
Remove-NetIPAddress -InterfaceIndex 6 -IPAddress [Incorrect_IP]

3. Re-apply the correct static IP with the Default Gateway included
New-NetIPAddress -InterfaceIndex 6 -IPAddress 192.168.x.x -PrefixLength 24 -DefaultGateway 192.168.x.1

4. Re-configure DNS for Active Directory functionality
Set-DnsClientServerAddress -InterfaceIndex 6 -ServerAddresses ("127.0.0.1", "8.8.8.8")
</p>
 <img src="blob:https://imgur.com/dc395571-bf85-4d62-a22f-aed4e16a626f"/>
<br />
<h2>Notes</h2>
<p>The use of Remove-NetIPAddress was critical here. PowerShell prevents "overwriting" an IP if a conflict exists on the same interface index. This workflow demonstrates the ability to audit network settings and perform manual remediation when standard management tools are restricted.</p>

<h1>II. Client-Side DNS Alignment</h1>

<p>Configuring the Windows 11 client to "see" the Domain Controller.</p>
<h2>Action Taken</h2>
<ul>
<li><strong>Network & Internet Settings > Advanced Network Settings > IPv4</strong></li>
<li><strong>Preferred DNS: Set to the exact static IP of the Windows Server (e.g., 192.168.42.128)</strong></li>
</ul>
<img src="blob:https://imgur.com/1e109140-afe3-4580-8959-2014ad1f22de"/>
<br />
<img src="https://i.imgur.com/z9pxwxt.png"/>
<br />
<h2>Notes</h2>
<p>The client cannot join the domain if it cannot find it. By pointing the client's DNS directly to the Domain Controller, we allow it to resolve the domain name (e.g., EastCharmer.local) to the server's IP.</p>


<h1>III. Computer Domain Join</h1>

<p>Executing the formal handshake between the workstation and the domain infrastructure.</p>
<h2>Configuration Path</h2>
<ul>
<li><strong>Settings > About > Advanced System Settings > Computer Name > Change</strong></li>
<li><strong>Member of: Selected "Domain" and entered the FQDN (Fully Qualified Domain Name)</strong></li>
<li><strong>Authentication: Entered Domain Admin credentials to authorize the join</strong></li>
</ul>
<img src="https://i.imgur.com/P0uMEJ1.png"/>
<br />

<h2>Notes</h2>
<p>This step creates a "Computer Object" in Active Directory. After the mandatory reboot, the machine is no longer a standalone entity but a managed asset of the enterprise.</p>


<h1>IV. GPO Linking & OU Management</h1>
<p>Organizing the new asset into the correct "bucket" to receive security policies.</p>
<h2>Action Taken</h2>
<ul>
<li><strong>Active Directory Users and Computers (ADUC): Moved the new computer from the "Computers" container to the targeted OU (e.g., USA > Computers)</li>
<li><strong>Group Policy Management Console (GPMC): Linked the Part II GPOs (Control Panel Restriction, Wallpaper, etc.) to the respective User and Computer OUs</li>
</ul>
 
<img src="https://i.imgur.com/4Pz1jvr.png"/>
<br />
<img src="https://i.imgur.com/K0qNjrS.png"/>
<br />

<h2>Notes</h2>
<p>Policies do not apply just because they exist. They must be "Linked" to an OU, and the user/computer objects must be physically moved into that OU within ADUC for the link to take effect.</p>


<h1>V. Policy Enforcement & Verification</h1>
<p>Manually triggering the Handshake to verify security controls are active.</p>
<h2>Action Taken</h2>
<ul>
<li><strong>Command: Executed gpupdate /force in the client Command Prompt</li>
<li><strong>Verification: Attempted to open the Control Panel to test the "Restrict Access" policy</li>
</ul>
<img src="https://i.imgur.com/sJpegQA.png"/>
<br />
<img src="https://i.imgur.com/mDIEvAX.png"/>
<br />

<h2>Notes</h2>
<p>While GPOs refresh automatically every 90 minutes, gpupdate /force is the essential Tier 1 troubleshooting tool to verify changes immediately. The successful block of the Control Panel confirms that our Part II security governance is functioning as intended.</p>

<h1>Key Takeaways</h1>
<ul>
<li><strong>DNS is the Foundation: 90% of domain join failures are DNS-related; the client must point to the DC</li>
<li><strong>Object Placement: Computers join a generic container by default; they must be moved to the correct OU to receive specific policies</li>
<li><strong>Verification: A successful lab isn't finished until the "Deny" or "Restriction" is visually confirmed on the client machine</li>
</ul>

<h1>Next Steps - Part IV</h1>
<ul>
In Part IV, I will focus on:
<li><strong>Setting up file shares and organizing department-specific folders for HR and IT</li>
<li><strong>Configuring NTFS and share permissions to manage folder visibility and user access levels</li>
<li><strong>Automating network drive mapping using Group Policy Preferences for domain users</li>
<li><strong>Implementing storage quotas and file screening with File Server Resource Manager (FSRM) to manage server space</li>
</ul>
