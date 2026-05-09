 TryHackMe - Tcpdump: The Basics(Write-up)

    1. Introduction
   
In this room, I learned how to use Tcpdump, which is a powerful command-line tool for network analysis. 
Unlike Wireshark, it works entirely in the terminal, making it very fast and efficient for inspecting network traffic on servers. 
It is built on the libpcap library.

    3. Key Commands & Flags I Learned
   
I learned that Tcpdump uses various "flags" to control its behavior:

-i: Used to specify the network interface to listen on.

-n: Used to display IP addresses in numeric format (skipping DNS lookups for speed).

-r: Used to read and analyze a saved .pcap file.

-w: Used to write captured traffic into a file.

-c: Used to limit the capture to a specific number of packets.

-e: Used to display link-level information, including MAC addresses.

-v / -vv: Used to increase the "verbosity" (level of detail) of the output.

    4. How I Approached the Challenges
    
Task: Filtering by Protocol & Port

Counting Packets: To count packets for a specific protocol (like ICMP), I learned to filter by the protocol name and
then pipe the output to the wc -l command to count the total lines.

DNS Inspection: I used port 53 to filter for DNS traffic. By limiting the count to the first packet (-c 1), I was 
able to identify the specific hostname being requested.

Task: Finding Hardware (MAC) Addresses

Logic: Since MAC addresses are not shown by default, I learned that the -e flag is essential.

Action: I filtered for ARP packets (which are used to find MAC addresses) and looked at the source address field to identify the host.

Task: Advanced Filtering (TCP Flags & Sizes)

TCP Flags: I learned how to use advanced expressions to look for specific TCP flags, such as the Reset (RST) flag.
This is done by checking the tcpflags field within the TCP header.

Filtering by Size: To find specific traffic based on packet length, I used the greater keyword. This allowed me to filter
out all small packets and focus only on those exceeding a certain byte size to find the source IP address.

    5. Conclusion
   
Tcpdump is an essential tool for any security professional. I now understand how to read capture files, apply filters based on hosts,
ports, and protocols, and even look into packet headers for specific flags. This room taught me that the command line can be just as
powerful as a graphical tool like Wireshark for network investigation.
