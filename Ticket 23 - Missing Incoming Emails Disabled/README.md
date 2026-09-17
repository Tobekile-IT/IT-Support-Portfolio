# Ticket #23 — Missing Incoming Emails: Disabled Mailbox

**Lab type:** ServiceDesk Simulator | **Status:** Resolved by simulator | **Assignee:** ZuluTech  
**Reported by:** David Wu, Engineering (working remotely)

## Incident summary
David reported that colleagues, including Jessica Tran, had asked why he had not replied. He had not seen new emails since the previous day. Time-sensitive internal and external communications were affected. Before contacting support, he checked his internet connection and restarted the Mail application.

## Objective
Investigate why David could not receive email, identify the issue using available simulator evidence, and restore mailbox access.

## Investigation and evidence
1. **Initial hypothesis — VPN:** Because David was working remotely, I asked about VPN connectivity and whether sending was also affected. He confirmed he was disconnected from the VPN and could not send emails.
2. **VPN test:** David connected to the company VPN; it displayed **Connected**. He sent a test email but reported that he still had not received any new messages. The recipient's receipt of his outgoing test email was not confirmed.
3. **Message trace:** I searched Mail Admin for messages from Jessica Tran to David. The trace showed a message marked **Failed** with error `550 5.2.1 Mailbox cannot be accessed`.
4. **Mailbox inspection:** Mailbox Admin showed David's primary mailbox at **2.39 / 5 GB**, general status **Normal**, but **Mailbox Status: Disabled**. The mailbox was not full.

## Resolution
In Mailbox Admin, I selected **Enable Mailbox** for David's account. The simulator automatically marked the ticket resolved.

## Outcome and verification limits
**Simulator outcome:** Resolved immediately after enabling the mailbox. The disabled mailbox was the identified configuration issue consistent with the message-trace failure. The simulator closed the ticket before I could independently confirm new inbound delivery, verify the outgoing test email's receipt, or determine why the mailbox had originally been disabled. Jessica's failed message may need to be resent; this was not tested.

## Lessons learned
- Remote work and a disconnected VPN are useful clues, not proof of the cause.
- Follow message-trace delivery errors before changing DNS or client settings.
- Distinguish general mailbox health and storage from the separate enabled/disabled state.
- Record what the simulator confirms separately from tests actually performed.

## Suggested evidence screenshots
- `evidence/01-message-trace-550-error.png` — Jessica-to-David failed delivery and error.
- `evidence/02-mailbox-disabled.png` — Mailbox Admin showing Disabled and 2.39 / 5 GB.

**Portfolio note:** This is a simulated service-desk incident, not paid professional work. Screenshots should be reviewed for unnecessary personal/contact information before publication.
