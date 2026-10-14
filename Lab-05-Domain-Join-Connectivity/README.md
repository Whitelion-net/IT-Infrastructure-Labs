# Lab 5 — Windows 10 Domain Join

## Objective
Join a Windows 10 client to an Active Directory domain and verify domain authentication and connectivity.

## Lab Environment
- Hypervisor: UTM
- Domain Controller: Windows Server 2022 (SERVER01)
- Client: Windows 10 (CLIENT01)
- Domain: corp.local
- Server IP: 192.168.64.4
- Client IP: 192.168.64.2
- Network: UTM Shared Network

## Exercises Completed

### 1. Network Configuration
- Verified IPv4 addresses, subnet masks, default gateways, and DHCP settings.
- Confirmed network connectivity between CLIENT01 and SERVER01.
- Tested TCP connectivity to LDAP port 389 using `Test-NetConnection`.

### 2. Active Directory and DNS Verification
- Verified domain configuration using `Get-ADDomain`.
- Checked DNS and NTDS services.
- Queried DNS A/AAAA and LDAP SRV records using `nslookup`.
- Configured the client to use the Domain Controller for DNS resolution.

### 3. Domain Join
- Opened System Properties on Windows 10.
- Joined CLIENT01 to the `corp.local` domain.
- Authenticated using domain administrator credentials.
- Restarted the client.

### 4. Domain User Authentication
- Logged into Windows 10 using `CORP\jsmith`.
- Verified the active domain user using `whoami`.
- Observed User Account Control (UAC) restrictions for a standard domain user.

### 5. Active Directory Computer Verification
- Used `Get-ADComputer` on the Domain Controller.
- Confirmed that CLIENT01 was registered in Active Directory.

## Results
- Successful domain join.
- Successful domain user login.
- DNS-based Domain Controller discovery verified.
- Active Directory computer account verified.

## Skills Demonstrated
Active Directory, Windows Server, DNS, DHCP, LDAP, Domain Join, PowerShell, Network Troubleshooting, and User Authentication.
