TryHackMe - Networking Secure Protocols (Write-up)

1. Introduction
   
In this room, I learned how data stays safe while traveling across the internet. In the past, data was sent in Cleartext (plain text),
 meaning anyone could see your passwords using tools like Wireshark. To fix this, we now use Secure Protocols.

2. Key Concepts I Learned
   
  A. SSL vs. TLS
  
SSL (Secure Sockets Layer): The old way of securing data (developed in 1995).

TLS (Transport Layer Security): The modern, upgraded version of SSL. It provides Confidentiality (hides data) and Integrity (ensures data isn't changed).

Logic: When you see an "S" at the end of a protocol (like HTTPS), it means it is running over TLS.

  B. Common Secure Protocols & Ports
  
I learned that secure versions of protocols use different "doors" or Ports:

Web: HTTP (80) - HTTPS (443)

Email: IMAP (143) - IMAPS (993) / SMTP (25) - SMTPS (465/587)

Remote Access: Telnet (23) - SSH (22)

Files: FTP (21) -SFTP (22) or FTPS (990)

  C. VPN (Virtual Private Network)
  
A VPN creates a secure "Tunnel" over the public internet.

It hides my real IP Address and identity from servers.

It allows employees to access office files safely from home.

3. Hands-on Challenge: Finding the Flags
   
Task 1: The FTP/FTPS Logic

I found a flag by matching insecure ports to their secure counterparts.

Logic: I realized that if I want to stay safe, I shouldn't use port 21 (FTP) but rather port 990 (FTPS).
Flag: THM{Protocols_secur3d}

Task 2: Decrypting TLS Traffic in Wireshark

This was the most exciting part! I learned that even if traffic is encrypted, if you have the Key, you can read it.

Steps I took:

Open Capture: I opened randy-chromium.pcapng in Wireshark. Initially, all data was hidden as "Application Data."

Add the Key: I went to Edit -> Preferences -> Protocols -> TLS and added the ssl-key.log file.

The Logic: Once the key was added, Wireshark decrypted the traffic, and "Application Data" turned into readable HTTP2 data.

Identify the Target: I searched for a POST request because that's how websites send login info.
I found Packet 365 (the request) and Packet 366 (the data).

Extract the Flag: I right-clicked Packet 366 and chose Show Packet Bytes. Under the Decrypted TLS tab, I saw the form data.
Flag found in the password field: THM{B8WM6P}

7. Conclusion
   
This room taught me that security isn't just about one tool; it's about using the right protocols (TLS, SSH, VPN) and ports.
Even strong encryption like TLS can be inspected if a researcher (or hacker) manages to get the session keys!
