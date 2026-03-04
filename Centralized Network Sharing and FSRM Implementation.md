# Enterprise Active Directory Security Governance Lab
<h1>Centralized Network Sharing and FSRM Implementation</h1>

<h2>Description</h2>
This lab is Part IV of a multipart Active Directory home lab series. This phase focuses on the implementation of centralized file services, the critical distinction between Share and NTFS permissions, and the automation of network resource access via Group Policy Preferences. Additionally, the lab introduces storage governance through File Server Resource Manager (FSRM) to enforce storage limits and restrict unauthorized file types
<br />

<h2>Objective</h2>

<p>Successfully provision and manage network resources to ensure data availability and storage security within the Enterprise environment.</p>
<ul>
<li><strong>Provision Shared Resources: Create a centralized "shared" folder and configure tiered access controls</li>
<li><strong>Establish Permission Hierarchies: Implement and differentiate between Share permissions (folder level) and NTFS security settings (file/subfolder level)</li>
<li><strong>Automate Resource Access: Utilize Group Policy Preferences to deploy persistent mapped drives to domain users, replacing inefficient manual mapping</li>
<li><strong>Implement Storage Governance: Deploy FSRM to manage storage limits via quotas and restrict unauthorized file types through screening</li>
</ul>

<h2>Languages and Utilities Used</h2>

- <b>VMware Workstation</b> 
- <b>Windows Server 2022 (Domain Controller)</b>
- <b>Windows 11 Enterprise (Client VM)</b>
- <b>File Server Resource Manager (FSRM)</b>
- <b>Group Policy Management Console (GPMC)</b>
- <b>Command Prompt (CMD)</b>

<h1>I. Network Share Provisioning & Permission Hierarchies</h1><br/>
 <p>Establishing a centralized repository for company data to make editing and sharing of files easier for all users in the environment. This process requires a two layered security approach: Share permissions for network level access and NTFS permissions for granular file level control.</p>

<p>To facilitate resource sharing, I created a directory on the server's local storage and configured access for the "Domain Users" group.</p>
<ul>
<li><strong>Directory Creation: Created a folder named "shared" in the Local Disk (C:) path.</li>

<img src="https://i.imgur.com/RsQyaPN.png"/>
<br />
  
<li><strong>Share Level Configuration: Navigated to Properties > Sharing > Advanced Sharing and enabled "Share this folder".</li>
<li><strong>Access Control: Added "Domain Users" to the permissions list and set them to Read access.</li>
  <li><strong> - Discovery: Share permissions apply only at the folder level and do not affect individual subfolders or files.</li>
    <img src="blob:https://imgur.com/640bdbfc-c082-43ac-812b-37212c0c0d75"/>
<br />
<li><strong>NTFS Security Integration: Switched to the Security tab to configure detailed NTFS permissions, which apply to all subfolders and files within the directory.</li>
  <img src="https://i.imgur.com/FgBqFxj.png"/>
<br />
</ul>

<h1>II. Manual Mapping vs. Automated GPO Drive Mapping</h1>

<p>Verifying client-side connectivity by mapping the network resource to a local drive letter. While manual mapping is useful for temporary access, Group Policy Objects (GPOs) are used for permanent, automated enterprise wide deployment.</p>
<h2>Action Taken</h2>
<p>I transitioned from a session-based manual map to a persistent GPO-driven network share to ensure all users maintain access after reboots.</p>
<ul>
<li><strong>Hostname Identification: Utilized the hostname command in the Server's CMD to identify the server name required for the UNC path.</strong></li>
  <img src="https://i.imgur.com/y3oyJ14.png"/>
<br />
<li><strong>Client Verification: On the Windows client, I mapped the S: drive to \\ServerName\shared to confirm the folder was accessible over the network.</strong></li>
  <img src="https://i.imgur.com/aFFyZYb.png"/>
<br />
  <img src="https://i.imgur.com/5cWFiTf.png"/>
