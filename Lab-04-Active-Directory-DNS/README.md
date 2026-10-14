# Lab 4 – Active Directory User and Group Management

## Objective

The goal of this lab was to configure Active Directory Domain Services
and practice basic Active Directory administration in a Windows Server
environment.

The lab included creating a new Active Directory forest, organizing users
with Organizational Units, creating domain users and security groups,
managing user accounts, and using PowerShell to query Active Directory.

---

## Environment

- Windows Server 2022
- UTM Virtual Machine
- Active Directory Domain Services (AD DS)
- Domain: corp.local
- Server: SERVER01

---

## Exercise 1 – Install and Configure Active Directory Domain Services

Installed the Active Directory Domain Services (AD DS) role using
Server Manager.

Promoted SERVER01 to a Domain Controller.

Created a new Active Directory forest:

corp.local

The server was also configured with the DNS Server role during the
Domain Controller promotion process.

---

## Exercise 2 – Create Organizational Units

Opened Active Directory Users and Computers (ADUC).

Created three Organizational Units to represent departments in the
organization:

- IT
- HR
- Sales

These OUs provide a logical structure for organizing users, groups,
computers, and future Group Policy configurations.

---

## Exercise 3 – Create Domain Users

Created three Active Directory domain user accounts.

IT:

- John Smith
- Username: jsmith

HR:

- Sarah Johnson
- Username: sjohnson

Sales:

- Mike Davis
- Username: mdavis

Configured the accounts so users must change their temporary password
at the next logon.

---

## Exercise 4 – Create Security Groups

Created Global Security Groups for each department:

- IT-Staff
- HR-Staff
- Sales-Staff

Security groups can be used to assign permissions to multiple users
instead of assigning permissions individually.

---

## Exercise 5 – Configure Group Membership

Added each user to the appropriate departmental security group:

John Smith → IT-Staff

Sarah Johnson → HR-Staff

Mike Davis → Sales-Staff

Verified group membership using Active Directory Users and Computers.

---

## Exercise 6 – User Account Management

Practiced common Active Directory account administration tasks.

Tasks performed:

- Disabled a domain user account
- Re-enabled the account
- Reset a user's password
- Required password change at next logon
- Reviewed account properties and configuration options

These are common tasks performed by IT support technicians and
system administrators.

---

## Exercise 7 – Active Directory PowerShell

Used PowerShell to query Active Directory.

### Display all domain users

Get-ADUser -Filter *

### Display usernames and account status

Get-ADUser -Filter * | Select-Object Name, SamAccountName, Enabled

### Display Active Directory groups

Get-ADGroup -Filter * | Select-Object Name, GroupScope

### Display members of security groups

Get-ADGroupMember -Identity "IT-Staff"

Get-ADGroupMember -Identity "HR-Staff"

Get-ADGroupMember -Identity "Sales-Staff"

PowerShell provides a faster and scalable method for administering
Active Directory environments.

---

## Skills Practiced

- Windows Server administration
- Active Directory Domain Services
- Domain Controller configuration
- DNS integration with Active Directory
- Organizational Units (OU)
- Domain user management
- Security group management
- Group membership
- Password resets
- Account disabling and enabling
- Active Directory Users and Computers
- Active Directory PowerShell commands

---

## Screenshots

### Active Directory Organizational Structure

![Active Directory Structure](screenshots/ad-structure.png)

### Security Group Membership

![Group Membership](screenshots/group-membership.png)

### Active Directory PowerShell

![PowerShell AD Commands](screenshots/powershell-ad.png)

---

## What I Learned

This lab provided hands-on experience with the basic administration of
a Windows Active Directory environment.

I learned how Active Directory organizes users and groups using
Organizational Units, how security groups can simplify permission
management, and how administrators can manage and query Active Directory
using both graphical tools and PowerShell.
