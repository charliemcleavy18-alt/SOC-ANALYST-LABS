# Case Study: The Summit (TryHackMe)
**Role:** Junior SOC Analyst  
**Objective:** Investigate and mitigate a multi-stage malware campaign using the Pyramid of Pain.

## 🛡️ Executive Summary
In this simulation, I acted as a SOC Analyst tasked with identifying malicious activity across various stages of the Pyramid of Pain. I moved from simple Hash identification to identifying TTPs (Tactics, Techniques, and Procedures).

## 🔍 Investigation Workflow
### 1. Hash & IP Analysis (The "Easy" Tier)
* **Observation:** Identified malicious file `[File_Name]` with MD5 hash `[Hash_Value]`.
* **Action:** Pivot to VirusTotal/Internal Logs to identify C2 infrastructure at `[IP_Address]`.

### 2. Tooling & Artifacts
* **Discovery:** Found evidence of `[Tool Name, e.g., Mimikatz or Netcat]` being used for lateral movement.
* **Mitigation:** Updated firewall rules to block the specific C2 domain.

### 3. TTP Identification (The "Tough" Tier)
* **Technique:** Observed the attacker using **[MITRE T1059]** (Command and Scripting Interpreter).
* **Framework Alignment:** This mapped directly to the **Exploitation** phase of the Cyber Kill Chain.

## 🏆 Key Skills Demonstrated
* **Detection Engineering:** Creating Sigma/YARA rules to detect the observed behavior.
* **Pyramid of Pain Application:** Moving beyond simple indicators to high-level behavioral blocking.
