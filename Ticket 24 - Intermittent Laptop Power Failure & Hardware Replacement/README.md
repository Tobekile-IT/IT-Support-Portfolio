# Ticket 24 — Intermittent Laptop Power Failure & Hardware Replacement

**Category:** Help Desk / Hardware Support  
**Environment:** Windows endpoint, Remote Desktop, Event Viewer, Computer Deployment, Asset Management  
**Scenario Type:** Service Desk Simulation

---

## Incident Summary

A Finance user reported that their laptop was unexpectedly powering off several times per week.

The laptop would:

- Suddenly go black and completely power off
- Provide no warning or blue screen
- Remain powered off until the power button was pressed
- Start normally afterward
- Experience the issue on both AC power and battery

The recurring shutdowns had already caused the user to lose work and made the laptop unreliable during meetings and deadline-sensitive tasks.

---

## Business Impact

The issue was affecting the user's ability to work reliably.

Because the unexpected shutdowns were occurring multiple times per week and had resulted in lost work, restoring a dependable workstation was a priority.

---

## Initial Troubleshooting

The following had already been tested:

- Different charger
- Different wall socket
- Windows power settings
- Operation while connected to AC power
- Operation while running on battery

The problem continued.

The user also confirmed that there were no visible error messages or blue screens before the laptop powered off.

---

## Investigation

### 1. System Updates

I checked the endpoint for available system updates.

Several updates were available, including:

- BIOS update
- Integrated graphics driver
- Onboard audio driver
- System firmware update
- Power management driver

The updates were applied as a troubleshooting step because firmware and power-management components could potentially contribute to system instability.

The available updates alone were not treated as proof of the root cause, and the investigation continued.

### 2. Remote Diagnostics

I connected to the affected endpoint using the simulator's Remote Desktop tool and opened:

**Event Viewer → Windows Logs → System**

The System log was filtered for **Critical** events.

Multiple **Kernel-Power — Event ID 41** entries were present across separate days and unrelated times.

The recurring events aligned with the user's reports of unexpected hard shutdowns.

> **Important:** Kernel-Power Event ID 41 indicates that Windows detected an unexpected shutdown or restart. It does not by itself identify which hardware component failed.

Considering the recurring hard power losses, previous troubleshooting, and continuing business impact, the laptop was treated as an unreliable hardware asset requiring replacement.

---

## Resolution

Rather than continuing to leave the user working on an unreliable endpoint, I proceeded with the hardware replacement workflow.

### Replacement Device Deployment

1. Confirmed that the affected endpoint was a **laptop**.
2. Opened **Computer Deployment**.
3. Built a replacement laptop using **Server Imaging**.
4. Waited for the provisioning process to complete.
5. Confirmed that the newly built device was available for deployment.

### Asset Registration

The replacement laptop was then registered through **Asset Management**.

The device was:

- Added as a new organizational asset
- Set to **Ready to deploy**
- Prepared for assignment to the affected user

### User Assignment

From the **By Users** view in Asset Management:

1. Located the affected user
2. Selected **Check out replacement**
3. Assigned the newly provisioned laptop to the user

### Shipping

The replacement workflow was completed through **Ship Manager**, where the required shipping information was obtained so the replacement device could be delivered to the user.

---

## Outcome

The unreliable laptop was removed from the user's normal workflow and replaced with a newly provisioned organizational laptop.

The service desk workflow included:

**Diagnosis → Remote investigation → System log analysis → Replacement decision → Device provisioning → Asset registration → User assignment → Shipping**

The exact internal component responsible for the original laptop's power failure was not identified.

The objective was to restore the user's ability to work reliably while removing the unstable endpoint from service for further hardware assessment.

---

## Evidence

### System Update Investigation

![System updates](evidence/system-update.png)

System updates were reviewed and applied during the investigation, including BIOS, firmware, and power-management updates.

### Remote Desktop Investigation

![Remote Desktop](evidence/remote.png)

The affected endpoint was accessed remotely for further investigation.

### Event Viewer

![Event Viewer](evidence/event-viewer.png)

The Windows System log was reviewed for critical events associated with the unexpected shutdowns.

### Kernel-Power Event ID 41

![Kernel-Power Event ID 41](evidence/kernel-power-41.png)

Multiple Kernel-Power Event ID 41 events provided evidence that Windows had experienced repeated unexpected shutdowns.

### Replacement Laptop Deployment

![Computer Deployment](evidence/deployment.png)

A replacement laptop was provisioned using the organization's Server Imaging workflow.

### Asset Management

![Asset Management](evidence/asset-manager.png)

The replacement device was registered and prepared for deployment through Asset Management.

### Shipping

![Ship Manager](evidence/ship-manager.png)

The replacement workflow was completed through the organization's shipping process.

---

## Key Lessons Learned

- Unexpected power loss should be distinguished from sleep, restart, and normal Windows shutdown behavior.
- A pending update is a troubleshooting lead, not automatically the root cause.
- Kernel-Power Event ID 41 confirms that an unexpected shutdown occurred but does not identify the failed hardware component.
- Available diagnostic tools should be reviewed before assuming a troubleshooting capability is unavailable.
- Troubleshooting hypotheses should change when new evidence becomes available.
- Restoring business productivity can take priority over prolonged troubleshooting of an unreliable endpoint.
- Hardware replacement in an enterprise environment involves more than swapping devices; provisioning, asset registration, assignment, and logistics are also part of the support lifecycle.

---

## Skills Demonstrated

- Incident triage
- End-user questioning
- Remote desktop support
- Windows Event Viewer
- Windows System log analysis
- Kernel-Power Event ID 41 interpretation
- BIOS, firmware, and driver update assessment
- Hardware troubleshooting
- Root-cause investigation
- Evidence-based escalation
- Computer deployment
- Server Imaging
- IT asset management
- Hardware lifecycle management
- Replacement device assignment
- End-user service restoration
- Technical documentation

---

## Portfolio Note

This ticket was completed in a **simulated enterprise service desk environment** and is documented as hands-on support practice.

It is not presented as a real customer incident.