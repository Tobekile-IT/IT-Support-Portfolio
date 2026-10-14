# Real Client Case 003 — Windows 11 Laptop Performance Troubleshooting & Optimisation

**Case type:** Independent IT support / real client  
**Device:** Rizzen NovaBook laptop  
**Status:** Technical optimisation completed; client acceptance not documented  
**Privacy:** Client identity and personal files excluded

## Client-reported issue
The client reported severe slowness after a 1 TB HDD upgrade and Windows 11 installation. The delays made routine work difficult, including the intended transfer of personal files from a mobile phone. The phone transfer itself was **not** performed as part of this case.

## System configuration
| Component | Finding |
|---|---|
| Operating system | Windows 11 (installed on C:) |
| RAM | 4 GB installed (~3.8 GB usable) |
| System disk (C:) | Toshiba MQ04ABF100, 1 TB SATA mechanical HDD |
| Secondary disk (D:) | VID:EA SA7211, approximately 64 GB SSD |

The suitability of the secondary SSD for hosting Windows and the feasibility of a RAM upgrade were **not verified**.

## Investigation and evidence
1. **Task Manager:** During a high-activity reading, the system HDD showed **100% active time**, **218 ms average response time**, and memory use of approximately **89%**. These are point-in-time observations, not a controlled benchmark. See [01 — high disk activity](evidence/01_high_disk_activity.png).
2. **PowerShell storage status:** `Get-PhysicalDisk | Select FriendlyName, MediaType, HealthStatus, OperationalStatus` reported the SSD and HDD as **Healthy / OK**. This is a basic status check, **not** a comprehensive SMART diagnosis or proof that the HDD is fault-free. See [02 — storage health](evidence/02_storage_health_redacted.png).
3. **Windows integrity:** `sfc /verifyonly` reported no Windows Resource Protection integrity violations.
4. **Startup review:** Several nonessential applications were enabled at startup. See [03 — startup configuration before changes](evidence/03_startup_apps_before_changes.png).

## Actions performed
- Disabled unnecessary startup entries: Acrobat Collaboration Synchronizer, Adobe ExpressStartUpService, Microsoft 365 Copilot, and Microsoft Edge. Left security-related entries enabled.
- In Microsoft Edge, disabled **Background mode** and **Startup boost**, while leaving graphics acceleration enabled.
- Rechecked background processes and monitored Task Manager.
- Tested routine responsiveness with File Explorer and web browsing.
- **Did not** reinstall Windows, replace hardware, disable Windows security services, format storage, or delete client files.

## Outcome
The laptop became noticeably more responsive during basic use. In a later **low-activity** Task Manager reading, resource use was approximately **65% memory, 10% CPU, and 2% disk**. See [04 — final low-activity reading](evidence/04_final_low_activity_reading.png).

**Important:** Initial and final screenshots were captured under **different workloads**. They must not be treated as a controlled before/after performance benchmark or proof of a permanent fix.

## Limitations and client guidance
- Windows 11 on 4 GB RAM and a mechanical system HDD remains resource-constrained, especially during multitasking, updates, and paging.
- The high disk activity may have contributed to the slowdown; **no specific HDD defect was confirmed**.
- Pending security updates should be addressed with the client's permission and an appropriate backup. A larger feature upgrade was deferred.
- No additional RAM or SSD purchase was recommended as an immediate requirement.
- The client should verify satisfactory performance and accept the handover before the service ticket is marked fully resolved.

## Evidence gallery
| Investigation | Final observation |
|---|---|
| ![Disk at 100% active time](evidence/01_high_disk_activity.png) | ![Final low-activity Task Manager reading](evidence/04_final_low_activity_reading.png) |

![Storage status in PowerShell, client username redacted](evidence/02_storage_health_redacted.png)

![Startup apps before changes](evidence/03_startup_apps_before_changes.png)

![Client laptop](evidence/05_client_laptop.jpg)

## Skills demonstrated
Windows 11 troubleshooting · Task Manager performance analysis · PowerShell diagnostics · Startup optimisation · Basic system integrity verification · Evidence-based decision-making · Client communication · Data privacy
