# Incident Report – Suspicious SSH Activity

## Incident Summary

An SSH brute-force attack was detected involving over 2000 failed authentication attempts within an 8-minute window. The attack originated from an internal host and targeted an internal SSH server, representing a high-risk security incident.

---

## Detection Method

The incident was detected using Splunk alerts for:
- High volumes of failed SSH authentication attempts
- Rapid sequential SSH failures from a single source
- Abnormal inbound SSH traffic patterns

---

## Timeline
- **First suspicious event:** 18-03-2012 01:11:13 IST 
- **Last suspicious event:** 18-03-2012 01:19:07 IST 
---

## Affected Assets

- **Source IP:** 192.168.202.141 
- **Destination IP:** 192.168.229.101 
- **Service Targeted:** SSH (port 22)

---

## Indicators of Compromise (IOCs)

- **Source IP:** `192.168.202.141`
- **Destination IP:** `192.168.229.101`
- **Protocol:** SSH
- **Authentication Result:** Failure
- **Attempt Volume:** 2000+ failures in 8 minutes

---

## Analysis

The observed behavior is consistent with an automated SSH brute-force attack. The volume and frequency of login attempts far exceed normal user behavior. No successful authentication attempts were observed during the incident window.

---

## Root Cause

The most likely cause is **malware infection** or unauthorized tool usage on the source host, resulting in automated credential guessing attempts.

---

## Impact

- No confirmed system compromise.
- High risk of unauthorized access if credentials are weak.
- Increased load on authentication services.

---

## Recommendations

- Immediately isolate and investigate the source host.
- Block the source IP at firewall and IDS/IPS levels.
- Enforce key-based authentication and disable password logins.
- Apply account lockout and rate limiting controls.
- Conduct endpoint security scans on the source host.
- Review SSH logs for successful logins before and after the incident.

---

## Evidence

- SSH logs showing over 2000 failed authentication attempts.
- Splunk dashboards highlighting brute-force patterns.
- Detection queries used for alerting and investigation.
