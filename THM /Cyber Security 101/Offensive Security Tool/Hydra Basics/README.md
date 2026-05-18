    Cracked My First Passwords with Hydra (writeup)

I just completed the Hydra lab on TryHackMe! I learned how attackers use brute-force attacks to guess passwords in seconds.

Here is what I did in simple terms:

The Mission


The target machine had a user named molly. I had to find her hidden passwords for two different services using the famous RockYou.txt wordlist.

    1. Web Login Form (Flag 1)
    
What I did: I used Hydra to automatically inject thousands of passwords into the website's login page using a POST request.

Result: Hydra caught the right password, and logging in gave me Flag 1 THM{2673a7dd116de68e85c48ec0b1f2612e}.

    2. SSH Server (Flag 2)
    
What I did: I switched to the terminal and attacked the SSH login using 4 parallel threads (-t 4) to speed things up.

Result: Hydra cracked the SSH password. I logged into her server via terminal and grabbed Flag 2 THM{c8eeb0468febbadea859baeb33b2541b}

    Key Takeaways

Weak Passwords = Easy Target: Simple passwords can be cracked in minutes using automatic tools.

Rate Limiting is Key: Secure websites must block users after 3-5 failed login attempts to stop tools like Hydra.
