# Analysis Notes – SSH Log Investigation

## Date
2026-01-28 
## Analyst
Suraj

---

## Log Source Details
- Log Type: SSH
- File Name: ssh.log.gz
- Time Range Analyzed: All available logs
- Total Events Reviewed: ~8000

---

## Initial Observations

- A single source IP (`192.168.202.141`) generated over 2000 failed SSH login attempts.
- The destination host (`192.168.229.101`) was targeted on port 22.
- Approx 2000+ login attempts, all authentication attempts resulted in failure.
- The attempts occurred within a short time window (8 minutes), indicating automation.

---

## Behavioral Analysis

- The volume and speed of attempts indicate a brute-force or credential stuffing attack.
- No successful logins were observed.
- This activity pattern is inconsistent with legitimate user behavior.

---

## Correlation

- No corresponding successful authentication events were found.
- No legitimate SSH sessions from this source IP were identified.

---

## Preliminary Assessment

This activity represents a **high-confidence SSH brute-force attack** against an internal host.

---

## Recommended Actions

- Immediately block the source IP.
- Enable account lockout and rate limiting on SSH services.
- Switch to key-based authentication and disable password logins.
- Escalate to Tier 2 SOC.
