Ransomware Incident Detection, Endpoint Isolation &
Security Escalation
Ticket
Department
Location
Issue
Initial Indicators
ServiceDesk Simulator — Brandon Wells
Marketing
Floor 1
Files would not open, filenames were scrambled, and files had a .locked extension.
README_RECOVER_FILES ransom note and black/red ransom wallpaper.
Suspected Vector
Scope Concern
Final Classification
1. Scenario
User reported opening a supplier invoice shortly before the incident.
Shared Marketing drive was reportedly showing similar encrypted/scrambled files.
Confirmed active ransomware / security incident
Brandon Wells reported that files in Documents and on the desktop would not open. Files had been renamed with
a .locked extension, filenames were scrambled, a README_RECOVER_FILES file appeared, and the desktop
wallpaper displayed a ransom demand. The shared Marketing drive was also reportedly beginning to show similar
symptoms.
2. Investigation
1. Reviewed the ticket and identified multiple indicators consistent with ransomware.
2. Remotely inspected the endpoint without interacting with the ransom demand.
3. Confirmed the ransomware wallpaper, ransom demand, encrypted .locked files, and recovery note.
4. Checked Mail Security and found quarantined suspicious/phishing messages, including malware-related
indicators.
5. Attempted a security scan; the scanner reported active file-encryption behavior and instructed that the PC be
isolated and escalated.
6. Identified the possible impact to the shared Marketing drive as a wider incident concern.
3. Containment
The simulator required the endpoint to be contained before escalation. The user was instructed to unplug the
Ethernet cable and hold the power button until the PC shut down completely. No attempt was made to decrypt,
rename, delete, or recover the affected files.
4. Escalation
The incident was documented and successfully escalated to the Security Team. The escalation included the
encrypted files, .locked extension, ransom note and wallpaper, active encryption detected by the scanner,
suspected supplier-invoice infection vector, and possible shared-drive impact.
5. Skills Demonstrated
Ransomware identification; security incident triage; evidence-based troubleshooting; endpoint containment;
malware/phishing investigation; incident documentation; security escalation; understanding of potential
network-share impact.
6. Key Learning
A ransomware event must not be treated as an ordinary file-corruption or desktop-support problem. The priority is
to recognize the indicators, contain the affected endpoint, preserve evidence, document the incident, and escalate
to the appropriate security team. Recovery should proceed only under the organization's incident-response
process.
7. Portfolio Summary
This lab demonstrates the ability to recognize, contain, document, and escalate a security incident using a
structured troubleshooting process