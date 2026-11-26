# 🛡️ Penetration Testing Report
## 🏥 Mediroza General Hospital | Week 4

> ⚠️ **Confidentiality Notice:** This report documents an authorised cybersecurity training exercise. Sensitive patient information, employee records, credentials, password hashes, and confidential database contents have been intentionally excluded from this public GitHub version.

---

<details open>
<summary><strong>📌 Project Overview</strong></summary>

| 📋 Category | 📝 Details |
|---|---|
| 🏥 Client / Target | Mediroza General Hospital |
| 🌐 Target Domain | `https://medirozahospital.com` |
| 🔐 Project | NetworkWalks Penetration Testing |
| 👥 Batch | B084 |
| 👤 Author | Cedrick Zion K. Padonga |
| ✅ Authorization | Written permission granted for the training exercise |

### 🎯 Project Milestones

- **🔎 M1 – Initial Access:** Retrieve the confidential patient laboratory reports.
- **📂 M2 – Data Extraction:** Recover access to the encrypted PDF files.
- **💻 M3 – Attack / Data Analysis:** Identify exposed employee salary and shareholder information.
- **📑 M4 – Pentest Report:** Document the findings, evidence, risk levels, and remediation recommendations.

</details>

---

<details>
<summary><strong>01 | 📊 Executive Summary</strong></summary>

### 🔍 Overview

This report presents the results of a black-box penetration testing exercise conducted against the Mediroza General Hospital web application as part of the NetworkWalks cybersecurity training program.

The assessment focused on identifying exposed resources, examining access restrictions, recovering access to encrypted PDF laboratory reports, and analysing additional confidential information discovered during the exercise.

Based on the evidence collected, the assessment identified several security concerns involving restricted document exposure, weak PDF password protection, and an exposed database backup containing sensitive organisational information.

### 🚨 Key Findings

| ID | 🔎 Finding | ⚠️ Risk |
|---|---|---|
| F-01 | Exposure of restricted patient PDF reports | 🔴 High |
| F-02 | Weak password protection on encrypted PDF files | 🔴 High |
| F-03 | Exposed database backup containing confidential records | 🚨 Critical |
| F-04 | Information disclosure through robots.txt and resource discovery | 🟠 Medium |
| F-05 | Web server and security technology disclosure | 🟢 Low |

### 🚨 Overall Risk

**Overall Risk: Critical**

The exposed database backup presents the most significant concern because it may provide direct access to confidential records without requiring access through the application's normal authentication process.

The combination of exposed documents, weak file-level password protection, and publicly accessible backup data demonstrates how multiple security weaknesses can contribute to a larger data exposure risk.

</details>

---

<details>
<summary><strong>02 | 🎯 Scope and Methodology</strong></summary>

### 🌐 Scope

The assessment was limited to the authorised target domain:

`https://medirozahospital.com`

The project instructions specified a full black-box penetration test within the agreed scope.

### 📜 Rules of Engagement

- ✅ Testing was conducted with written authorisation.
- 🎯 Testing was limited to the target domain.
- 🚫 Social engineering was excluded.
- 🚫 Denial-of-service testing was excluded.
- 🔒 Systems outside the agreed scope were not included.

### 🔬 Methodology

The assessment followed the project milestones:

1. 🔎 Reconnaissance and identification of exposed entry points.
2. 📂 Discovery of restricted resources and accessible documents.
3. 🔐 Examination of PDF encryption and password protection.
4. 📄 Analysis of retrieved files and their contents.
5. 🕵️ Identification and documentation of confidential data exposure.
6. 🛠️ Risk assessment and remediation recommendations.

### 🧰 Tools Used

| 🛠️ Tool | 🎯 Purpose |
|---|---|
| Kali Linux | Testing environment |
| WHOIS | Domain registration information |
| WhatWeb | Web technology fingerprinting |
| Nslookup | DNS resolution |
| cURL | HTTP headers and web resource inspection |
| Wafw00f | Web Application Firewall detection |
| Nikto | Web server and resource checks |
| Directory / resource enumeration tools | Identify accessible paths |
| PDF hash extraction and password recovery tool | Examine PDF protection in the authorised lab |
| SQL database inspection | Analyse the exposed database backup |

### ⚠️ Limitations

The report is based on the evidence documented in the submitted sample report. It does not include a complete independent retest of the target.

Risk ratings are qualitative assessments based on the demonstrated evidence and potential impact. They are not formal CVSS scores.

</details>

---

<details>
<summary><strong>03 | 🔓 Findings and Proof of Exploitation</strong></summary>

## 🔴 F-01: Exposure of Restricted Patient PDF Reports

**⚠️ Risk Rating: High**

### 📝 Description

During the assessment, restricted patient laboratory report files were identified and retrieved from the target environment.

The evidence indicates that confidential PDF documents could be accessed through exposed or insufficiently protected web resources.

