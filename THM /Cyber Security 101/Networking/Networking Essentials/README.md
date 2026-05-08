TryHackMe - Networking Essentials(writeups)

Introduction

This module explains how devices connect and communicate within a network. It bridges the gap between basic concepts and real-world network operations.

1. DHCP (Dynamic Host Configuration Protocol)
   
Purpose: Automatically assigns network settings to devices.

The Process (DORA):

Discover: The client asks, "Is there a DHCP server?" (Sent to 255.255.255.255).

Offer: The server replies, "I have an IP for you."

Request: The client says, "I'll take that IP!"

Acknowledge: The server confirms, "It's yours now."

Key Fact: The client starts with IP 0.0.0.0 before getting a real address.

3. ARP (Address Resolution Protocol)
   
Purpose: Connects Layer 3 (IP Address) to Layer 2 (MAC Address).

How it works: When a device knows an IP but not the MAC address, it sends a Broadcast (ff:ff:ff:ff:ff:ff) asking, "Who has this IP?"

Hacking Context: Attackers can use ARP Spoofing to trick devices into sending data to them instead of the router.

6. ICMP (Troubleshooting & Diagnostics)
   
Purpose: Error reporting and network testing.

Ping: Uses Echo Request (Type 8) and Echo Reply (Type 0) to check if a system is "alive."

Traceroute: Uses the TTL (Time-to-Live) field in the IP header. By increasing TTL (1, 2, 3...), we force each router to drop the packet and 
reveal its IP address.

9. Routing & Protocols

Purpose: Decides the best path for data packets.

OSPF: Finds the shortest/fastest path like Google Maps.

BGP: The "King of the Internet" that connects different ISPs.

EIGRP: A Cisco-only protocol that considers speed and delay.

RIP: A simple protocol that only counts the number of routers (Hops).

10. NAT (Network Address Translation)
    
Purpose: Saves IPv4 addresses by letting many devices share one Public IP.

The Concept: Your home devices have Private IPs (192.168.x.x). When you go online, the router translates them into a single Public IP.

Tracking: The router uses Port Numbers (up to 65,000) to remember which device asked for which website.

12. Transport Protocols: TCP vs. UDP
    
TCP: Reliable and slow. It uses a 3-way handshake and makes sure every bit of data arrives (Web, Email).

UDP: Fast but unreliable. It doesn't check for errors (Live Streaming, Gaming).

Ports: Common ports include 80 (HTTP), 443 (HTTPS), and 22 (SSH).

Conclusion

I learned that IP addresses are just the "location," while MAC addresses are the "physical ID." 
I also understood how hackers can manipulate these protocols (like ARP Spoofing or Route Poisoning) to intercept data.
Knowing these basics is essential before moving into advanced Cyber Security.
