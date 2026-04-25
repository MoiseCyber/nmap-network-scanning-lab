# Scan Findings Report

## Network Overview
- **Scan Date:** April 25, 2026
- **Tool Used:** Nmap 7.99
- **Network Range Scanned:** [target-network]/24
- **Total Hosts Discovered:** 2

## Findings Table

| IP Address | Port | Service | Version | Notes |
|------------|------|---------|---------|-------|
| [host-1] | 135/tcp | msrpc | Microsoft Windows RPC | Normal Windows service |
| [host-1] | 139/tcp | netbios-ssn | Microsoft Windows NetBIOS | File sharing protocol |
| [host-1] | 445/tcp | microsoft-ds | Unknown | SMB - monitor closely |
| [host-1] | 5357/tcp | http | Microsoft HTTPAPI 2.0 | UPnP enabled |
| [host-1] | 8000/tcp | http | Splunkd httpd | SIEM tool detected |
| [host-1] | 8089/tcp | ssl/http | Splunkd httpd | Splunk HTTPS interface |
| [host-1] | 16992/tcp | http | Intel AMT 14.1.77.2497 | Remote management |

## Summary
The scan revealed 2 active hosts on the network. The primary
host is running Windows OS with several services including
Splunk SIEM and Intel AMT remote management technology.

## Risk Observations
- **SMB (445)** — Should be monitored for unauthorized access attempts
- **Intel AMT (16992)** — Remote management port exposed, ensure access is restricted
- **UPnP (5357)** — Can expose network to unauthorized device discovery
- **Splunk (8000/8089)** — Ensure access is restricted to authorized users only

- ## Task 2 — TCP SYN Scan Findings

| Port | State | Service | Comments |
|------|-------|---------|----------|
| 135/tcp | open | msrpc | Windows RPC, expected service |
| 139/tcp | open | netbios-ssn | Windows NetBIOS file sharing |
| 445/tcp | open | microsoft-ds | SMB, monitor for unauthorized access |
| 8000/tcp | open | http-alt | Splunk web interface |
| 8089/tcp | open | unknown | Splunk HTTPS interface |
| 16992/tcp | open | amt-soap-http | Intel AMT remote management |
| 994+ ports | closed | — | Normal behavior |

**Findings:** All open ports are consistent with Task 1 results,
confirming accuracy. No unexpected services detected.
SYN scan completed in 0.88 seconds, significantly faster than version scans.

-
-   ## Task 4 — Port State Reasons

| Port | State | Service | Reason | Comment |
|------|-------|---------|--------|---------|
| 135/tcp | open | msrpc | syn-ack ttl 128 | Windows RPC |
| 137/tcp | filtered | netbios-ns | no-response | Firewall blocking |
| 139/tcp | open | netbios-ssn | syn-ack ttl 128 | NetBIOS file sharing |
| 445/tcp | open | microsoft-ds | syn-ack ttl 128 | SMB |
| 8000/tcp | open | http-alt | syn-ack ttl 128 | Splunk web interface |
| 8089/tcp | open | unknown | syn-ack ttl 128 | Splunk HTTPS |
| 16992/tcp | open | amt-soap-http | syn-ack ttl 128 | Intel AMT |
| 49664-50131/tcp | open | unknown | syn-ack ttl 128 | Windows dynamic ports |

**Findings:** TTL 128 confirms Windows OS on target host. All open ports
responded with syn-ack, meaning no firewall interference on LAN.
Port 137 is the only filtered port, blocked by the host firewall.
