# Case #002 — Windows 7 to Windows 10 Upgrade Assessment

**Case type:** Real-world independent IT support | **Status:** Upgrade not performed  
**Environment:** Customer site | **Device:** Desktop PC

## Incident summary

The customer had an older desktop computer running Windows 7 Professional and wanted the system upgraded to Windows 10.

Before attempting the operating-system upgrade, I reviewed the existing system information and hardware specifications to determine whether proceeding would provide a reasonable experience for the user.

## Objective

Assess the existing Windows 7 desktop, determine whether proceeding with a Windows 10 upgrade was appropriate, and avoid making a change that could negatively affect the usability of the customer's computer.

## Investigation and evidence

1. **Existing operating system:** System Information confirmed that the desktop was running Windows 7 Professional Service Pack 1 on an x64-based system.

2. **Hardware assessment:** The system used an Intel Celeron G1620 @ 2.70 GHz processor and had 2 GB of installed physical memory (RAM).

3. **Memory consideration:** The 2 GB RAM configuration was identified as a significant limitation for the intended Windows 10 upgrade.

4. **Upgrade assessment:** Although the customer's request was to move from Windows 7 to Windows 10, I decided that proceeding on the existing 2 GB RAM configuration could result in poor system performance and an unsatisfactory user experience.

## Resolution / recommendation

The Windows 10 installation was **not performed**.

Rather than completing the requested upgrade without considering the machine's existing hardware, I recommended addressing the limited RAM before proceeding with the operating-system upgrade.

This avoided knowingly making a change that I expected could leave the customer with a noticeably slower or less responsive computer.

## Outcome and verification limits

**Outcome:** Windows 10 upgrade deferred because of the system's limited 2 GB RAM configuration.

No Windows 10 installation was attempted during the visit, so Windows 10 performance, driver compatibility, application compatibility, activation, and post-upgrade functionality were not tested on this machine.

The assessment was therefore limited to the existing Windows 7 environment and the hardware information available during the visit.

## Lessons learned

- Assess hardware before performing an operating-system upgrade.
- Completing the customer's requested change is not always the same as providing the best support outcome.
- Consider the user's experience after a change, not only whether the change can technically be attempted.
- Older systems may require hardware upgrades before an operating-system upgrade is appropriate.
- Clearly document when work is intentionally deferred and why.
- Avoid claiming that an upgrade is technically impossible when the decision is based on expected usability or performance.

## Skills demonstrated

- Windows operating-system assessment
- Windows 7 system inspection
- System Information (`msinfo32`) review
- Hardware specification assessment
- RAM capacity assessment
- Legacy desktop support
- Operating-system upgrade planning
- Customer-impact consideration
- Technical decision-making
- Upgrade recommendation
- Technical documentation

## Suggested evidence screenshots/photos

- `evidence/01-windows-7-system-information.jpg` — Windows 7 System Information showing the existing operating system, processor, system architecture, and installed memory used during the upgrade assessment.

**Portfolio note:** This case documents independent real-world IT support performed on a customer device. Customer-identifying information has been removed from the published evidence.