# Missing Incoming Emails — Mail-Service Incident Investigation

**Environment:** ServiceDesk Simulator (training scenario)  
**Incident:** “Emails to me are going missing, the sender says they were sent”  
**Reported by:** David Lee, Support department  
**Status:** Resolved automatically by simulator after mail-server reboot  
**Scope:** Simulated incident; not paid or production IT experience

## 1. Objective
Investigate why a user could not receive expected email, distinguish a client-side issue from mailbox or shared mail-service issues, and document the evidence, action taken, and limits of verification.

## 2. Initial report
David reported that Rachel Green's messages from the previous day and that morning had not arrived. Asking Rachel to resend and restarting the Mail application had not helped. The business impact was missing correspondence and attachments.

## 3. Environment and tools
- ServiceDesk Simulator ticket and user communication
- Remote-support view of David's mail application
- Webmail and mailbox folder checks
- Mail Admin: Message Trace and Mailbox Admin
- Mail Security: quarantine and blocked-sender view
- Simulator server-room status and reboot control

## 4. Investigation and evidence

| Step | Action | Observation / significance |
| --- | --- | --- |
| 1 | Clarified the scope with David | He reported missing mail from other people too, not only Rachel. This broadened the investigation beyond one sender. |
| 2 | Checked webmail, Junk and Deleted Items with David | The missing messages were not visible there. A Mail-app-only issue became less likely. |
| 3 | Used remote support to inspect David's mailbox | Rachel's messages were not visible. A suspicious account-suspension email was found in Junk. |
| 4 | Asked whether David clicked the suspicious link or entered credentials | David said he had not. The message was treated as a separate security clue, not proof of compromise or the outage's cause. |
| 5 | Ran a message trace for David | Earlier messages showed **Delivered**, while three later messages from different senders showed **Pending** with `452 4.3.2 System not accepting network messages`. |
| 6 | Checked David's mailbox in Mailbox Admin | Mailbox **Enabled**, status **Normal**, storage **2.77 / 5 GB**; a full or disabled mailbox was not supported by this view. |
| 7 | Reviewed Mail Security | Visible quarantine contained suspicious messages, not the reported missing messages. Nothing was released. |
| 8 | Independently traced Rachel's mailbox | Three messages to Rachel from different senders were also **Pending** with the same `452 4.3.2` response. This supported a wider service issue rather than a David-only issue. |
| 9 | Inspected the server room | Mail server status was **Degraded**. The available controls were Reboot and Shut Down. |

### Key diagnostic clue

```text
Status: Pending
452 4.3.2 System not accepting network messages
```

The shared error across David's and Rachel's traces supported investigating the mail service. The response and degraded status did **not** identify the underlying technical cause by themselves.

## 5. Action taken
Rebooted the degraded mail server using the simulator's available **Reboot** control. The simulator automatically marked the ticket as resolved.

## 6. Outcome and verification limits
- **Observed outcome:** The simulator changed the ticket to resolved after the reboot.
- **Not independently verified:** Post-reboot server health, delivery of previously pending messages, or a new end-to-end test email. The ticket closed automatically before these checks were reported.
- **Root cause:** Not conclusively established. A degraded mail server was observed, but no service logs or specific failure details were available in the recorded investigation.

## 7. Lessons learned
1. Start by determining whether an email problem affects one sender, one mailbox, or multiple users.
2. Compare the mail application with webmail before repairing a local client.
3. Use message trace to distinguish messages that were delivered from those still pending.
4. Cross-check another mailbox when the evidence suggests a shared issue.
5. Treat suspicious email carefully, but do not attribute an outage to phishing without supporting evidence.
6. Record the difference between an action that makes a simulator close a ticket and a fix verified by fresh delivery tests.
7. In a production environment, a server reboot should follow appropriate incident/change procedures and communication; follow up on why the server degraded.

## 8. Evidence to include in the portfolio
Add screenshots if available, with personal addresses or other identifying details redacted where appropriate:

- `evidence/01-david-message-trace.png` — pending messages and `452 4.3.2` response
- `evidence/02-david-mailbox-admin.png` — enabled mailbox and storage status
- `evidence/03-rachel-message-trace.png` — same error for another user
- `evidence/04-mail-security.png` — security review, no messages released
- `evidence/05-degraded-mail-server.png` — degraded status **only if captured**
- `evidence/06-ticket-resolved.png` — simulator resolution **only if captured**

**Evidence note:** These filenames are suggested placeholders. Do not claim an image exists or upload one unless it was actually captured.

---
**Portfolio classification:** Hands-on simulated service-desk incident investigation. No claim of production administration, paid client work, or confirmed underlying root cause.
