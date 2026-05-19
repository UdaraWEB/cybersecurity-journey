TryHackMe - Gobuster Basics (writeup)

I just wrapped up the basics of Gobuster on TryHackMe! If you are getting into web penetration testing or bug hunting,
this command-line tool is a total game-changer for the reconnaissance phase. It is incredibly fast because it is written in Go.

Here is a super simple breakdown of what I learned and how it works in the real world.

    What is Gobuster?

In plain terms, Gobuster is an automated guessing machine. When developers build a website, they often leave hidden folders,
backup files, or subdomains sitting on the server. You can't see them just by clicking around the homepage. Gobuster takes a text file full
of thousands of common names (a wordlist) and smashes them against the target URL to see what sticks.

I mastered the three main modes it offers:

    1. Directory Mode (dir)
    
This mode hunts for hidden folders and files inside a website.

The Command I Used: gobuster dir -u "http://offensivetools.thm" -w /usr/share/wordlists/dirb/common.txt

How it went: Gobuster automatically appended words from my list to the URL. It uncovered a hidden directory named /secret/.

The Win: I used the curl command to inspect a JavaScript file inside that hidden folder (curl http://offensivetools.thm) and snatched
the secret flag: THM{ReconWasAsuccess}!

    2. DNS Mode (dns)
    
This mode is all about finding subdomains (like ://example.com or ://example.com). Companies often secure their main website but
forget to patch their older test subdomains.

How it worked: Gobuster performed fast DNS lookups using a subdomain wordlist.

The Win: I successfully mapped out the target and discovered 4 active subdomains that were up and running.

    3. Virtual Host Mode (vhost)
    
Sometimes, a single server IP hosts multiple different websites under the hood (Virtual Hosts). This mode manipulates the HTTP Host:
 headers in web requests to see if the server serves a different page.
 
Pro-Tip I Learned: Real-world scans get messy with false positives (annoying 404 pages). I learned how to use the
--exclude-length 0-500 flag to hide those useless 404 responses and keep my terminal completely clean.

The Win: Filtered out the noise and found 3 true positive vhosts responding with a clean Status 200 OK.

    Troubleshooting Lessons
    
Since I was running this on my own Kali Linux machine instead of the TryHackMe AttackBox, the custom domain wasn't loading at first. 
I learned a crucial real-world networking skill: fixing the connection error by manually mapping the target IP address to the hostname
directly inside my /etc/hosts file. Once that was done, everything ran smoothly!

Final Thoughts

Gobuster showed me how easy it is to find exposed areas on a server if the admin doesn't configure things properly. Moving forward, I’m 
installing SecLists to get access to much bigger, real-world wordlists.
