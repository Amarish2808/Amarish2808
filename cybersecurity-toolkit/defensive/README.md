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

