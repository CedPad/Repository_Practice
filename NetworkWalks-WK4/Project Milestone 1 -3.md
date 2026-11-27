# 🏥 Week 4: Mediroza General Hospital

## 🔎 Penetration Testing Report

> **⚠️ Confidentiality Notice**
>
> This report documents a cybersecurity training activity conducted in a controlled or authorized environment. Sensitive patient information, personal identifiers, credentials, password hashes, and confidential database contents have been excluded from this public GitHub version. Screenshots should be reviewed and redacted before publication.

---

<details>
<summary><strong>📌 Project Overview</strong></summary>

This activity focused on identifying security weaknesses in the Mediroza General Hospital web application through reconnaissance, web resource inspection, initial access investigation, and file password analysis.

| Category | Details |
|---|---|
| Project | Mediroza General Hospital |
| Activity | Week 4 |
| Focus | Web application security |
| Tools | WHOIS, DNSRecon, WhatWeb, WAFW00F, Nikto, cURL, Burp Suite, SQL tools, John the Ripper |
| Main Objectives | Identify exposed resources, analyze access controls, and assess the security of protected files |

</details>

---

## 🧭 Milestone 1: Initial Access

<details>
<summary><strong>🎯 Objective — Reconnaissance and Resource Discovery</strong></summary>

The objective of this milestone was to perform reconnaissance and identify publicly accessible resources within the hospital web application.

### 1. WHOIS Lookup

I started by performing a WHOIS lookup:

```bash
whois medirozahospital.com
```

<img width="600" src="https://github.com/user-attachments/assets/65da5bac-2dab-49e5-92e7-ce38235bf117" alt="WHOIS lookup results"/>

The output displayed domain registration information, including the registrar and name servers. This information helped establish the initial footprint of the target domain.

### 2. DNS Enumeration

Next, I used DNSRecon to enumerate DNS records:

```bash
dnsrecon -d medirozahospital.com
```

<img width="600" src="https://github.com/user-attachments/assets/1683579a-b4a3-4c0a-9b4d-b9c9944dabfa" alt="DNSRecon enumeration results"/>
<img width="600" src="https://github.com/user-attachments/assets/2129c155-e818-4669-9796-13141670f520" alt="Additional DNSRecon output"/>

DNSRecon completed successfully and returned 12 DNS records, providing additional information about the domain's configuration.

### 3. Web Application Firewall Detection

I used WAFW00F to identify whether a Web Application Firewall (WAF) was present:

```bash
wafw00f medirozahospital.com
```

<img width="600" src="https://github.com/user-attachments/assets/c230799c-326d-4e03-ab8a-8752bf129bd0" alt="WAFW00F detection results"/>

The tool identified a LiteSpeed Web Application Firewall.

### 4. Web Server and Resource Scanning

I used Nikto to inspect the web server and identify potentially exposed resources:

```bash
nikto -h https://medirozahospital.com
```

<img width="600" src="https://github.com/user-attachments/assets/33cc4b81-343f-4b1d-afa1-c2a78b94eb67" alt="Nikto web server scan results"/>

The scan identified entries in `robots.txt`, including `/staff/`, `/old/`, and `/patient/`.

The scan also reported HTTP 200 responses and directory indexing on these paths, indicating that the resources were accessible in the lab environment.

### 5. Inspecting robots.txt

I inspected the site's `robots.txt` file using cURL:

```bash
curl -s https://medirozahospital.com/robots.txt
```

<img width="600" src="https://github.com/user-attachments/assets/0c7987c2-e0b4-4fe6-b58a-463f845c354b" alt="robots.txt contents"/>

The file listed several directories that were disallowed for search engine crawlers. These entries provided clues for further resource inspection.

### 6. Directory and Resource Inspection

I inspected the patient directory:

```bash
curl -s https://medirozahospital.com/patient/
```

<img width="600" src="https://github.com/user-attachments/assets/be1cd81d-50d4-4153-a4c7-451be5102375" alt="Patient directory listing"/>

The directory listing exposed references to reports, PHP files, and an `error_log` file.

I also inspected the staff directory:

<img width="600" src="https://github.com/user-attachments/assets/4806535c-fe45-4b30-8455-4609dba73b6d" alt="Staff directory listing"/>

And the old directory:

<img width="600" src="https://github.com/user-attachments/assets/b135c186-8cff-4090-b90c-946bd91c56c2" alt="Old directory listing"/>

These findings demonstrated the risk of leaving directory indexing enabled and sensitive resources exposed.

### 7. Patient Portal Login Investigation

I attempted to access the patient portal using a common username and password combination in the training environment.

