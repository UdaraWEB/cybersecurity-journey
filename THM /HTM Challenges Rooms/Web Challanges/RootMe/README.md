TryHackMe - RootMe Room (writeup)

Today, I completed the "RootMe" room on TryHackMe. Unlike my previous room which was a Windows exploit, 
this lab was an amazing hands-on experience focused on hacking a Linux Web Server.


Here is a simple breakdown of the attack steps and the valuable lessons I learned along the way.

    1. Reconnaissance (Information Gathering)
    
I started by running a quick network scan with Nmap to see what services were active. I found two open ports: 22 (SSH) 
and 80 (HTTP Web Server). Since port 80 was running a web server, I used a directory bruteforcing tool called Gobuster 
to scan for hidden web directories. This led me to discover two hidden pages: /panel/ and /uploads/.

    2. File Upload Bypass & Gaining Access
    
The /panel/ directory had a file upload form. I decided to try uploading a standard PHP reverse shell script. However,
the server's security configurations blocked the .php extension. To bypass this defense, I renamed the file extension to 
.phtml. This simple trick fooled the server, and the file uploaded successfully!

Next, I set up a Netcat listener (nc -lvnp 1234) on my AttackBox, went to the /uploads/ directory on my browser, and
clicked on my uploaded script. Boom! The reverse shell executed, and I instantly got entry-level terminal access to the 
server as the www-data user. I then located and read the first flag inside user.txt.

    3. Privilege Escalation (Becoming Root )
    
As a basic web user, my terminal permissions were highly restricted. To become the administrator (root), I searched for
files with misconfigured SUID permissions using a specific find command. I discovered that Python 2.7 was allowed to run
with root execution rights—which is a major security flaw in the real world.

I leveraged this vulnerability by spawning a privileged shell directly through Python. Although the terminal prompt went 
completely blank (a typical dumb shell behavior), I typed the whoami command and confirmed I was now root. From there,
I easily read the final flag inside /root/root.txt to finish the room.

     Key Lessons I Learned from RootMe

How Web Hacking Works: I learned how attackers combine web directory discovery (Gobuster) with misconfigured application 
features (like unregulated file upload forms) to sneak malicious code inside a server.

Bypassing Input Restrictions: This lab proved that weak file filtering (just blocking .php but forgetting extensions like 
.phtml) cannot stop an attacker. Input validation must always be airtight.

Handling Dumb Linux Shells: I learned that when a terminal goes silent or frozen after upgrading privileges, it doesn't
mean it failed. It taught me to trust my commands (like typing blind) and troubleshoot patiently.

The Danger of SUID Misconfigurations: I realized how critical it is for system administrators to secure system binaries.
Leaving powerful utilities like Python with SUID rights gives any low-privilege attacker a free pass to take over the entire 
server.
