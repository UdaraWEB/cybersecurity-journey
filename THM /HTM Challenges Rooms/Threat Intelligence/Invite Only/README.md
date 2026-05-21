    TryHackMe - Invite Only (Writeup)

A quick and simple walkthrough for the **Invite Only** challenge on TryHackMe. This room focuses on Malware Analysis, Threat Intelligence

---

### Task 1: Malware Analysis (Using TryDetectThis 2.0)

We started with the provided malicious SHA256 hash:  
`5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f`

1. **What is the file name of the provided hash?**
   * **Answer:** `syshelpers.exe`
   * *How to find:* Searched the hash in the tool and checked the top header/details.

2. **What is the file type?**
   * **Answer:** `Win32 EXE`
   * *How to find:* Looked at the "Type" field inside the **Details** tab.

3. **What are the execution parents of this file?**
   * **Answer:** `361GJX7J,installer.exe`
   * *How to find:* Opened the **Relations** tab and checked the **Execution Parents** section.

4. **What is the name of the dropped file?**
   * **Answer:** `Aclient.exe`
   * *How to find:* Scrolled down to the **Dropped Files** section in the same Relations tab.

---

### Task 2: Analyzing the Parent Installer

Next, we copied the hash of the parent file `installer.exe`:  
`fa102d4e3cfbe85f5189da70a52c1d266925f3efd122091cdc8fe0fc39033942`  
Then, we searched this new hash in the application.

5. **What are the malicious dropped files from the installer?**
   * **Answer:** `searchhost.exe,syshelpers.exe,nat.vbs,runsys.vbs`
   * *How to find:* Looked at the **Dropped Files** list from top to bottom. (Note: changed `nat1.vbs` to `nat.vbs` for the platform's answer format).

6. **What is the malware family?**
   * **Answer:** `asyncrat`
   * *How to find:* Checked the threat labels and virus detections on the page.

---

### Task 3: OSINT (Google Investigation)

For the final questions, we used Google to search for the threat intelligence report using the context found earlier.

7. **What is the title of the threat intelligence report?**
   * **Answer:** `From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery`

8. **What is the name of the cookie stealing tool used?**
   * **Answer:** `ChromeKatz`

9. **What is the phishing technique used in this campaign?**
   * **Answer:** `ClickFix`

10. **What platform was used to deliver the malware?**
    * **Answer:** `Discord`


