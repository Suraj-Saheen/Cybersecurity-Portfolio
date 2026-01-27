# Incident Report – Suspicious FTP Activity

## Incident Summary

Suspicious FTP activity was detected from internal hosts (**192.168.202.102** and **192.168.202.118**) exhibiting abnormal command usage, including binary payloads, oversized arguments, and exploit-like patterns. This activity is consistent with **FTP-based exploitation attempts** or **malware propagation**.

## Detection Method

The incident was detected using Splunk alerts for:
- Non-ASCII and binary data in FTP commands
- Excessively long FTP command arguments
- Abnormal usage of `APPE` and `PORT` commands
- Repeated exploit-like behavior from the same source IPs

## Timeline

- **First suspicious event:** 2012-03-16 19:39:49 UTC 
- **Last suspicious event:** 2012-03-18 01:52:19 UTC 

## Affected Assets

- **Host IPs:**
  - 192.168.202.102
  - 192.168.202.118
- **Network Segment:** Internal LAN
- **Service Targeted:** FTP (port 21)

## Indicators of Compromise (IOCs)

- **Source IPs:**
  - `192.168.202.102`
  - `192.168.202.118`

- **Suspicious Commands:**
  - `APPE` with binary payload
  - `PORT` with malformed arguments

- **Payload Indicators:**
  - Presence of NOP sleds (`\x90\x90\x90`)
  - Embedded shellcode-like byte sequences

## Analysis

The FTP sessions from the affected hosts contained commands with:
- Random binary data
- Extremely long arguments
- Shellcode patterns and memory manipulation sequences

These characteristics strongly indicate **buffer overflow exploitation attempts** or **malware payload delivery** via FTP. This behavior is abnormal and deviates significantly from legitimate FTP usage, which typically includes readable file paths and standard commands such as `RETR`, `STOR`, or `LIST`.

In contrast, traffic from **192.168.202.94** demonstrated normal FTP behavior with valid authentication and legitimate file downloads, confirming a baseline for comparison.

## Root Cause

The most likely cause is **malware infection** on the affected hosts, potentially originating from phishing, malicious downloads, or exploitation of vulnerable services, resulting in automated exploit attempts against internal FTP servers.

## Impact

There is a high risk of:
- Unauthorized system access
- Malware propagation
- Data compromise or service disruption

No confirmed data exfiltration was identified at this time; however, the threat level remains high.

## Recommendations

- Immediately isolate affected hosts.
- Conduct full malware scanning and memory analysis.
- Patch and harden all FTP services or disable FTP if unnecessary.
- Block identified IOCs at firewall and IDS/IPS levels.
- Reset affected credentials.
- Implement stricter FTP monitoring and alerting thresholds.

## Evidence

- FTP logs showing binary payloads in `APPE` and `PORT` commands(screenshots provided in 'screenshots' directory).
- Splunk dashboards highlighting abnormal command lengths and non-printable characters.
- Detection queries used for identification.
