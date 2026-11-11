# 🛡️ My Cybersecurity Activity Week 2 – Footprinting and Reconnaissance

**PENETRATION TESTING REPORT**  
**FOOTPRINTING & NETWORK SCANNING PHASES**  
`W2-PM-FINAL` | `CYBERSECURITY` | `NETWORKWALKS`

| Field | Details |
| :--- | :--- |
| **Pentester Name** | Cedrick Zion K. Padonga |
| **Program / Batch** | B084 - Networkwalks |
| **Date** | 9 October 2025 |
| **Modules Completed** | `W2-PM4` (theHarvester)<br>`W2-PM5` (Zenmap Scanning)<br>`W2-PM-FINAL`(Penetration Testing Report) |
| **Client / Target** | 1. `microsoft.com` (Passive OSINT only)<br>2. Local LAN Network (`192.168.5.0/24`) |
| **Permission Secured?** | Yes (Authorized lab scope & personal network) |
| **Phases Covered** | **Phase 1:** Reconnaissance & Footprinting with theHarvester<br>**Phase 2:** Scanning & Network Discovery with Zenmap<br>**Phase 3:** Risk Analysis and Potential Impact <br> **Phase 4:** Recommendations <br>**Phase 5:** Conclusion<br>**Phase 6:** Evidenece Collected |

---

## 1. Liability Disclaimer
> I have performed these activities only on systems and devices where I had authorized scope or on devices and networks that I own myself. All materials in this repository are for educational and research purposes only. Do not use anything from this report to break the law. The instructor, authors, and Networkwalks are not responsible for how this knowledge is used. Every action you take is your own responsibility, as unauthorized access is a crime in most jurisdictions even when no damage occurs.

---

## 2. Introduction
This report covers passive footprinting and reconnaissance of the `microsoft.com` domain using **theHarvester** in Kali Linux (`W2-PM4`), alongside active network scanning of my own local network using **Zenmap** on a Windows PC (`W2-PM5`). Together, these two modules demonstrate how an attacker transitions from collecting publicly available intelligence—such as email addresses, subdomains, and hostnames—to actively probing and mapping live hosts, open ports, and network topology on a target network.

Submitted as the Week 2 deliverable for my ongoing internship program at Networkwalks, every step documented below includes the exact command or scan profile used, the observed output, screenshots as evidence, and an analysis of why the findings matter from an attacker's perspective.

---

## 3. Tools Used
The table below lists each tool used in this report and its purpose.

| Tool | Purpose |
| :--- | :--- |
| **Kali Linux & Windows** | Operating systems used for passive footprinting and active scanning activities. |
| **theHarvester** | Gathers public emails, subdomains, hosts, and banners from search engines and public databases. |
| **Zenmap (Nmap GUI)** | Scans the local subnet to discover live hosts, IP/MAC addresses, and network topology. |
| **Windows CMD** | Identifies local host IP configuration and subnet details via `ipconfig`. |

---

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance (`W2-PM4`)
I performed passive reconnaissance against the `microsoft.com` domain using **theHarvester** in Kali Linux to gather public information—including emails, subdomains, hosts, employee names, open ports, and banners—from search engines, PGP key servers, and public databases.

### 🔍 Interactive Task Walkthrough (`theHarvester`)

Click on each task below to expand the command breakdown, key findings, and terminal screenshot evidence.

<details open>
<summary><strong>📌 Task 1: Targeted Search via Baidu (<code>-b baidu</code>)</strong></summary>
<br>

In the terminal window, I executed the following command to query **Baidu** for up to 1,000 results targeting `microsoft.com`:

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

* **Observed Output:** Returned **1 email pattern** (`*@microsoft.com`) with 0 IPs, people, or hosts listed.
* **Evidence Screenshot:**

<p align="center">
  <img width="450" alt="theHarvester Baidu Scan Evidence" src="https://github.com/user-attachments/assets/b49ace2a-7658-4130-add1-d813ab866c3b" />
</p>

</details>

---

<details>
<summary><strong>📌 Task 2: Broad Multi-Source Search (<code>-b all</code>)</strong></summary>
<br>

In the terminal window, I executed the following command to query **all available data sources** with a limit of 50 results per source:

```bash
theHarvester -d microsoft.com -l 50 -b all
```

* **Observed Output:** Aggregated varying sets of IP addresses, subdomains, and hosts across multiple public sources and certificate logs on each run.
* **Evidence Screenshot:**

<p align="center">
  <img width="600" alt="theHarvester All Sources Scan Evidence" src="https://github.com/user-attachments/assets/19a09dac-edaa-42d3-8807-ae9effc9a033" />
</p>

* 📄 **Raw Output:** [View theHarvester XML Report](./harvest_report.xml)

</details>


---

* **Commands Executed:**
  ```bash
  theHarvester -d microsoft.com -l 1000 -b baidu
  theHarvester -d microsoft.com -l 50 -b all
  ```
* **Key Observation:** After running both commands multiple times, the `-b all` command produced varying results on each run due to search engine rate-limiting and API restrictions, whereas the `-b baidu` command consistently returned the same findings.

