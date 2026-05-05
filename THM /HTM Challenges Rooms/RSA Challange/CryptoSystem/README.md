TryHackMe - CryptoSystem (Writeup)

Challenge Overview:

The goal was to decrypt an RSA-encrypted message (the flag). I was given a Python script that generated the keys and the ciphertext.

Identifying the Weakness:

In the source code, I noticed a specific line: q = primo(p). This function picks 

q as the very next prime number after p.In RSA security, p and q must be chosen randomly and kept far apart. When they are too close,

the modulus (n) becomes vulnerable to Fermat's Factorization Method.
 
The Attack:

Since p and q are almost equal (⁵, ₅) is very close to both of them. I used a Python script to calculate the integer square root of n
and then found the factors p and q in seconds.

Decryption Steps:

Factorization: Calculated p and q from n.

Calculate Phi: Computed x=(p-1)*(q-1)

Private Key: Calculated the private exponent d using the modular inverse of e modulo x.

Decrypt: Used the formula m = cᵈ(mod n) to get the original message

Final Flag:
THM{Just_s0m3_small_amount_of_RSA!}

Conclusion:

This challenge shows that RSA isn't secure just because the numbers are large; the way primes are chosen matters. If 
p and qare close, even a standard laptop can crack a 2048-bit key instantly.



