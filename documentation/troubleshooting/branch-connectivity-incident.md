# Branch-to-Corporate Connectivity Incident

## Scenario

A user at a simulated branch location reports that they cannot reach an application hosted on the corporate network.

## Environment

- Source network: `10.20.20.0/24`
- Destination network: `10.10.10.0/24`
- Branch default gateway: `10.20.20.1`
- Corporate application server: `10.10.10.10`

## Reported Symptoms

The user can access local branch resources but cannot reach the corporate application.

The purpose of the investigation is to determine whether the issue originates from:

- The endpoint
- Local network configuration
- DNS
- Routing
- VPN connectivity
- Firewall policy
- NAT
- The destination service

## Step 1: Validate the Client Configuration

Review the client network configuration.

```powershell
ipconfig /all
```
Confirm:

- The client has a valid IP address
- The subnet mask is correct
- The default gateway is correct
- The expected DNS servers are configured
- The network adapter is operational

## Step 2: Test the Local Network

Test the loopback interface:

```powershell
ping 127.0.0.1
```

Test the branch gateway:

```powershell
ping 10.20.20.1
```

Successful communication with the gateway indicates that basic local connectivity is working.

## Step 3: Test the Remote Destination

Test connectivity to the corporate application server:

```powershell
ping 10.10.10.10
```

In this scenario, the test fails.

This suggests that the problem exists beyond the local branch network.

## Step 4: Review the Network Path

Use traceroute to identify where traffic stops.

```powershell
tracert 10.10.10.10
```

Review the routing table:

```powershell
route print
```

Check for:

- Missing routes
- Incorrect routes
- Unexpected gateways
- Traffic stopping before reaching the remote network

## Step 5: Validate DNS Separately

If users access the application by hostname, test DNS resolution.

```powershell
nslookup app.example.internal
```

If DNS successfully returns `10.10.10.10`, name resolution is working and troubleshooting can remain focused on network connectivity.

## Step 6: Review VPN Connectivity

Because the branch and corporate networks communicate across a simulated site-to-site VPN, verify:

- The VPN tunnel is established
- Both network ranges are included in the tunnel
- Routes exist in both directions
- The expected traffic is permitted through the VPN

## Step 7: Review Firewall and NAT Behaviour

Review the simulated firewall policy.

Confirm:

- Traffic from `10.20.20.0/24` to `10.10.10.0/24` is permitted
- Required ports are allowed
- Return traffic is permitted
- NAT is not incorrectly modifying internal VPN traffic

## Step 8: Analyze Traffic with Wireshark

Capture traffic while reproducing the connectivity issue.

Useful Wireshark filters:

```text
icmp
ip.addr == 10.20.20.10
ip.addr == 10.10.10.10
```

Look for:

- ICMP echo requests leaving the branch client
- Whether echo replies return
- TCP SYN packets without responses
- Retransmissions
- Unexpected resets
- DNS failures

## Findings

The packet capture shows traffic leaving the branch client toward the corporate network, but the expected return traffic is not observed.

Local connectivity and DNS resolution are functioning correctly.

The investigation therefore focuses on routing, VPN connectivity, and firewall policy between the two networks.

## Root Cause

For this simulated incident, the root cause is a configuration issue affecting communication between the branch and corporate networks.

## Resolution

The simulated network configuration is corrected to restore communication between:

`10.20.20.0/24`

and

`10.10.10.0/24`

## Validation

After the correction, connectivity is retested using:

```powershell
ping 10.10.10.10
tracert 10.10.10.10
```

Wireshark is used to confirm successful two-way communication.

## Documentation and Escalation

The incident record should include:

- User-reported symptoms
- Affected network
- Troubleshooting performed
- Commands used
- Packet-analysis findings
- Identified root cause
- Corrective action
- Validation results
- Any follow-up required

If the required correction involves a router, firewall, VPN gateway, or infrastructure outside the analyst's permissions, the issue should be escalated with all investigation results attached.

## Key Takeaway

This scenario demonstrates a structured troubleshooting approach: validate the endpoint first, then progressively test local connectivity, DNS, routing, VPN connectivity, firewall policy, and packet flow before determining the root cause.
