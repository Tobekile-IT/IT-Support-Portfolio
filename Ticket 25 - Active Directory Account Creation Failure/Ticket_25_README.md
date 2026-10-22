# Ticket 25 — Active Directory Account Creation Failure

**Environment:** ServiceDesk Simulator (hands-on training)  
**Incident:** INC787789 — New starter's account couldn't be created  
**Priority:** High  
**Status:** Resolved in simulator  
**Focus:** Windows Server, Active Directory, Event Viewer, storage troubleshooting

## Incident summary

An Engineering team member reported that HR could not create an account for a new starter due to join the following day. A separate request to update a team group membership had also failed. Existing staff could still sign in and access their files, suggesting that the issue affected directory changes rather than all authentication activity.

![Original incident](Screenshots/Ticket(2).png)

## Investigation and evidence

1. **Checked domain controller health.** Both domain controllers were online, but **DC01's disk was 99% utilised**. DC02 was substantially less utilised (38% at investigation).
2. **Inspected DC01 storage.** The 127 GB system disk had approximately **125.9 GB used and 1.1 GB free**. The storage view identified **47 archived Security event logs consuming 73.8 GB**.
3. **Reviewed Windows Event Viewer.** The Directory Service log contained **NTDS General Event ID 1393**, explicitly reporting that updates to the directory database were failing because its disk was out of space. System log warnings included **Event ID 2013** for low disk space.
4. **Correlated symptoms with the evidence.** Both new account creation and group membership changes require directory writes. DC01's storage exhaustion was consistent with these failures, even though existing users could still work.

### DC01 disk utilisation before remediation

![DC01 at 99 percent disk utilisation](Screenshots/DC01%20-%2099%25.png)

### Archived Security logs consuming disk space

![DC01 storage showing 47 archived logs](Screenshots/DC%20Storage.png)

### Directory Service Event ID 1393

![Event Viewer displaying Event ID 1393 and database write failure](Screenshots/Directory%20Service%20Event%20ID%201393.png)

## Root cause

DC01 ran critically low on disk space because Security event logs were configured to **archive when full rather than overwrite events**. Accumulated archived logs occupied approximately 73.8 GB. Event ID 1393 confirmed that insufficient disk space was preventing Active Directory database updates.

## Remediation performed in the simulator

- Moved **47 archived Security log files** from `C:\WorkstationOS\System32\winevt\Logs` to the archive share `\\FILESERV01\IT-Archive\DC01-Logs`.
- Changed the Security log's maximum-size behavior to **Overwrite events as needed (oldest events first)**, following the simulator's guided remediation.
- Checked DC01 storage after the move. Disk utilisation dropped from **99% to 41%**, a **58-percentage-point reduction**.

### DC01 disk utilisation after remediation

![DC01 at 41 percent disk utilisation](Screenshots/DC01%20-%2041%25.png)

## Outcome and verification limitation

The **ServiceDesk Simulator marked INC787789 as Resolved** after remediation. The requester’s final chat response referred to internet connectivity rather than explicitly confirming that HR could create the account or update group membership. Accordingly, the simulator resolution is documented here, but successful completion of those two directory operations was **not independently verified in the available evidence**.

## Real-world support considerations

In a production environment, an L1 technician should collect the error details, check authorised monitoring information, document disk utilisation and relevant Event Viewer findings, and **escalate to an authorised server administrator** before moving audit logs or changing Security log retention. Security records may be subject to audit, incident-response and compliance requirements. Centralised log collection, approved retention policies, storage monitoring and capacity alerts are preferable to unapproved deletion or overwriting.

## Skills demonstrated

- Incident triage and symptom correlation
- Domain controller health and disk-capacity analysis
- Windows Event Viewer investigation (Events 1393 and 2013)
- Active Directory write-failure root-cause analysis
- Storage recovery and post-change measurement in a simulated environment
- Documentation, evidence handling and escalation awareness

---

*This is a ServiceDesk Simulator training case, not a production customer incident.*
