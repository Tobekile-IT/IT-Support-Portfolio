# Tobekile Mazula | IT Support & Systems Portfolio

I'm an aspiring IT Support professional building hands-on experience in Windows administration, Active Directory, Microsoft 365, networking, virtualization, and cybersecurity incident response through practical simulations and home lab projects.

I am currently expanding my skills toward Network Engineering through structured troubleshooting scenarios, Windows Server administration, networking labs, and enterprise-style support simulations.

My goal is to continuously expand this portfolio with practical troubleshooting scenarios, system administration tasks, networking projects, and home lab implementations that demonstrate my technical development and problem-solving process.

---

## 🏆 Professional Certifications

### Google IT Support Professional Certificate

- Covered IT support fundamentals, operating systems, networking, system administration, security, and troubleshooting.

### Cisco Networking Academy — Network Technician Career Path

- Covered networking fundamentals, switching, routing concepts, TCP/IP, VLANs, and enterprise network troubleshooting.

### Cisco Networking Academy — IT Support Specialist Career Path

- Covered IT support fundamentals, troubleshooting methodology, hardware and software support, operating systems, networking, security, customer support, and technical documentation.

---

## 📚 Currently Studying

- Cisco CCNA / Introduction to Networks
- ITIL 4

---

## 🛠 Technical Skills

### Operating Systems

- Windows 10
- Windows 11
- Windows Server
- Ubuntu Linux

### Identity & Administration

- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Organizational Unit (OU) Management
- User Account Administration
- Security Group Management
- Password Resets & Account Unlocks
- Microsoft 365 Administration
- Multi-Factor Authentication (MFA)

### Windows Server & File Services

- Windows Server Administration
- SMB File Sharing
- NTFS Permissions
- Share Permissions
- Group-Based Access Control
- Departmental File Shares
- File & Folder Access Troubleshooting
- Group Policy Management
- Group Policy Preferences
- Mapped Network Drive Deployment
- Item-Level Targeting

### Networking

- TCP/IP
- DNS Troubleshooting
- DHCP Fundamentals
- IP Configuration
- Network Connectivity Testing
- SMB Connectivity
- VLAN Fundamentals
- VPN Troubleshooting
- NTP / Windows Time Troubleshooting

### Virtualization

- Oracle VirtualBox
- Windows Server Virtual Machine
- Windows 10 Virtual Machine
- Ubuntu Linux Virtual Machine
- Virtual Network Configuration

### Troubleshooting & Support Tools

- PowerShell
- Command Prompt
- `ipconfig`
- `ping`
- `tracert`
- `nslookup`
- `netstat`
- `arp`
- `net use`
- `gpupdate`
- `w32tm`
- `tzutil`
- Event Viewer
- Task Manager
- Remote Desktop (RDP)
- AnyDesk

### IT Support

- Hardware Diagnostics
- Software Installation
- Printer Troubleshooting
- User Account Management
- Remote Support
- Network Troubleshooting
- DNS Troubleshooting
- File & Folder Access Management
- Group Policy Troubleshooting
- Incident Documentation
- Service Desk Troubleshooting
- Root Cause Analysis
- Basic SLA Awareness

---

# 🖥️ IT Support Projects

The following projects demonstrate hands-on practice in IT Support, system administration, Windows Server, networking, cybersecurity, and enterprise troubleshooting through practical simulations and home lab environments.

Each project documents the troubleshooting process, configuration steps, commands used, verification, resolution, and lessons learned.

---

# 🎫 Help Desk & System Administration

Hands-on Service Desk tickets completed through practical simulations and home lab scenarios.

The tickets cover hardware troubleshooting, Active Directory, Microsoft 365 administration, account management, file and folder permissions, employee onboarding, cybersecurity incident response, endpoint support, DNS, networking, remote connectivity, Windows administration, SMB file services, Active Directory access control, and Group Policy administration.

## Completed Tickets

