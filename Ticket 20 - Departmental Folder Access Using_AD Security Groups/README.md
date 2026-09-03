# Ticket 20 — Departmental Folder Access Using Active Directory Security Groups

> **Simulated Home-Lab Support Ticket**  
> Active Directory | SMB | NTFS Permissions | Windows

## Ticket Overview

A departmental Finance file share was configured so that access is controlled through the `CORP\Finance Users` Active Directory security group.

The lab verifies both sides of access control:

- An account without the required group-based permissions is denied access.
- An authorised Finance user can authenticate to the SMB share, browse the folder, and create a file.

> **Portfolio Note:** This is a simulated home-lab ticket created for practical IT support training. It is not presented as paid production or customer experience.

---

## Environment

| Component | Configuration |
|---|---|
| Domain | `corp.local` |
| LAB-DC01 | `10.10.10.10` — Windows Server / Domain Controller / Active Directory |
| Windows 10 Lab | `10.10.10.21` — SMB share host |
| Folder | `C:\Finance-Share` |
| UNC Path | `\\10.10.10.21\Finance-Share` |
| AD Security Group | `CORP\Finance Users` |
| Authorised Test User | `CORP\apetrova` — Anna AP. Petrova |
| Unauthorised Test | `CORP\Administrator` |

---

## Objective

Configure a Finance departmental share using group-based access rather than assigning permissions directly to individual users.

The lab must confirm that:

1. Members of `CORP\Finance Users` receive the required access.
2. Accounts outside the authorised group are denied.
3. The authorised user can perform a write operation across the network share.

---

## Active Directory Verification

The existing `Finance Users` security group was verified on **LAB-DC01 (`10.10.10.10`)**.

```powershell
Get-ADGroupMember -Identity "Finance Users" | Select-Object Name,SamAccountName
```

Verified members:

- Derek DC. Chambers — `dchambers`
- Anna AP. Petrova — `apetrova`
- Laura LS. Santos — `lsantos`

For the authorised access test, Anna's account (`CORP\apetrova`) was used because she was confirmed as a member of `CORP\Finance Users`.

### Evidence

![Finance Group Membership](screenshots/Finance_Group_Members.png)

---

## SMB Share Configuration

The Finance share is hosted on the **Windows 10 Lab (`10.10.10.21`)** at:

```text
C:\Finance-Share
```

UNC path:

```text
\\10.10.10.21\Finance-Share
```

During configuration, an initial baseline share used `Everyone` with Read access.

An attempt to revoke that entry unexpectedly resulted in:

```text
Everyone    Deny    Full
```

Instead of continuing to modify an uncertain permission configuration, the share was removed and recreated cleanly.

```powershell
Remove-SmbShare -Name "Finance-Share" -Force
```

The share was recreated with the Finance security group:

```powershell
New-SmbShare -Name "Finance-Share" -Path "C:\Finance-Share" -ChangeAccess "CORP\Finance Users"
```

The final permissions were verified:

```powershell
Get-SmbShareAccess -Name "Finance-Share"
```

Result:

```text
CORP\Finance Users    Allow    Change
```

### Evidence

![Finance SMB Permissions](screenshots/Finance_SMB_Permissions.png)

---

## NTFS Permission Configuration

NTFS permissions were configured through **Advanced Security** on the Windows 10 Lab (`10.10.10.21`).

This allowed me to practise both GUI-based administration and PowerShell verification.

The following changes were made:

- Disabled inheritance.
- Converted inherited permissions into explicit permissions.
- Removed `Authenticated Users`.
- Removed the local `Users` entry.
- Added `CORP\Finance Users`.
- Granted `Modify`.
- Applied the permission to the folder, subfolders and files.
- Retained `SYSTEM` and `Administrators` with Full Control.

The final ACL was verified using PowerShell:

```powershell
(Get-Acl "C:\Finance-Share").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited -AutoSize
```

Final permissions:

```text
NT AUTHORITY\SYSTEM       FullControl          Allow    False
BUILTIN\Administrators   FullControl          Allow    False
CORP\Finance Users       Modify, Synchronize  Allow    False
```

### Evidence

![Finance NTFS Permissions](screenshots/Finance_NTFS_Permissions.png)

---

# Access Testing

## Test 1 — Unauthorised Account

Testing was performed from **LAB-DC01 (`10.10.10.10`)**.

