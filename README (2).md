# Nmap Scan — README

## Overview
This repository contains the results and documentation for **Task 1: Basic Network Scanning with Nmap**. The objective was to perform a network scan on a local VM/subnet, identify open ports and running services, and document findings and their significance.

---

## Contents
- `nmap_scan_results.txt` — Raw Nmap output (if available).
- `nmap_report_txt.pdf` — Uploaded scan report (source used to generate updated PDF).
- `nmap_task_report_updated.pdf` — Generated PDF report (includes summary, findings, and screenshot).
- `screenshots/` — Directory containing screenshots of the Nmap output (if provided).
- `README.md` — This file.

---

## Environment
- Host OS: Kali Linux (VirtualBox VM)
- Nmap version used: 7.95 (as observed in the scan outputs)
- Target subnet (example): `10.98.216.0/24`
- Example scanned hosts seen in the readings: `10.98.216.16`, `10.98.216.84`, `10.98.216.193`

---

## Commands used (examples)
Use these commands from a Kali Linux terminal. Replace `<target>` with the IP or network range you want to scan.

- Basic service/version scan across a subnet:
```
nmap -sV 10.98.216.0/24
```

- Aggressive scan (OS detection, version, scripts, traceroute):
```
nmap -A <target IP>
```

- Scan all TCP ports (0-65535):
```
nmap -p- <target IP>
```

- Save output to a file (normal + grepable + XML):
```
nmap -sV -oN nmap_scan_results.txt -oG nmap_scan_results.gnmap -oX nmap_scan_results.xml <target>
```

---

## How to interpret the results
- **Open** — A service is listening on the port. Investigate which application and whether it should be exposed.
- **Closed** — The port is reachable but nothing is listening. Less risky but still provides host information.
- **Filtered** — Firewall or packet filtering is blocking probes; Nmap cannot determine if the port is open.
- **Ignored / Unknown** — Nmap couldn't determine the state (often due to network devices or rate limiting).

### Security significance
- Open ports correspond to services that can be attacked if vulnerable. Reduce exposed services to the minimum required, patch frequently, and use host-based firewalls.
- Filtered ports are good for security (obscuring services) but ensure legitimate services remain reachable where necessary.
- Regular scans help detect changes and misconfigurations early.

---

## Deliverables for GitHub (what to include)
1. `nmap_scan_results.txt` — Raw nmap output file (create using `-oN`).  
2. `README.md` — This file explaining the results and steps.  
3. `screenshots/` — Folder with screenshots showing the Nmap terminal output (evidence).  
4. `nmap_task_report_updated.pdf` — The formatted PDF report summarizing the work.  
5. Optionally: `demo_video.mp4` — Short screencast demonstrating how the scan was run and results interpreted.

---

## Reproducing the scan (quick steps)
1. Boot Kali Linux VM. Ensure the VM network is configured (NAT/Bridged) to reach target hosts.  
2. Open a terminal and run a discovery scan: `nmap -sn 10.98.216.0/24` to find live hosts.  
3. Pick a live host and run: `nmap -sV -A -oN nmap_scan_results.txt <target>`  
4. Review `nmap_scan_results.txt` and include the file in the repository. Take screenshots of the terminal for evidence.

---

## Notes & Recommendations
- Always obtain authorization before scanning networks you do not own. Scanning without permission may be illegal.  
- Use `-sS` (TCP SYN scan) for stealthier host discovery in permitted environments.  
- For thorough assessments, combine Nmap results with vulnerability scanners and manual verification.

---
*Report generated from provided scan outputs and screenshots.*
