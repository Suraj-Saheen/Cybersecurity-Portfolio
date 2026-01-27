#DNS Log - Splunk Queries

## Environment
- SIEM: Splunk Enterprise
- Index: dns_logs
- Sourcetype: dns

## 1. High NXDOMAIN Rate (Malware / DGA)

**Objective:** Detect hosts generating excessive failed DNS lookups.

```spl
index=dns_logs response_code=NXDOMAIN
| stats count by src_ip
| where count > 100
```

**Severity:** Medium
**MITRE ATT&CK:** T1071.004 – Application Layer Protocol: DNS



## 2. Long Domain Names (DNS Tunneling Detection)

**Objective:** Identify unusually long domain queries that may indicate tunneling.

```spl
index=dns_logs
| eval domain_length=len(query)
| where domain_length > 50
| table _time src_ip query domain_length
```

**Severity:** High
**MITRE ATT&CK:** T1071.004 – Application Layer Protocol: DNS


## 3. Rare Domain Queries

**Objective:** Detect communication with rarely seen domains (communication with C2 server without getting noticed).

```spl
index=dns_logs
| eval domain_length=len(query)
| where domain_length > 50
| table _time src_ip query domain_length
```

**Severity:** Medium
**MITRE ATT&CK:** T1071.001 – Application Layer Protocol: Web Protocols



## 4. Beaconing Behavior (Regular Interval Queries)

**Objective:** Detect possible malware beaconing patterns.

```spl
index=dns_logs
| bucket _time span=1m
| stats count by src_ip, _time
| eventstats avg(count) as avg_count by src_ip
| where count > avg_count*2
```

**Severity:** High
**MITRE ATT&CK:** T1071 – Application Layer Protocol
