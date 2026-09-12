# 🔑 Hashcat Cheat Sheet

Hashcat is the world's fastest and most advanced password recovery utility. This reference covers the most common attack modes and hash types used during CTFs and Active Directory engagements.

---

## 🔍 1. Identifying Hashes
Before cracking, you need to know the hash type. 
* **Tool:** Use `hashid` or `name-that-hash` in Kali Linux.
* **Common Hashcat Modes (`-m`):**
  * `0` = MD5
  * `1000` = NTLM (Windows Active Directory)
  * `1800` = SHA-512 (Linux `/etc/shadow`)
  * `13100` = Kerberos 5 TGS-REP (Kerberoasting)
  * `10000` = Django (PBKDF2-SHA256)

## ⚔️ 2. Attack Modes (`-a`)
* `-a 0` = Straight (Dictionary Attack)
* `-a 1` = Combination (Combines words from multiple wordlists)
* `-a 3` = Brute-force (Mask Attack)

## 📖 3. Dictionary Attacks (Mode 0)
The standard attack using a wordlist (like `rockyou.txt`).

* **Basic Dictionary Attack:**
  `hashcat -a 0 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt`
* **Using Rules (Mutations):**
  Applies rules like appending numbers, capitalizing, etc., to your wordlist.
  `hashcat -a 0 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule`

## 🎭 4. Mask Attacks (Mode 3)
Used when you know the password policy or format (e.g., exactly 8 characters, starts with a capital letter, ends with a number).

**Character Sets:**
* `?l` = Lowercase (`a-z`)
* `?u` = Uppercase (`A-Z`)
* `?d` = Digits (`0-9`)
* `?s` = Symbols (`!"#$%...`)
* `?a` = All of the above

**Examples:**
* **8-character password, lowercase only:**
  `hashcat -a 3 -m 0 hashes.txt ?l?l?l?l?l?l?l?l`
* **Password like "Admin123!" (Uppercase, 4 lowercase, 3 digits, 1 symbol):**
  `hashcat -a 3 -m 1000 hashes.txt ?u?l?l?l?l?d?d?d?s`

## 🛠️ 5. Helpful Commands
* **Show cracked passwords (don't crack again):** Append `--show`
* **Force Hashcat to ignore warnings:** Append `--force`
* **Optimize for your specific hardware:** Append `-O`
