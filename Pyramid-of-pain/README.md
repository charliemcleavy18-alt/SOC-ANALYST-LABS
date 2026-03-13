# Case Study: The Summit (TryHackMe)
**Role:** Junior SOC Analyst  
**Objective:** Investigate and mitigate a multi-stage malware campaign using the Pyramid of Pain.

## 🛡️ Executive Summary
In this lab, I transitioned from identifying simple Indicators of Compromise (IoCs) like hashes and IP addresses to detecting high-level Tactics, Techniques, and Procedures (TTPs). By implementing Sigma rules and monitoring registry changes, I successfully neutralized a multi-stage attack and documented the defensive mitigations.

## 🔍 Investigation Workflow
### 1. Hash & IP Analysis (The "Easy" Tier)
Firstly i identified the MD5 hash associated with the sample1.exe and added it to the blacklist

<img width="1900" height="797" alt="1" src="https://github.com/user-attachments/assets/63e93b56-2304-4577-8b6c-399dbcbce2ba" />


For the second sample (sample2.exe) I detected the IP Address 154.35.10.113 and created a Firewall Rule to Deny Egress connections from this IP, meaning that any connection attempting to reach out to this IP will be blocked

<img width="1067" height="237" alt="2" src="https://github.com/user-attachments/assets/e8eb52f4-1925-4f5f-a00c-00eb20f43cbb" />

### 2. DNS/Domains (Simple)

After neautralizing initial hashes and IP's I had to identify the Domains that the adversary was making connections to in order to obtain C2 callback (command-and-control).
<img width="1372" height="854" alt="dns" src="https://github.com/user-attachments/assets/5d702ac5-e2d4-4360-979d-4685c5aad01c" /> <br>
<br>

**Marker 1:** Shows the sequence of requests where the process fetches the backdoor.exe payload.

**Marker 2:** Highlights the specific DNS request that provided the trigger for the block rule.


**Detection:** Analyzing the network activity of sample3.exe (PID 1021) revealed persistent HTTP GET requests and DNS resolutions to a suspicious external domain.

**Indicator:** Malicious Domain: emudyn.bresonicz.info


<img width="1885" height="549" alt="3" src="https://github.com/user-attachments/assets/87a46dd1-ff05-44e4-b621-556811749f71" /> <br>
<br>

Mitigation: Created a DNS filter rule named "Backdoor" to deny all traffic to this domain. This prevents the malware from resolving its C2 server, effectively "killing" the connection even if the attacker changes the underlying IP address.


### 3. Tooling & Artifacts


### 4. TTP Identification (The "Tough" Tier)


## 🏆 Key Skills Demonstrated

