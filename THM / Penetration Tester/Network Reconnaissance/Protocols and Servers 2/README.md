     TryHackMe: Protocols and Servers 2 - writeup

Hello everyone! This is my detailed walkthrough and learning notes for the **Protocols and Servers 2** room on TryHackMe. This room dives deep into network sniffing, Man-in-the-Middle (MITM) techniques, SSL/TLS mechanisms, SSH hardening, and automated password cracking using Hydra.

---

## Task 1 & 2: Sniffing Attacks
Sniffing involves capturing unencrypted packets in transit using tools like `tcpdump` or `Wireshark`. If cleartext protocols are used, credentials and message content can be easily stolen.

### Useful filters learned:
* `sudo tcpdump port 23 -A` (Capture Telnet traffic in ASCII format)
* Wireshark filter: `imap` (Filters and displays only IMAP traffic)

### Answers:
1. **What do you need to add to the command sudo tcpdump to capture only Telnet traffic?** `port 23`
2. **What is the simplest display filter you can use with Wireshark to show only IMAP traffic?** `imap`

---

## Task 3: Man-in-the-Middle (MITM) Attacks
An attacker intercepts communication between two parties to read or alter messages. Common redirection techniques include ARP Spoofing, DNS Spoofing, and Rogue Access Points. 

### Core Tools:
* **Bettercap:** Modern, active successor to Ettercap.
* **Ettercap:** Classic LAN MITM tool with 3 interfaces (Text `-T`, GUI `-G`, Ncurses `-C`).

### Answers:
1. **How many different interfaces does Ettercap offer?** `3`
2. **In how many ways can you invoke Bettercap?** `2`

---

## Task 4: Transport Layer Security (TLS)
TLS secures communication by operating below the application layer to encrypt traffic. 
* **Implicit TLS:** Connection is encrypted from the start on a dedicated port (e.g., HTTPS on 443, IMAPS on 993, DoT on 853).
* **STARTTLS:** Upgrades an existing cleartext connection to TLS on the same port.

### Answers:
1. **What is the default port used by DNS over TLS (DoT)?** `853`
2. **Which command allows upgrading an existing cleartext connection to a TLS connection on the same port?** `STARTTLS`

---

## Task 5: SSH (Secure Shell) Hardening & Operations
SSH (**Port 22**) provides encrypted remote administration. File transfers can be securely done via **SFTP** or **SCP**.

### Operational Lab Walkthrough:
* Connecting to the target machine: `ssh mark@MACHINE_IP` (Password: `XBtc49AB`)
* Checking Kernel release: `uname -r` $\rightarrow$ `5.15.0-119-generic`
* Securely copying a file: `scp mark@MACHINE_IP:/home/mark/book.txt .` $\rightarrow$ Displays a download size of `415 KB`.

### Answers:
1. **Using uname -r, find the Kernel release?** `5.15.0-119-generic`
2. **Use SSH to download the file book.txt from the remote system. How many KBs did scp display as download size?** `415`

---

## Task 6: Password Attacks & THC Hydra
Hydra is a lightning-fast password cracking tool targeting network services (FTP, SSH, IMAP, etc.). 

### Practical Attack Command Used:
```bash
hydra -l lazie -P /usr/share/wordlists/rockyou.txt 10.49.137.245 imap
```
Hydra tested the `rockyou.txt` wordlist against the IMAP service and successfully recovered the valid plaintext password.

### Answer:
* **What is the password used to access the IMAP service on 10.49.137.245 for user lazie?** `butterfly`

---

## Defensive Checklist & Key Takeaways
* **Decommission Plaintext:** Ensure Telnet, FTP, and plain HTTP are completely disabled in favor of SSH, SFTP, and HTTPS.
* **Implement HSTS & Pinning:** Prevent SSL stripping using Strict Transport Security headers.
* **Enforce MFA:** Since passwords remain a major vector for brute-forcing, implementing Multi-Factor Authentication or passwordless keys (FIDO2) is critical to building a Zero-Trust network environment.
