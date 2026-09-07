# Ticket 21 – Automatic Finance Drive Mapping Using Group Policy

**Windows Server Home Lab | Active Directory | Group Policy Preferences | SMB | NTFS | Troubleshooting**

**Author:** Tobekile Mazula  
**Lab Date:** 7 September 2026

---

# 1. Scenario

Finance users needed automatic access to the departmental Finance network share without manually entering a UNC path or mapping a drive.

The objective was to use **Group Policy Preferences** to map the existing Finance share as drive `F:` for authorised Finance users.

---

# 2. Environment

| Component | Configuration |
|---|---|
| Domain | `corp.local` |
| Domain Controller | `LAB-DC01 – 10.10.10.10` |
| Domain Workstation / File Share Host | `Windows 10 Lab – 10.10.10.21` |
| Test User | `CORP\apetrova (Anna Petrova)` |
| Security Group | `CORP\Finance Users` |
| SMB Share | `\\10.10.10.21\Finance-Share` |
| Mapped Drive | `Finance (F:)` |

---

# 3. Prerequisite Verification

Connectivity between `LAB-DC01` and the Windows 10 lab workstation was verified.

The workstation was confirmed as joined to the `corp.local` Active Directory domain, and the existing Finance SMB share was confirmed on `10.10.10.21`.

### Domain User Verification

```powershell
whoami
```

Result:

```text
corp\administrator
```

### Domain Membership Verification

```powershell
systeminfo | findstr /B /C:"Domain"
```

Result:

```text
Domain: corp.local
```

### Finance Share Verification

```powershell
Get-SmbShare -Name "Finance-Share"
```

Result:

```text
Name          ScopeName Path
----          --------- ----
Finance-Share *         C:\Finance-Share
```

Active Directory Users and Computers also confirmed that **Anna Petrova** was located in the Finance OU and that the **Finance Users** security group existed.

---

# 4. Group Policy Configuration

A new Group Policy Object named:

```text
Finance Drive Mapping
```

was created and linked to the **Finance Organizational Unit**.

The drive mapping was configured under:

```text
User Configuration
    > Preferences
        > Windows Settings
            > Drive Maps
```

The mapped-drive preference used the following settings:

| Setting | Value |
|---|---|
| Action | `Update` |
| Location | `\\10.10.10.21\Finance-Share` |
| Label | `Finance` |
| Drive Letter | `F:` |
| Reconnect | Enabled |
| Connect As | Blank – uses the logged-in user's credentials |

The completed configuration mapped:

```text
F:
```

to:

```text
\\10.10.10.21\Finance-Share
```

---

# 5. Item-Level Targeting

Item-Level Targeting was enabled so the drive mapping would apply only when the logged-in user was a member of:

```text
CORP\Finance Users
```

The targeting rule was configured as:

```text
The user is a member of the security group CORP\Finance Users
```

**User in group** was selected.

This added a second layer of control.

The GPO was linked to the **Finance OU**, while the individual Drive Maps preference also checked membership in the **Finance Users security group**.

The deployment logic therefore became:

```text
Finance OU
    |
    v
Finance Drive Mapping GPO
    |
    v
User member of CORP\Finance Users?
    |
    +---- Yes ---> Map Finance (F:)
    |
    +---- No ----> Do not map drive
```

---

# 6. Troubleshooting Incident – Group Policy Time Synchronization

During testing as:

```text
CORP\apetrova
```

the following command was executed:

```cmd
gpupdate /force
```

The initial Group Policy refresh reported that **Computer Policy could not be updated successfully**.

Windows reported that the workstation clock was not synchronized with a Domain Controller.

The message indicated that Windows could not determine whether new Group Policy settings should be enforced because the computer clock was not synchronized with the clock of a Domain Controller.

Interestingly, the same refresh reported:

```text
User Policy update has completed successfully.
```

Although User Policy succeeded, the domain time issue was investigated and corrected before completing final validation.

---

## 6.1 Workstation Time Source Verification

On the Windows 10 workstation, the Windows Time source was checked using:

```cmd
w32tm /query /source
```

Result:

```text
LAB-DC01.corp.local
```

The workstation was therefore correctly configured to obtain its domain time from the Domain Controller.

Additional status information was collected using:

```cmd
w32tm /query /status
```

The output included:

