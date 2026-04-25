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
