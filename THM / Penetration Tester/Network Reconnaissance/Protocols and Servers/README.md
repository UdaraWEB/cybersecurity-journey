    TryHackMe: Protocols and Servers - writeup

Hello! This is my comprehensive walkthrough and learning notes for the **Protocols and Servers** room on TryHackMe. This room focuses on understanding common application-layer protocols, how they operate under the hood, and why plaintext protocols pose severe security risks.

---

## Task 1: Telnet Protocol
Telnet (developed in 1969) allows remote CLI access to another machine over **TCP port 23**. It transmits everything—including usernames and passwords—in cleartext. Today, it is completely replaced by **SSH (Port 22)**.

### Answer:
* **To which port will the telnet command with the default parameters try to connect?** `23`

---

## Task 2: HTTP (Hypertext Transfer Protocol)
HTTP (**Port 80**) is used to transfer web pages. Like Telnet, it is a cleartext protocol, whereas **HTTPS (Port 443)** uses TLS encryption to secure traffic. We can use Telnet/Netcat to manually send HTTP requests to grab web server versions from headers.

### Answer:
* **Connect using Telnet to MACHINE_IP 80 and retrieve the file flag.thm. What does it contain?**
  * *Command sequence used:*
    ```text
    telnet 10.48.174.91 80
    GET /flag.thm HTTP/1.1
    host: telnet
    (Press Enter twice)
    ```
  * *Flag discovered:* `THM{e3eb0a1df437f3f97a64aca5952c8ea0}`

---

## Task 3: FTP (File Transfer Protocol)
FTP (**Port 21**) is designed for transferring files. It uses a dual-connection architecture: a *Control Channel* (Port 21) for commands and a *Data Channel* (Port 20 or dynamic) for actual file transfers. Because of this, standard Telnet cannot download files; a dedicated **FTP Client** must be used. Secure alternatives include **SFTP** and **FTPS**.

### Answer:
* **Using an FTP client, connect to the VM and try to recover the flag file. What is the flag?**
  * *Command sequence used:*
    ```bash
    ftp 10.48.174.91
    Name: frank
    Password: D2xc9CgD
    ftp> ls
    ftp> get flag.txt
    ftp> exit
    cat flag.txt
    ```
  * *Flag discovered:* `THM{364db6ad0e3ddfe7bf0b1870fb06fbdf}`

---

## Task 4 & 5: SMTP (Simple Mail Transfer Protocol)
SMTP (**Port 25**) is utilized for *sending* emails between Mail Transfer Agents (MTAs). Traditional SMTP does not verify sender identities, allowing **Email Spoofing** (a primary vector for phishing). Secure submission happens over **Port 587 (STARTTLS)** or **Port 465 (SMTPS)**.

### Answer:
* **Connect to the SMTP port of the target VM. What is the flag that you can get?**
  * *Command used:* `telnet 10.48.174.91 25`
  * *Flag discovered in the welcome banner:* `THM{5b31ddfc0c11d81eba776e983c35e9b5}`

---

## Task 6: POP3 (Post Office Protocol v3)
POP3 (**Port 110**) is a Mail Delivery Agent (MDA) protocol used to download emails. It follows a "download-and-delete" model, meaning emails are removed from the server once downloaded to a single local device. The `STAT` command returns the number of messages and total mailbox size. Secure version: **POP3S (Port 995)**.

### Answers:
1. **What is the response you get to STAT?** `+OK 0 0` *(Note: Requires logging in via `USER frank` and `PASS D2xc9CgD` first).*
2. **How many email messages are available to download via POP3?** `0`

---

## Task 7: IMAP (Internet Message Access Protocol)
IMAP (**Port 143**) is a more sophisticated MDA protocol than POP3. It keeps emails stored on the server and synchronizes read/unread status and folders across multiple devices seamlessly. Each manual command must be preceded by a unique tag (e.g., `c1 LOGIN`). Secure version: **IMAPS (Port 993)**.

### Answer:
* **What is the default port used by IMAP?** `143`

---

## Key Takeaways & Conclusion
* **Cleartext Risk:** Telnet, HTTP, FTP, SMTP, POP3, and IMAP all transmit authentication credentials in plaintext, making them highly vulnerable to packet sniffing and man-in-the-middle (MITM) attacks.
* **The Power of Telnet Client:** Although Telnet servers are obsolete, the Telnet client is an invaluable tool for passive/active banner grabbing and manual protocol interaction.
* **Always Encrypt:** In modern security architectures, plain protocols must be disabled in favor of encrypted variants like **SSH, HTTPS, SFTP, and IMAPS**.
