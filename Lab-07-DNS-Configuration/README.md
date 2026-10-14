# Lab 7 — DNS Configuration & Troubleshooting

## Objective
Configure and troubleshoot DNS services in a Windows Server Active Directory environment. Create and verify DNS records and test name resolution from a Windows 10 client.

## Lab Environment
- Hypervisor: UTM
- Server OS: Windows Server 2022
- Client OS: Windows 10
- Active Directory Domain: corp.local
- DNS Server: 192.168.64.4
- Network: UTM Shared Network

## Exercises Completed

### Exercise 1 — DNS Server Verification
- Opened DNS Manager on Windows Server 2022.
- Verified Forward Lookup Zones and Reverse Lookup Zones.
- Identified the existing Active Directory DNS zone: corp.local.

### Exercise 2 — DNS A Record
- Created an A record for testpc.corp.local.
- Assigned IPv4 address 192.168.64.100.
- Verified forward DNS resolution using nslookup.

### Exercise 3 — DNS CNAME Record
- Created a CNAME record for computer.corp.local.
- Configured the alias to point to testpc.corp.local.
- Verified that the alias resolves to 192.168.64.100.

### Exercise 4 — Reverse Lookup Zone
- Created an IPv4 reverse lookup zone for the 192.168.64.0/24 network.
- Created a PTR record mapping 192.168.64.100 to testpc.corp.local.
- Verified reverse DNS resolution using nslookup.

### Exercise 5 — DNS Server PTR Troubleshooting
- Investigated the "Server: UnKnown" message in nslookup.
- Created a PTR record for 192.168.64.4.
- Configured reverse DNS resolution for server01.corp.local.

### Exercise 6 — DNS Troubleshooting
- Used Resolve-DnsName to query DNS records.
- Verified A, CNAME, and PTR records.
- Used ping and Test-NetConnection to distinguish DNS resolution from network connectivity.

### Exercise 7 — Windows 10 DNS Client Configuration
- Configured Windows 10 to use 192.168.64.4 as its IPv4 DNS server.
- Examined IPv4 and IPv6 DNS client settings.
- Successfully queried the Windows Server DNS service from Windows 10.
- Verified both A and CNAME record resolution.

## Commands Used

```powershell
nslookup testpc.corp.local 192.168.64.4
nslookup computer.corp.local 192.168.64.4
nslookup 192.168.64.100 192.168.64.4

Resolve-DnsName testpc.corp.local -Server 192.168.64.4
Resolve-DnsName computer.corp.local -Type CNAME -Server 192.168.64.4
Resolve-DnsName 192.168.64.100 -Server 192.168.64.4

Get-DnsClientServerAddress
ping testpc.corp.local
Test-NetConnection testpc.corp.local -Port 80
```

## Results
- Successfully configured forward and reverse DNS records.
- Verified DNS resolution from Windows Server 2022.
- Confirmed successful DNS queries from a separate Windows 10 virtual machine.
- Demonstrated the difference between hostname resolution and network connectivity.

## Skills Demonstrated
- Windows Server DNS Administration
- Active Directory DNS
- Forward and Reverse DNS Lookup
- DNS A, CNAME, and PTR Records
- PowerShell Network Diagnostics
- DNS Client Configuration
- Basic DNS Troubleshooting
