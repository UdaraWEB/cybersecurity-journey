    TryHackMe: CAPA The Basics - Write-up

Hey!  This is my personal write-up for the **CAPA: The Basics** room on TryHackMe. 

In this room, I learned how malware analysts and threat hunters look inside suspicious files to understand what they can do without actually running them and risking infection. Here is a simple breakdown of what I learned.

---

##  What is CAPA and What Does It Do?

* **What is it?** CAPA (Common Analysis Platform for Artifacts) is an open-source tool developed by the **FireEye Mandiant** team.
* **What does it do?** It does **Static Analysis**. This means if you get a suspicious file (like `test.exe`), you don't double-click or run it. Instead, you give it to CAPA.
* **The Magic:** CAPA looks inside the file like an X-ray machine. It checks the code against a set of rules and tells you the file's **Capabilities** (e.g., *"This file can delete logs, steal passwords, or connect to the internet"*).

---

##  Key Concepts I Learned

### 1. Tracking and Labeling Malware
* **MITRE ATT&CK:** CAPA maps the malware's behavior to the global MITRE playbook using specific IDs (like `T1027` for Obfuscation).
* **MBC (Malware Behavior Catalogue):** A standard language used to label what malware is trying to achieve. It uses standard formats like:
  `OBJECTIVE::Behavior::Method [Identifier]`

### 2. Objectives vs. Micro-Objectives
* **Objectives:** Serious malicious goals like `Credential Access` (stealing passwords) or `Persistence` (staying hidden inside the PC for a long time).
* **Micro-Objectives:** Low-level behaviors like `Memory Allocation` or `HTTP Communication`. Safe software (like WhatsApp) does this too, but malware abuses them.

### 3. Capabilities & Rules (.yml files)
CAPA finds bugs using rules written in `.yml` (YAML) format. The name of the capability is exactly the name of the file but with dashes.
* Example: `delete file` uses the rule `delete-file.yml`.
* **Nursery Folder:** This is a temporary staging area in CAPA for new or unpolished rules.

---

##  Essential CAPA Commands (Cheat Sheet)

Here are the most important parameters I learned to use in the terminal:

* **Basic Scan:**
  ```
  capa test.exe
  ```
* **Detailed Scan (-v for Verbose):** Shows more information about the malware's capabilities.
  ```
  capa -v test.exe
  ```
* **Very Detailed Scan (-vv for Very Verbose):** Shows exactly which line of code or string triggered the rule.
  ```
  capa -vv test.exe
  ```
* **Export to JSON:** When `-vv` gives thousands of lines, we save it as a JSON file to read easily.
  ```
  capa -j -vv test.exe > report.json
  ```

###  CAPA Web Explorer
Reading a 3,000-line text file is impossible. So, I learned that we can upload the `.json` report to the **CAPA Web Explorer** tool. It converts the boring text into a beautiful web interface where we can use a **Global Search Box** to find matches like `/schtasks/i` (Scheduled Tasks) or `/VMWare/i` (Anti-VM tricks).




---
*If this write-up helped you understand CAPA, feel free to star ⭐ this repository!*