<br />
<li><strong>GPO Automation: Because manual maps are not persistent after a reboot, I created a GPO named "map drives".</strong></li>
<li><strong>Configuration: Under User Configuration > Preferences > Windows Settings > Drive Maps, I defined a new mapped drive with the server path and assigned it to drive letter S:</strong></li>
  <img src="https://i.imgur.com/uXqzBFO.png"/>
<br />

<img src="https://i.imgur.com/mIwDFLm.png"/>
<br />
<li><strong>Final Deployment: Linked the GPO to the Users OU and ran gpupdate /force on the client to automate the mapping process.</strong></li>

<img src="https://i.imgur.com/aVQA7Jd.png"/>
<br />
<img src="https://i.imgur.com/CaQMHer.png"/>
<br />
</ul>

<h2>Notes</h2>
<p></p>


<h1>III. Storage Governance via File Server Resource Manager (FSRM)</h1>

<p>Implementing administrative controls to manage and classify data stored on file servers. This prevents storage depletion by setting limits and restricting the upload of non-business related files.</p>
<h2>Action Path</h2>
<p>I installed the FSRM tool and implemented quotas and file screening on the "shared" folder to manage finite server hardware.</p>
<ul>
<li><strong>Tool Installation: Utilized Add Roles and Features in Server Manager to install File Server Resource Manager under File and Storage Services.</strong></li>

<img src="blob:https://imgur.com/e7866e3d-5261-4884-b75d-debda71d3981"/>
<br />
  
<li><strong>Quota Management: Created a custom quota for the "shared" folder with a 10GB limit.</strong></li>
<li><strong>Threshold Configuration: Set an 80% notification threshold to alert administrators before the storage limit is reached.</strong></li>

<img src="https://i.imgur.com/jeIl46d.png"/>
<br />
<img src="https://i.imgur.com/zkiiEwe.png"/>
<br />
<img src="https://i.imgur.com/PbFS38D.png"/>
<br />
<li><strong>Quota Management: Created a custom quota for the "shared" folder with a 10GB limit.</strong></li>
<li><strong>Threshold Configuration: Set an 80% notification threshold to alert administrators before the storage limit is reached.</strong></li>

<img src="<img width="821" height="281" alt="image" src="https://github.com/user-attachments/assets/4c367e43-f857-4315-93e4-d9e9d67783ca" />
"/>
<br />
<img src=""/>
<br />
<img src=""/>
<br />
<li><strong>File Screening: Implemented a screen to block Audio and Video files, Executable files, and Image files.</strong></li>
<li><strong>Final Configuration: Restricted the folder to text and document file types to prevent multimedia files from consuming excessive storage space.</strong></li>
<img src=""/>
<br />
<img src=""/>
<br />


</ul>
<h2>Notes</h2>
<p>Automating drive mapping via GPO Preferences ensures a consistent user experience while reducing manual administrative tasks. Simultaneously, FSRM provides a critical layer of storage governance, ensuring that the file server remains operational and is not filled with unauthorized or heavy multimedia data</p>



<h1>Key Takeaways</h1>
<ul>
<li><strong>DNS is the Foundation: 90% of domain join failures are DNS related; the client must point to the DC</li>
<li><strong>Object Placement: Computers join a generic container by default; they must be moved to the correct OU to receive specific policies</li>
<li><strong>Verification: A successful lab isn't finished until the Deny or Restriction is visually confirmed on the client machine</li>
</ul>

<h1>Next Steps - Part IV</h1>
<ul>
In Part IV, I will focus on:
<li><strong>Setting up file shares and organizing department specific folders for HR and IT</li>
<li><strong>Configuring NTFS and share permissions to manage folder visibility and user access levels</li>
<li><strong>Automating network drive mapping using Group Policy Preferences for domain users</li>
<li><strong>Implementing storage quotas and file screening with File Server Resource Manager (FSRM) to manage server space</li>
</ul>