The retrieved documents contained sensitive patient information, including personal details and laboratory results.

### 📸 Evidence

- Patient PDF reports were retrieved during the initial access milestone.
- Screenshots in the sample report document the recovered files.
- The report also shows restricted patient-related paths returning access-denied responses in some cases.

### 💥 Impact

If exploited by an unauthorised individual, this weakness could result in:

- 🏥 Exposure of confidential patient information.
- 🔒 Violation of patient privacy.
- 📉 Reputational damage.
- ⚖️ Potential legal and regulatory consequences.
- 🤝 Loss of trust in the organisation.

### 🛠️ Recommendation

- Store confidential documents outside publicly accessible web directories.
- Enforce authentication and authorisation before serving patient files.
- Use server-side access controls for every document request.
- Avoid relying on hidden URLs or directory names as a security measure.
- Review access logs for unauthorised document retrieval.

---

## 🔴 F-02: Weak Password Protection on PDF Files

**⚠️ Risk Rating: High**

### 📝 Description

The retrieved PDF laboratory reports were encrypted and required passwords to open.

During the authorised exercise, password recovery techniques were used to demonstrate that the protection applied to the files could be defeated using a limited password list.

The sample report contains screenshots showing successful password recovery for two patient PDF files.

### 📸 Evidence

- PDF password hashes were extracted for testing.
- Password recovery was performed using a wordlist-based approach.
- Successful recovery results were documented in the sample report.

### 💥 Impact

Weak PDF passwords may allow an attacker who obtains an encrypted file to recover its contents.

This can lead to:

- 🔓 Exposure of confidential patient records.
- 🔐 Circumvention of file-level protection.
- 📂 Increased risk when documents are stored in public or shared locations.

### 🛠️ Recommendation

- Do not use PDF passwords as the primary access-control mechanism for confidential records.
- Use strong, unique passwords when file encryption is required.
- Apply appropriate encryption standards.
- Store confidential documents in systems with enforced access controls.
- Avoid predictable passwords and commonly used password patterns.

---

## 🚨 F-03: Exposed Database Backup Containing Confidential Records

**⚠️ Risk Rating: Critical**

### 📝 Description

During the analysis of the retrieved materials, a database backup was identified.

The evidence shows that the backup contained database structure and records associated with hospital staff information.

The sample report includes a screenshot of SQL statements and inserted records, indicating that the backup contained confidential organisational data.

### 📸 Evidence

- A database backup file was identified in the collected evidence.
- The backup contained SQL table definitions and data insertion statements.
- The visible database structure included staff-related fields such as names, job titles, departments, contact information, salary information, and other personal details.

### 💥 Impact

An exposed database backup may allow an unauthorised party to access large amounts of confidential information without interacting with the application's normal security controls.

Potential consequences include:

- 👤 Exposure of employee personal information.
- 💰 Disclosure of salary and organisational information.
- 🎣 Increased risk of identity theft and targeted phishing.
- 🏢 Exposure of business-sensitive information.
- 📉 Serious reputational and operational damage.

### 🛠️ Recommendation

- Remove database backups from public web directories immediately.
- Store backups in restricted storage locations.
- Encrypt backup files using strong encryption.
- Enforce access controls based on business requirements.
- Review backup creation and retention procedures.
- Rotate any credentials or secrets found within exposed backup files.
- Investigate access logs to determine whether the backup was accessed by unauthorised parties.

---

## 🟠 F-04: Information Disclosure Through robots.txt and Resource Discovery

**⚠️ Risk Rating: Medium**

### 📝 Description

The assessment identified a robots.txt file containing entries that referenced restricted or sensitive application paths.

The sample report also documents the discovery of patient-related and staff-related resources through web resource inspection and directory enumeration.

Although robots.txt is intended to guide search engine crawlers, it does not provide access control.

### 📸 Evidence

The collected screenshots documented:

- Restricted paths listed in robots.txt.
- Patient and staff-related application paths.
- Resource discovery results.
- Access-denied responses when attempting to access certain restricted locations.

### 💥 Impact

Information disclosed through robots.txt and resource enumeration may help an attacker identify:

- 🔎 Sensitive application areas.
- 🔐 Authentication endpoints.
- 📂 Restricted document locations.
- 🕸️ Potentially exposed legacy resources.

### 🛠️ Recommendation

- Do not use robots.txt to protect confidential resources.
- Remove unnecessary sensitive path references from public files.
- Enforce authentication and authorisation on restricted resources.
- Review legacy and unused application paths.
- Ensure directory listing is disabled where it is not required.

---

## 🟢 F-05: Web Server and Security Technology Disclosure

**⚠️ Risk Rating: Low**

### 📝 Description

Web technology fingerprinting and HTTP response inspection revealed information about the server environment.

The evidence identified LiteSpeed-related server technology and indicated that the website used a web application firewall or similar security solution.

