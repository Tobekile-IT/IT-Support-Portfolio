# 🎫 Ticket 19 — SMB File Share Permission Troubleshooting

## 📌 Ticket Overview

**Environment:** Windows Server Home Lab  
**Category:** File Sharing / SMB / Permissions  
**Status:** ✅ Resolved  
**Type:** Simulated IT Support Ticket

### Reported Issue

A client computer could successfully access the shared network folder and view existing files, but the user was unable to create a new file inside the shared folder.

The objective was to identify whether the issue was caused by network connectivity, SMB configuration, or permissions.

---

## 🖥️ Lab Environment

| Component | Configuration |
|---|---|
| SMB Host | `10.10.10.21` |
| Client | `10.10.10.10` |
| Shared Folder | `C:\IT-Share` |
| Share Name | `IT-Share` |
| UNC Path | `\\10.10.10.21\IT-Share` |
| Testing Method | File Explorer + PowerShell |

---

## 🔎 Initial Testing

From the client machine, I accessed the network share using:

```text
\\10.10.10.21\IT-Share
```

The shared folder opened successfully and the existing file:

```text
test.txt
```

was visible.

This confirmed that:

- The client could communicate with the host.
- The SMB share was accessible over the network.
- The client had permission to read existing files.

However, when I attempted to create a new text document from the client, Windows reported that permission was required to perform the action.

### Initial Result

**Read access:** ✅ Working  
**Write access:** ❌ Failed

Because the client could already access the share, I focused the investigation on permissions rather than basic network connectivity.

---

## 🛠️ Troubleshooting

On the host machine, I checked the current SMB share permissions using PowerShell:

```powershell
Get-SmbShareAccess -Name "IT-Share"
```

The result showed:

```text
AccountName    AccessControlType    AccessRight
Everyone       Allow                Read
```

This identified the cause of the problem.

The `Everyone` group only had **Read** permission on the SMB share.

This allowed the client to open the folder and read existing files but prevented the client from creating or modifying files through the network share.

---

## 🎯 Root Cause

The SMB share-level permission was configured as:

```text
Everyone → Read
```

The client therefore had sufficient permission to view the contents of `IT-Share`, but not enough permission to perform write operations.

---

## 🔧 Resolution

I changed the SMB share permission from **Read** to **Change** using PowerShell:

```powershell
Grant-SmbShareAccess -Name "IT-Share" -AccountName "Everyone" -AccessRight Change -Force
```

I then verified the updated SMB permissions.

The resulting configuration showed:

```text
Everyone → Allow → Change
```

This provided the required share-level permission for the client to create and modify files, subject to the underlying NTFS permissions.

---

## ✅ Verification

After applying the change, I returned to the client machine and accessed:

```text
\\10.10.10.21\IT-Share
```

I attempted to create a new file named:

```text
Client-Test.txt
```

The file was created successfully.

### Final Result

| Test | Result |
|---|---|
| Access SMB share | ✅ Pass |
| View existing `test.txt` | ✅ Pass |
| Create new file before fix | ❌ Failed |
| SMB permission inspected | ✅ `Everyone: Read` |
| Permission changed to `Change` | ✅ Successful |
| Create `Client-Test.txt` after fix | ✅ Pass |

The issue was successfully resolved.

---

## 📸 Evidence

### SMB Share Configuration

![SMB File Sharing](./screenshots/SMB_file_sharing.png)

### SMB PowerShell Commands

![SMB Commands](./screenshots/SMB_commands.png)

### Permission Troubleshooting and Resolution

![SMB Share Permission Fix](./screenshots/SMB_Share_Permission_Fix.png)

The screenshot above demonstrates the original `Read` permission, the PowerShell command used to change the permission, and the resulting `Change` permission.

### Client Write Access Verification

![SMB Write Access Verified](./screenshots/SMB_Write_Access_Verified.png)

The client was able to create `Client-Test.txt` after the SMB permission was corrected.

---

## 🧠 What I Learned

Through this ticket I gained practical experience with:

- Configuring and testing SMB network shares.
- Accessing shared folders using UNC paths.
- Using PowerShell to inspect SMB permissions.
- Troubleshooting read-versus-write access problems.
- Understanding the difference between `Read` and `Change` share permissions.
- Understanding how SMB share permissions and NTFS permissions contribute to effective access.
- Applying a permission change using PowerShell.
- Verifying a solution from the affected client's perspective.
- Documenting a technical issue from initial symptoms through resolution.

---

## 🧰 Commands Used

```powershell
Get-SmbShare

Get-SmbShareAccess -Name "IT-Share"

Grant-SmbShareAccess -Name "IT-Share" -AccountName "Everyone" -AccessRight Change -Force
```

Client network path:

```text
\\10.10.10.21\IT-Share
```

---

## 🔄 Troubleshooting Workflow

```text
User reports write-access problem
            ↓
Reproduce the issue from client
            ↓
Confirm SMB share is accessible
            ↓
Read access works / Write access fails
            ↓
Inspect SMB share permissions
            ↓
Everyone = Read
            ↓
Identify share-level permission restriction
            ↓
Change permission: Read → Change
            ↓
Retest from client
            ↓
Client-Test.txt successfully created
            ↓
Ticket Resolved ✅
```

---

## 📚 Key Takeaway

A user being able to open a network share does not necessarily mean they have permission to modify its contents.

When troubleshooting shared-folder access, both **SMB share permissions** and **NTFS permissions** should be considered.

Testing the solution from the affected client is also essential before considering the incident resolved.

---

> **Portfolio Note:** This ticket was created and completed in a personal Windows home lab to demonstrate practical IT support, SMB administration, PowerShell, permissions troubleshooting, and technical documentation. It represents simulated hands-on support experience rather than paid professional IT employment.