---

### 4.2 Network Scanning with Zenmap (`W2-PM5`)
For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required identifying my local IP address and subnet, discovering live hosts, recording their IP and MAC addresses, and generating a visual network topology.

1. **Identify Local Network:** Ran `ipconfig` in Windows CMD to determine my local IP address and LAN subnet.

<p align="center">
<img width="400" height="450" alt="image" src="https://github.com/user-attachments/assets/eca18ca8-4033-4d5e-81f8-c90bef16f735" />
</p>
  
2. **Host Discovery:** Entered the local subnet into Zenmap and executed a **Ping Scan** (`nmap -sn`) to identify active devices.

<p align="center"> 
<img width="500" height="113" alt="image" src="https://github.com/user-attachments/assets/2f3fd444-fa5d-4674-8cd7-b733b121721b" />
</p>

* **How many hosts are live in your subnet?**
  * There are **5 live hosts** (including my host PC) discovered in **11.8 seconds**.

* **Discovered Live Host IP Addresses:**
  * `192.168.5.1`
  * `192.168.5.12`
  * `192.168.5.27`
  * `192.168.5.52`
  * `192.168.5.150`

* **Discovered Hardware MAC Addresses:**
  * `50:0F:F5:21:14:18`
  * `50:0F:F5:20:41:78`
  * `50:0F:F5:21:C4:C8`
  * `86:A3:9E:27:D3:34`

* **Display & Save Output Topology:**
  * After completing the scan, I opened the **Topology** tab in Zenmap, enabled the legend, and exported the network topology map in PDF format as required by the practical task.

---

## 5. Risk Analysis & Potential Impact
Based on the intelligence collected during the footprinting and network scanning phases, I identified the following potential risks:

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Regional Infrastructure Exposure** | Querying Baidu (`-l 1000 -b baidu`) consistently returned the same set of public hosts, subdomains, and email patterns across multiple runs. | Exposed email addresses and corporate naming formats allow an attacker to build a verified recipient list for spear-phishing campaigns. | 🟡 **Low – Medium** |
| **2** | **Attack Surface Mapping** | Querying all sources (`-l 50 -b all`) produced varying sets of IPs, subdomains, and hosts per run alongside API key warnings. | Aggregating certificate transparency logs (`crtsh`), DNS records, and search engines uncovers forgotten staging or legacy subdomains. | 🟠 **Medium** |
| **3** | **Internal Host & MAC Enumeration** | Zenmap's Ping Scan mapped 5 active local devices, their IP assignments, hardware MAC addresses, and network topology. | Provides an attacker on the local network with a complete inventory of live targets and device vendors for targeted port scanning or ARP spoofing. | 🟠 **Medium** |

> **Risk Level Key:** 🔴 Critical | 🟠 Medium | 🟡 Low  
> *Note: The risks above represent intelligence observations from passive reconnaissance and host discovery exercises, not confirmed vulnerabilities. No exploitation or vulnerability validation was performed during these two modules. Further authorized security testing would be required to confirm actual vulnerabilities.*

---

## 6. Recommendations
Based on the observations from these activities, I recommend the following security improvements:

1. **Use Generic Role-Based Emails:** Avoid publishing personal employee email addresses on public websites. Use role-based aliases (e.g., `info@`, `support@`) to protect staff naming conventions from automated harvesters.
2. **Audit and Clean Up Unused Subdomains:** Regularly review DNS records and SSL certificate transparency logs to decommission forgotten staging, testing, or legacy subdomains before attackers discover them.
3. **Enable Host-Based Firewalls & Network Segmentation:** Keep **Windows Defender Firewall** enabled and configured to block unsolicited incoming connections on all local devices, and isolate guest or IoT devices onto separate VLANs.

---

## 7. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering passive footprinting, reconnaissance, and active network scanning.

These exercises showed me that information gathering is a critical first step in cybersecurity, as analyzing public data and network responses reveals a great deal about a target environment before any exploitation occurs. I also learned the importance of clear technical documentation—explaining what was performed, what was discovered, the potential attacker impact, and how to mitigate those risks. Finally, these tasks reinforced that reconnaissance and scanning must always be conducted responsibly and strictly within an authorized scope.

---

## 8. Evidences Collected

### theHarvester Output Evidence
<img width="500" height="500" alt="theHarvester Scan Evidence 1" src="https://github.com/user-attachments/assets/b49ace2a-7658-4130-add1-d813ab866c3b" />

---

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/19a09dac-edaa-42d3-8807-ae9effc9a033" />

### Zenmap Network Scan & Topology Evidence

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/cbe9cc20-d5bb-4859-8bf5-3bdfe42bd170" />

---

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/7b787444-f78f-4309-b630-a3c3ff133fce" />

---

*— End of Report —*

### 👤 Author
**Cedrick Zion K. Padonga**  
Cybersecurity Intern | Batch B084 – Networkwalks  

### 📌 Project Information
**Program Name:** Cybersecurity Program at Networkwalks | **Week:** 02 | **Repository:** GitHub
