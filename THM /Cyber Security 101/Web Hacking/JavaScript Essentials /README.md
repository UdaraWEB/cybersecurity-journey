TryHackMe - JavaScript Essentials (writeup)

I just finished the JavaScript Essentials module on TryHackMe! Here is a simple summary of what I learned
about how JavaScript (JS) works and why it matters for web security.

    1. The Basics of JS
    
JavaScript is an interpreted language. This means the browser executes the code directly without
needing to compile it first. I learned the core building blocks:

Variables: Containers (var, let, const) used to store data.

Data Types: The type of data stored, like Strings, Numbers, or Booleans.

Functions: Blocks of code written once and reused multiple times.

Loops: Used to run a piece of code repeatedly based on a condition.

    2. Internal vs. External JS
    
There are two ways to add JS to HTML:

Internal: Code is written directly inside <script> tags in the HTML file.

External: Code is saved in a separate .js file and linked using the src attribute (e.g., <script src="script.js">).

Security Tip: As a pentester, you can right-click any webpage and select View Page Source to see these scripts
and look for vulnerabilities.

    3. Dialogue Boxes & Exploits
    
JS has built-in functions to talk to users: alert() (shows a message), prompt() (asks for input), and confirm() (asks for yes/no).

The Hacking Connection: Attackers can abuse these functions via Cross-Site Scripting (XSS). For example, using a for loop to pop
up 500 alerts can freeze a user's browser!

    4. Client-Side Authentication Bypass
    
I practiced with a login.html file. Some weak websites check usernames and passwords using JS directly in the browser
(client-side). This is highly insecure because anyone can open the Chrome Console or Inspect Element and see the 
hardcoded password right in the code!

    5. Minification and Obfuscation
    
Minification shrinks file size by removing spaces and comments to make the site load faster.

Obfuscation hides the logic of the code by turning it into random-looking characters
(like changing a variable to a hex value like 0x247e).

While it makes the code hard for humans to read, the browser can still run it perfectly. As security researchers, 
we can use online Deobfuscator tools to unwrap and read this hidden code.

For Web Safety:

Never trust client-side validation alone; always double-check data on the server side.

Never hardcode sensitive data like API keys or passwords in JS files.

Never blindly import untrusted third-party libraries into your project.
