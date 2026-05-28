---

     Task 6: Web Browser & Developer Tools

The web browser is one of the most powerful and stealthy tools for active reconnaissance because its traffic blends in perfectly with normal user activity. 

By opening the **Developer Tools (Ctrl + Shift + I)**, we can inspect vital information:
* **Network Tab:** Shows live HTTP/HTTPS requests, status codes, and server banners.
* **Sources/Debugger Tab:** Allows us to view JavaScript files, which often contain hidden developer comments, API endpoints, or directory structures.
* **Application/Storage Tab:** Explores session tokens and cookies.

### Answers:
* **Using Developer Tools, figure out the total number of questions:** `6` *(Note: This was found by inspecting the
* JavaScript source file under the Sources tab).*

---

## Task 7: Ping

The `ping` command uses the **ICMP (Internet Control Message Protocol)** to check if a remote host is online and reachable. 
It sends an ICMP Echo Request (Type 8) and listens for an ICMP Echo Reply (Type 0). 

It also reveals the **TTL (Time To Live)** value, which helps in OS fingerprinting (Linux usually starts at 64, while Windows starts at 128).

### Answers:
1. **Which option would you use to set the size of the data carried by the ICMP echo request?** `-s`
2. **What is the size of the ICMP header in bytes?** `8`
3. **Does MS Windows Firewall block ping by default?** `Y`
4. **How many ping replies did you get back after issuing ping -c 10?** `10`

---

## Task 8: Traceroute

`traceroute` (or `tracert` on Windows) tracks the path that network packets take to reach a destination by mapping every router
(hop) along the way. It does this by sending packets with incrementally increasing TTL values (starting at 1).

### Answers:
1. **In Traceroute A, what is the IP address of the last router/hop before reaching tryhackme.com?** `100.92.9.83`
2. **In Traceroute B, what is the IP address of the last router/hop before reaching tryhackme.com?** `99.83.89.19`
3. **In Traceroute B, how many routers are between the two systems?** `25` *(Calculated by taking the total hops of 26 and
4. subtracting the final destination system).*

---

## Task 9: TELNET & Banner Grabbing

Telnet operates over TCP (default port 23) but sends everything in cleartext, making it highly insecure compared to SSH. However, 
it is an excellent tool for **Banner Grabbing**—connecting to an open TCP port (like port 80) to read the server's welcome message, 
which often discloses the software name and version.

### Answers:
1. **What is the name of the running server on port 80?** `Apache`
2. **What is the version of the running server?** `2.4.41`

---

## Task 10: Netcat (nc)

Netcat is often called the "Swiss Army Knife" of networking. It can act as a client (to connect to ports and grab banners) or as a server 
(listening on a port using `nc -vnlp`). Unlike HTTP on port 80, when you connect to a service like FTP on port 21 using Netcat, it grabs and 
displays the version banner immediately without needing any user commands.

### Answers:
* **Use Netcat to connect to the VM port 21. What is the version of the running server?** 
  * *Command used:* `nc 10.48.185.53 21`
  * *Banner output:* `FTP server (Version 6.4/OpenBSD/Linux-ftpd-0.17) ready.`
  * *Answer:* `6.4` *(The prompt requested a `_._` format, matching the main FTP server version).*

---

## Final Thoughts on Active Reconnaissance
Active recon requires direct interaction with the target, meaning our activities can be logged by Firewalls, IDS/IPS, or WAFs. 
Tools like Netcat, Telnet, and even basic web browsers are fundamental for discovering active services and mapping out potential 
vulnerabilities before moving into deeper scanning phases.
