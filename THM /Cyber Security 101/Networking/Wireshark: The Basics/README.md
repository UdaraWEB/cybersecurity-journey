Write-up: TryHackMe - Wireshark: The Basics

    1. Introduction
   
In this room, I learned how to use Wireshark, which is the world's most popular tool for looking at network traffic. 
It’s like an "X-ray machine" for the internet. It doesn't change data; it just reads it so we can find problems or security threats.

    3. Key Things I Learned.
   
A. The Interface (GUI)

I learned that Wireshark splits packet information into three main parts:

Packet List: The big list of all messages moving in the network.

Packet Details: Shows the "OSI Layers" of a single packet.

Packet Bytes: Shows the raw data in Hex and text.

B. OSI Layers in Action

I learned how to "dissect" a packet. By clicking a packet, I could see:

Layer 1 (Frame): Arrival time and packet size.

Layer 3 (IP): Source and Destination IP addresses and the TTL (Time to Live).

Layer 4 (TCP/UDP): Port numbers and the Payload (actual data).

C. Display Filters

This is a superpower! Instead of looking at 5,000 packets, I can use filters like:

http (to see only web traffic)

ip.addr == x.x.x.x (to see traffic from a specific computer)

Follow Stream: This turns messy packets into a readable "chat log" between a server and a user.

    4. How I Solved the Challenges
    
Task: File Properties

Logic: I used the Statistics -> Capture File Properties menu.

What I found: I found the SHA256 hash of the file, the total packet count (5862), and a hidden
Flag in the "Capture Comments" section: TryHackMe_Wireshark_Demo.

Task: Finding Hidden Info

Searching: I used Ctrl + F to search for a string like "r4w" in the packet details. This led me to find an artist named "randy."

Packet Comments: I went to Packet 12, read the comment, and followed a "trail" to Packet 39765.
I exported the image bytes and used the md5sum command in the terminal to get the file's hash.

Task: Exporting Objects

Logic: I learned that hackers or users often send files over the network.

Action: I went to File -> Export Objects -> HTTP. I found a file named note.txt. Inside, I found the name of an alien: P3T3R.

Task: Following the Stream

Step: I went to Packet 33790, right-clicked, and chose Follow -> HTTP Stream.

Finding: By scrolling down through the code, I found a list of artists.

Results: Total artists = 3, and the second artist was blake.

    5. Conclusion
   
This room taught me how to navigate through massive amounts of network data. I now know how to filter for specific protocols,
look into the "guts" of a packet using OSI layers, and even extract hidden files from a capture.
