# 🕵️‍♂️ Gobuster Cheat Sheet

Gobuster is a fast, Go-based tool used to brute-force URIs (directories and files), DNS subdomains, and Virtual Host names on target web servers.

---

## 📂 1. Directory & File Brute-Forcing (`dir` mode)
Used to find hidden directories and files on a web server.

* **Basic Directory Scan:** 
  `gobuster dir -u http://192.168.1.10 -w /usr/share/wordlists/dirb/common.txt`
* **Scan for Specific File Extensions (e.g., .php, .txt, .html):** 
  `gobuster dir -u http://192.168.1.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html`
* **Bypass SSL Certificate Errors (for HTTPS):** 
  `gobuster dir -u https://10.10.10.10 -w /usr/share/wordlists/dirb/common.txt -k`
* **Hide Specific Status Codes (e.g., Hide 404s and 403s):** 
  `gobuster dir -u http://192.168.1.10 -w wordlist.txt -b 403,404`

## 🌐 2. Virtual Host Discovery (`vhost` mode)
Crucial for finding hidden subdomains hosted on the same IP address (common in CTFs and bug bounties).

* **Standard VHost Scan:** 
  `gobuster vhost -u http://example.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`
* **Append Domain to Wordlist (if needed):** 
  `gobuster vhost -u http://192.168.1.10 -w subdomains.txt --append-domain`

## 📡 3. DNS Subdomain Brute-Forcing (`dns` mode)
Used for external reconnaissance to find subdomains of a target domain.

* **Basic DNS Brute-Force:** 
  `gobuster dns -d example.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt`
* **Show CNAME Records:** 
  `gobuster dns -d example.com -w wordlist.txt -c`

## 💡 Recommended Wordlists (Kali Linux Defaults)
* **Quick/Basic:** `/usr/share/wordlists/dirb/common.txt`
* **Thorough (Web):** `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
* **APIs & Specifics:** Use `SecLists` (`/usr/share/wordlists/SecLists/Discovery/Web-Content/`)
