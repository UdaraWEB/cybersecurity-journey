TryHackMe - Public Key Cryptography (write-up)

Today, I explored the basics of Public Key Cryptography (Asymmetric Encryption). It sounds complex, but it’s
actually based on simple logic we use in real life. Here is the breakdown of what I’ve learned:

    1. The Core Idea (The Coffee Shop Analogy)
    
Think about meeting a friend at a cafe. You can see them (Authentication), you know the voice is theirs (Authenticity), 
no one can change what they say mid-air (Integrity), and by whispering, you keep it private (Confidentiality). In the digital world,
we use math to achieve these same four things.

    2. How Keys Work (The Box & Lock)
    
The biggest challenge in security is sharing a secret password without a hacker stealing it.

Public Key (The Lock): I give everyone an open padlock. Anyone can use it to lock a box and send it to me.

Private Key (The Key): Only I have the physical key to open those locks.

Even if a hacker steals the locked box while it's being delivered, they can't open it because they don't have my private key.

    3. The Math (RSA & Diffie-Hellman)
    
RSA: This is based on the fact that multiplying two huge prime numbers is easy, but finding those original numbers
from the result is nearly impossible for a computer. This "math wall" is what keeps our data safe.

Diffie-Hellman: This is a cool trick where two people can create a "shared secret" key over the internet
without ever actually sending the key itself. They exchange some public numbers, mix them with their own 
private numbers, and magically end up with the same result on both ends.

    4. Real-World Tools: SSH & GPG
    
SSH: This is how we log into servers. Instead of typing a password every time, we use "SSH Keys." It’s much safer because
your private key never leaves your own computer.

GPG (Pretty Good Privacy): I used this to encrypt and decrypt files. By importing a private key into my terminal and 
running a simple gpg --decrypt command, I was able to reveal hidden messages (like the secret word "Pineapple"!).

    5. Certificates & Trust
    
Lastly, I learned about HTTPS. When you see the padlock icon in your browser, it means the website showed
a "Certificate" to prove it’s real. Organizations like Let's Encrypt give these out for free so that the whole internet
can stay encrypted.
