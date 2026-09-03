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

### Networking

- TCP/IP
- DNS Troubleshooting
- DHCP Fundamentals
- IP Configuration
- Network Connectivity Testing
- SMB Connectivity
- VLAN Fundamentals
- VPN Troubleshooting

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
- Incident Documentation
- Service Desk Troubleshooting
- Basic SLA Awareness

---

# 🖥️ IT Support Projects

The following projects demonstrate hands-on practice in IT Support, system administration, Windows Server, networking, cybersecurity, and enterprise troubleshooting through practical simulations and home lab environments.

Each project documents the troubleshooting process, configuration steps, commands used, verification, resolution, and lessons learned.

---

# 🎫 Help Desk & System Administration

Hands-on Service Desk tickets completed through practical simulations and home lab scenarios.

The tickets cover hardware troubleshooting, Active Directory, Microsoft 365 administration, account management, file and folder permissions, employee onboarding, cybersecurity incident response, endpoint support, DNS, networking, remote connectivity, and Windows administration.

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

---

## 🆕 Recent Home Lab Tickets

### Ticket 19 — SMB File Share Permission Troubleshooting

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

### Ticket 20 — Departmental Folder Access Using Active Directory Security Groups

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

## 🔧 Recent Skills Demonstrated

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
- DNS troubleshooting
- Network connectivity troubleshooting
- PowerShell administration
- Command-line troubleshooting
- Ransomware identification
- Endpoint isolation
- Security incident escalation
- Incident documentation

---

# 🖥️ Windows Server Home Lab

A dedicated Windows Server and Windows client home lab built to strengthen practical system administration, Active Directory, networking, access-control, and troubleshooting skills.

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
- Domain administration
- PowerShell Active Directory management

### Windows 10 Lab

```text
IP Address: 10.10.10.21
Role: Windows client / SMB file-share host
Domain Environment: corp.local
```

Used for:

- SMB file shares
- NTFS permissions
- Network access testing
- Windows troubleshooting
- Client/server connectivity testing

---

## Completed Windows Home Lab Projects

### Lab 01 — Active Directory Organizational Units & User Account Management

Practised:

- Creating and managing OUs
- User account administration
- Security groups
- Department-based identity organisation
- Active Directory administration

### Ticket 19 — SMB File Share Permission Troubleshooting

Practised:

- SMB shares
- Share permissions
- NTFS permissions
- Port 445 testing
- Network file access
- Read/write troubleshooting

### Ticket 20 — Departmental Folder Access Using AD Security Groups

Practised:

- AD security groups
- Department-based permissions
- SMB Change permissions
- NTFS Modify permissions
- Authorised/unauthorised testing
- SMB session troubleshooting
- Group-based access control

---

# 🧪 Home Lab Environment

- ✅ Windows Server Virtual Machine
- ✅ Windows 10 Virtual Machine
- ✅ Ubuntu Linux Virtual Machine
- ✅ Active Directory Domain Environment
- ✅ Active Directory Users & Groups
- ✅ Organizational Units
- ✅ SMB File Sharing
- ✅ NTFS Permissions
- ✅ Group-Based File Access
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
- 🔄 Group Policy Management
- 🔄 Mapped Network Drives
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
