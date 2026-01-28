# Detection Queries – SSH Logs (Splunk)

## Environment
- SIEM: Splunk
- Index: ssh_logs
- Sourcetype: ssh

---

## 1. Detect Failed SSH Login Attempts

```spl
index=ssh_logs sourcetype=ssh auth_result=failure
| stats count by src_ip, dest_ip
| where count > 3
```

## 2. Detect SSH Brute-Force Attempts

```spl
index=ssh_logs sourcetype=ssh auth_result=failure
| bucket _time span=5m
| stats count by src_ip, _time
| where count > 10
```


## 3. Detect Inbound SSH Connections from Unusual IPs

```spl
index=ssh_logs sourcetype=ssh direction=INBOUND
| stats count by src_ip
| where count > 5
```


## 4. Detect Deprecated or Vulnerable SSH Versions

```spl
index=ssh_logs sourcetype=ssh
| stats values(client_version), values(server_version) by dest_ip
```

## 5. Detect High-Volume Failed SSH Logins

```spl
index=ssh_logs sourcetype=ssh auth_result=failure
| bucket _time span=5m
| stats count by src_ip, dest_ip, _time
| where count > 50