<img width="600" src="https://github.com/user-attachments/assets/b80f9436-1afd-44f8-a107-5145867a3adc" alt="Patient portal login attempt"/>

The portal returned an `Incorrect password` message. This indicated that the login form was processing the submitted username and password, but it did not confirm successful authentication.

### 8. Login Request Inspection

I used SQL testing tools and Burp Suite to inspect the login page and its request behavior.

<img width="600" src="https://github.com/user-attachments/assets/5285818d-2b02-40af-bad5-beeadc4930f8" alt="Login request inspection"/>

This step helped me examine how the application handled login requests and identify areas for further security assessment.

</details>

---

## 📂 Milestone 2: Data Extraction

<details>
<summary><strong>🎯 Objective — Analyze Password-Protected PDF Files</strong></summary>

The objective of this milestone was to analyze the password protection applied to three PDF files obtained during the authorized training activity.

### 1. Extracting PDF Hashes

I used the Online Hash Crack PDF Hash Extractor to extract the password hashes from the PDF files.

🔗 [Online Hash Crack – PDF Hash Extractor](https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php)

<img width="600" src="https://github.com/user-attachments/assets/40165d68-e8e8-4e45-baca-f9ddc0e8e530" alt="PDF hash extraction example"/>

### 2. Password Recovery

I used the NetworkWalks tools and John the Ripper CLI to perform password recovery against the extracted hashes.

The results were documented for each file:

#### 📄 PDF 1

<img width="600" src="https://github.com/user-attachments/assets/b8750ae1-1c55-4c76-8fed-8bdd69fba98e" alt="PDF 1 password recovery result"/>

**File analysis:**

<img width="600" src="https://github.com/user-attachments/assets/33587f33-1552-4376-aaf7-a1da25dcdb2d" alt="PDF 1 analysis screenshot"/>

#### 📄 PDF 2

<img width="600" src="https://github.com/user-attachments/assets/e46b7dd3-b5ec-44c8-b4e0-39b90f9e7829" alt="PDF 2 password recovery result"/>

**File analysis:**

<img width="600" src="https://github.com/user-attachments/assets/f5f0ac23-007c-4ba2-8e9e-c9ec348a4d10" alt="PDF 2 analysis screenshot"/>

#### 📄 PDF 3

<img width="600" src="https://github.com/user-attachments/assets/95c2dec8-998f-4d19-bdd1-87a3918e4c31" alt="PDF 3 password recovery result"/>

</details>

---

## 🗄️ Milestone 3: Database Exposure Analysis

<details>
<summary><strong>🎯 Objective — Identify Exposed Staff and Shareholder Information</strong></summary>

The objective of this milestone was to investigate exposed resources and assess the impact of an accessible database backup.

### 1. Reviewing Scan Results

I revisited the Nikto scan results:

```bash
nikto -h https://medirozahospital.com
```

<img width="600" src="https://github.com/user-attachments/assets/33cc4b81-343f-4b1d-afa1-c2a78b94eb67" alt="Nikto scan results"/>

The scan identified publicly accessible directories, including `/staff/`, `/old/`, and `/patient/`.

### 2. Database Backup Discovery

While inspecting the old directory, I identified a reference to a database backup:

```text
/mediroza_db_backup_2019.sql
```

The backup was associated with the old directory path:

```text
https://medirozahospital.com/patient/old/
```

<img width="600" src="https://github.com/user-attachments/assets/b135c186-8cff-4090-b90c-946bd91c56c2" alt="Old directory contents"/>

### 3. Security Impact

The database backup contained references to staff salary and shareholder information.

The exposed database structure included sensitive fields such as:

- Staff and shareholder identifiers
- Email addresses
- Phone numbers
- Salary-related information
- Other confidential records

This demonstrated how an exposed database backup could create risks such as identity exposure, targeted phishing, and unauthorized disclosure of confidential information.

</details>

---

## 🛡️ Key Security Observations

<details>
<summary><strong>📌 Findings and Lessons Learned</strong></summary>

| Finding | Potential Risk |
|---|---|
| Directory indexing enabled | Exposed files and application resources |
| Sensitive paths listed in `robots.txt` | Provided clues for resource discovery |
| Publicly accessible PDF reports | Risk of confidential document disclosure |
| Password-protected PDFs | Weak passwords may be vulnerable to offline recovery |
| Exposed database backup | Potential disclosure of staff and shareholder data |
| Login behavior revealing errors | May assist username enumeration |


</details>

---

## 🧠 Reflection

This activity helped me understand how reconnaissance, resource discovery, and misconfigured web directories can lead to the exposure of sensitive information. It also demonstrated the importance of proper access control, secure file storage, and regular security assessments in protecting confidential data.

