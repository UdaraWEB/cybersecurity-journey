    TryHackMe - OWASP Top 10 writeup

Hi everyone! I recently completed the OWASP Top 10 modules on TryHackMe. It was an amazing hands-on experience covering modern web application vulnerabilities and insecure data handling flaws. 

Here is my personal, straight-to-the-point walkthrough of all the challenges I solved and what I learned from them.

---

## 1. Security Misconfiguration
* **The Vulnerability:** The developers left active debugging traces, verbose error logs, and testing endpoints open inside the backend User Management API.
* **How I Solved It:** I explored the application endpoints and noticed how the user paths worked. By performing ID enumeration and manually querying the admin endpoint (`/api/user/admin`), the misconfigured server leaked a full backend error trace containing the hidden flag.
* **Flag Captured:** `THM{V3RB0S3_3RR0R_L34K}`

---

## 2. Software Supply Chain Failures
* **The Vulnerability:** The web application relied on an outdated third-party Python utility component (`lib/vulnerable_utils.py`) which contained a hidden, insecure debug mode.
* **How I Solved It:** I bypassed the front-end interface and used my terminal to send a direct cURL POST request with a custom JSON payload `{"data":"debug"}` to the processing endpoint (`/api/process`). The outdated backend script executed it and dumped the flag.
* **Flag Captured:** `THM{SUPPLY_CH41N_VULN3R4B1L1TY}`

---

## 3. Cryptographic Failures (Hard-coded Keys)
* **The Vulnerability:** The application tried to secure files using encryption, but the developers made a critical mistake by hard-coding the actual AES secret decryption key directly inside the public client-side JavaScript code.
* **How I Solved It:** I opened the Browser Developer Tools (F12), inspected the `decrypt.js` file, and found `const SECRET_KEY = "my-secret-key-16"`. I then took the encrypted document string and decoded it using CyberChef with the AES-ECB mode to reveal the plaintext flag.
* **Flag Captured:** `THM{CRYPTO_FAILURE_H4RDCOD3D_K3Y}`

---

## 4. Insecure Design
* **The Vulnerability:** The developers built a chat application assuming only mobile devices could ever access it. They put access restrictions on the web front-end but completely forgot to secure or authenticate the underlying backend API.
* **How I Solved It:** Front-end restrictions are easily bypassed. I interacted with the backend service directly using my terminal and sent a cURL request to the admin chat log path (`/api/messages/admin`), which instantly leaked the flag.
* **Flag Captured:** `THM{1NS3CUR3_D35IGN_4SSUMPT10N}`

---

## 5. Cryptographic Failures (Weak Shared Keys)
* **The Vulnerability:** A note-sharing service used a highly predictable, weak repeating XOR derivative key (`KEY1`) to protect private user notes instead of utilizing secure, standard encryption libraries.
* **How I Solved It:** Due to the weak nature of the key derivation, the cryptographic layer was easily cracked. By submitting the missing key parameter (`KEY1`) to the decryption engine on the web app, all notes were unlocked, exposing the flag inside a decrypted note.
* **Flag Captured:** `THM{WEAK_CRYPTO_FLAG}`

---

## 6. Injection (SSTI)
* **The Vulnerability:** A Server-Side Template Injection (SSTI) flaw existed because the application accepted user text inputs and rendered them directly using the Python Jinja2 template engine without sanitization.
* **How I Solved It:** I injected a malicious Python payload containing double underscores into the input box to access Python built-ins. The payload forced the server to read the local directory and output the flag file directly on screen.
* **Flag Captured:** `THM{SSTI_FLAG_OBTAINED}`

---

## 7. Software and Data Integrity Failures (Insecure Deserialization)
* **The Vulnerability:** The application accepted user-supplied serialization data and passed it straight into Python's `pickle.loads()` function without verifying its integrity or authenticity.
* **How I Solved It:** I generated a custom Python object embedded with a malicious `__reduce__` method designed to execute system commands and read `flag.txt`. I serialized it, encoded it into a Base64 string, and submitted it to the application to trigger Remote Code Execution (RCE).
* **Flag Captured:** `THM{INSECURE_DESERIALIZATION}`

---

##  Key Lessons I Learned
1. **Never Trust Client-Side:** Front-end restrictions and hidden JavaScript files are fully visible to anyone. Never put secret keys or security controls there.
2. **Backend Authentication is Mandatory:** Every API endpoint must enforce proper authentication and authorization, regardless of the device type or context.
3. **Validate and Sanitize All Inputs:** Treat all user input as highly dangerous. Use parameterized queries and secure template rendering to prevent injection attacks.
4. **Secure Deserialization & Supply Chains:** Never deserialize untrusted objects using weak tools like `pickle` without integrity checks, and always keep third-party packages updated.


