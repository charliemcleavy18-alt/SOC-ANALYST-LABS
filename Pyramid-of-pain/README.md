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

**Mitigation:** Created a DNS filter rule named "Backdoor" to deny all traffic to this domain. This prevents the malware from resolving its C2 server, effectively "killing" the connection even if the attacker changes the underlying IP address.


### 3. Tooling & Artifacts

At this stage, the adversary began attempting to manipulate the host's internal security settings to evade detection. I focused on identifying Registry Artifacts—specific footprints left in the Windows Registry.

**1. Defense Evasion: Disabling Windows Defender**

Observation : The malware (sample4.exe) attempted to impair the system's defenses by modifying the Registry.

Registry Key: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection

Registry Name: DisableRealtimeMonitoring

Value Change: Set to 1 (Disabled).

Detection Logic: I developed a Sigma Rule targeting Sysmon Event ID 13 (Registry Value Set) to alert on any attempts to disable real-time protection.

MITRE ATT&CK Mapping: T1562.001 - Impair Defenses: Disable or Modify Tools.

   <img width="1096" height="731" alt="4" src="https://github.com/user-attachments/assets/660f9a2a-494d-4993-a897-213d7b0d6963" />
<br>

**2. Network Beaconing (Tooling Artifacts)**
  ![connection logs](https://github.com/user-attachments/assets/ae4082f9-03b9-4bfe-a041-5653ae8c6bcf)
  <br>
**Detection:** Analysis of the 12-hour network logs revealed a highly consistent "heartbeat" or beaconing pattern.

**Artifact:** Regular outbound connections to 51.102.10.19 every 1800 seconds with a fixed packet size of 97 bytes.

**Significance:** This suggests automated Command & Control (C2) software rather than human activity.

**Detection Logic:** Created a behavioral Sigma rule to flag any egress traffic matching this exact frequency and size profile, making it resistant to simple IP changes.

**Blocking a registry key or a beaconing pattern is 'Annoying' for an attacker. Unlike a hash, they can't just recompile the code. They have to re-program their tool's persistence logic or change their C2 communication          intervals, which costs them time and research.**


### 4. TTP Identification (The "Tough" Tier)
![command logs for ttp](https://github.com/user-attachments/assets/741d1c2a-2af0-4241-9216-80b42d604b05)
<br>
As seen within the logs, the Malware is sending information to "%temp%\exfiltr8.log" file. This is enough information to create a Sigma Rule
<br>
<br>
Now before the rule can be created, we need to add the information we gained from the connection.log file. Starting with the file path is where the file is located, this would be %temp% . Next up is the filename, which is exfiltr8.log . Lastly, we have choose the correct ATT&CK ID what matches what the Sphinx is trying to do. In this case, they are trying to Exfiltrate data meaning Exfiltration (TA0010) is what we want to choose. Finally, click on the Validate Rule button.
<br>
<br>
![TTP](https://github.com/user-attachments/assets/bffc7c68-c85e-4383-af4e-050b188d0729)
<br>
<br>

## 🏆 Key Skills Demonstrated
Indicator Lifecycle Management: Demonstrated the ability to identify and neutralize threats across all tiers of the Pyramid of Pain, from trivial hashes to complex TTPs.

Detection Engineering (Sigma): Authored behavioral detection rules using Sigma syntax to identify Defense Evasion (Registry manipulation) and automated C2 beaconing.

Traffic & Log Analysis: Performed deep-packet and log analysis (Sysmon Event ID 3 & 13) to differentiate between legitimate administrative activity and malicious heartbeats.

Threat Mapping (MITRE ATT&CK): Successfully mapped observed adversary behaviors to the MITRE ATT&CK framework, specifically T1562.001 (Impair Defenses) and T1071.001 (Application Layer Protocol).

Infrastructure Mitigation: Implemented defensive controls at the network level via DNS Sinkholing and IP blacklisting to disrupt command-and-control (C2) channels.

Analytical Documentation: Translated complex technical investigations into a structured Incident Report suitable for both technical and executive review.
