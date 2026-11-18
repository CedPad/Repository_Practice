# 🔐 Password Cracking Using John the Ripper (GUI)

## 📌 Background

John the Ripper (JTR) is a password security auditing tool used by security professionals to evaluate password strength. It supports different password hash formats and can be used to recover passwords from protected files, including PDF documents.

**Johnny** is the graphical user interface (GUI) for John the Ripper. It provides a beginner-friendly interface that allows users to perform password-cracking tasks without relying entirely on command-line instructions.

In this activity, I used **Johnny** to recover the passwords of three password-protected PDF files.

## 📚 Supporting Documents

The following PDF files were used during the activity. Click the links to download them.

| Document     | Download                                                     |
| ------------ | ------------------------------------------------------------ |
| Locked PDF 1 | [⬇️ Download PDF 1](Documents/My-Locked-PDF1.pdf?download=1) |
| Locked PDF 2 | [⬇️ Download PDF 2](Documents/My-Locked-PDF2.pdf?download=1) |
| Locked PDF 3 | [⬇️ Download PDF 3](Documents/My-Locked-PDF3.pdf?download=1) |

---

## 🛠️ Activity: Password Cracking Using Johnny

Before attempting to recover the passwords, I first needed to extract the password hashes from the protected PDF files.

### Step 1: Extract the PDF Hash

I used the [Online Hash Crack PDF Hash Extractor](https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php) to extract the password hash from each PDF document.

\<img width="500" alt="Extracting the PDF hash" src="[https://github.com/user-attachments/assets/5cafc316-67b1-404d-88ea-600abaf7fa06](https://github.com/user-attachments/assets/5cafc316-67b1-404d-88ea-600abaf7fa06)" />

### Step 2: Save the Extracted Hash

After extracting the hash, I copied and saved it into a `.txt` file. This file was then used as input for John the Ripper.

\<img width="500" alt="Saving the extracted hash in a text file" src="[https://github.com/user-attachments/assets/dbfdc443-ab7d-4b64-ba6a-ec5e48e6d7c4](https://github.com/user-attachments/assets/dbfdc443-ab7d-4b64-ba6a-ec5e48e6d7c4)" />

### Step 3: Crack the PDF Password Using Johnny

I opened Johnny and loaded the extracted hash file to begin the password-cracking process.

\<img width="500" alt="Using Johnny to crack the PDF password" src="[https://github.com/user-attachments/assets/bbb2e772-064b-4806-903e-9512b6f018ca](https://github.com/user-attachments/assets/bbb2e772-064b-4806-903e-9512b6f018ca)" />

### Step 4: Verify the Recovered Password

After recovering the passwords, I used them to open the protected PDF documents and verify their contents.

**Example of an Unlocked PDF:**

\<img width="600" alt="Content of the unlocked PDF document" src="[https://github.com/user-attachments/assets/1bfb312f-b44d-4073-a273-48ccb740f5bd](https://github.com/user-attachments/assets/1bfb312f-b44d-4073-a273-48ccb740f5bd)" />

---

## 📝 Activity Summary

Through this activity, I learned how to extract password hashes from protected PDF files and use Johnny, the graphical interface of John the Ripper, to recover their passwords.

This exercise demonstrated how password hashes can be analyzed and why strong passwords are important for protecting sensitive documents.

---

\<details> \<summary>\<strong>🔎 Alternative Method: Using the NetworkWalks Password Cracking Tool\</strong>\</summary>

### Overview

Aside from Johnny, I also explored the NetworkWalks tool to perform password-cracking activities using extracted PDF hashes.

### Step 1: Extract the File Hash

I used the Hash Calculator feature to extract the password hash from the protected PDF document.

\<img width="500" alt="Extracting the PDF hash using Hash Calculator" src="[https://github.com/user-attachments/assets/56789d6f-7872-4e98-83d0-e968f51d422a](https://github.com/user-attachments/assets/56789d6f-7872-4e98-83d0-e968f51d422a)" />

### Step 2: Submit the Hash

I copied the extracted hash and pasted it into the Password Cracker tool provided by NetworkWalks.

\<img width="500" alt="Submitting the hash to NetworkWalks Password Cracker" src="[https://github.com/user-attachments/assets/f2a75a70-7bb4-459a-a37b-fd1a59106bb4](https://github.com/user-attachments/assets/f2a75a70-7bb4-459a-a37b-fd1a59106bb4)" />

### Step 3: Start the Cracking Process

I started the password-cracking process and checked the results returned by the tool.

**Locked PDF 3 – Result**

\<img width="500" alt="Password cracking result for PDF 3" src="[https://github.com/user-attachments/assets/1d0ddb82-dd55-4913-b9f0-2409ad4626ba](https://github.com/user-attachments/assets/1d0ddb82-dd55-4913-b9f0-2409ad4626ba)" />

**Locked PDF 1 – Result**

\<img width="500" alt="Password cracking result for PDF 1" src="[https://github.com/user-attachments/assets/5f2d603f-0e00-4687-9d7a-d477898a9a19](https://github.com/user-attachments/assets/5f2d603f-0e00-4687-9d7a-d477898a9a19)" />

### Summary

Using NetworkWalks, I was able to practice extracting PDF hashes, submitting them to a password-cracking tool, and examining the returned results.

\</details>

---

## 🎯 Key Takeaways

- Learned how to extract password hashes from protected PDF documents.
- Gained practical experience using John the Ripper through its Johnny GUI.
- Explored an alternative password-cracking tool through NetworkWalks.
- Understood the importance of password strength and document security.

**Tools Used:** John the Ripper, Johnny GUI, NetworkWalks, PDF Hash Extractor.
