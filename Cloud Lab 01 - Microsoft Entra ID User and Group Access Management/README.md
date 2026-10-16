# Cloud Lab 01 — Microsoft Entra ID User and Group Access Management

**Date:** 16 October 2026  
**Platform:** Microsoft Entra ID  
**Type:** Hands-on cloud identity administration

## Objective
Practise Microsoft Entra user onboarding, security group configuration, group membership changes, and least-privilege verification.

## Environment
- Existing **Finance Users** security group and fictional employee **Lerato Mokeana**
- Newly created **IT Support Users** security group
- Newly created fictional employee **Sipho Dlamini**

## Work performed
1. Inspected Finance Users: Security type, Assigned membership, owner, and Lerato's membership.
2. Verified Lerato's user-to-group relationship, enabled status, department, and lack of directory administrator roles.
3. Created IT Support Users with Assigned membership and a designated owner; not configured for Entra role assignment.
4. Onboarded Sipho with department **IT Support** and job title **Junior IT Support Technician**.
5. Assigned Sipho to IT Support Users and verified membership, enabled account status, and absence of assigned directory roles.
6. Removed Sipho's membership, verified the group became empty, then restored and verified his membership.

## Evidence
| Image | Verification |
|---|---|
| [01 — Finance Users overview](Screenshots/Lab01_Evidence_01.png) | Group configuration and membership count |
| [02 — Finance group membership](Screenshots/Lab01_Evidence_02.png) | Lerato listed as member |
| [03 — IT Support group properties](Screenshots/Lab01_Evidence_03.png) | Security / Assigned configuration |
| [04 — IT Support membership](Screenshots/Lab01_Evidence_04.png) | Sipho listed as member |
| [05 — Sipho job information](Screenshots/Lab01_Evidence_05.png) | Department and job title |
| [06 — Sipho directory roles](Screenshots/Lab01_Evidence_06.png) | No directory roles assigned |

## Scope and lessons learned
- **Group membership is not the same as resource access.** No application or resource access was assigned or tested in this lab.
- **Least privilege:** no Microsoft Entra directory administrative roles were assigned to the test employees.
- **Verification matters:** group membership was checked from both user and group views, and the membership change was verified after removal and restoration.
- The temporary removal was performed and verified during the lab, but was not separately captured in the final screenshots.

**Full report:** [Cloud Lab 01 PDF](Cloud_Lab_01_Entra_ID_User_and_Group_Management.pdf)