```text
Leap Indicator: 0 (no warning)
Source: LAB-DC01.corp.local
Source IP: 10.10.10.10
Last Successful Sync Time: 9/7/2026 8:38:39 PM
```

This showed that the workstation recognised `LAB-DC01` as its Windows Time source.

---

## 6.2 Domain DNS Verification

Because Active Directory and Group Policy rely heavily on DNS, the workstation DNS configuration was also verified.

```cmd
ipconfig /all
```

The configured DNS server was:

```text
10.10.10.10
```

This correctly pointed the Windows 10 domain workstation to:

```text
LAB-DC01
```

DNS misconfiguration was therefore ruled out as the cause of the Group Policy problem.

---

## 6.3 Domain Controller Time Investigation

Windows Time status was then checked directly on `LAB-DC01`.

```cmd
w32tm /query /status
```

The Domain Controller reported:

```text
Source: Local CMOS Clock
```

The full Windows Time configuration was inspected using:

```cmd
w32tm /query /configuration
```

The configuration showed that the Windows Time service was enabled and that the NTP client configuration used:

```text
Type: NT5DS
```

Further investigation was required to determine why the workstation continued reporting a clock synchronization problem.

---

## 6.4 Time Zone Comparison

The configured Windows time zone was checked on both systems using:

```cmd
tzutil /g
```

The Windows 10 workstation returned:

```text
South Africa Standard Time
```

However, `LAB-DC01` initially returned:

```text
Pacific Standard Time
```

The Domain Controller's time zone was corrected using:

```cmd
tzutil /s "South Africa Standard Time"
```

The change was verified using:

```cmd
tzutil /g
```

Result:

```text
South Africa Standard Time
```

---

## 6.5 Measuring the Actual Clock Offset

Rather than relying only on the visible Windows clock, the actual time difference between the workstation and Domain Controller was measured using Windows Time.

On the Windows 10 workstation:

```cmd
w32tm /stripchart /computer:LAB-DC01.corp.local /samples:5 /dataonly
```

The initial result showed measurements around:

```text
+32398 seconds
```

This represented an underlying difference of approximately **nine hours**.

The offset remained extremely consistent across the five samples.

This confirmed that a significant time discrepancy existed even though the clocks initially appeared similar in the Windows graphical interface.

---

## 6.6 UTC Comparison

To determine which system had the incorrect underlying time, UTC was compared directly using PowerShell.

The following command was executed on both systems:

```powershell
(Get-Date).ToUniversalTime()
```

The Windows 10 workstation returned approximately:

```text
Monday, September 7, 2026 7:46:31 PM
```

The Domain Controller returned:

```text
Tuesday, September 8, 2026 4:39:20 AM
```

The comparison confirmed that the Domain Controller's underlying time was incorrect.

This also corresponded with the approximately nine-hour discrepancy reported by:

```cmd
w32tm /stripchart
```

---

## 6.7 Time Synchronization Resolution

The Domain Controller's time zone and clock were corrected.

The Windows 10 workstation was then resynchronized with the Domain Controller from an elevated Command Prompt:

```cmd
w32tm /resync
```

Result:

```text
Sending resync command to local computer
The command completed successfully.
```

The offset was measured again using:

```cmd
w32tm /stripchart /computer:LAB-DC01.corp.local /samples:5 /dataonly
```

The original approximately nine-hour discrepancy was dramatically reduced.

Further comparison of the local clocks showed that the systems were now much closer in time.

---

## 6.8 Successful Group Policy Refresh

After correcting the time synchronization issue, Group Policy was refreshed again while logged in as:

```text
CORP\apetrova
```

Command:

```cmd
gpupdate /force
```

This time the result was:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

The Group Policy processing problem was successfully resolved.

---

# 7. Validation

After Group Policy successfully refreshed, **File Explorer > This PC** was opened on the Windows 10 workstation while Anna Petrova was logged in.

Under **Network locations**, Windows displayed:

```text
Finance (F:)
```

The drive had been automatically deployed through Group Policy.

No manual drive mapping was performed during Anna's session.

---

## 7.1 Mapped Drive Access Test

The newly mapped:

```text
Finance (F:)
```

drive was opened.

The existing file:

```text
Finance - Test.txt
```

was visible.

This confirmed that Anna could successfully access the underlying SMB resource through the GPO-deployed mapped drive.

