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

<p>
- <b>VMware Workstation</b> 
- <b>Windows Server 2022 (Domain Controller)</b>
- <b>Windows 11 Pro/Enterprise (Client VM)</b>
- <b>Command Prompt (CMD)</b>
- <b>PowerShell</b>
</p>

<p align="center">
First visual of Group Policy Management: <br/>
<img src="https://i.imgur.com/wjQv2oA.png" alt="Disk Sanitization Steps"/>
<br />
<h1>I. Password Policy (New GPO)</h1><br/>
 <p>Enforce strong password requirements across the domain to improve security posture.</p>
<h2>Configuration Path</h2>
<p>Computer Configuration</p>
<ul>
<li><strong>Policies</li>
<li><strong>Windows Settings</li>
<li><strong>Security Settings</li>
<li><strong>Account Policies</li>
<li><strong>Password Policy</li>
</ul>
<img src="https://i.imgur.com/sAkdpA7.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/s17w6r8.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/sm6VB0Q.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/dhzPe5D.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Notes</h2>
<p>Password policies are configured under Computer Configuration because they apply at the domain level rather than per user.
Using Policies ensures the settings cannot be overridden by end users.

This reinforces centralized credential security and aligns with baseline enterprise password standards.</p>
 <br><br>

<h1>II. Drive Mapping</h1>

<p>Automatically map network drives for users upon login.</p>
<h2>Configuration Path</h2>
<p>User Configuration</p>
<ul>
<li><strong>Preferences</strong></li>
<li><strong>Windows Settings</strong></li>
<li><strong>Drive Maps</strong></li>
</ul>
<img src="https://i.imgur.com/M1w0pOp.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Notes</h2>
<p>Drive mapping was configured using Preferences rather than Policies because:</p>
<ul>
<li><strong>Preferences allow flexibility</strong></li>
<li><strong>Settings can be changed or removed without strict enforcement</strong></li>
<li><strong>This mirrors real world environments where mapped drives may vary by role or department</strong></li>
</ul>
<p>This demonstrates the difference between user convenience configurations and security enforcement.</p>

<h1>III. Desktop Wallpaper Policy</h1>

<p>Set a default desktop wallpaper for all users and prevent users from changing it.</p>
<h2>Configuration Path</h2>
<p>User Configuration</p>
<ul>
<li><strong>Policies</strong></li>
<li><strong>Administrative Templates </strong></li>
<li><strong>Desktop</strong></li>
<li><strong>Desktop Wallpaper</strong></li>
</ul>
<img src="https://i.imgur.com/riLGrof.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/LtzSohI.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/Uij1oTM.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Configuration Details</h2>
<ul>
<li><strong>Enabled Desktop Wallpaper policy</strong></li>
<li><strong>Set a defined file path for the wallpaper location</strong></li>
<li><strong>Configured wallpaper style to Fill</strong></li>
<li><strong>Applied and enforced the policy</strong></li>
</ul>
<h2>Notes</h2>
<p>This policy was intentionally placed under User Configuration → Policies because:</p>
<ul>
<li><strong>The setting is user facing</strong></li>
<li><strong>Administrative enforcement is required</strong></li>
<li><strong>Users should not be able to override or modify the wallpaper</strong></li>
</ul>
<p>This mirrors corporate branding and compliance scenarios in enterprise environments.</p>

<h1>IV. Restrict Access to Control Panel</h1>
<p>Prevent users from accessing the Control Panel and PC Settings.</p>
<h2>Configuration Path</h2>
<p>User Configuration</p>
<ul>
<li><strong>Policies</li>
<li><strong>Administrative Templates</li>
<li><strong>Control Panel</li>
<li><strong>Prohibit access to Control Panel and PC settings</li>
</ul>
<img src="https://i.imgur.com/zoK3yiB.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/U5qeD21.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Configuration Details</h2>
<ul>
<li><strong>Enabled “Prohibit access to Control Panel and PC settings”</strong></li>
<li><strong>Applied and enforced the GPO</strong></li>
</ul>
<h2>Notes</h2>
<p>This GPO was deliberately named after its function to maintain clarity and manageability.
Using Policies ensures the restriction is enforced and cannot be bypassed by the user.

This reflects common enterprise security practices where users are limited from altering system configurations.</p>

 <br/>
 By assigning the ticket to another specific higher tier, the ticket would be escalated.<br/>


<h1>V. Disable USB Storage</h1>
<p>Prevent the use of USB storage devices to reduce data exfiltration risk.</p>
<h2>Configuration Path</h2>
<p>Computer Configuration</p>
<ul>
<li><strong>Policies</li>
<li><strong>Administrative Templates</li>
<li><strong>Control Panel</li>
<li><strong>System</li>
<li><strong>Removable Storage Access</li>
</ul>
<img src="https://i.imgur.com/oee84Co.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/Y4qUIBM.png" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/P5RLxgd.png" alt="Disk Sanitization Steps"/>
<br />
</p>
<h2>Configuration Details</h2>
<ul>
<li><strong>Enabled “Prohibit access to Control Panel and PC settings”</strong></li>
<li><strong>Applied and enforced the GPO</strong></li>
</ul>
<h2>Notes</h2>
<p>This policy was applied under Computer Configuration because:</p>
<ul>
<li><strong>The restriction applies to the machine itself, not individual users</strong></li>
<li><strong>USB access should remain disabled regardless of who logs in</strong></li>
</ul>
<p>Using Policies ensures the setting cannot be overridden locally, which aligns with high security environments.</p>

This reflects common enterprise security practices where users are limited from altering system configurations.</p>

<h1>VI. Account Lockout Policy</h1>
<p>Mitigate brute force login attempts by enforcing account lockout rules.</p>
<h2>Configuration Path</h2>
<p>Computer Configuration</p>
<ul>
<li><strong>Policies</li>
<li><strong>Windows Settings</li>
<li><strong>Security Settings</li>
<li><strong>Account Policies</li>
<li><strong>Account Lockout Policy</li>
</ul>
 <img src="https://i.imgur.com/8tPdpU3.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Configuration Details</h2>
<ul>
<li><strong>Account lockout threshold: 5 invalid logon attempts</strong></li>
<li><strong>Account lockout duration: 30 minutes</li>
<li><strong>Reset account lockout counter after: 30 minutes</li>
</ul>
<h2>Notes</h2>
<p>This configuration balances:</p>
<ul>
<li><strong>Security against brute force attacks</li>
<li><strong>Usability to avoid excessive lockouts from accidental failures</li>
</ul>
<p>This is a foundational security control commonly found in real world domain environments.</p>

<h1>Key Takeaways</h1>
<ul>
<li><strong>GPO placement matters: User vs Computer Configuration determines scope and impact</li>
<li><strong>Policies enforce non-negotiable rules, while Preferences allow flexibility</li>
<li><strong>Naming GPOs clearly improves long term manageability</li>
<li><strong>Many enterprise security controls are implemented silently through GPOs</li>
<li><strong>Small configuration choices (like USB access or lockout thresholds) have large security implications</li>
</ul>

<h1>Next Steps – Part III</h1>
<ul>
In Part III, I will focus on:
<li><strong>Applying and testing GPOs on domain joined machines</li>
<li><strong>Verifying policy behavior using real user and computer logins</li>
<li><strong>Testing computer domain join behavior and how GPOs apply during and after the join process</li>
</ul>
This next phase will validate that the policies configured in this lab are functioning as intended in practice, not just configured correctly.
