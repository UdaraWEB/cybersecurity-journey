TryHackMe - Networking Core Protocols (Write-up) 

Today, I completed the Networking Core Protocols module on TryHackMe. It was an amazing hands-on experience 
learning how the internet works behind the scenes. Here’s a summary of what I learned and how I captured the flags.

1. DNS (Domain Name System)
   
DNS is like the phonebook of the internet. It maps human-friendly names (like google.com) to IP addresses.

Key Learning: I learned about different record types like A (IPv4), AAAA (IPv6), MX (Mail servers), and CNAME (Aliases).
Flag: Identified that AAAA is the record for IPv6.

3. WHOIS
   
WHOIS is a protocol used to find out who owns a domain, when it was created, and when it expires.

Key Learning: I used the whois command to look up domain registration details.

Flag: Found the creation dates for domains like x.com and twitter.com by analyzing the WHOIS records.

5. HTTP & HTTPS
   
These are the protocols we use to browse the web. HTTP (Port 80) is plain text, while HTTPS (Port 443) is secure.

Key Learning: I learned about methods like GET (to retrieve data) and POST (to send data).

Flag Hunt: I used telnet to manually talk to a web server. By sending a manual request (GET /flag.html HTTP/1.1),
I captured the hidden flag: THM{TELNET-HTTP}.

7. FTP (File Transfer Protocol)
   
FTP (Port 21) is used for efficient file transfers.

Key Learning: I learned how to log in as an anonymous user and use commands like ls to list files and get to download them.

Flag Hunt: I connected to the FTP server, located flag.txt, and downloaded it to get the flag.

9. Email Protocols (SMTP, POP3, IMAP)
    
I explored the three main protocols that handle our emails:

SMTP (Port 25): Used for sending emails. I learned commands like MAIL FROM, RCPT TO, and DATA.

POP3 (Port 110): Used for downloading emails to a single device.

Flag Hunt: I logged in as 'linda' via telnet using the password Pa$$123. By using the RETR 4 command, 
I read the 4th email and found the flag: THM{TELNET_RETR_EMAIL}.

IMAP (Port 143): Used for syncing emails across multiple devices. I learned that FETCH is the command used to retrieve messages here.

Conclusion

This room was a great reminder that even though we use fancy browsers and apps today, everything still relies on these core text-based protocols.
Using telnet to manually interact with these services was a real eye-opener!
