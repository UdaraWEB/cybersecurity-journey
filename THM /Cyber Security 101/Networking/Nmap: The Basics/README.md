Write-up: TryHackMe - Nmap: The Basics

    1. Introduction
   
In this room, I learned how to use Nmap (Network Mapper), the most famous tool for scanning networks. 
While Wireshark and Tcpdump help us "listen" to traffic, Nmap helps us "find" targets, open ports, and services running on a network.

    3. Key Concepts I Learned
   
A. Host Discovery

Before scanning for ports, we need to know who is online.

Logic: I learned that Nmap can scan ranges (e.g., 192.168.0.1-10) or subnets (e.g., /24).

The Ping Scan (-sn): This is used to find live hosts without checking ports. On a local network, it uses ARP; on
a remote network, it uses ICMP and TCP packets.

B. Port Scanning Techniques

I learned the difference between how Nmap talks to a target:

Connect Scan (-sT): Completes the full "Three-way Handshake." This is the default for local users without sudo access.

SYN Scan (-sS): Also called a Stealth Scan. It only does the first step of the handshake. It’s faster and harder to log.

UDP Scan (-sU): Used for services like DNS or DHCP that don't use TCP.

C. Detection & Stealth

Service Version (-sV): This tells me exactly what software is running on a port (e.g., Golang 1.16).

OS Detection (-O): Tries to guess if the target is Linux or Windows.

Timing Templates (-T0 to -T5): I learned how to control speed. -T0 is very slow (Paranoid), while -T4 is Aggressive and great for labs.

    4. How I Solved the Challenges
   
Task: Subnet Math

Question: What is the last IP in a /27 subnet starting at 192.168.0.1?

Logic: A /27 mask means a block of 32 IPs. Starting from .0, the block goes from .0 to .31.

Result: 192.168.0.31

Task: Practical Port Scanning

Action: I ran nmap -sS 10.49.140.79 on the target.

Finding: I saw 6 ports marked as "open" (including 7, 9, 13, 17, 22, and 8008).

Web Server Flag: I noticed port 8008 was running HTTP. I opened the browser in the AttackBox and went to http://10.49.140.79:8008.

Flag: I found the flag THM{web_server_2h3n} on the page.


Task: Version Detection

Action: I ran nmap -sV -p 8008 10.49.140.79.

Result: Nmap identified the web server as Golang 1.16.15.

Task: Timing & Flags

Logic: I learned that -T4 is the same as saying aggressive.

Debug Mode: I found that the -d flag is used to see technical debugging info.

Privileges: I learned that if I run Nmap without sudo, it defaults to a connect scan because it doesn't have permission to build raw SYN packets.

    5. Summary & Conclusion
   
Nmap is like a Swiss Army knife for hackers and admins. I now know how to find live hosts, identify what
software they are running, and control how fast the scan goes to avoid being caught. The most important takeaway: always use sudo to
get the full power of Nmap!
