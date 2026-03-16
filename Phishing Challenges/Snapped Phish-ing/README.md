# Case Study: Snapped Phish-ing
**Role:** Junior SOC Analyst  
**Objective:** Investigate phishing emails and perform analysis


<br>


## 🛡️ Executive Summary
In this lab i conducted analysis of a live phishing campaign. The investication involved working with malicious .zip files whilst utilising cyberchef to defang any harmful URLs, tracing stolen credentials to an exfiltration email address.


## Phase 1: Initial Investigation
<br>
<br>
<br>
<img width="726" height="308" alt="2" src="https://github.com/user-attachments/assets/f4b7f5d3-12b9-44fb-9aa3-372c06d4d38e" />
<br>
<img width="647" height="549" alt="3" src="https://github.com/user-attachments/assets/ac3ad513-01d8-4609-90eb-31e5b9c724e1" />

<br>
<br>
Within the email there was a suspicious email attachment (Direct Credit Advice.html). Using the Linux cat command, I identified the link was redirecting victims to the malicious domain: kennaroads[.]buzz. 
<br>
As seen above, I utilised CyberChef to defang the URL so that it is not accidentally clicked. An important safety procedure.
<br>

##  Phase 2: C2 Server discovery & File analysis.

<br>
<br>
<img width="913" height="699" alt="4" src="https://github.com/user-attachments/assets/b6b283f3-fce3-4a25-a4b7-fea258a7c9ab" />
<br>
<img width="628" height="621" alt="5" src="https://github.com/user-attachments/assets/7d2c1219-3de1-4406-8e6b-7d39d446db40" />
<br>
Here i enumerated the URL and found that there was a ZIP archive titled "Update365.zip" which was likely to contain the phishing kit.
<br>
I proceded to defang the ZIP using CyberChef for good measure.

<br>
I then downloaded the archive and generated a SHA-256 hash using the terminal. This allowed me to cross reference the file against threat intelligence databases such as VirusTotal.
<br>
<img width="717" height="162" alt="6" src="https://github.com/user-attachments/assets/c867f557-b1cf-48d8-9d5e-00b254caab4c" />
<img width="1009" height="785" alt="7" src="https://github.com/user-attachments/assets/30f37733-59b2-489f-8b9c-570b000876b4" />
<br>

## Phase 3: Exfiltration Trace.
<br>
<img width="765" height="514" alt="9" src="https://github.com/user-attachments/assets/902f3940-d00c-48ac-9c9e-e13b76b2e03b" />
<br>
Using the grep command i was able to filter through the emails. $send is indicitave of where the data was being sent to.
<br>

## Skills demonstrated.
Linux Command Line: File navigation (ls, cd), content inspection (cat), and cryptographic hashing (sha256sum).

Static Analysis: Identifying malicious redirection logic within HTML source code.

Network Reconnaissance: Exploring C2 server structures and identifying exposed sensitive files.

Incident Documentation: Translating raw terminal output into an actionable intelligence report.
