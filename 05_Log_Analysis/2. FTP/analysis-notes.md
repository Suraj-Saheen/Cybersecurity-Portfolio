# Analysis Notes – FTP Log Investigation

## Date  
2026-01-19

## Analyst  
Suraj

---

## Log Source Details
- **Log Type:** FTP 
- **File Name:** ftp.log.gz 
- **Time Range Analyzed:** All available logs 
- **Total Events:** ~6000

---

## Initial Observations

1. Two internal hosts (**192.168.202.102** and **192.168.202.118**) issued FTP commands containing **binary and non-ASCII payloads**.
2. The `APPE` and `PORT` commands were used in abnormal ways, including:
   - Extremely long arguments
   - Embedded binary data
   - Repetitive NOP sleds (`\x90\x90\x90...`)
3. Another host (**192.168.202.94**) showed normal FTP usage with valid credentials and legitimate file transfers.

---

## Behavioral Analysis

- The payloads observed in `APPE` and `PORT` commands resemble **shellcode** and **buffer overflow exploit patterns**.
- Repeated sequences such as `\x90\x90\x90`, random binary bytes, and oversized command arguments indicate:
  - **Exploit delivery attempts**
  - Possible **malware propagation** or **unauthorized access attempts**
- The activity was automated and did not follow normal FTP session behavior (USER → PASS → RETR/STOR → QUIT).

---

## Preliminary Assessment

The observed activity strongly suggests:
- **FTP-based exploitation attempts**
- Possible **buffer overflow attacks** or **malware payload delivery**
- High likelihood of **compromised internal hosts**

---

## Recommended Actions

- Immediately **isolate** the affected hosts (`192.168.202.102`, `192.168.202.118`).
- Perform **full malware scans** and **memory forensics**.
- Review FTP server logs for successful exploitation.
- **Block** suspicious IPs and disable FTP if not required.
- Escalate to **Tier 2 SOC** and initiate incident response procedures.