### 📸 Evidence

- WhatWeb identified LiteSpeed-related technology.
- HTTP response headers exposed server information.
- Wafw00f reported LiteSpeed Web Application Firewall detection.
- Some requests were blocked or terminated during testing.

### 💥 Impact

Technology disclosure may assist attackers in identifying the software and security technologies used by the target.

This information alone does not confirm a vulnerability, but it may help attackers select targeted techniques.

### 🛠️ Recommendation

- Minimise unnecessary server information in HTTP response headers.
- Keep server software and security components updated.
- Review security configurations regularly.
- Monitor blocked requests and suspicious scanning activity.

</details>

---

<details>
<summary><strong>04 | 📈 Risk Rating Summary</strong></summary>

| Finding | ⚠️ Severity | 📝 Justification |
|---|---|---|
| F-01 | 🔴 High | Confidential patient documents were retrieved during the exercise. |
| F-02 | 🔴 High | Password protection on recovered PDF files was successfully defeated in the documented evidence. |
| F-03 | 🚨 Critical | An exposed database backup contained confidential staff and organisational records. |
| F-04 | 🟠 Medium | Public resource information could assist reconnaissance and attack-surface mapping. |
| F-05 | 🟢 Low | Server technology information was disclosed, but this alone does not confirm a vulnerability. |

### 🔍 Risk Assessment

The most significant issue is the exposed database backup because it may provide direct access to confidential records.

The patient document exposure and weak PDF password protection further increase the potential impact of the overall security weaknesses.

The risk ratings reflect the evidence collected during the authorised training exercise.

</details>

---

<details>
<summary><strong>05 | 🛠️ Recommendations and Remediation</strong></summary>

### 🚨 Immediate Actions

1. 🔒 Remove exposed database backups and confidential documents from publicly accessible locations.
2. 🔐 Restrict access to patient and staff-related resources.
3. 📋 Review web server access logs for suspicious requests.
4. 🔑 Rotate credentials or secrets that may have been exposed.
5. ✅ Confirm that sensitive files are no longer accessible without proper authorisation.

### ⏳ Short-Term Improvements

- Implement proper authentication and server-side authorisation.
- Store confidential files outside the public web root.
- Apply strong encryption to backup files.
- Use strong and unique passwords for encrypted documents.
- Disable unnecessary directory listing.
- Remove sensitive path information from public robots.txt files.
- Review legacy and unused application resources.

### 📅 Long-Term Improvements

- Establish a secure backup management policy.
- Conduct regular vulnerability assessments.
- Perform periodic access-control reviews.
- Implement centralised logging and monitoring.
- Provide security awareness training for personnel.
- Establish an incident response process for suspected data exposure.

### 🎯 Recommended Remediation Priority

| Priority | 🛠️ Action |
|---|---|
| 🔴 1 | Secure the exposed database backup |
| 🔴 2 | Restrict access to confidential patient documents |
| 🟠 3 | Review and strengthen PDF protection |
| 🟡 4 | Audit exposed and legacy web resources |
| 🟢 5 | Reduce unnecessary technology disclosure |

</details>

---

<details>
<summary><strong>06 | 📝 Conclusion</strong></summary>

The Week 4 penetration testing exercise demonstrated how exposed web resources, weak document protection, and insufficiently secured backup files can contribute to confidential data exposure.

The assessment successfully documented access to restricted PDF reports, password recovery evidence, and the discovery of a database backup containing sensitive organisational information.

These findings highlight the importance of implementing proper access controls, protecting confidential files, and securing backup storage.

The exercise also reinforced the importance of documenting each finding with supporting evidence, assessing its potential impact, and providing practical remediation recommendations.

All activities were conducted within the authorised training scope. The findings in this report are based on the evidence collected during the exercise and should be validated through remediation and an authorised retest.

</details>





</details>

---

<details>
<summary><strong>👤 Author and Project Information</strong></summary>

**👤 Author:** Cedrick Zion K. Padonga  
**🎓 Program:** NetworkWalks Cybersecurity Training  
**👥 Batch:** B084  
**🏥 Project:** Mediroza General Hospital – Week 4  
**📑 Module:** M4 – Penetration Testing Report

🔗 LinkedIn: [Cedrick Padonga](https://www.linkedin.com/in/cedrick-padonga-82bb94310/)

</details>

---

## ⚖️ Disclaimer

This repository is intended for educational and research purposes only. The activities documented were conducted within an authorised cybersecurity training environment.

🛡️ Never perform penetration testing against systems without explicit written permission from the owner. Unauthorised access or misuse of security tools may violate applicable laws and regulations.

The author and training organisation are not responsible for unauthorised use of the information presented in this repository.

---

<p align="center">
  <strong>🔐 Learn • Test • Secure • Document</strong>
  <br>
  <sub>NetworkWalks | Cybersecurity Training | Week 4</sub>
</p>
