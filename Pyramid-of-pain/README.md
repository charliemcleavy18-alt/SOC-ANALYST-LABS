# Case Study: The Summit (TryHackMe)
**Role:** Junior SOC Analyst  
**Objective:** Investigate and mitigate a multi-stage malware campaign using the Pyramid of Pain.

## 🛡️ Executive Summary
In this simulation, I acted as a SOC Analyst tasked with identifying malicious activity across various stages of the Pyramid of Pain for "PicoSecure". I moved from simple Hash identification to identifying TTPs (Tactics, Techniques, and Procedures). 

## 🔍 Investigation Workflow
### 1. Hash & IP Analysis (The "Easy" Tier)
Firstly i identified the MD5 hash associated with the sample1.exe and added it to the blacklist

<img width="1900" height="797" alt="1" src="https://github.com/user-attachments/assets/63e93b56-2304-4577-8b6c-399dbcbce2ba" />


For the second sample (sample2.exe) I detected the IP Address 154.35.10.113 and created a Firewall Rule to Deny Egress connections from this IP, meaning that any connection attempting to reach out to this IP will be blocked

<img width="1067" height="237" alt="2" src="https://github.com/user-attachments/assets/e8eb52f4-1925-4f5f-a00c-00eb20f43cbb" />


### 2. Tooling & Artifacts


### 3. TTP Identification (The "Tough" Tier)


## 🏆 Key Skills Demonstrated

