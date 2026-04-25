# 🔍 Network Scanning & Host Enumeration with Nmap

## 📋 Project Overview
Hands-on cybersecurity lab focused on network scanning and host enumeration using Nmap. 
This project simulates the reconnaissance phase of a security assessment to identify 
active hosts, open ports, and running services on a local network.

## 🎯 Objectives
- Discover active hosts on a local network
- Identify open ports and running services
- Perform OS detection and service version enumeration
- Document findings in a structured security assessment format

## 🛠️ Tools Used
- Nmap 7.99 (Windows)
- Command Prompt (Windows)
- VS Code / Notepad (documentation)

## 📁 Repository Structure
- `/screenshots` — Step-by-step evidence of scans performed
- `/findings` — Documented results and risk observations

## ⚠️ Legal Disclaimer
All scans were performed on a personal local network in a controlled lab environment. 
No unauthorized systems were scanned.
## 🖥️ Lab Walkthrough

### Step 1 — Nmap Installation Verification
Confirmed successful installation of Nmap 7.99 on Windows.
The version output validates the environment is ready for network scanning operations.

![Nmap Version](nmap%20version.png)

### Step 2 — Network Interface Discovery (ipconfig)
Used the `ipconfig` command to identify the active network interfaces
and determine the local IP range to be used for scanning.

**Key findings:**
- Multiple network adapters detected
- Active Wi-Fi adapter identified with a /24 subnet
- Network range determined for use in Nmap scanning

![ipconfig output part 1](02-ipconfig-network-discovery-part1.png)
![ipconfig output part 2](02-ipconfig-network-discovery-part2.png)

### Step 3 — Ping Sweep (Host Discovery)
Used `nmap -sn` to perform a ping sweep across the entire /24 subnet
to identify all active hosts without triggering port scans.

**Command used:**

nmap -sn  [target-ip]

**Results:**
- Scanned 256 IP addresses
- Discovered 2 active hosts on the network
- Scan completed in 12.43 seconds

![Ping Sweep Results](03-ping-sweep-host-discovery.png)

### Step 4 — Port Scan (Service Discovery)
Performed a default port scan on the active host to identify
open ports and running services.

**Command used:**

nmap [target-ip]

**Results — 9 open ports discovered:**

| Port | Service | Notes |
|------|---------|-------|
| 135/tcp | msrpc | Windows RPC |
| 139/tcp | netbios-ssn | Windows NetBIOS file sharing |
| 445/tcp | microsoft-ds | SMB file sharing |
| 5357/tcp | wsdapi | Windows device discovery |
| 6666/tcp | irc | Unusual — warrants investigation |
| 8000/tcp | http-alt | HTTP service |
| 8080/tcp | http-proxy | HTTP proxy service |
| 8089/tcp | unknown | Unidentified service |
| 16992/tcp | amt-soap-http | Intel AMT remote management |

![Port Scan Results](04-port-scan-host.png)

### Step 4 — Service Version Detection
Ran a deeper scan using `-sV` to identify specific service 
versions running on each open port.

**Command used:**

nmap -sV [target-ip]

**Results — Services identified:**

| Port | Service | Version |
|------|---------|---------|
| 135/tcp | msrpc | Microsoft Windows RPC |
| 139/tcp | netbios-ssn | Microsoft Windows NetBIOS |
| 445/tcp | microsoft-ds | SMB |
| 5357/tcp | http | Microsoft HTTPAPI 2.0 (SSDP/UPnP) |
| 6666/tcp | irc | Unconfirmed |
| 8000/tcp | http | Splunkd httpd |
| 8080/tcp | http-proxy | Unconfirmed |
| 8089/tcp | ssl/http | Splunkd httpd |
| 16992/tcp | http | Intel AMT v14.1.77.2497 |

**Key findings:**
- OS confirmed as Windows
- Splunk SIEM running on ports 8000 and 8089
- Intel Active Management Technology detected
- UPnP enabled on port 5357

![Service Version Detection](05-service-version-detection.png)

### Step 4b — Saving Scan Results to File
Used the `-oN` flag to export scan results to a text file
for documentation and reporting purposes.

**Command used:**

nmap -sV -oN scan_results.txt [target-ip]

**Why this matters:**
In real security assessments, saving scan output is essential
for documentation, audit trails, and reporting to stakeholders.

📄 [View Full Scan Results](scan_results.txt)

## 📊 Findings Report step 5
A detailed findings report documenting all discovered hosts,
open ports, services, and risk observations from the scan.

📄 [View Full Findings Report](findings/scan-findings.md)

### Step 6 — Investigate and Interpret

#### Task 1 — Operating System Detection

##### Part 1 — OS Detection Scan
Used `-O` flag to identify the operating system running on the target host.

**Command used:**

nmap -O [target-ip] -oN task1_os_detection.txt

**Results:**
- Device type: General purpose
- OS detected: Microsoft Windows 11 24H2 - 25H2
- Network Distance: 0 hops
- OS CPE: cpe:/o:microsoft:windows_11

![OS Detection Scan](06-os-detection-scan.png)

##### Part 2 — Service Confirmation Scan
Ran a follow-up service scan to verify consistency between
detected OS and running services.

**Command used:**

nmap -sV [target-ip] -oN task1_service_confirm.txt

**Results:**
- Services confirmed consistent with Windows OS
- Splunk SIEM confirmed on ports 8000 and 8089
- Intel AMT confirmed on port 16992
- No discrepancies detected

![Service Confirmation Scan](07-service-confirmation-scan.png)

## Task 2 — TCP SYN Scan Findings

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

#### Task 2 — TCP SYN Scan

Performed a TCP SYN scan for stealthy and fast port detection.

**Command used:**

nmap -sS [target-ip] -oN task2_syn_scan.txt

**Key observations:**
- Scan completed in 0.88 seconds — much faster than version scans
- 6 open ports detected, consistent with Task 1 results
- No unexpected services detected

![TCP SYN Scan Output File](08b-task2-syn-scan-output-file.png)

📄 [View Raw Scan Output](task2_syn_scan.txt)
