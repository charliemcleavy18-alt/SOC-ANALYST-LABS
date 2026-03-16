# Case Study: Snapped Phish-ing
**Role:** Junior SOC Analyst  
**Objective:** Investigate phishing emails and perform analysis


<br>
<br>
<br>

## 🛡️ Executive Summary
In this lab i conducted analysis of a live phishing campaign. The investication involved working with malicious .zip files whilst utilising cyberchef to defang any harmful URLs, tracing stolen credentials to an exfiltration email address.


## Phase 1: Initial Investigation
<br>
<br>
<br>
<img width="726" height="308" alt="2" src="https://github.com/user-attachments/assets/f4b7f5d3-12b9-44fb-9aa3-372c06d4d38e" />

<img width="647" height="549" alt="3" src="https://github.com/user-attachments/assets/ac3ad513-01d8-4609-90eb-31e5b9c724e1" />

<br>
<br>
Within the email there was a suspicious email attachment (Direct Credit Advice.html). Using the Linux cat command, I identified the link was redirecting victims to the malicious domain: kennaroads[.]buzz. As seen above, I utilised CyberChef to defang the URL so that it is not accidentally clicked. An important safety procedure.

<br>
<br>

## Phase 2: C2 Server discovery & File analysis.
<br>
<br>
<br>

