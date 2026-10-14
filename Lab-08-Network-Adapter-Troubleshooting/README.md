# Lab 8 — DHCP Server Configuration

## Objective

Install and configure a DHCP Server on Windows Server 2022, create an IPv4 scope, configure DHCP options, and troubleshoot client connectivity.

## Lab Environment

- Hypervisor: UTM (macOS)
- Server OS: Windows Server 2022
- Client OS: Windows 10
- Domain: corp.local
- Server: SERVER01
- Server Primary IP: 192.168.64.4
- DHCP Interface: 10.10.10.1/24

## Exercise 1 — Network Configuration

Examined network interfaces using PowerShell.

Commands:

```powershell
ipconfig /all
Get-NetAdapter
Get-NetIPAddress -AddressFamily IPv4
```

Configured a second network adapter with a static IPv4 address of 10.10.10.1/24.

## Exercise 2 — DHCP Server Installation

Installed the DHCP Server role and management tools.

```powershell
Install-WindowsFeature -Name DHCP -IncludeManagementTools
```

Authorized the DHCP Server in Active Directory.

```powershell
Add-DhcpServerInDC -DnsName "SERVER01.corp.local" -IPAddress 192.168.64.4
```

## Exercise 3 — DHCP Scope Configuration

Created a DHCP scope with the following settings:

| Setting | Value |
|---|---|
| Scope Name | Lab-Network |
| Network | 10.10.10.0/24 |
| Start Address | 10.10.10.100 |
| End Address | 10.10.10.200 |
| Subnet Mask | 255.255.255.0 |
| Lease Duration | 8 days |

Activated the DHCP scope.

```powershell
Set-DhcpServerv4Scope -ScopeId 10.10.10.0 -State Active
```

## Exercise 4 — DHCP Options

Configured DHCP options:

- Option 006 — DNS Server: 10.10.10.1
- Option 015 — DNS Domain Name: corp.local
- Option 051 — Lease Duration: 8 days

```powershell
Set-DhcpServerv4OptionValue -ScopeId 10.10.10.0 -DnsServer 10.10.10.1 -DnsDomain "corp.local"
```

Verified the configuration using:

```powershell
Get-DhcpServerv4OptionValue -ScopeId 10.10.10.0
```

## Exercise 5 — DHCP Bindings

Verified that the DHCP Server was bound to the correct network interface.

```powershell
Get-DhcpServerv4Binding
```

Confirmed that DHCP was enabled on Ethernet 2 (10.10.10.1).

## Exercise 6 — Client Testing and Troubleshooting

Attempted to configure a Windows 10 client to receive an IPv4 address automatically.

Troubleshooting included:

- Checking network adapter status
- Verifying DHCP configuration
- Testing connectivity using ping
- Examining ARP neighbor entries
- Investigating UTM virtual networking settings

The client received an address from UTM's built-in DHCP service instead of the Windows DHCP Server.

ARP troubleshooting showed that the client could not reach the server's isolated interface.

**Limitation:** End-to-end DHCP lease assignment from Windows Server to Windows 10 was not successfully verified because of virtual network connectivity and competing DHCP services in the UTM environment.

## Screenshots

### Network Configuration
![Network Configuration](screenshots/01-network-configuration.png)

### DHCP Scope
![DHCP Scope](screenshots/02-dhcp-scope.png)

### DHCP Options
![DHCP Options](screenshots/03-dhcp-options.png)

### DHCP Binding
![DHCP Binding](screenshots/04-dhcp-binding.png)

## Skills Practiced

- Windows Server administration
- DHCP Server installation
- Active Directory DHCP authorization
- IPv4 scope configuration
- DHCP options management
- Network interface configuration
- PowerShell administration
- DHCP and Layer 2 troubleshooting

## Conclusion

Successfully installed and configured the Windows Server DHCP role, authorized the server in Active Directory, activated an IPv4 scope, and verified DHCP options and interface bindings.

Client DHCP lease testing remains incomplete because of limitations encountered in the virtual network environment.
