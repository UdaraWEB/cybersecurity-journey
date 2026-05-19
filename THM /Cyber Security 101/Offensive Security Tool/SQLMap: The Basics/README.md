TryHackMe - SQLMap: The Basics (writeup)

I just wrapped up the SQLMap: The Basics lab on TryHackMe! SQL Injection (SQLi) is one of the most critical web vulnerabilities out there,
and learning how to safely automate its exploitation was mind-blowing.

Here is a short and simple breakdown of my practical walkthrough:

    The Mission

The target was a vulnerable login page located at a local IP address. Since the web input didn't sanitize data properly, my goal was to inject
SQL commands, bypass authentication, and dump the backend database records.

Step-by-Step Breakthrough

    1. Hunting for Databases
    
First, I needed to see what databases were running under the hood. I passed the vulnerable URL format into SQLMap and used deep
scanning flags to extract the names:

sqlmap -u 'http://<TARGET_IP>/ai/includes/user_login?email=test&password=test' --level=5 --dbs

Result: SQLMap bypassed the login logic and exposed 6 available databases including the main one named ai.

    2. Mapping the Tables
    
Once I knew the database name, I focused directly on it to map out its tables (file cabinets):

sqlmap -u 'http://<TARGET_IP>...' --level=5 -D ai --tables

Result: It successfully mapped the structural layout and discovered a table named users.

    3. Dumping the Secret Credentials
    
Finally, it was time to extract the actual data stored inside that users table:

sqlmap -u 'http://<TARGET_IP>...' --level=5 -D ai -T users --dump

Result: SQLMap dumped a beautiful credential chart on my terminal screen. Right there, I found the target email test@chatai.com and
its cracked plaintext password!

Key Lesson

Automated tools like SQLMap are incredibly powerful during a penetration test because they can save hours of manual testing. However,
the ultimate defensive takeaway is clear: Developers must use Parameterized Queries (Prepared Statements) and strictly sanitize user inputs 
to ensure databases remain completely safe from injection attacks.