---

## 7.2 Write Permission Verification

A final functional test was performed to verify that Anna's membership in:

```text
CORP\Finance Users
```

provided the intended NTFS **Modify** permissions.

While logged in as Anna, a new text file was created inside:

```text
Finance (F:)
```

The file was named:

```text
Anna-GPO-write-Test.txt
```

The file was created successfully without an **Access Denied** error.

This confirmed the complete access chain:

```text
CORP\apetrova
      |
      v
Finance OU
      |
      v
Finance Drive Mapping GPO
      |
      v
CORP\Finance Users
Item-Level Targeting
      |
      v
Finance (F:)
      |
      v
\\10.10.10.21\Finance-Share
      |
      v
NTFS Modify Permission
      |
      v
Successful File Creation
```

---

# 8. Result

**Ticket resolved successfully.**

Authorised Finance users can receive the Finance departmental network share automatically as:

```text
Finance (F:)
```

through Active Directory Group Policy Preferences.

The test user successfully:

- Received the `F:` drive automatically
- Opened the mapped Finance share
- Viewed existing Finance content
- Created a new file
- Verified NTFS Modify/write access

The lab also demonstrated troubleshooting of a real Group Policy processing failure caused by domain time synchronization.

---

# 9. Skills Demonstrated

This lab demonstrated practical experience with:

- Windows Server Administration
- Active Directory Domain Services
- Active Directory Organizational Units
- Active Directory Security Groups
- Group Policy Management
- Group Policy Preferences
- Group Policy Drive Maps
- Item-Level Targeting
- Mapped Network Drives
- SMB File Sharing
- NTFS Permissions
- Role-Based Access Control
- Windows Domain Authentication
- DNS Verification
- Windows Time Service
- NTP Troubleshooting
- Time Zone Configuration
- NTP Offset Analysis
- PowerShell
- Windows Command Line
- Group Policy Troubleshooting
- Root Cause Analysis
- End-User Access Testing
- Technical Documentation

---

# 10. Evidence Screenshots

The following screenshots were collected as evidence of the implementation and successful testing.

### 1. Finance Drive Mapping GPO

```text
Ticket-21-Finance-Drive-Mapping-GPO.png
```

Shows the completed `F:` drive mapping configured through Group Policy Preferences using:

```text
\\10.10.10.21\Finance-Share
```

### 2. Finance Users Item-Level Targeting

```text
Ticket-21-Finance-Users-Item-Level-Targeting.png
```

Shows the targeting rule:

```text
CORP\Finance Users
```

with **User in group** selected.

### 3. Finance Drive Automatically Mapped

```text
Ticket-21-Finance-Drive-Automatically-Mapped.png
```

Shows `Finance (F:)` automatically appearing under **Network locations** in Anna Petrova's Windows session.

### 4. Finance Mapped Drive Access Test

```text
Ticket-21-Finance-Mapped-Drive-Access-Test.png
```

Shows the successfully opened `Finance (F:)` drive and the existing:

```text
Finance - Test.txt
```

file.

### 5. Finance GPO Write Access Verified

```text
Ticket-21-Finance-GPO-Write-Access-Verified.png
```

Shows:

```text
Anna-GPO-write-Test.txt
Finance - Test.txt
```

inside the mapped Finance drive.

This provides final evidence that Anna could successfully write to the departmental share.

---

# Portfolio Note

This lab reflects an enterprise-style workflow in which departmental resources are centrally delivered through **Active Directory Group Policy** rather than relying on users or technicians to manually configure mapped drives on individual workstations.

The lab also documents the troubleshooting process rather than presenting only the successful final configuration.

An unexpected Group Policy failure required investigation of:

```text
Group Policy
      |
      v
Domain Time Synchronization
      |
      v
Windows Time Service
      |
      v
DNS Verification
      |
      v
NTP Offset Measurement
      |
      v
Time Zone / UTC Investigation
      |
      v
Root Cause Identification
      |
      v
Resolution
      |
      v
Successful GPO Deployment
```

This provided additional hands-on experience with **systematic troubleshooting, root cause analysis, Windows domain services, and technical documentation**.

---

**Author:** Tobekile Mazula  
**Project:** Windows Server Home Lab  
**Ticket:** 21 – Automatic Finance Drive Mapping Using Group Policy