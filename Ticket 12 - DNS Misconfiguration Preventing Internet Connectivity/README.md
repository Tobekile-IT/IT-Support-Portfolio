IT Support Ticket Documentation
DNS Misconfiguration Preventing Internet Connectivity
Reported by: Derek Chambers (Finance Department)
Issue Description
The user reported having no internet connectivity after changing network settings. All websites and
internal company resources were unreachable. Other users on the same floor had normal
connectivity.
Business Impact
The user was unable to access the finance reporting portal or internet resources, preventing
month-end financial work.
Investigation
After reviewing the ticket, the initial hypothesis was that the issue was related to DNS because the
user admitted changing DNS settings manually. The internal Knowledge Base under Network &
Connectivity was consulted to verify the organization's approved DNS configuration before making
any changes.
Root Cause
The workstation had been configured with incorrect manual DNS settings. As a result, the computer
could not resolve company or public domain names.
Resolution
Using Remote Support, the network adapter settings were opened. The DNS configuration was
changed from manually configured DNS servers to 'Obtain DNS server address automatically'.
After applying the change, internet connectivity was restored immediately and the user regained
access to company resources.
Skills Demonstrated
• DNS Troubleshooting
• Windows Network Configuration
• Remote Support
• Knowledge Base Utilization
• Root Cause Analysis
• Enterprise IT Troubleshooting
Status: Resolved Successfully