# Lab 09 — Cisco VLAN & Trunking Configuration

## Overview

In this lab, I used Cisco Packet Tracer to build and configure a small network consisting of two Cisco Catalyst 2960 switches and four PCs.

I configured static IP addressing, VLAN segmentation, access ports, and an IEEE 802.1Q trunk connection between the switches. I also verified network connectivity and demonstrated traffic isolation between VLANs.

## Lab Environment

- **Simulation Software:** Cisco Packet Tracer
- **Switches:** 2 × Cisco Catalyst 2960
- **End Devices:** 4 × PCs
- **Networking:** Ethernet, IPv4, VLANs, IEEE 802.1Q
- **Management Interface:** Cisco IOS CLI

## Network Topology

| Device | IP Address | VLAN | Switch Port |
|---|---|---|---|
| PC0 | 192.168.1.10/24 | 10 — SALES | SW1 Fa0/1 |
| PC1 | 192.168.1.20/24 | 20 — IT | SW1 Fa0/2 |
| PC2 | 192.168.1.30/24 | 10 — SALES | SW2 Fa0/1 |
| PC3 | 192.168.1.40/24 | 20 — IT | SW2 Fa0/2 |

SW1 and SW2 were connected through their GigabitEthernet0/1 interfaces using an 802.1Q trunk.

All PCs were assigned addresses from the same subnet for this Layer 2 isolation demonstration. In a production network, separate VLANs would normally use separate IP subnets.

![Network Topology](screenshots/05-network-topology.png)

## Exercise 1 — Basic Network Connectivity

**Objective:** Build a basic LAN and verify connectivity between two devices.

Steps performed:

1. Added a Cisco Catalyst 2960 switch and two PCs.
2. Connected both PCs using copper straight-through cables.
3. Assigned static IPv4 addresses.
4. Verified connectivity using ICMP ping.

Commands used:

```cmd
ping 192.168.1.20
ping 192.168.1.10
```

**Result:** Both PCs successfully communicated while connected to the same default VLAN.

## Exercise 2 — Cisco IOS CLI Configuration

**Objective:** Learn Cisco IOS command modes and basic switch management.

Commands used:

```text
enable
show mac address-table
configure terminal
hostname SW1
end
copy running-config startup-config
```

Verified dynamically learned MAC addresses and their associated switch ports.

Changed the switch hostname and saved the configuration to NVRAM.

**Result:** Successfully accessed Privileged EXEC and Global Configuration modes, inspected the MAC address table, and saved the configuration.

## Exercise 3 — VLAN Configuration

**Objective:** Create separate Layer 2 broadcast domains and configure access ports.

Created VLAN 10 (SALES) and VLAN 20 (IT).

Configuration:

```text
enable
configure terminal
vlan 10
name SALES
exit
vlan 20
name IT
exit
interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit
interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
exit
end
```

Verification:

```text
show vlan brief
```

![VLAN Configuration](screenshots/01-vlan-creation.png)

Tested connectivity between PC0 and PC1 after assigning them to separate VLANs.

**Result:** The ping failed as expected because the PCs belonged to different Layer 2 broadcast domains and no inter-VLAN routing was configured.

![VLAN Isolation](screenshots/02-vlan-isolation.png)

## Exercise 4 — 802.1Q Trunk Configuration

**Objective:** Extend VLANs across multiple switches using a trunk connection.

Added a second Cisco Catalyst 2960 switch and configured GigabitEthernet0/1 as a trunk interface on both switches.

Configuration applied on each switch:

```text
configure terminal
interface gigabitEthernet 0/1
switchport mode trunk
switchport trunk allowed vlan 10,20
end
```

Created VLAN 10 and VLAN 20 on SW2 and assigned its FastEthernet0/1 and FastEthernet0/2 interfaces to the corresponding VLANs.

Verification:

```text
show interfaces trunk
show vlan brief
```

![Trunk Configuration](screenshots/03-trunk-configuration.png)

**Result:** The trunk was configured to carry VLAN 10 and VLAN 20 traffic between SW1 and SW2.

## Exercise 5 — Network Connectivity Verification

**Objective:** Verify same-VLAN connectivity across switches and confirm inter-VLAN isolation.

Performed the following tests:

| Source | Destination | Expected Result | Observed Result |
|---|---|---|---|
| PC0 — VLAN 10 | PC2 — VLAN 10 | Success | Success |
| PC1 — VLAN 20 | PC3 — VLAN 20 | Success | Success |
| PC0 — VLAN 10 | PC3 — VLAN 20 | Failure | Failure |

Commands used:

```cmd
ping 192.168.1.30
ping 192.168.1.40
```

**Result:** Devices belonging to the same VLAN successfully communicated across the trunk. Devices belonging to different VLANs remained isolated.

![Connectivity Verification](screenshots/04-trunk-connectivity.png)

## Final Verification and Configuration Backup

Executed the following commands:

```text
show vlan brief
show interfaces trunk
show mac address-table
copy running-config startup-config
```

Saved the Cisco Packet Tracer project as:

`Lab09-VLAN-Trunking.pkt`

## Skills Demonstrated

- Cisco IOS CLI navigation
- Layer 2 switching and MAC address learning
- Static IPv4 configuration
- VLAN creation and management
- Access port configuration
- IEEE 802.1Q trunk configuration
- VLAN segmentation and isolation
- ICMP connectivity testing
- Network configuration verification
- Saving switch configurations

## Key Takeaways

This lab demonstrated how VLANs logically segment a network and how 802.1Q trunking extends those VLANs across multiple switches.

I verified that devices in the same VLAN can communicate across a trunk while devices in different VLANs remain isolated without inter-VLAN routing.

The lab strengthened my understanding of Cisco switch configuration, Layer 2 networking, and basic network troubleshooting.
