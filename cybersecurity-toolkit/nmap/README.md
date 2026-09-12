# 🗺️ Nmap (Network Mapper) Cheat Sheet

A quick-reference guide for Nmap scanning techniques, optimized for reconnaissance, enumeration, and firewall evasion during penetration tests.

---

## 🚀 1. Host Discovery (Ping Sweeps)
Used to identify active devices on a network without port scanning them.

* **Ping Sweep (No Port Scan):** `nmap -sn 192.168.1.0/24`
* **ARP Ping (Local Network):** `nmap -PR -sn 192.168.1.0/24`
* **Disable Ping (Assume Host is Up):** `nmap -Pn 192.168.1.10` *(Crucial for bypassing firewalls that block ICMP)*

## 🔍 2. Port Scanning Techniques
Different methods to identify open ports and bypass basic filtering.

* **TCP SYN Scan (Stealth Scan - Default as root):** `nmap -sS 192.168.1.10`
* **TCP Connect Scan (Default without root):** `nmap -sT 192.168.1.10`
* **UDP Scan:** `nmap -sU 192.168.1.10` *(Often slow, consider combining with `--top-ports 20`)*
* **Scan All 65,535 Ports:** `nmap -p- 192.168.1.10`
* **Fast Scan (Top 100 Ports):** `nmap -F 192.168.1.10`

## 🧩 3. Service & OS Enumeration
Extracting version numbers and operating system details.

* **Service Version Detection:** `nmap -sV 192.168.1.10`
* **Aggressive Service Detection:** `nmap -sV --version-all 192.168.1.10`
* **OS Detection:** `nmap -O 192.168.1.10`
* **The "Everything" Scan (OS, Services, Default Scripts, Traceroute):** `nmap -A 192.168.1.10`

## 📜 4. Nmap Scripting Engine (NSE)
Automating vulnerability checks and advanced enumeration.

* **Run Default Safe Scripts:** `nmap -sC 192.168.1.10`
* **Scan for Known Vulnerabilities:** `nmap --script vuln 192.168.1.10`
* **SMB Enumeration (Shares & OS):** `nmap --script smb-os-discovery,smb-enum-shares -p 139,445 192.168.1.10`
* **HTTP Directory Brute-force:** `nmap --script http-enum -p 80,443 192.168.1.10`

## ⏱️ 5. Timing & Performance
Optimizing scan speeds (T0 is the slowest, T5 is the fastest).

* **Polite/Sneaky (T1/T2):** `nmap -T2 192.168.1.10` *(Used to evade basic IDS/IPS)*
* **Normal (T3):** Default speed.
* **Aggressive (T4):** `nmap -T4 192.168.1.10` *(Best for CTFs and fast, reliable local network scans)*
* **Insane (T5):** `nmap -T5 192.168.1.10` *(High risk of missing open ports due to packet drops)*

## 🗄️ 6. Output & Reporting
Always save your scan results for later analysis or reporting.

* **Output to Normal Text File:** `nmap -oN scan_results.txt 192.168.1.10`
* **Output to Greppable Format:** `nmap -oG scan_results.grep 192.168.1.10`
* **Output to XML:** `nmap -oX scan_results.xml 192.168.1.10`
* **Output to ALL Formats:** `nmap -oA initial_scan 192.168.1.10`
