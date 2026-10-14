# LAB 1 — Windows 10 Client & Basic Network Diagnostic

## Objective

Set up a Windows 10 client and practice basic network configuration and inspect connectivity using built-in Windows commands.

## Environment

* Host: MacBook with Apple M2
* Virtualization: UTM
* Guest OS: Windows 10 ARM64
* VM Name: CLIENT01
* RAM: 4 GB
* vCPU: 2
* Network: Shared Network

## Tasks Completed

### 1. Network Adapter

Tested the Windows network adapter and verified that the adapter was available and functioning.

### 2. IP Configuration

Used `ipconfig` to inspect the client's network configuration, including:

* IPv4 address
* Subnet mask
* Default gateway
* DNS server information

### 3. DNS Testing

Tested DNS connectivity and verified that the client could resolve network names.

### 4. TCP Connection Testing

Tested TCP connectivity to verify whether a network service could be reached.

### 5. Ping Testing

Used `ping` to test connectivity to IP addresses and determine whether hosts were reachable.

## Troubleshooting Approach

The lab demonstrated a basic network troubleshooting workflow:

1. Verify the network adapter.
2. Check IP configuration.
3. Verify the default gateway.
4. Test connectivity using `ping`.
5. Test DNS resolution.
6. Test TCP connectivity.

This provides a basic foundation for diagnosing client-side network connectivity problems.

## Evidence

Screenshots documenting the completed tests are stored in:

`screenshots/`

## Skills Practiced

* Windows 10 administration
* Network adapter troubleshooting
* IPv4 configuration
* `ipconfig`
* DNS troubleshooting
* TCP connectivity testing
* `ping`
* Basic network troubleshooting methodology
