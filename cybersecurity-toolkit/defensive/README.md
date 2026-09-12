# 🛡️ Blue Team & Defensive Operations

A quick reference guide for Network Traffic Analysis (Wireshark), SIEM querying (Splunk), and Intrusion Detection (Snort/Suricata).

---

## 🦈 1. Wireshark (Packet Analysis)
Crucial display filters for isolating malicious traffic in PCAP files.

* **Filter by IP:** `ip.addr == 192.168.1.10`
* **Filter by Source/Destination:** `ip.src == 10.10.10.10` or `ip.dst == 10.10.10.10`
* **Find HTTP POST Requests (Often used for data exfiltration or logins):**
  `http.request.method == "POST"`
* **Filter by Port (e.g., SSH, HTTP):**
  `tcp.port == 22` or `tcp.port == 80`
* **Find failed TCP connections (SYN sent, no SYN-ACK):**
  `tcp.flags.syn==1 && tcp.flags.ack==0`

## 📊 2. Splunk (SIEM & Log Analysis)
Basic SPL (Search Processing Language) queries for threat hunting.

* **Find failed login attempts (Windows Event ID 4625):**
  `index=windows source="WinEventLog:Security" EventCode=4625 | stats count by Account_Name, Source_Network_Address`
* **Detect multiple failed logins followed by a success (Brute-Force success):**
  `index=windows EventCode=4624 OR EventCode=4625 | transaction Account_Name maxspan=5m | search eventcount>5 EventCode=4624`
* **Identify unusual outbound traffic on non-standard ports:**
  `index=firewall action=allowed NOT (dest_port=80 OR dest_port=443 OR dest_port=53)`

## 🚨 3. Snort & Suricata (IDS/IPS)
Basic rule syntax for detecting network anomalies.

* **Syntax Structure:**
  `[action] [protocol] [Source IP] [Source Port] -> [Dest IP] [Dest Port] ( [Rule Options] )`
* **Example: Detect Nmap XMAS Scan:**
  `alert tcp any any -> $HOME_NET any (msg:"Nmap XMAS Scan Detected"; flags:FPU; sid:1000001; rev:1;)`
* **Example: Detect cleartext FTP login attempt:**
  `alert tcp any any -> $HOME_NET 21 (msg:"FTP Login Attempt"; content:"USER"; nocase; sid:1000002; rev:1;)`