- **Ticket 01** – Customer PC Won't Turn On
- **Ticket 02** – BitLocker Recovery Key
- **Ticket 03** – VPN Connection Drops Intermittently
- **Ticket 04** – Phishing Email Malware Incident Response
- **Ticket 05** – Browser Scareware Removal
- **Ticket 06** – Warehouse Laptop Replacement and Deployment
- **Ticket 07** – Incident Response – Suspected Account Compromise
- **Ticket 08** – Enterprise Identity and Access Management
- **Ticket 09** – Mail Client Attachment Download Failure and Application Repair
- **Ticket 10** – External Monitors Went Black After Desk Relocation
- **Ticket 11** – Remote Connection Drops Due to ISP Connectivity Issues
- **Ticket 12** – DNS Misconfiguration Preventing Internet Access
- **Ticket 13** – Reset Locked Account
- **Ticket 14** – New Employee Setup – Create AD Account and Assign Groups
- **Ticket 15** – User Cannot Open Shared Folder
- **Ticket 16** – Promotion – Erik Karlsson Moving from Sales to IT
- **Ticket 17** – Onboarding – New Finance Employee Needs Full Setup
- **Ticket 18** – Ransomware Incident
- **Ticket 19** – SMB File Share Permission Troubleshooting
- **Ticket 20** – Departmental Folder Access Using Active Directory Security Groups
- **Ticket 21** – Automatic Finance Drive Mapping Using Group Policy

---

# 🆕 Recent Home Lab Tickets

## Ticket 19 — SMB File Share Permission Troubleshooting

Configured and troubleshot an SMB file share between Windows lab systems.

The scenario demonstrated how SMB share permissions and NTFS permissions combine to determine effective network access.

### Skills Demonstrated

- SMB file sharing
- TCP port 445 connectivity testing
- Share permission troubleshooting
- NTFS permission analysis
- PowerShell administration
- UNC path testing
- Read vs write permission troubleshooting
- Effective permission analysis
- Network file-access verification

### Key Troubleshooting Result

The client could successfully reach and read the SMB share but could not create files.

Investigation showed that the SMB share permission allowed:

```text
Everyone → Read
```

while the underlying NTFS permissions allowed broader access.

The share permission was updated to:

```text
Everyone → Change
```

Write access was then successfully verified from the client.

---

## Ticket 20 — Departmental Folder Access Using Active Directory Security Groups

Configured a departmental Finance file share using Active Directory security-group-based access control.

Instead of assigning permissions directly to individual users, access was assigned through:

```text
CORP\Finance Users
```

### Access Design

```text
Active Directory User
        ↓
Finance Users Security Group
        ↓
SMB Share Permission: Change
        ↓
NTFS Permission: Modify
        ↓
Departmental File Access
```

### Skills Demonstrated

- Active Directory security groups
- Group membership verification
- SMB share configuration
- NTFS permissions
- Permission inheritance
- Group-based access control
- PowerShell ACL verification
- SMB session troubleshooting
- Credential-based network authentication
- Authorised vs unauthorised access testing

### Verification

The final configuration successfully demonstrated:

```text
CORP\Administrator → Access Denied

CORP\apetrova
      ↓
Finance Users
      ↓
SMB: Change
      ↓
NTFS: Modify
      ↓
Access Allowed
      ↓
Finance-Test.txt Created Successfully
```

This confirmed both authorised access and write permissions while demonstrating that an account outside the Finance access configuration was denied.

---

## Ticket 21 — Automatic Finance Drive Mapping Using Group Policy

Configured an Active Directory Group Policy to automatically deploy the Finance departmental network share to authorised domain users.

A Group Policy Object named:

```text
Finance Drive Mapping
```

was linked to the Finance Organizational Unit.

Using **Group Policy Preferences**, the following drive mapping was configured:

```text
Finance (F:)
      ↓
\\10.10.10.21\Finance-Share
```

### Group Policy Configuration

The mapped drive was configured through:

```text
User Configuration
      ↓
Preferences
      ↓
Windows Settings
      ↓
Drive Maps
```

The configuration used:

```text
Action:       Update
Location:     \\10.10.10.21\Finance-Share
Label:        Finance
Drive Letter: F:
Reconnect:    Enabled
```

### Security Group Targeting

Item-Level Targeting was configured so that the mapped drive would only be deployed when the logged-in user was a member of:

```text
CORP\Finance Users
```

The deployment design was:

