# Password Cracking with JtR and NetworkWalks Tools

**Author:** Chukwu PraiseGod

**Internship:** Networkwalks Cybersecurity Internship, Batch B083

**Week:** 3

**Modules:** PM1 Password Cracking with JtR (John the Ripper), PM2 Password Cracking with Networkwalks Tools (Hash Calculator and Password Cracker)

**Date:** 21 September 2026

**Classification:** Educational, Authorised Lab

---

## Overview

In this project, I recovered the passwords of three encrypted PDF files using two different approaches: a locally installed offline tool (John the Ripper, through the Johnny GUI) and a fully web based workflow (Networkwalks Hash Calculator and Password Cracker tool). 

For each PDF, I extracted its password hash, ran a dictionary attack against that hash until I recovered the correct password, then confirmed success by reopening the PDF with the password I had cracked.

This README serves as a complete walkthrough of the project. All supporting evidence lives in the screenshots folder, referenced inline below, and all working files (locked PDFs, extracted hashes, and wordlist) are kept in their own folders as described in the repo structure section.

## Repo Structure

```
NETWORKWALKS-B083-WK3-PASSWORD-CRACKING
├── README.md
├── locked-pdfs/
├── cracked-pdf-hashes/
├── wordlist/
└── screenshots/
    ├── pm1/
    └── pm2/
```

## Tools Used

| Tool | Purpose | Module |
|---|---|---|
| John the Ripper (JtR) | Offline password hash cracking engine | PM1 |
| Johnny | Graphical front end for John the Ripper | PM1 |
| Online Hash Crack, PDF Hash Extractor | Extracts the `$pdf$` hash from a locked PDF | PM1 |
| Networkwalks Hash Calculator | Web based tool to extract a PDF's password hash | PM2 |
| Networkwalks Password Cracker | Web based dictionary attack tool | PM2 |
| rockyou-75.txt | Wordlist used for the dictionary attack | PM2 |

---

## PM1: Password Cracking With JtR (John the Ripper)

### Step 1: Install John the Ripper

I downloaded John the Ripper for Windows from the official site, `https://www.openwall.com/john/`, with `https://distro.ibiblio.org/openwall/projects/john/1.9.0/`

> Note: On Kali Linux, John the Ripper comes pre installed

### Step 2: Install and Configure Johnny (GUI for John)

Downloaded Johnny, the graphical interface for John the Ripper, from `https://openwall.info/wiki/john/johnny`. After running the installer, I opened Johnny, went to Settings, and browsed to the `john.exe` executable inside John's `run` folder to link the two tools together.

![John loaded in Johnny](./screenshots/pm1/john-loaded-in-johnny.png)

### Step 3: Extract, Crack, and Verify Each PDF Password

Repeated the process below individually for `My Locked PDF1.pdf`, `PDF2`, and `PDF3`.

1. **Extract the hash.** Upload each locked PDF to the Online Hash Crack PDF Hash Extractor at `https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php` and copy the resulting hash value. Making sure the hash started with `$pdf$`.

   ![PDF1 cracked hash](./screenshots/pm1/pdf1-cracked-hash.png)
   ![PDF2 cracked hash](./screenshots/pm1/pdf2-cracked-hash.png)
   ![PDF3 cracked hash](./screenshots/pm1/pdf3-cracked-hash.png)


2. **Save the hash to a text file.** Paste each hash into Notepad and save it as a plain text file (`hash1.txt`, `hash2.txt`, `hash3.txt`).

      ![PDF1 extracted hash](./screenshots/pm1/pdf1-extracted-hash.png)
      ![PDF2 extracted hash](./screenshots/pm1/pdf2-extracted-hash.png)
      ![PDF3 extracted hash](./screenshots/pm1/pdf3-extracted-hash.png)

3. **Load the hash into Johnny.** In Johnny, click "Open password file" and browse to the relevant hash file to open it.

4. **Start the attack.** Click "Start new attack" to set John the Ripper running against the loaded hash. Cracking time varied depending on how complex each password was.

5. **Record the recovered password.** Once John finished, I read the cracked password directly from Johnny's display.

   ![PDF1 password via JtR](./screenshots/pm1/pdf1-password-jtr.png)
   ![PDF2 password via JtR](./screenshots/pm1/pdf2-password-jtr.png)
   ![PDF3 password via JtR](./screenshots/pm1/pdf3-password-jtr.png)

6. **Verify by opening the PDF.** Open each encrypted PDF and enter the recovered password, confirming access to the file.

   ![PDF1 flag](./screenshots/pm1/pdf1-flag.png)
   ![PDF2 flag](./screenshots/pm1/pdf2-flag.png)
   ![PDF3 flag](./screenshots/pm1/pdf3-flag.png)

---

## PM2: Password Cracking With Networkwalks Tools 

### Step 1: Download the Locked PDF

