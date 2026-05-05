TryHackM Web Challange - Hidden Deep into my Heart (Write-up)

Introduction

In this challenge, I had to find a hidden flag on a web application. It was a fun experience where I learned how to look for hidden information that developers sometimes leave behind.

The Process (Step-by-Step)

1.Accessing the Site: First, I opened the target IP address http://<TARGET_IP>:5000 in my browser.
I saw a simple Valentine-themed web page.

2.Checking for Hidden Files: I checked the robots.txt file by going to http://<TARGET_IP>:5000/robots.txt. 
This is a common place where website owners tell search engines which pages to hide.

3.Finding the Flag: Inside the robots.txt file, I found a comment: # cupid_arrow_2026!!!. At first, it looked like a password, 
but after looking closer, I realized the flag was right there!

4.The Flag: THM{l0v3_is_in_th3_r0b0ts_txt}

What I Learned (Lessons)

Information Leakage: I learned that developers often leave sensitive information (like passwords or secrets) in comments or
configuration files like robots.txt.

Don't Overcomplicate: I realized that sometimes the answer is simpler than we think. 
I was looking for a login page, but the flag was already visible in the text file.

Directory Knowledge: I learned how to navigate through different directories in a URL to find hidden paths.

Where I Made Mistakes

Wrong Paths: I spent some time trying to find an /administrator page inside the vault, which gave me "404 Not Found" errors. 
This happened because I assumed there was a login step.

URL Errors: A few times, I forgot to include the port :5000 or used https instead of http, which caused connection errors. 
This taught me to be very careful with the syntax of a URL.

Conclusion

This challenge taught me the importance of basic reconnaissance. Always check the simple things first, like robots.txt and page source code,
before trying advanced hacking tools!
