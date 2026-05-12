TryHackMe : Hashing Basics (Write-up)

    1. What I Learned About Hashing
    
I learned that Hashing is like a "digital fingerprint." It’s a one-way process that turns any data into a fixed string of characters. 
Unlike encryption, you aren't supposed to "decrypt" it back to the original word. It's mainly used for:

Storing Passwords: So even if a database leaks, hackers can't see the real passwords immediately.

Data Integrity: To check if a file was changed or corrupted during download.

    2. Identifying Hashes
I learned that you can identify a hash by its length or its "prefix" (the symbols at the start):

MD5: 32 characters long (very fast but old and insecure).

Bcrypt: Usually starts with $2a$ or $2y$.

SHA-512: Usually starts with $6$.

Yescrypt: Starts with $y$.

    3. Tools I Used
    
I practiced using professional tools to crack and identify hashes:

Hashcat: A powerful tool that uses specific "Mode Codes" to crack hashes.

-m 0 for MD5

-m 1400 for SHA2-256

-m 1800 for SHA512crypt

-m 3200 for Bcrypt

John the Ripper: Another great tool for cracking passwords using wordlists like rockyou.txt.

CrackStation: An online service that uses huge "Rainbow Tables" to find passwords for hashes instantly.

    4. Key Concepts
    
Salting: Adding random characters to a password before hashing it to stop "Rainbow Table" attacks.

HMAC: A special type of hash that uses a "Secret Key" to prove both who sent the message and that it wasn't changed.

Encoding vs. Encryption: I learned that Base64 is just encoding (it's easy to reverse/decode) and doesn't actually hide data like encryption does.

    5. My Practical Skills
    
I successfully used the Linux terminal to:

Generate SHA256 sums using sha256sum.

Decode Base64 strings using base64 -d.

Run dictionary attacks using hashcat and the rockyou.txt wordlist.
