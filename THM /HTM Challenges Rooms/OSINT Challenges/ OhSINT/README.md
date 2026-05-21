     TryHackMe: OhSINT (writeup)

A straightforward walkthrough for the **OhSINT** challenge on TryHackMe. This room focuses on Open-Source Intelligence (OSINT), Metadata Analysis, and Social Media tracking.

---

### Initial Clue
We were given a single image file named `WindowsXP.jpg`. 

To extract the initial details, we used the `exiftool` command in Linux:
```bash
exiftool WindowsXP.jpg
```
This revealed a copyright name / author nickname: **`OWoodflint`**. We used this username to search across the web.

---

### Questions & Answers

#### 1. What is this user's avatar of?
* **Answer:** `cat`
* *How to find:* Searched Google for `OWoodflint` and found his Twitter profile. His profile picture (avatar) is a cat.

#### 2. What city is this person in?
* **Answer:** `London`
* *How to find:* Looked at his Twitter posts and found a tweet containing a BSSID address. Searched this BSSID on [Wigle.net](https://wigle.net) using Advanced Search, which mapped the location to London.

#### 3. What is the SSID of the WAP he connected to?
* **Answer:** `UnileverWiFi`
* *How to find:* Zoomed completely into the marker on the Wigle.net map to reveal the exact network name (SSID).

#### 4. What is his personal email address?
* **Answer:** `OWoodflint@gmail.com`
* *How to find:* Searched Google for `OWoodflint` and opened his GitHub profile. Checked the `README.md` file or repository code to extract the email address.

#### 5. What site did you find his email address on?
* **Answer:** `GitHub`
* *How to find:* The email address was discovered inside his personal GitHub profile page.

#### 6. Where has he gone on holiday?
* **Answer:** `New York`
* *How to find:* Found his WordPress blog via Google search. One of his blog posts explicitly mentions taking a holiday in New York.

#### 7. What is the person's password?
* **Answer:** `pennYDr0pper.!`
* *How to find:* Visited the WordPress blog post. Used `Ctrl + A` to highlight all text on the webpage. This revealed hidden text written in white font matching the background, which contained the password.


