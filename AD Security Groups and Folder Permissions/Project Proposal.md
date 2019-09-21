# AD Security Group and Folder Permission Overhaul

### Index
* [Overview](#overview)  
* [Goals](#goals)  
* [Specification](#specificaiton)
* [Process](#process)
    - [Planning](#planning)
    - [Review](#review)
* [Milestones](#milestones)

## Overview
Currently access to the network shares is given to an individual by explicitly adding that user onto a folder or file. This goes against [best practises](https://www.netwrix.com/ntfs_permissions_management.html), as well as creating extra workload when onboarding new staff, as a users individual permissions are not easily ascertained or replicated.

This project aims to remedy this by creating a selection of AD Security Groups corresponding to the various roles of the Briscoe Group Head Office Employees.

Permissions on the network shares would then be granted based on roles through a selection of security groups, conforming with best practices and reducing the workload when onboarding new staff.


## Goals
* To remove all explicit user permissions on network shares.
* To create standardized access levels based on roles.
* To bring the Network shares into line with best practises.
* To make the onboarding/offboarding process easier.


## Process

#### Planning

**Step 1**  
Create spreadsheet of all current head office job roles.  
Asign all head office staff members to a role.    
Create security group structure.  
Breakdown by:  
- Head Office Security Group OU  
- Department OU  
- Role Security Group  
- Seperate nested OU for the Department Managers    

![HO Security Groups Page 1](resources/AD_Security_Group_tree-1.jpg)  
![HO Security Groups Page 2](resources/AD_Security_Group_tree-2.jpg)  
PDF Available Here [PDF](resources/AD_Security_Group_tree.pdf)

**Step 2**  
Write Powershell script to export user folder permissions.  
Detail which Security Groups are to be applied to each Network share folder.

**Step 3**  
Create Script to add security group along side user on folders.  
Leave for a week to allow changes to propagate.

**Step 4**  
Select a group of test users and remove their explicit permissions from network shares.  
Test if they still have the same access.  

**Step 5**  
Remove a minor department's (Loss Prevention) explicit user permissions from Network Shares.  
Test if they still have the same access

**Step 6**  
Remove a major department's (Human Resources) explict user persmissions from Network Shares.  
Test if they still have the same access.

**Step 7**  
Remove all explicit user permissions.  
Test user access has remained the same.

**Step 8**  
Ensure no new explicit permissions are added onto network shares.  
Write Powershell Script to periodically scan through Network Shares and export any explicit user permissions that may have been added.


#### Review



## Milestones

1. Get sign off from IT Manager and Team Lead to begin project.

2. Create outline of proposed Security Group structure and members.
  
3. Meet with and get sign off for proposed structure from all department heads.

4. Create backup of existing network share fodler permissions.

5. Security Groups created and members added into their respective group.

6. Export and collate user permissions on network shares.

7. Plan which Security Group to apply to each network share folder.

8. Insure all Security Groups have been added onto folders.

9. Test users getting access only through Security Groups.

10. Confirm first minor department getting access only through Security Groups.

11. Confirm first major department getting access only through Security Groups.

12. Ensure all Departments getting access through only Security Groups.

