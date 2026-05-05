Linux Shell  (TryHackMe Write-up)

In this room, I learned how to interact with the Linux operating system using the Command Line Interface (CLI) and Shell Scripting.
Here is a quick summary of what I did:

1.Understanding Shells

I learned that the Shell is the middleman between me (the user) and the OS.

 Bash is the most common shell, but there are others like Fish (which has built-in syntax highlighting) and Zsh.

 I used echo $SHELL to see my current shell and cat /etc/shells to see all available shells.

2.Basic Commands I Used

Before scripting, I practiced these essential commands:

 pwd: To see which folder I am in.

 ls: To list all files and folders in a directory.

 cat: To read the text inside a file.

 grep: To search for a specific word inside a file.

3.Shell Scripting Basics

I learned that every Bash script starts with a Shebang (#!/bin/bash). To make a script run, I used the chmod +x command to give it execution permissions.

4.The Practical Challenge (The Flag Hunt)

The final task was the most interesting. I had to find a hidden keyword (thm-flag01-script) inside the /var/log directory.

 Becoming Root: I used sudo su to get full admin access.

 Fixing the Script: I used the nano editor to edit a script named flag_hunt.sh. I filled in the missing keyword and the directory path.

 Manual Search: When the script gave an error, I used a powerful manual command:
grep -r "thm-flag01-script" /var/log

Results:

 The File: The keyword was found in /var/log/authentication.log.

 The Secret: I used cat /var/log/authentication.log and found the answer: "the cat is sleeping under the table".

Conclusion

This lab taught me that using the CLI is much more powerful than the GUI. I am now comfortable with searching files and writing basic automation scripts!
