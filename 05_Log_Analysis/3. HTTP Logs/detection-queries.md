# Detection Queries – HTTP Log Attacks (Splunk)

## Environment
- SIEM: Splunk
- Index: http_logs
- Sourcetype: http

---

## 1. Detect Login Brute-Force Attempts

```spl
index=http_logs sourcetype=http method=POST uri="/login"
| stats count by src_ip, dest_ip
| where count > 5
```


## 2. Detect Repeated Failed Login Attempts

```spl
index=http_logs sourcetype=http method=POST uri="/login" status=404
| stats count by src_ip
| where count > 10
```


## 3. Detect Directory Brute-Force / Enumeration (DirBuster)

```spl
index=http_logs sourcetype=http method=HEAD user_agent="*DirBuster*"
| stats count by src_ip
| where count > 5
```


## 4. Detect High-Frequency HTTP Requests from Single Source

```spl
index=http_logs sourcetype=http
| bucket _time span=1s
| stats count by src_ip, _time
| where count > 10
```

## 5. Detect Scanning of Random or Uncommon Directories

```spl
index=http_logs sourcetype=http method=HEAD status=404
| regex uri=".*[0-9A-Za-z]{10,}.*"
| stats count by src_ip, uri
| where count > 3
```
