# Network Connectivity Troubleshooting Runbook

## Purpose

This runbook provides a structured approach for investigating common network connectivity incidents.

## 1. Confirm the Scope

Identify:

- Affected user or device
- Location
- Source IP address
- Destination system or service
- Time the issue began
- Whether one user or multiple users are affected
- Whether the issue is intermittent or persistent

## 2. Verify Local Configuration

Check:

- IP address
- Subnet mask
- Default gateway
- DNS servers
- Network interface status

Windows commands:

```powershell
ipconfig /all
```

## 3. Test Connectivity

Test progressively:

1. Loopback address
2. Local host IP
3. Default gateway
4. Remote IP address
5. Destination hostname

Example:

```powershell
ping 127.0.0.1
ping 10.20.20.1
ping 10.10.10.10
```

## 4. Test DNS

Use DNS tools to determine whether the problem is related to connectivity or name resolution.

```powershell
nslookup example.internal
```

Check whether:

- The DNS server responds
- The hostname resolves to the expected IP address
- The client is using the correct DNS server

## 5. Review the Network Path

Use traceroute and the local routing table to determine how traffic is being forwarded.

```powershell
tracert 10.10.10.10
route print
```

Look for:

- An unexpected route
- A missing route
- The point where traffic stops
- An incorrect default gateway

## 6. Review ARP Information

```powershell
arp -a
```

Use the ARP table to confirm local Layer 2 address resolution where appropriate.

## 7. Review VPN and Firewall Controls

Determine whether:

- The VPN tunnel is established
- The correct local and remote networks are included
- Routing exists in both directions
- Firewall policy permits the required traffic
- The required protocol and destination port are allowed
- NAT is being applied correctly

## 8. Capture and Analyze Traffic

Use Wireshark when additional packet-level visibility is required.

Useful display filters:

```text
icmp
dns
tcp
ip.addr == 10.20.20.10
```

Packet analysis can help determine:

- Whether traffic leaves the source device
- Whether the destination responds
- Whether TCP connections are established
- Whether DNS requests and responses are successful
- Whether retransmissions or connection failures are occurring

## 9. Escalate When Required

Escalate the incident when:

- The issue involves infrastructure outside the analyst's level of access
- Router, switch, firewall, VPN, or service-provider changes are required
- The issue affects multiple locations or critical services
- Additional engineering analysis is required

Include all troubleshooting already completed when escalating.

## 10. Document the Resolution

Record:

- Reported symptoms
- Affected users or systems
- Scope of the incident
- Investigation steps
- Commands and tests performed
- Findings
- Root cause
- Corrective action
- Validation performed
- Escalation or follow-up required

## Troubleshooting Principle

Start close to the affected device and work outward through the network path. Validate each layer before moving to the next rather than changing multiple things at once.
