    TryHackMe: Passive Reconnaissance (writeup)

Hello everyone! This is my personal write-up and learning notes for the **Network Reconnaissance** room under the Junior Penetration Tester pathway on TryHackMe. 

Reconnaissance is always the very first phase of any ethical hacking or penetration testing engagement. Below is a breakdown of what I learned from each task, along with the solutions.

---

## Task 1: Passive vs. Active Reconnaissance

In this task, I learned the core difference between the two main types of intelligence gathering.

* **Passive Reconnaissance:** Relying only on publicly available information. No direct packets are sent to the target (like watching a house from a distance using binoculars).
* **Active Reconnaissance:** Direct engagement with the target network or personnel. Packets are logged, and there is a risk of being detected.

### Answers:
1. **Visiting a company's Facebook page to find employee names:** `P` (Passive, because we only check public social media).
2. **Pinging the IP address of the company web server:** `A` (Active, because we are actively sending ICMP traffic to their server).
3. **Meeting an IT admin at a party and using social engineering:** `A` (Active, because interacting directly with a person affiliated with the target is always active).

---

## Task 2: WHOIS & RDAP

This task covers how to query registration data for domain names using the traditional WHOIS protocol (TCP port 43) and its modern successor, **RDAP** (Registration Data Access Protocol). RDAP is secure (uses HTTPS) and provides output in structured JSON.

Using the AttackBox terminal, I queried `tryhackme.com` to find key administrative details.

### Answers:
1. **When was TryHackMe.com registered?** `2018-07-05`
2. **What is the registrar of TryHackMe.com?** `NAMECHEAP INC`
3. **Which company is TryHackMe.com using for name servers?** `CLOUDFLARE.COM`

---

## Task 3: DNS Lookup (nslookup & dig)

Here, I explored how to query DNS records using two tools: `nslookup` (older tool) and `dig` (the modern, preferred tool). These lookups are passive because queries are sent to public resolvers (like `1.1.1.1`), not directly to the target.

### Answers:
* **Check the TXT records of thmlabs.com. What is the flag there?** 
  * *Command used:* `dig thmlabs.com TXT`
  * *Flag discovered:* `THM{thms_dns_exploration_revealed}` *(Note: Check your own AttackBox output as flags can sometimes vary)*

---

## Task 4: Subdomain Enumeration

Standard DNS lookups only work if you already know the subdomain name. This task teaches how to find hidden or unadvertised subdomains (like `admin.` or `dev.`) using public OSINT platforms without alerting the target.

* **DNSDumpster:** An excellent tool that gathers open DNS data and creates a visual map of the infrastructure.
* **Certificate Transparency (CT) Logs:** Using platforms like `crt.sh`, we can see every SSL/TLS certificate ever issued for a domain.

### Answers:
* **Lookup tryhackme.com on DNSDumpster. What is one interesting subdomain discovered?** `remote`

---

## Task 5: Shodan.io

Shodan is essentially a search engine for internet-connected devices (servers, routers, IoT, cameras) rather than web pages. It continuously scans the web and grabs "banners" from open ports. It allows testers to see exposed services passively.

### Answers:
1. **First country in the world in terms of publicly accessible Apache servers:** `United States`
2. **3rd most common port used for Apache:** `8080`
3. **Most common port used for nginx:** `80` *(Depending on your room version, if it asks for the 3rd most common port, the answer is `5001` or `8888`)*

---

## Key Takeaways
* Always start with **Passive Recon** to avoid triggering firewall alerts (IDS/IPS).
* CT Logs (`crt.sh`) and Shodan are incredibly powerful for mapping an organization's external attack surface without ever sending a single packet to their network.


