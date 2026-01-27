# Incident Report – Suspicious HTTP Activity

## Incident Summary

Suspicious HTTP activity was detected from internal hosts (**192.168.202.102** and **192.168.203.63**) exhibiting abnormal request behavior, including repeated login attempts and directory brute-force scanning. This activity is consistent with **web-based exploitation attempts** and **reconnaissance activity**.

---

## Detection Method

The incident was detected using Splunk alerts for:
- Repeated failed HTTP login attempts (`POST /login`)
- High-frequency HTTP requests from a single source
- Abnormal usage of the `HEAD` method
- Known scanning tool User-Agents (e.g., DirBuster)

---

## Timeline
### 1. Login Brute-Force Attempt
- **First suspicious event from IP - 192.168.202.102:** 16-03-2012 23:42:51 IST 
- **Last suspicious event from IP - 192.168.202.102:** 16-03-2012 23:423:24 IST 
### 2. Directory Brute-Force / Enumeration Attack
- **First suspicious event from IP - 192.168.203.63:** 16-03-2012 21:34:47 IST 
- **Last suspicious event from IP - 192.168.203.63:** 16-03-2012 23:58:11 IST 

---

## Affected Assets

- **Host IPs:**
  - 192.168.202.102
  - 192.168.203.63
- **Network Segment:** Internal LAN
- **Service Targeted:** HTTP (port 80)
- **Target Server:** 192.168.229.101

---

## Indicators of Compromise (IOCs)

- **Source IPs:**
  - `192.168.202.102`
  - `192.168.203.63`

- **Suspicious Requests:**
  - Repeated `POST /login` requests with 404 responses
  - `HEAD` requests to random or non-existent directories

- **User-Agent Indicators:**
  - `Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1)`
  - `DirBuster-0.12 (http://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)`

---

## Analysis

The HTTP sessions from the affected hosts showed two distinct malicious patterns:

1. **Login Brute-Force Attempt**
   - Multiple POST requests to `/login` within milliseconds.
   - Uniform payload sizes and rapidly changing source ports.
   - Consistent 404 responses indicate failed authentication attempts.

2. **Directory Enumeration Scan**
   - High-volume HEAD requests to random and uncommon directories.
   - User-Agent explicitly identifies the DirBuster scanning tool.
   - All responses returned 404, indicating unsuccessful directory discovery.

These behaviors strongly indicate **automated attack activity** and **web reconnaissance**.

---

## Root Cause

The most likely cause is **compromised internal hosts** or misuse of internal systems to perform unauthorized scanning and attack activities against internal web infrastructure.

---

## Impact

- No successful authentication or data exfiltration was observed.
- However, the behavior represents a **high security risk** and could lead to exploitation if not addressed.
- Indicates possible lateral movement or insider threat behavior.

---

## Recommendations

- Immediately isolate affected hosts.
- Block source IPs at firewall and WAF levels.
- Enable rate limiting and CAPTCHA on login endpoints.
- Implement account lockout policies.
- Monitor for follow-up exploitation attempts.
- Conduct endpoint security scans on affected systems.

---

## Evidence

- HTTP logs showing repeated `POST /login` attempts (screenshots in `screenshots/` directory).
- HTTP logs showing DirBuster directory scanning activity.
- Splunk dashboards highlighting abnormal request rates and tool identification.
- Detection queries used for alerting and investigation.