```text
Finance OU
      ↓
Finance Drive Mapping GPO
      ↓
User Configuration
      ↓
Group Policy Preferences
      ↓
CORP\Finance Users
Item-Level Targeting
      ↓
Finance (F:)
      ↓
\\10.10.10.21\Finance-Share
```

### Group Policy Troubleshooting

During deployment testing, the following command was used:

```cmd
gpupdate /force
```

Computer Policy initially failed because Windows reported that the workstation clock was not synchronized with a Domain Controller.

The issue was investigated rather than bypassed.

The troubleshooting process included:

```text
Verify domain connectivity
      ↓
Verify DNS configuration
      ↓
Verify Windows Time source
      ↓
Inspect Domain Controller time configuration
      ↓
Compare Windows time zones
      ↓
Measure NTP clock offset
      ↓
Compare UTC values
      ↓
Identify Domain Controller clock discrepancy
      ↓
Correct time configuration
      ↓
Resynchronize workstation
      ↓
Reapply Group Policy
```

### Diagnostic Tools Used

```text
w32tm /query /source
w32tm /query /status
w32tm /query /configuration
w32tm /stripchart
w32tm /resync
tzutil
ipconfig
Get-Date
gpupdate
```

The Windows 10 workstation correctly used:

```text
LAB-DC01.corp.local
```

as its Windows Time source and:

```text
10.10.10.10
```

as its DNS server.

NTP testing using:

```cmd
w32tm /stripchart /computer:LAB-DC01.corp.local /samples:5 /dataonly
```

identified a significant underlying clock discrepancy.

The Domain Controller's time configuration was corrected and the workstation was resynchronized.

Group Policy was then successfully refreshed:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

### Verification

The policy was tested using:

```text
CORP\apetrova
```

After Group Policy successfully applied, Windows automatically displayed:

```text
Finance (F:)
```

under **Network locations**.

No manual drive mapping was performed during Anna's session.

Anna successfully opened the mapped drive and accessed the existing Finance content.

A final write test was performed by creating:

```text
Anna-GPO-write-Test.txt
```

inside:

```text
Finance (F:)
```

The file was successfully created.

This verified the complete access chain:

```text
CORP\apetrova
      ↓
Finance OU
      ↓
Finance Drive Mapping GPO
      ↓
CORP\Finance Users
      ↓
Item-Level Targeting
      ↓
Finance (F:)
      ↓
SMB Share
      ↓
NTFS Modify Permission
      ↓
Successful Write Access
```

### Skills Demonstrated

- Group Policy Management
- Group Policy Preferences
- User Configuration policies
- Mapped network drive deployment
- Item-Level Targeting
- Active Directory security groups
- Organizational Unit-based policy deployment
- SMB file sharing
- NTFS permission verification
- Domain-user policy testing
- Windows Time Service troubleshooting
- NTP offset analysis
- DNS verification
- `gpupdate` troubleshooting
- PowerShell administration
- Command-line diagnostics
- Root cause analysis
- End-user access validation

---

# 🔧 Recent Skills Demonstrated

Recent ServiceDesk, TechSim, and Windows home lab projects have expanded my practical experience into:

- Active Directory user administration
- Organizational Unit (OU) management
- Security group management
- Account lockout troubleshooting
- Employee onboarding
- Role-based access management
- Microsoft 365 licensing
- SMB file sharing
- NTFS permissions
- Share permissions
- Group-based access control
- Departmental folder access
- SMB session troubleshooting
- File and shared-folder access
- Group Policy Management
- Group Policy Preferences
- Mapped network drive deployment
- Item-Level Targeting
- Organizational Unit-based policy deployment
- DNS troubleshooting
- Network connectivity troubleshooting
- Windows Time Service troubleshooting
- NTP synchronization troubleshooting
- Group Policy troubleshooting
- PowerShell administration
- Command-line troubleshooting
- Root cause analysis
- Ransomware identification
- Endpoint isolation
- Security incident escalation
- Incident documentation

---

# 🖥️ Windows Server Home Lab

A dedicated Windows Server and Windows client home lab built to strengthen practical system administration, Active Directory, networking, access-control, Group Policy, and troubleshooting skills.

## Current Environment

