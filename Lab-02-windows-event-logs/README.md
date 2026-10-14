# LAB 2 — Windows Troubleshooting

## Objective

Practice diagnosing and resolving common Windows issues using built-in administrative tools and PowerShell.

## Environment

* Operating System: Windows 10 ARM64
* Virtualization: UTM
* VM Name: CLIENT01
* Host: MacBook with Apple M2

## Exercises Completed

### 1. CPU Usage Investigation

**Tools:** Task Manager, PowerShell

* Created a temporary CPU-intensive workload.
* Monitored CPU usage in Task Manager.
* Identified the PowerShell process.
* Used `Get-Process` to inspect running processes.
* Stopped the workload and verified CPU usage afterward.

### 2. Windows Service Troubleshooting

**Tools:** Services (`services.msc`), PowerShell

* Inspected the Print Spooler service.
* Checked its status and startup type.
* Stopped and restarted the service.
* Verified the service status using PowerShell.

**Commands:**

```powershell
Get-Service -Name Spooler
Restart-Service -Name Spooler
```

### 3. Event Viewer Investigation

**Tool:** Windows Event Viewer (`eventvwr.msc`)

* Explored Windows Application and System logs.
* Inspected event levels, sources, timestamps, and Event IDs.
* Used event filters to narrow down log entries.
* Opened event details and reviewed event descriptions.

**Outcome:** Practiced interpreting Windows event logs and identifying information relevant to troubleshooting.

### 4. Disk Space Investigation

**Tools:** Windows Storage Settings, PowerShell

* Inspected disk capacity and available space.
* Reviewed storage usage categories.
* Examined temporary files and available cleanup options.
* Checked disk space using PowerShell.

**Commands:**

```powershell
Get-Volume
Get-PSDrive -PSProvider FileSystem
Get-PSDrive -Name C
```

### 5. System File Integrity

**Tool:** System File Checker (SFC)

* Ran a system file integrity check.
* Reviewed the verification results.
* Learned about DISM as an additional Windows image repair and diagnostic tool.

**Command:**

```powershell
sfc /scannow
```

**Result:** [Insert the actual SFC result.]

## Skills Practiced

* Windows client troubleshooting
* CPU and process monitoring
* Windows service management
* Event Viewer log investigation
* Disk space analysis
* PowerShell administration
* System file integrity checks
* Basic troubleshooting and verification

## Evidence

Screenshots documenting selected exercises are stored in the `screenshots/` directory.

## Key Takeaways

This lab provided hands-on experience with common Windows troubleshooting tools and workflows, including identifying resource-intensive processes, managing services, investigating event logs, checking storage usage, and verifying system file integrity.
