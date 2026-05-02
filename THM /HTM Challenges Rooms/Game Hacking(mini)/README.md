Tetrix Game Hacking (Write-up)

Objective

The goal was to uncover a hidden secret (Flag) buried within a Windows executable file named Tetrix.exe.

What I Learned

Static Analysis: I learned how to inspect the contents of a compiled file without actually running it.
Strings Extraction: I understood that even compiled programs often contain plain-text data that can be extracted easily.
Tools Proficiency: I gained hands-on experience using CyberChef, a powerful web-based tool for data analysis and decoding.

How I Found the Flag

Preparation: I started by extracting the task files and identified the main target, Tetrix.exe.
Analysis: Since I couldn't read the code in a standard text editor, I uploaded the file to CyberChef.
Extraction: I applied the "Strings" operation to filter out all the non-readable binary data, leaving only human-readable text.
Discovery: I searched the output for the standard flag format THM{.
Result: I successfully located the flag: THM{I_CAN_READ_IT_ALL}
