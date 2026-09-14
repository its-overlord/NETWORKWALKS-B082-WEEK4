# networkwalks-B082-week4
Performing Penetration Testing on the Mediroza Hospital Website with written authorization to help in detecting the vulnerabilities they have in their system.


</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C0000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Ibunkunoluwa%20Fasesan-E0FFFF?style=flat-square" />
</p>

---

|  Pentester Name       | Ibunkunoluwa Fasesan   |
| ------------------ | ------------------  |
|  Program/Batch         | B082-Networkwalks        |
|  Date       | 11th September 2026               |
| Modules completed       | W4 Black Box Penetration Testing    |
| Client/Target      | Mediroza Hospital  |
| Permission secured from client?     | Yes  |

---

## 🔔 Liability Disclaimer

I have performed these activities only on the systems &amp; devices where I had secured written permission
or the devices/systems that I own myself. All these materials are for education and research purpose
only. Do not use anything from here to break the law. Every action you take is your own responsibility.
Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most
countries unauthorized access is a crime even when nothing is damaged.

---

## 🔰 Introduction/ Project Summary

This report contains black box penetration testing activities completed in the 4th week of the internship program with Networkwalks. This lab had the following primary activities:
1. Milestone 1 — Initial Access 
2. Milestone 2 — Crack the Encryption 
3. Milestone 3 — Deep Reconnaissance
4. Milestone 4 — Penetration Testing Report
This report documents my hands-on experience and a step-by-step guide on how tested for vulnerabilities in the system.

---

## ⚙️ Tools and Technologies

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

|  Tool       | Purpose |
| ------------------ | ------------------  |
| Kali       | This test was performed in the virtual box       |
| Curl      | HTTP header and server information gathering.  |
|  NetworkWalks Hash-Calculator      | Used this to find the hashing for encrypted documents  |
| NetworkWalks Password-Cracker     | Used to break the encrypted documents using directories |

---

## 1️⃣ Milestone 1 — Initial Access

The goal was to get access to the any of the login pages and gather any information I can on the target. The first thing I did was to perform basic reconnaissance using all the footprinting steps I learnt in week 2. I gathered information on the firewall type using waw00f, I also used the 'whois' command to get information on domain registration and other target information that i felt would be useful. I started the project using brute force which after a bit of research, showed that the server might block me out if I try too many attempts.

Then I decided to use the robots.txt file that all web browsers - it shows what pages can or cannot be accessed in a website. 
<img width="522" height="373" alt="image" src="https://github.com/user-attachments/assets/9c751d83-ed70-425f-8ff1-0082f1a5341d" />

But during the period where I was trying brute force, I noticed a weakness with the patient portal.  **When going into the patient portal, it explicitly tells you what is wrong (username is wrong), which should not be so; it is supposed to give general info so that bad actors would not be able to guess which info they have is wrong or right (login failed).**
So then I decided that getting a username would be easier. Used the username, entered in any password and then decided the SSH Injection would be able to break the login page.
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/d6e0533f-d06c-460b-919b-038704a51c99" />
GOT INTO THE PATIENT PORTAL AND DOWNLOADED THE ENCRYPTED DOCUMENTS.

---

## 2️⃣ Milestone 2 — Crack the Encryption

Cracking the encrypted document was much easier and took the least amount of time. The first thing that was done was to get the hash of all the encrypted documents using the Networkwalks Hash Calculator. Once that was achieved, the password cracker was used (you can also use Johnny at this step but the networkwalks tool was used for this project). I also had to use multiple directories/wordlist to get the right password for all three documents.
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/dc28f3af-d574-4182-89b0-4892bc725059" />
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/613d4a65-013b-45ee-80c3-dc0ade7edb73" />
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/ebff84fd-0d13-4424-bcfa-de10c6f424c4" />
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/8c0e5306-f600-4281-8152-284ff923f7f3" />
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/704b2d26-ccc6-413b-a3bd-7cce37e4a918" />
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/c5704dec-9670-4b0a-893b-b52c65ba9b6c" />

---

## 3️⃣ Milestone 3 — Deep Reconnaissance

At this point I was told to get some more private information on the hospital website, so I opened a cmd terminal in the documents that have now been unlocked and I used this command **'exiftool report3_open.pdf '** to know if some information was moved or where they are located. This led me to the /old file from the roborts.txt previously.
Searched https://medirozahospital.com/old/ and it loaded up the back end information and the hidden server.
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/b22164fd-5b9c-4247-bc89-7fbf2db5d076" />

Clicked on the link and got redirected to a sql document that had all staff information, their salaries, phone numbers even shareholders information!!
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/e954a2db-e76e-4ec7-81e2-94373042f0dd" />

This information can also be copied and saved on my personal device and fine-tuned to be sold to bad actors.

The overall vulnerability of the system is very high to bad actors!!

