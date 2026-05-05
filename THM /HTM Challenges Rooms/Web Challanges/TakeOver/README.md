TryHackMm Web Challange - TakeOver ( Write-up )

The Goal

The objective was to find a hidden flag on the futurevera.thm website by exploring its subdomains.

Step 1: Preparation

I started by adding the target IP to my /etc/hosts file so that my Kali machine could recognize the domain.

Target IP: 10.48.176.48

Action: Added futurevera.thm and its subdomains to the hosts file.

Step 2: Hunting for Subdomains

Using ffuf, I scanned for hidden subdomains. I found a few, but the most interesting one was support.futurevera.thm.

Step 3: Finding the Secret Link

I visited the support site, but there was nothing on the page. I decided to check the SSL Certificate of the site. 
In the certificate details (Subject Alternative Name), I found a very long, hidden subdomain:

secrethelpdesk934752.support.futurevera.thm

Step 4: Getting the Flag (Terminal Magic)

I added this new secret subdomain to my hosts file. However, when I tried to open it in my web browser,
it didn't work properly and wouldn't show the flag due to some browser-related issues.

To bypass this, I used the Terminal and ran a curl command to see what was happening behind the scenes:

Command: curl -I http://secrethelpdesk934752.support.futurevera.thm

The server responded with a "302 Found" redirect. In the Location header of that response,
I finally found the flag attached to the end of the URL!

Flag: flag{beea0d6edfcee06a59b83fb50ae81b2f}

Key Takeaways

SSL Leakage: Always check SSL certificates; they often leak internal subdomains.

CLI over GUI: When the browser fails to load a page correctly, curl is a powerful way to see the real response from the server.

HTTP vs HTTPS: Sometimes, certain flags or redirects only work over plain HTTP.
