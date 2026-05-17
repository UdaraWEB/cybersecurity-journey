TryHackMe - Burp Suite Basics (writeup)

I just completed the Burp Suite: The Basics module on TryHackMe, and honestly, it completely changed how I look at web applications. 
If you want to get into Ethical Hacking or Bug Bounty, this tool is an absolute must.

Here is a quick break down of everything I learned in simple terms!

    What exactly is Burp Suite?

Think of Burp Suite as a middleman (a proxy) that sits right between your web browser and the target server. Whenever you click
a button on a website, your browser sends a request. Burp catches that request mid-air, lets you look inside it, modify the data,
and then send it to the server. It gives you total control over web traffic.

    The Different Flavors (Editions)

I learned that Burp comes in three versions:

Community Edition: Fully free, amazing for manual testing, but has some speed limits. This is what I used!

Professional Edition: Used by real pros. It has an automatic vulnerability scanner and runs super fast.

Enterprise Edition: This one stays on a server and constantly scans massive company web apps for bugs 24/7.

    My Favorite Tools Inside the Framework

Navigating the interface was tricky at first, but using shortcuts like Ctrl + Shift + P (Proxy) and Ctrl + Shift + R (Repeater) 
made it super fast. Here are the core tools I explored:

  The Proxy Tab: The backbone of Burp. I used it to intercept and read raw HTTP requests. Turning Intercept is on holds the request 
  so you can play with the inputs before the server sees them.
  
  The Target Tab & Site Map: This automatically builds a beautiful folder tree of every single page, script, and API endpoint you visit. 
  I even used it to solve a challenge by hunting down a weird, hidden endpoint URL and finding a secret flag!

  Repeater: This is a lifesaver. Instead of refreshing your browser a million times, Repeater lets you take a single request, tweak the
  parameters, and resend it over and over to see how the server responds.

  Intruder: This is Burp’s automated attack weapon. It lets you spray a login page with thousands of passwords to perform brute-force
  attacks or test fuzzing endpoints.

  Scope Settings: I learned how to set up a project scope. This tells Burp to only log traffic from my specific target IP (http://10.48.180.171)
  and completely ignore background noise like Google or Windows updates. It keeps your dashboard incredibly clean.

    Troubleshooting pro-tips I picked up:

  The Sandbox Error: When using Burp's built-in browser on Linux/AttackBox as a root user, it sometimes crashes. I fixed this by going to Settings,
  searching for "sandbox", and checking Allow Burp's browser to run without a sandbox.

  CA Certificate: To intercept secure HTTPS websites without getting security warnings, you have to download Burp's certificate from http://burp/cert
  and import it into your browser's trusted authorities.