Downloaded the encrypted PDF file from the Networkwalks lab page at `https://networkwalks.com/project-task-lab-password-cracking-with-networkwalks-tools/` and saved it into the `locked-pdfs/` folder alongside the files I used in PM1.

### Step 2: Extract the Hash With the Networkwalks Hash Calculator

Open the Networkwalks Hash Calculator in a browser at `https://networkwalks.com/hash-calculator/`. Upload each locked PDF in turn, and the tool return a hash value starting with `$pdf$`.

![PDF1 Networkwalks hash](./screenshots/pm2/pdf1-nw-hash.png)
![PDF2 Networkwalks hash](./screenshots/pm2/pdf2-nw-hash.png)
![PDF3 Networkwalks hash](./screenshots/pm2/pdf3-nw-hash.png)

Copy the complete hash in full, starting from `$pdf$`, taking care not to miss any part of it.

### Step 3: Attempt the Attack With the Default Wordlist

Open the Networkwalks Password Cracker at `https://networkwalks.com/password-cracker/` and paste in the extracted hash for PDF1. 

**I started the attack using the tool's default built in wordlist (100 passwords), but this first attempt failed to find a match.**

![PDF1 access denied with default wordlist](./screenshots/pm2/pdf1-access-denied.png)

### Step 4: Import the rockyou-75.txt Wordlist

Since the default wordlist was too small to contain PDF1's password, I imported a customized version of the `rockyou-75.txt` wordlist into the Password Cracker instead.

![Loaded rockyou wordlist](./screenshots/pm2/loaded-rockyou-wordlist.png)

**I used this same wordlist for the attack against all three PDFs.**

### Step 5: Run the Attack and Record Each Password

With `rockyou-75.txt` loaded, rerun the attack against each PDF's hash in turn. 

The tool worked through the wordlist until it found a match, and I recorded the cracked password as it appeared on screen.

![PDF1 Networkwalks password](./screenshots/pm2/pdf1-nw-password.png)
![PDF2 Networkwalks password](./screenshots/pm2/pdf2-nw-password.png)
![PDF3 Networkwalks password](./screenshots/pm2/pdf3-nw-password.png)

### Step 6: Verify by Opening the PDF

Open each locked PDF and enter the password the Networkwalks Password Cracker had recovered, confirming that the file unlocked successfully.

![PDF1 flag](./screenshots/pm2/pdf1-flag.png)
![PDF2 flag](./screenshots/pm2/pdf2-flag.png)
![PDF3 flag](./screenshots/pm2/pdf3-flag.png)

---

## Results Summary

| PDF | Module | Wordlist Used | Password Recovered |
|---|---|---|---|
| My Locked PDF1.pdf | PM1 | John the Ripper default rules | *see [`pdf1-password-jtr.png`](/screenshots/pm1/pdf1-password-jtr.png)* |
| My Locked PDF2.pdf | PM1 | John the Ripper default rules | *see [`pdf2-password-jtr.png`](/screenshots/pm1/pdf2-password-jtr.png)* |
| My Locked PDF3.pdf | PM1 | John the Ripper default rules | *see [`pdf3-password-jtr.png`](/screenshots/pm1/pdf3-password-jtr.png)* |
| My Locked PDF1.pdf | PM2 | rockyou-75.txt (default wordlist failed first) | *see [`pdf1-nw-password.png`](/screenshots/pm2/pdf1-nw-password.png)* |
| My Locked PDF2.pdf | PM2 | rockyou-75.txt | *see [`pdf2-nw-password.png`](/screenshots/pm2/pdf2-nw-password.png)* |
| My Locked PDF3.pdf | PM2 | rockyou-75.txt | *see [`pdf3-nw-password.png`](/screenshots/pm2/pdf3-nw-password.png)* |

## Lessons Learned

* I learned that a PDF's encryption does not need to be broken directly. Once I extracted the password hash in the `$pdf$` format, the problem became a standard offline or online dictionary attack, no different in principle from cracking any other password hash.
* I saw firsthand that wordlist choice matters as much as the cracking tool itself. The Networkwalks default wordlist, at only 100 entries, was too small to contain even PDF1's password, while `rockyou-75.txt`, a small sample drawn from the much larger and well known rockyou password list, got me through all three files.
* Running the same attack through two different tool chains, a locally installed John the Ripper plus Johnny on one side, and a fully web based Networkwalks workflow on the other, gave me the same end result both times. That reinforced for me that password cracking comes down to hash format, wordlist coverage, and time, not which specific tool I happen to use.

## Disclaimer

I completed this project for educational purposes as part of an authorised cybersecurity internship lab exercise. All PDF files I cracked in this project were provided specifically for this lab and were not obtained from, or used against, any third party system. Distribution of this repository should be limited to course instructors, assessors, and my professional portfolio audience.

