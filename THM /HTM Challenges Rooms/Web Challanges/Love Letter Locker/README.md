Write-up: LoveLetterLocker (TryHackMe)

Introduction

In this room, I played the role of a security researcher testing a private "Love Letter" storage service. The goal was to see if I could read letters belonging to other users.

The Process (Step-by-Step)

1.Exploration: I started by creating a new account and logging into the system.

2.The Clue: On the "My Letters" page, there was a tip stating that every letter gets a unique number in the archive.

3.Testing the Logic: I created my own letter, and it was assigned the ID 3. The URL looked like this: http://10.48.158.

4.The Attack (IDOR): I wondered if I could see letters 1 and 2 by changing the number in the URL. I changed the 3 to 1 in the address bar.

5.Finding the Flag: By navigating to http://10.48.158, I was able to access a private letter that didn't belong to me! Inside 
that letter, I found the flag.

6.The Flag: THM{1_c4n_r3ad_4ll_l3tters_w1th_th1s_1d0r}

What I Learned (Lessons)

 What is IDOR?: I learned about IDOR (Insecure Direct Object Reference). This happens when a website uses a simple ID (like a number)
to access data and doesn't check if the user actually has permission to see it.

 Logical Thinking: I learned that hacking isn't always about using complex tools; sometimes it's 
just about understanding how the website's logic works and testing its limits.

 URL Manipulation: I practiced how to manually edit URL parameters to discover hidden or unauthorized content.

Where I Improved

 Connecting the Dots: At first, I looked at letter ID 2 and didn't find the flag. Instead of giving up, I tried ID 1,
which taught me to check all possible values when I find a vulnerability.

 Faster Navigation: I am becoming more comfortable navigating through web applications and understanding common patterns
like "Login" and "Dashboard" areas.

Conclusion
This was a great lesson in data privacy. It showed me how a small mistake in the code (forgetting to check user permissions) 
can lead to a huge data breach where anyone can read everyone's private messages.
