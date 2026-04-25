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