### LAB-DC01

```text
IP Address: 10.10.10.10
Role: Windows Server / Domain Controller
Domain: corp.local
```

Used for:

- Active Directory Domain Services
- User administration
- Organizational Units
- Security groups
- Group membership
- Group Policy Management
- Group Policy Preferences
- Domain administration
- Windows Time administration and troubleshooting
- PowerShell Active Directory management

### Windows 10 Lab

```text
IP Address: 10.10.10.21
Role: Windows client / SMB file-share host
Domain Environment: corp.local
```

Used for:

- Domain-user testing
- Group Policy testing
- Automatically mapped network drives
- SMB file shares
- NTFS permissions
- Network access testing
- Windows troubleshooting
- Client/server connectivity testing

---

# ✅ Completed Windows Home Lab Projects

## Lab 01 — Active Directory Organizational Units & User Account Management

Practised:

- Creating and managing OUs
- User account administration
- Security groups
- Department-based identity organisation
- Active Directory administration

---

## Ticket 19 — SMB File Share Permission Troubleshooting

Practised:

- SMB shares
- Share permissions
- NTFS permissions
- Port 445 testing
- Network file access
- Read/write troubleshooting

---

## Ticket 20 — Departmental Folder Access Using AD Security Groups

Practised:

- AD security groups
- Department-based permissions
- SMB Change permissions
- NTFS Modify permissions
- Authorised/unauthorised testing
- SMB session troubleshooting
- Group-based access control

---

## Ticket 21 — Automatic Finance Drive Mapping Using Group Policy

Practised:

- Group Policy Management
- Group Policy Preferences
- User Configuration policies
- Mapped network drives
- Item-Level Targeting
- Security group targeting
- OU-based policy deployment
- Domain-user policy testing
- `gpupdate` troubleshooting
- Windows Time Service troubleshooting
- NTP offset analysis
- DNS verification
- End-user access validation
- Root cause analysis

---

# 🧪 Home Lab Environment

- ✅ Windows Server Virtual Machine
- ✅ Windows 10 Virtual Machine
- ✅ Ubuntu Linux Virtual Machine
- ✅ Active Directory Domain Environment
- ✅ Active Directory Users & Groups
- ✅ Organizational Units
- ✅ Security Group-Based Access Control
- ✅ SMB File Sharing
- ✅ NTFS Permissions
- ✅ Share Permissions
- ✅ Group-Based File Access
- ✅ Departmental File Shares
- ✅ Group Policy Management
- ✅ Group Policy Preferences
- ✅ Automated Mapped Network Drives
- ✅ Item-Level Targeting
- ✅ Windows Time / Domain Time Troubleshooting
- ✅ Windows Installation & Deployment
- ✅ Virtual Machine Configuration
- ✅ ISO Installation & Virtual Disk Management
- ✅ Client/Server Network Connectivity

---

# 🚧 Planned Lab Expansion

The home lab will continue expanding into:

- 🔄 Domain-Joined Workstation Administration
- 🔄 DNS Server Administration
- 🔄 DHCP Server Administration
- 🔄 Advanced Group Policy Configuration
- 🔄 Advanced Account & Access Troubleshooting
- 🔄 Server & Network Troubleshooting
- 🔄 File & Print Services
- 🔄 Windows Server Backup

---

# 🎯 Career Development

My current focus is strengthening practical IT Support and networking skills while progressing toward Network Engineering.

Current development areas include:

```text
IT Support
    ↓
Windows / Active Directory Administration
    ↓
Networking & Troubleshooting
    ↓
CCNA
    ↓
Network Support / Network Technician
    ↓
Network Engineering
```

The goal of this portfolio is to document that progression through practical work rather than certifications alone.

---

# 📬 Contact

📧 **Email:** Tobekilemazula111@gmail.com

💼 **LinkedIn:**  
www.linkedin.com/in/tobekile-mazula-39b04a1ba

💻 **GitHub:**  
https://github.com/Tobekile-IT

---

⭐ **Thank you for visiting my portfolio.**

This repository is continuously updated with new troubleshooting scenarios, Windows Server projects, networking labs, Service Desk simulations, and home lab implementations as I continue developing my IT career.
