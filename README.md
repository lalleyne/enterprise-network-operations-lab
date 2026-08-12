# Enterprise Network Operations Lab

## Overview

This project demonstrates practical network operations and troubleshooting skills in a simulated enterprise environment.

The lab focuses on network connectivity, routing, firewall policy, NAT, VPN concepts, packet analysis, and structured troubleshooting.

The goal is to demonstrate how I approach a network issue from initial triage through investigation, validation, resolution, and documentation.

## Skills Demonstrated

- TCP/IP troubleshooting
- LAN and WAN concepts
- DNS and DHCP troubleshooting
- Routing and route validation
- Firewall rule analysis
- NAT concepts
- VPN connectivity
- Network traffic analysis with Wireshark
- Connectivity testing
- Incident triage
- Root cause analysis
- Technical documentation
- Knowledge base / runbook development

## Lab Environment

The project uses a fictionalized enterprise network so that no employer, customer, or proprietary information is included.

| Network | Address Range |
|---|---|
| Corporate LAN | 10.10.10.0/24 |
| Branch LAN | 10.20.20.0/24 |
| DMZ | 10.30.30.0/24 |
| Remote Access VPN Pool | 10.40.40.0/24 |

## Network Topology

The lab uses a fictional enterprise environment containing a corporate LAN, branch network, DMZ, firewall, site-to-site VPN, and remote-access VPN.

➡️ [View the Enterprise Network Topology](diagrams/network-topology.md)

## Troubleshooting Scenario

### Reported Issue

Users on the branch network are unable to reach a service hosted on the corporate network.

### Initial Troubleshooting

1. Verify local IP configuration.
2. Confirm the default gateway is reachable.
3. Test local network connectivity.
4. Test connectivity to the remote network.
5. Review DNS resolution.
6. Inspect the routing path.
7. Verify VPN connectivity.
8. Review applicable firewall rules.
9. Capture network traffic with Wireshark where additional visibility is required.

### Validation Tools

- `ipconfig /all`
- `ping`
- `tracert`
- `nslookup`
- `route print`
- `arp -a`
- Wireshark

## Project Documentation

### Network Topology

➡️ [Enterprise Network Topology](diagrams/network-topology.md)

Shows the simulated corporate LAN, branch LAN, DMZ, firewall, VPN connectivity, and network segmentation used throughout the project.

### Network Troubleshooting Runbook

➡️ [Network Connectivity Troubleshooting Runbook](documentation/network-troubleshooting-runbook.md)

A structured workflow for investigating endpoint, DNS, routing, VPN, firewall, NAT, and connectivity problems.

### Incident Walkthrough

➡️ [Branch-to-Corporate Connectivity Incident](troubleshooting/branch-connectivity-incident.md)

A simulated incident demonstrating how a branch connectivity problem can be triaged, investigated, escalated, and documented.

### Wireshark Packet Analysis

➡️ [Wireshark Packet Analysis](analysis/wireshark-packet-analysis.md)

A hands-on packet-analysis exercise demonstrating ICMP connectivity testing, DNS resolution analysis, and TCP three-way handshake validation using Wireshark.

## Important Note

This is an independent portfolio lab. All network names, IP addresses, configurations, screenshots, and scenarios are fictionalized or recreated for demonstration purposes. No confidential employer or customer information is included.