The current account was verified:

```cmd
whoami
```

Result:

```text
corp\administrator
```

`CORP\Administrator` attempted to access:

```text
\\10.10.10.21\Finance-Share
```

Windows returned an access-denied message.

### Result

❌ **Access Denied**

This demonstrated that an account outside the Finance access configuration did not automatically receive access to the departmental share.

### Evidence

![Unauthorised Access Denied](screenshots/Finance_Unauthorized_Access_Denied.png)

---

## Test 2 — Authorised Finance User

Anna AP. Petrova (`CORP\apetrova`) was selected for the authorised access test.

Anna was already confirmed as a member of:

```text
CORP\Finance Users
```

Her lab password was reset through **Active Directory Users and Computers** for controlled testing.

The first connection attempt contained a syntax mistake:

```cmd
net use \\10.10.10.21\Finance-Share/user:CORP\apetrova
```

This returned:

```text
System error 53
The network path was not found.
```

The syntax was corrected:

```cmd
net use \\10.10.10.21\Finance-Share /user:CORP\apetrova
```

The SMB connection succeeded.

However, File Explorer initially continued to display **Access Denied**.

Instead of changing the permissions, the existing SMB session was investigated.

```cmd
net use
```

An active connection to the Finance share was present.

The existing connection was removed:

```cmd
net use \\10.10.10.21\Finance-Share /delete
```

A clean authenticated connection was then established:

```cmd
net use \\10.10.10.21\Finance-Share /user:CORP\apetrova *
```

The share was tested directly:

```cmd
dir \\10.10.10.21\Finance-Share
```

The directory listing succeeded.

### Result

✅ **Authorised Finance-user access verified**

---

# Write-Access Verification

After establishing the clean authenticated SMB session as `CORP\apetrova`, the Finance share was opened from LAB-DC01:

```text
\\10.10.10.21\Finance-Share
```

A new text document was created:

```text
Finance-Test.txt
```

The file was created successfully.

### Result

✅ **Write / Modify access verified**

This confirmed that Anna's membership in `CORP\Finance Users`, combined with the SMB `Change` permission and NTFS `Modify` permission, provided the intended departmental access.

### Evidence

![Authorised Finance Access](screenshots/Finance_Authorized_Access_Verified.png)

---

# Troubleshooting

## Issue 1 — Unexpected SMB Deny Permission

When removing the original `Everyone` share permission, the share unexpectedly displayed:

```text
Everyone    Deny    Full
```

Rather than continuing to modify the existing configuration, the share was removed.

```powershell
Remove-SmbShare -Name "Finance-Share" -Force
```

It was recreated cleanly:

```powershell
New-SmbShare -Name "Finance-Share" -Path "C:\Finance-Share" -ChangeAccess "CORP\Finance Users"
```

Verification showed:

```text
CORP\Finance Users    Allow    Change
```

### Resolution

The SMB share now contained only the intended Finance group access.

---

## Issue 2 — Explorer Continued Showing Access Denied

After authenticating as Anna, File Explorer initially continued to display Access Denied.

Instead of immediately changing the ACL, the NTFS permissions were verified first.

The permissions were correct.

The active SMB connection was then removed:

```cmd
net use \\10.10.10.21\Finance-Share /delete
```

A new authenticated connection was established:

```cmd
net use \\10.10.10.21\Finance-Share /user:CORP\apetrova *
```

Access was tested using:

```cmd
dir \\10.10.10.21\Finance-Share
```

The directory listing succeeded.

### Resolution

The configured permissions were working correctly.

Clearing the existing SMB connection and authenticating with the authorised Finance account provided a clean test session without unnecessarily changing the ACL.

---

# Root Cause / Access-Control Finding

The Finance folder was intentionally restricted to the `CORP\Finance Users` security group.

Successful access depended on the complete permission chain:

```text
Active Directory User
        ↓
Finance Users Security Group
        ↓
SMB Share Permission
        ↓
Change
        ↓
NTFS Permission
        ↓
Modify
        ↓
Authorised Network Access
```

An account outside the authorised access configuration was denied.

The authorised Finance account successfully received the expected access.

---

# Resolution

The Finance departmental share was successfully secured using Active Directory group-based permissions.

Final configuration:

