     TryHackMe: FlareVM Arsenal of Tools - Write-up

Hey there!  This is my personal write-up for the **FlareVM: Arsenal of Tools** room on TryHackMe. 

While REMnux is for Linux-based malware analysis, **FlareVM** is a specialized **Windows-based** environment developed by the **FireEye Mandiant** team. 
It is packed with tools for malware analysis, reverse engineering, and digital forensics. Here is a simple breakdown of what I learned.

---

## What I Learned (Core Tools & Concepts)

### 1. Static Analysis (Inspecting files without running them)
* **PEStudio:** A fantastic tool to check the basic properties of an executable. 
  * **Entropy:** If a file has a high entropy score (e.g., `7.839`), it means the code is highly randomized, indicating that the malware is likely **encrypted or packed** to hide from Antivirus.
  * **Manifest:** Tells us the execution level required by the app (Example: `requireAdministrator`).
* **CFF Explorer:** Used to view and edit Portable Executable (PE) headers. I learned that every valid Windows executable has a DOS Header magic value of **`4D5A` (MZ)**.
* **FLOSS:** A tool used to automatically extract hidden or obfuscated strings (like IPs or passwords) embedded inside a malware binary.

### 2. Dynamic Analysis (Monitoring live malware behavior)
* **Process Explorer (procexp):** Like a supercharged Windows Task Manager. It shows a **Parent-Child relationship** between processes. 
  * If you double-click and run a file from the Desktop manually, its parent process will always be **`explorer.exe`**.
  * By checking the **TCP/IP tab** in a process's properties, you can instantly see the hacker's Command & Control (C2) IP address and destination port.
* **Process Monitor (Procmon):** Logs real-time system activity (Registry changes, file creations, network connections). Because it captures thousands of lines, using filters (`Ctrl + L`) like `Process Name -> contains -> [malware_name]` is essential to isolate the data.

---

##  Practical Lab Answers

### Task 2: General Tool Identification
* Open-source debugger for x64/x32 formats? -> `x64dbg`
* Analyze and edit Portable Executable (PE) files? -> `CFF Explorer`
* Sophisticated memory editor and process watcher? -> `Process Hacker`
* Tool for Disc image acquisition and forensic use? -> `FTK Imager`
* View and edit binary files? -> `HxD`

### Task 5: Live Analysis Practice (`windows.exe` & `cobaltstrike.exe`)
* Entropy value of `windows.exe`? -> `7.839`
* Value under requestedExecutionLevel? -> `requireAdministrator`
* Function allowing a process to use OS shell? -> `set_UseShellExecute`
* Cryptographic API starting with R? -> `RijndaelManaged`
* Imphash of `cobaltstrike.exe`? -> `f34d5f2d4577ed6d9ceec516c1f5a744`
* Defanged IP address of the C2 connection? -> `47[.]120[.]46[.]210` *(Defanged format maps to `47.120.46.210` to avoid accidental clicks).*
* Destination port number used by Cobalt Strike? -> `81`
* Parent process of `cobaltstrike.exe`? -> `explorer.exe`


