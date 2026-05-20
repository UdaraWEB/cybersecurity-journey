TryHackMe - Firewall Fundamentals Room (Writeup)

I will share the solutions and a quick summary for the Firewall Fundamentals room on TryHackMe. This room is great for beginners 
to understand how firewalls protect networks.

    Task 1: Introduction to Firewalls
    
This task explains what a firewall is using a simple example. Just like a security guard stands outside a bank to check visitors, 
a firewall checks the data packets (traffic) entering and leaving our digital devices.

Question: Which security solution inspects the incoming and outgoing traffic of a device or a network?

Answer: Firewall

    Task 2: Types of Firewalls
    
Here, we learn about the 4 main types of firewalls and which OSI layer they work on:

Stateless: Very fast but does not remember past connections (Layer 3 & 4).

Stateful: Tracks connections using a state table (Layer 3 & 4).

Proxy: Looks deep inside the application data (Layer 7).

Next-Generation (NGFW): The most advanced one. Has IPS and decrypts SSL traffic (Layer 3 to 7).

Question: Which type of firewall maintains the state of connections?

Answer: Stateful Firewall

Question: Which type of firewall offers heuristic analysis for the traffic?

Answer: Next-Generation Firewall

Question: Which type of firewall inspects the traffic coming to an application?

Answer: Proxy Firewall

    Task 3: Firewall Rules
    
Rules tell the firewall what to do with the network traffic. Every rule has a source, destination, port, and an action (Allow, Deny, or Forward).

Question: Which type of action should be defined in a rule to permit any traffic?

Answer: Allow

Question: What is the direction of the rule that is created for the traffic leaving our network?

Answer: Outbound

    Task 4: Windows Defender Firewall (Hands-on)
    
In this lab, we look at the advanced settings of the Windows built-in firewall. The security team has already set up some custom rules. 
We just need to check the Inbound Rules list.

Question: What is the name of the rule that was created to block all incoming traffic on the SSH port?

Answer: Core Op (Note: In older THM room versions, this was "Block SSH")

Question: A rule was created to allow SSH from one single IP address. What is the rule name?

Answer: Infra team (Note: In older versions, this was "Allow SSH")

Question: Which IP address is allowed under this rule?

Answer: 192.168.13.7 (You can find this by double-clicking the "Infra team" rule and checking the Scope tab)

    Task 5: Linux Built-in Firewall (UFW)
    
This task shows how Linux manages its firewall using tools based on the Netfilter framework. We learn how to use UFW (Uncomplicated Firewall)
via simple terminal commands.

Question: Which Linux firewall utility is considered to be the successor of "iptables"?

Answer: nftables

Question: What rule would you issue with ufw to deny all outgoing traffic from your machine as a default policy? (answer without sudo)

Answer: ufw default deny outgoing
