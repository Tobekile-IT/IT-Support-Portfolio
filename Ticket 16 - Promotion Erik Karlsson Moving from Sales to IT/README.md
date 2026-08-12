Active Directory Role Change & Access Management
Ticket
Employee
Previous Department
New Department
Previous Group
New Group
Previous M365 License
New M365 License
#1235 — Promotion: Erik Karlsson moving from Sales to IT
Erik Karlsson
Sales
IT
Sales-GG
IT-Admins
E1
E3
Target OU
Result
1. Scenario
IT
Verified successfully
Erik Karlsson was promoted from Sales to IT. The existing account needed to be updated so that his Active
Directory location, group membership, and Microsoft 365 licensing matched his new role.
2. Objective
Remove the employee's previous Sales-specific access and apply the IT access and licensing required for the new
role.
3. Changes Performed
1. Located Erik Karlsson's existing Active Directory account.
2. Moved the account from the Sales OU to the IT OU.
3. Removed the Sales-GG group membership.
4. Added the IT-Admins group membership.
5. Upgraded the Microsoft 365 license from E1 to E3.
6. Verified the account configuration against the ticket requirements.
7. Ran the ServiceDesk Simulator verification and confirmed the solution.
8. Closed the ticket.
4. Verification
The required final state was confirmed: Erik's account was in the IT OU, was a member of IT-Admins, was no
longer a member of Sales-GG, and had the Microsoft 365 E3 license.
5. Skills Demonstrated
Active Directory user administration; OU management; group membership changes; role-based access
management; Microsoft 365 licensing; employee promotion/role-change administration; configuration verification;
service desk ticket handling.
6. Key Learning
When an employee changes roles, access should be updated to reflect the new responsibilities. This includes
removing obsolete department access, applying the new role's group membership, moving the account to the
appropriate OU, and updating cloud licensing.
7. Portfolio Summary
This lab demonstrates practical identity and access administration for an employee role change, including Active
Directory OU and group management and Microsoft 365 license administration