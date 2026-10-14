# Lab 10 — Inter-VLAN Routing (Router-on-a-Stick)

## Objective

Configure inter-VLAN routing using a Cisco router and switch in Cisco Packet Tracer. Create two VLANs, configure an IEEE 802.1Q trunk, and implement Router-on-a-Stick to enable communication between devices in different VLANs.

## Tools and Equipment

- Cisco Packet Tracer
- Cisco 2911 Router (R1)
- Cisco 2960 Switch (SW1)
- 2 PCs (PC1 and PC2)
- Copper Straight-Through Ethernet cables

## Network Topology

The network consists of one router connected to one switch, with two PCs assigned to separate VLANs.

**Physical Connections:**

| Device | Interface | Connected To |
|---|---|---|
| R1 | GigabitEthernet0/0 | SW1 Gi0/1 |
| SW1 | FastEthernet0/1 | PC1 |
| SW1 | FastEthernet0/2 | PC2 |

**IP Addressing:**

| Device | IP Address | Subnet Mask | Default Gateway | VLAN |
|---|---|---|---|---|
| PC1 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 | 10 |
| PC2 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 | 20 |
| R1 Gi0/0.10 | 192.168.10.1 | 255.255.255.0 | N/A | 10 |
| R1 Gi0/0.20 | 192.168.20.1 | 255.255.255.0 | N/A | 20 |

## Exercises Completed

### Exercise 1 — Network Topology Setup

- Added a Cisco 2911 router, Cisco 2960 switch, and two PCs.
- Connected all devices using Ethernet cables.
- Configured router and switch hostnames through Cisco IOS CLI.
- Saved the network topology in Cisco Packet Tracer.

### Exercise 2 — VLAN Configuration

- Created VLAN 10 (SALES) and VLAN 20 (IT).
- Assigned switch interface Fa0/1 to VLAN 10.
- Assigned switch interface Fa0/2 to VLAN 20.
- Verified VLAN assignments using `show vlan brief`.

### Exercise 3 — Trunk Configuration

- Configured Gi0/1 on SW1 as a trunk port.
- Enabled IEEE 802.1Q VLAN tagging.
- Allowed VLANs 10 and 20 across the trunk.
- Enabled the physical router interface Gi0/0.
- Verified trunk status using `show interfaces trunk`.

**Verification:** The switch reported Gi0/1 as trunking with VLANs 10 and 20 allowed and active.

### Exercise 4 — Router-on-a-Stick Configuration

- Created router subinterface Gi0/0.10 for VLAN 10.
- Created router subinterface Gi0/0.20 for VLAN 20.
- Configured 802.1Q encapsulation on both subinterfaces.
- Assigned gateway IP addresses to both VLANs.
- Verified router interfaces using `show ip interface brief`.

### Exercise 5 — Inter-VLAN Connectivity Testing

- Assigned static IPv4 addresses to PC1 and PC2.
- Configured the appropriate default gateways.
- Tested connectivity from PC1 to its default gateway.
- Tested communication between VLAN 10 and VLAN 20 using ICMP ping.

## Verification Commands

**SW1 — Switch**

- `show vlan brief`
- `show interfaces trunk`

**R1 — Router**

- `show ip interface brief`

**PC1 — Command Prompt**

- `ping 192.168.10.1`
- `ping 192.168.20.10`

## Troubleshooting

During trunk configuration, the `show interfaces trunk` command initially returned no active trunk interfaces.

**Cause:** The router's physical interface was administratively down.

**Solution:** Enabled GigabitEthernet0/0 on R1 using the `no shutdown` command. The switch subsequently reported the trunk as operational.

Also practiced identifying Cisco IOS command modes and resolving command-entry errors when saving configurations.

## Screenshots

1. `01-network-topology.png` — Complete network topology.
2. `02-vlan-configuration.png` — VLAN assignments on SW1.
3. `03-trunk-configuration.png` — Operational 802.1Q trunk.
4. `04-router-subinterfaces.png` — Router subinterface configuration.
5. `05-intervlan-ping.png` — Connectivity test between VLANs.

## Skills Demonstrated

- Cisco IOS CLI configuration
- VLAN creation and port assignment
- Access and trunk port configuration
- IEEE 802.1Q tagging
- Router-on-a-Stick implementation
- IPv4 addressing and subnet configuration
- Default gateway configuration
- Inter-VLAN routing
- Network connectivity verification
- Basic Cisco IOS troubleshooting
- Saving running configurations to startup configurations

## Conclusion

This lab demonstrated how a router can enable communication between devices belonging to separate VLANs through a single physical interface.

The exercise provided practical experience configuring VLAN segmentation, trunk links, router subinterfaces, and basic inter-VLAN routing using Cisco Packet Tracer.
