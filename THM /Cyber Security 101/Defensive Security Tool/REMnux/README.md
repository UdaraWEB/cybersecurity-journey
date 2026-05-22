    TryHackMe: REMnux - Write-up

Hey!  This is my personal write-up for the **REMnux: Getting Started** room on TryHackMe. 

REMnux is a special Linux distribution built specifically for **Malware Analysis and Digital Forensics**. In this room, I learned how to use three powerful built-in tools (`oledump.py`, `INetSim`, and `Volatility 3`) to dissect malware and analyze memory images.

---

##  What I Learned & Tools Used

### 1. Analyzing Malicious Documents (`oledump.py`)
* **Concept:** Hackers often hide malware inside Excel (`.xlsm`) or Word (`.docx`) files using hidden scripts called **Macros (VBA)**.
* **The Tool:** `oledump.py` allows us to look inside these files and extract hidden code without opening the document safely.
* **Key Indicators:** In the tool's output, a capital **"M"** next to a data stream means a Macro is present.
* **Decompression:** Using `--vbadecompress` extracts the hidden macro into human-readable code. In the lab, I found a hidden PowerShell script designed to download an executable virus (`Doc-3737122pdf.exe`) into a temporary folder (`$TempFile`) and run it silently.

### 2. Simulating Fake Networks (`INetSim`)
* **Concept:** When analyzing live malware, you cannot let it connect to the real internet because it might talk to the hacker's server. 
* **The Tool:** `INetSim` creates a completely **Fake Network** inside your lab. It tricks the malware into thinking it is connected to the internet.
* **How it works:** When the malware tries to download a file from a URL, INetSim intercepts the request using the **HTTP GET** method and serves a harmless fake file instead. This protects the machine while revealing the malware's network intentions.

### 3. Memory Forensics (`Volatility 3`)
* **Concept:** Even if a hacker deletes a virus from the hard drive, active traces and evidence remain inside the **RAM (Memory Image)**.
* **The Tool:** `vol3` analyzes memory captures (`.mem`) to extract evidence.
* **Crucial Plugins to Remember:**
  * `windows.pslist.PsList` -> Lists all active processes running at the time.
  * `windows.pstree.PsTree` -> Groups processes in a parent-child tree format.
  * `windows.cmdline.CmdLine` -> Shows exact commands typed into CMD/PowerShell.
  * `windows.malfind.Malfind` -> Finds hidden or injected code inside system processes (like `csrss.exe` or `winlogon.exe`).
  * `windows.dlllist.DllList` -> Reveals file paths where running binaries are stored.

---

##  Practical Lab Answers

### Task 3: oledump.py Answers
* What Python tool analyzes OLE2 files? -> `oledump.py`
* Parameter to select a particular data stream? -> `-s`
* PowerShell command to download files? -> `Invoke-WebRequest`
* File downloaded by the script? -> `Doc-3737122pdf.exe`
* Where will the downloaded file be stored? -> `$TempFile`
* Data streams in `possible_malicious.docx`? -> `16`
* Stream number indicating a macro? -> `8`

### Task 4: INetSim Answers
* What is the flag? -> `Tryhackme{remnux_edition}`
* What URL Method was used to get the file flag.txt? -> `GET`

### Task 5: Volatility 3 Answers
* Plugin lists processes in a tree based on Parent ID? -> `PsTree`
* Plugin to list active processes? -> `PsList`
* Linux utility to extract ASCII/Unicode text? -> `strings`
* 1st process identified with injected code? -> `csrss.exe`
* 2nd process identified with injected code? -> `winlogon.exe`
* File path of the binary `@WanaDecryptor@.exe`? -> `C:\Intel\ivecuqmanpnirkt615`

