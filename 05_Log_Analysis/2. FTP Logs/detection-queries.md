# FTP Log - Splunk Queries

## Environment
- SIEM: Splunk Enterprise
- Index: ftp_logs
- Sourcetype: ftp_log

## 1. Binary Payloads in FTP Commands

**Objective:** Detect FTP commands containing non-ASCII or binary data (exploit attempts).

```spl
index=ftp_logs
| where match(command, "[^[:print:]]")
| table _time src_ip dst_ip command
```

**Severity:** High
**MITRE ATT&CK:** T1190 – Exploit Public-Facing Application



## 2. Excessively Long FTP Command Arguments

**Objective:** Identify oversized FTP commands that may indicate buffer overflow attempts.

```spl
index=ftp_logs
| eval cmd_length=len(command)
| where cmd_length > 100
| table _time src_ip dst_ip command cmd_length
```

**Severity:** High
**MITRE ATT&CK:** T1059 – Command and Scripting Interpreter


## 3. Abnormal Use of APPE Command

**Objective:** Detect suspicious usage of the APPE command for payload delivery.

```spl
index=ftp_logs command=APPE
| table _time src_ip dst_ip command
```

**Severity:** Medium
**MITRE ATT&CK:** T1105 – Ingress Tool Transfer



## 4. Repeated FTP Exploit Attempts from Same Host

**Objective:** Identify hosts repeatedly issuing suspicious FTP commands.

```spl
index=ftp_logs
| where match(command, "[^[:print:]]")
| stats count by src_ip
| where count > 5
```

**Severity:** High
**MITRE ATT&CK:** T1027 – Obfuscated Files or Information
