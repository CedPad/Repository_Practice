# Using Jhon the Ripper (GUI) for Password Cracking

Background
John the Ripper (JTR) is a popular password cracking tool used by security professional to test how strong passwords are. 
It can check many types of password hashes and also unlock password protected files like PDF, ZIP, and Office documents. 

Johnny  is the graphical version of John the Ripper. 
It gives a simple point and click screen, so beginners can use JTR without typing long commands.

On this Activity I'm going to use **Johnny**

The task is to crack the password of the following pdf files.

## 📚 Supporting Documents

| Document | |
|---|---|
| [Lab 01 - Network Fundamentals](Documents/My-Locked-PDF1.pdf) | 
| [Lab 02 - Wireshark Analysis](Documents/My-Locked-PDF2.pdf) | 
| [Lab 03 - Network Investigation](Documents/My-Locked-PDF3.pdf) | 

Before we can crack the files of the documents we need to extract the **hash** of the pdf files.

During the activity I used the given link to extract the pdf hash: <https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php/>

Step 1. Extract the hash of the file.

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/5cafc316-67b1-404d-88ea-600abaf7fa06" />

Step 2. Then I saved the hash to a txt file. 

<img width="500" height="112" alt="image" src="https://github.com/user-attachments/assets/dbfdc443-ab7d-4b64-ba6a-ec5e48e6d7c4" />

Step 3. Using **Johnny** to crack the password of the pdf files

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/bbb2e772-064b-4806-903e-9512b6f018ca" />

I type the passwords in each of the pdf file to know the content

Content of one pdf file.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/1bfb312f-b44d-4073-a273-48ccb740f5bd" />

