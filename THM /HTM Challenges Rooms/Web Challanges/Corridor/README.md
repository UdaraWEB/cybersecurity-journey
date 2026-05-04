TRYHACKME - Corridor (Writeup)

In this challenge, the goal was to find the flag by exploring the website.

First, I opened the target machine in the browser and noticed that the URL contained long hexadecimal strings (hash-like values). The hint mentioned IDOR, so I understood that these values might be predictable.

Then I used the Linux terminal to generate an MD5 hash of the number 0:

echo -n 0 | md5sum

After that, I copied the hash and placed it at the end of the URL. When I searched it in the browser, the page loaded and the flag was visible.

---

What I learned

- IDOR vulnerabilities happen when applications use predictable IDs
- Even hashed values (like MD5) can be guessed if the input is simple
- Using the terminal to generate hashes is useful during testing

---

Conclusion

This challenge showed that hiding IDs with hashes is not secure. If the input is predictable, attackers can still access hidden resources and find sensitive data like flags.
