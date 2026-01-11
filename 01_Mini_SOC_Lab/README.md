#Mini SOC Lab – Attack Detection & Incident Response

##Overview
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
This project simulates a **real-world Security Operations Center (SOC)** environment to demonstrate hands-on experience with **log collection, threat detection, alerting, and incident response**.

The lab recreates common attacker techniques such as **RDP brute-force attacks, malicious PowerShell execution, and suspicious process creation**, while leveraging **Sysmon and Splunk** for detection and investigation.

This project is designed to mirror **Tier 1 / Tier 2 SOC analyst workflows**.


##Lab Components
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- **Windows 10 VM** – Victim / Target Machine

- **Kali Linux VM** – Attacker Machine

- **Sysmon** – Endpoint telemetry generation

- **Splunk Enterprise (Free)** – Log ingestion, detection, and analysis


##Architecture Flow
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
        Kali Linux (Attacker)
               |
               |RDP / Network Traffic
               v
        Windows 10 (Victim)
               |
               | Sysmon + Windows Event Logs
               v
         Splunk SIEM



#Attack Scenarios Simulated
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 1️⃣ RDP Brute-Force Attack

- Tool: `hydra`
- Target: Windows RDP service
- Logs Generated:
  - Windows Security Event ID **4625** (Failed Logon)
  - Windows Security Event ID **4624** (Successful Logon)

### 2️⃣ Malicious PowerShell Execution

- Technique: Base64-encoded PowerShell command
- Payload: `calc.exe`
- Detection:
  - Sysmon Event ID **1** (Process Creation)
  - Suspicious use of `-EncodedCommand`

### 3️⃣ Suspicious Executable Execution

- Created fake malware:
copy notepad.exe evil.exe
evil.exe
- Detection:
- Sysmon Event ID **1**
- File hash analysis (MD5, SHA256)


#Alerts Created in Splunk
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

###Alert 1: RDP Brute-Force Detection

**Description:** Detects multiple failed RDP login attempts from a single source.

**SPL Query:**
```spl
index=security EventCode=4625| stats count by Account_Name, Source_Network_Address| where count > 5 ```

Trigger: More than 5 failed attempts in 5 minutes

Severity: High

File: Splunk-Alerts/brute-force-alert.txt

###Alert 2: Suspicious PowerShell Encoded Command
Description: Detects encoded PowerShell execution.

SPL Query:


index=sysmon EventCode=1 Image="*powershell.exe" CommandLine="*-enc*"
Severity: Medium

File: Splunk-Alerts/powershell-alert.txt

🔔 Alert 3: Unknown Outbound Network Connection
Description: Detects outbound connections to non-internal IPs.

SPL Query:

spl
Copy code
index=sysmon EventCode=3
| where NOT (
    cidrmatch("10.0.0.0/8", DestinationIp) OR
    cidrmatch("172.16.0.0/12", DestinationIp) OR
    cidrmatch("192.168.0.0/16", DestinationIp)
)
Severity: Medium

File: splunk-alerts/outbound-connection-alert.txt

🕵️ Incident Investigation
📄 Incident: RDP Brute Force Attack
A successful RDP login was detected after multiple failed attempts from an internal IP, indicating potential lateral movement or compromised internal host.

📁 Full report available at:
incident-reports/brute-force-report.md

Investigation Highlights
Identified attacker source IP

Confirmed targeted account

Correlated failed and successful logons

Detected post-compromise activity using Sysmon

Assessed risk and recommended mitigations

🧾 Evidence Collected
Windows Security Logs (4624, 4625)

Sysmon Logs (Event IDs 1 and 3)

Process execution details

Network connection telemetry

Hash values for suspicious executables

Sample logs available in:
logs-samples/sample-sysmon-events.json

🛠️ Tools & Technologies Used
Splunk Enterprise (Free)

Sysmon (Sysinternals)

Kali Linux

Hydra

Windows Event Logging

PowerShell

Git & GitHub

📈 Skills Demonstrated
SOC alert creation and tuning

Log analysis and correlation

Incident investigation & reporting

Windows endpoint monitoring

MITRE ATT&CK-aligned attack detection

SIEM usage (Splunk)

Security documentation

📌 Future Improvements
Add Sigma rule equivalents

Integrate MITRE ATT&CK mappings

Automate log parsing with Splunk props/transforms

Add additional attack scenarios (C2 beaconing, persistence)

📬 Author
Suraj Saheen
Cybersecurity | SOC Analyst (Aspiring)
GitHub: https://github.com/Suraj-Saheen
