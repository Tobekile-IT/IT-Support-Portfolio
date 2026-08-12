Shared Folder Access
Ticket
User / Department
System
Resource
Issue
#1233 — User cannot open shared folder
David Stål — Sales
Windows file server / shared folders
\\fileserver\Sales
David could not open the Sales shared folder. The ticket indicated the Sales-GG group was not being allowed access.
Root Cause
Tool
The Sales shared-folder access configuration did not provide the required access.
Computer Management fi Shared Folders fi Shares
Troubleshooting Process
1. Reviewed the user's inability to access the UNC path \\fileserver\Sales.
2. Opened Computer Management and navigated to Shared Folders fi Shares.
3. Located the Sales share and confirmed that the share existed.
4. Used Grant Access for the Sales share to provide the required access.
5. The Service Desk simulator verified the change and marked the ticket as resolved.
Skills Demonstrated
Windows file-share troubleshooting, UNC paths, shared-folder administration, group-based access, Computer
Management, and permissions troubleshooting.
Key Learning
A shared-folder problem does not always require mapping a drive on the user's PC. Verify the share and
investigate access permissions/group membership from the administrator side