# Windows Server 2022 Enterprise Infrastructure
<h1>Active Directory Domain Services (AD DS) Foundation & Initial Setup</h1>



<h2>Description</h2>
This project demonstrates the deployment of a Windows Server Active Directory environment designed to mirror a small corporate network. A Windows Server virtual machine was installed and promoted to a Domain Controller to establish centralized authentication and management. A custom domain (JosephMinton.local) was created, along with a structured Organizational Unit (OU) hierarchy for departments such as IT, HR, and Sales. User accounts and department-based security groups were configured within these OUs to support organized administration and role-based access control.
<br />

<h2>Objective</h2>

<p>Set up an Active Directory (AD) domain from scratch to simulate a corporate IT environment and practice standard AD administrative tasks.</p>
<ul>
<li><strong>Install windows server in a virtual machine.</li>
<li><strong>Promote the server to a Domain Controller (DC)</li>
<li><strong>Create an AD domain (e.g., JosephMinton.local).</li>
<li><strong>Create organizational units (OUs) for different departments (e.g., IT, HR, Sales).</li>
<li><strong>Create user accounts and groups within these OUs.</li>
</ul>

<h2>Languages and Utilities Used</h2>

- <b>VMware Workstation</b> 
- <b>Server Windows 2022</b>
- <b>Active Directory</b>

<h2>Environments Used </h2>

<p align="center">
Enviornment Setup: <br/>
<img src="https://i.imgur.com/UILWFbG.png" alt="Disk Sanitization Steps"/>
<br />

- <b>Installed Windows Server in a virtual machine to provide a controlled environment for Active Directory testing.</b> 
- <b>Promoted the server to a Domain Controller (DC) to manage domain services such as authentication, authorization, and policy enforcement.</b>
- <b>Created an AD domain: JosephMinton.local. This naming convention follows common lab practice using .local for internal networks.</b>

Azure Active Directory is Microsoft’s cloud-based identity and access management service that lets organizations securely manage users, devices, and app access.
 
 <br/>
 First look of Active Directory  <br/>
<img src="https://i.imgur.com/Ln6tg4z.png" alt="Disk Sanitization Steps"/>
<br />

An Organizational Unit (OU) is a container in Active Directory that organizes users, computers, and groups, making administration and Group Policy management easier without changing security boundaries.
 
Everything worked on in this lab is found under AD domain (JosephMinton.local)

<h2>I. Create OUs for different departments.</h2>
<ul>
  <li>USA</li>
  <li>Europe</li>
  <li>Asia</li>
</ul>
<br/>
 Adding the primary OUs  <br/>
<img src="https://i.imgur.com/uYsJayZ.png" alt="Disk Sanitization Steps"/>
<br />
<h2>II. Create user accounts and groups within these OUs.</h2>
<p>Add the following groups: Users, Computers, and Servers.</p>
<i>You can create another OU within an already made OU.</i>
<h3>Users</h3>
<ul>
  <li>IT</li>
  <li>Accounting</li>
  <li>HR</li>
  <li>Sales</li>
  <li>Executive</li>
  <li>Inactive</li>
</ul>
<h3>Computers</h3>
<ul>
  <li>IT-Workstation01</li>
  <li>IT-Workstation2</li>
  <li>IT-Workstation3</li>
</ul>
<h3>Servers</h3>
<ul>
  <li>USA-Accounting-SVR01</li>
  <li>USA-HR-SVR01</li>
  <li>USA-IT-SVR01</li>
  <li>USA-IT-SVR02</li>
  <li>USA-Sales-SVR01</li>
  <li>USA-Executive-SVR01</li>
</ul>
<p>When creating a new group inside an OU for example Users, you can name the group but you also have the option of selecting the Group scope and Group type. Avoid naming conflicts: groups and OUs can share names in different OUs, but objects within the same container must have unique names. </p>
 <br/>
 Creating a new Object Group  <br/>
<img src="https://i.imgur.com/zUlWxbz.png" alt="Disk Sanitization Steps"/>
<br />
<h2>Group Scope</h2>
<p>Active Directory groups have three scope options that determine where the group can be used and what it can contain:</p>
<ul>
    <li><strong>Domain Local:</strong> Used to assign permissions to resources within a single domain.</li>
    <li><strong>Global:</strong> Used to group users from the same domain. Commonly used for role-based access.</li>
    <li><strong>Universal:</strong> Used across multiple domains in a forest. Typically avoided unless necessary due to replication impact.</li>
</ul>

<h2>Group Type</h2>
<p>Active Directory supports two group types:</p>
<ul>
    <li><strong>Security:</strong> Used to assign permissions to resources such as files, folders, and applications.</li>
    <li><strong>Distribution (Distrolist):</strong> Used only for email distribution lists and cannot be used for access control.</li>
</ul>
<p>In this lab, Global Security Groups were used to organize users by department, following standard Active Directory best practices. Nesting OUs and using department-specific groups improves organization while maintaining flexibility for applying targeted Group Policies.</p>
<h3>Group Strategy Used</h3>
<ul>
  <li>Global Security Groups were created for each department.</li>
  <li>Users were added to department-specific Global groups.</li>
  <li>This approach supports role-based access and scalability.</li>
</ul>
<p>Department based OUs were created to simplify user administration and support future Group Policy assignment.</p>
 <br/>
 Brief visual of the final result  <br/>
<img src="https://i.imgur.com/7xqkbvQ.png" alt="Disk Sanitization Steps"/>
<br />
</p>

<h1>Key Takeaways</h1>
<ul>
<li><strong>Gained hands-on experience promoting a Windows Server to a Domain Controller and configuring core AD services.</li>
<li><strong>Designed and implemented a structured OU hierarchy based on geography and departments to support scalable administration.</li>
<li><strong>Created and managed user accounts, computers, servers, and groups within appropriate OUs.</li>
<li><strong>Applied Active Directory best practices by using Global Security Groups for department-based role assignment.</li>
 
</ul>
