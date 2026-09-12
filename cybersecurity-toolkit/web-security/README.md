# 🕸️ Burp Suite Reference Guide

A collection of methodologies, Intruder attack types, and payload references for Web Application Penetration Testing using Burp Suite.

---

## 🎯 1. Intruder Attack Types
Choosing the right attack type for brute-forcing or fuzzing.

* **Sniper:** Uses a single payload set. It targets each payload position one by one. (Best for testing a single parameter, like a password field).
* **Battering Ram:** Uses a single payload set. It places the *same* payload in *all* defined positions simultaneously.
* **Pitchfork:** Uses multiple payload sets. It iterates through the payload sets simultaneously (e.g., testing known `username:password` pairs together).
* **Cluster Bomb:** Uses multiple payload sets. It tests all possible combinations of the payloads (Best for full credential brute-forcing, though very slow).

## 🛠️ 2. Essential Extensions (BApp Store)
Tools to install to make testing significantly easier:

* **Autorize:** Essential for testing Insecure Direct Object References (IDOR) and authorization bypasses.
* **Logger++:** Advanced logging for all tools in Burp Suite, great for tracking down complex interactions.
* **JSON Web Tokens (JWT):** Decodes and allows manipulation of JWTs for session hijacking/bypasses.
* **Param Miner:** Discovers hidden, unlinked parameters. Crucial for finding Web Cache Poisoning vulnerabilities.

## 💉 3. Common Payload Quick-Reference
*Note: Always utilize `SecLists` for comprehensive fuzzing. These are just quick manual checks.*

### SQL Injection (Authentication Bypass)
* `' OR 1=1--`
* `admin' --`
* `" OR ""="`

### Cross-Site Scripting (XSS)
* `<script>alert(1)</script>`
* `"><svg/onload=alert(1)>`
* `javascript:alert(1)` (For testing href attributes)

### Local File Inclusion (LFI)
* `../../../../etc/passwd`
* `....//....//....//etc/passwd` (Bypass basic filter)
* `%2e%2e%2f%2e%2e%2fetc%2fpasswd` (URL Encoded)

## 🔄 4. Match and Replace Rules (Proxy Options)
Useful for bypassing client-side controls automatically:
* Require HTML5 form validation? -> Replace `type="hidden"` with `type="text"`
* Faking internal access? -> Add Header: `X-Forwarded-For: 127.0.0.1`