```text
Active Directory
----------------
CORP\Finance Users

SMB Share
---------
CORP\Finance Users → Change

NTFS
----
CORP\Finance Users → Modify
SYSTEM → Full Control
Administrators → Full Control
```

Testing confirmed:

```text
CORP\Administrator → Access Denied

CORP\apetrova
       ↓
Finance Users
       ↓
Share Access Allowed
       ↓
Finance-Test.txt created successfully
```

---

# Verification

The completed configuration was verified by:

- Confirming Anna is a member of `Finance Users`.
- Confirming SMB permission is `Finance Users → Change`.
- Confirming NTFS permission is `Finance Users → Modify`.
- Testing an unauthorised account and receiving Access Denied.
- Authenticating to the share as Anna.
- Successfully listing the Finance directory.
- Successfully opening the Finance share.
- Successfully creating `Finance-Test.txt`.

---

# Evidence Collected

The following screenshots were collected during the lab:

1. **Finance Group Membership**
   - Shows the users belonging to the `Finance Users` AD security group.

2. **Finance SMB Permissions**
   - Shows `CORP\Finance Users → Allow → Change`.

3. **Finance NTFS Permissions**
   - Shows `CORP\Finance Users → Modify`.

4. **Unauthorised Access Denied**
   - Shows `CORP\Administrator` being denied access to the Finance share.

5. **Authorised Finance Access**
   - Shows `Finance-Test.txt` successfully created inside the network share.

6. **Command-Line Authentication / Access Test**
   - Additional troubleshooting evidence showing successful `net use` and `dir` testing as `CORP\apetrova`.

---

# What I Learned

- Active Directory security groups provide a cleaner and more scalable way of assigning departmental access than assigning permissions directly to individual users.

- Effective network file access depends on both **SMB share permissions** and **NTFS permissions**.

- SMB `Change` combined with NTFS `Modify` can provide departmental users with appropriate read/write access without granting Full Control.

- Active Directory group membership alone is not enough. The group must also receive the appropriate SMB and NTFS permissions.

- Existing SMB sessions can affect access testing and should be investigated when authentication results appear inconsistent.

- Permissions should be verified before being changed.

- Checking the existing ACL prevented unnecessary permission changes when Explorer initially continued showing Access Denied.

- Read access and write access should be tested separately.

- Creating `Finance-Test.txt` provided direct evidence that network write access was functioning.

---

# Commands Used

## Active Directory

```powershell
Get-ADGroupMember -Identity "Finance Users" | Select-Object Name,SamAccountName
```

## SMB Share

```powershell
Get-SmbShareAccess -Name "Finance-Share"
```

```powershell
Remove-SmbShare -Name "Finance-Share" -Force
```

```powershell
New-SmbShare -Name "Finance-Share" -Path "C:\Finance-Share" -ChangeAccess "CORP\Finance Users"
```

## NTFS Permissions

```powershell
(Get-Acl "C:\Finance-Share").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited -AutoSize
```

## SMB Session / Access Testing

```cmd
net use
```

```cmd
net use \\10.10.10.21\Finance-Share /delete
```

```cmd
net use \\10.10.10.21\Finance-Share /user:CORP\apetrova *
```

```cmd
dir \\10.10.10.21\Finance-Share
```

---

# Workflow

```text
Verify Finance AD group membership
              ↓
Create Finance SMB share
              ↓
Finance Users → SMB Change
              ↓
Configure NTFS permissions
              ↓
Finance Users → NTFS Modify
              ↓
Test unauthorised account
              ↓
Access Denied
              ↓
Authenticate as Finance user
              ↓
Investigate existing SMB session
              ↓
Clear SMB connection
              ↓
Re-authenticate as Anna
              ↓
Verify directory access
              ↓
Open Finance share
              ↓
Create Finance-Test.txt
              ↓
Write access confirmed
```

---

# Key Takeaway

**Group-based access control works as a chain.**

The user must belong to the correct Active Directory security group, the group must receive the appropriate SMB share permission, and the group must receive the appropriate NTFS permission.

In this lab:

```text
CORP\apetrova
      ↓
CORP\Finance Users
      ↓
SMB: Change
      ↓
NTFS: Modify
      ↓
Successful Finance Share Access
      ↓
Finance-Test.txt Created
```

Testing both an authorised and unauthorised account demonstrated that the access-control design was working as intended.

---

**Ticket Status: Resolved ✅**