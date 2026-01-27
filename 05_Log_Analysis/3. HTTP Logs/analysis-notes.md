# Analysis Notes – HTTP Log Investigation

## Date
2026-01-27

## Analyst
Suraj

---

## Log Source Details
- Log Type: HTTP
- File Name: http.log.gz
- Time Range Analyzed: All available logs
- Total Events: ~2M

---

## Observed Activities

### 1. Login Brute-Force Attempt

- Source IP: 192.168.202.102
- Destination IP: 192.168.229.101
- Method: POST
- URI: /login
- Status Code: 404 (Not Found)
- User-Agent: Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1)

#### Behavior:
- Multiple POST requests to `/login` within milliseconds.
- Rapidly changing source ports.
- Uniform payload sizes.
- All attempts failed.

#### Assessment:
This activity is consistent with a **brute-force or credential stuffing attack** targeting a web login endpoint.

---

### 2. Directory Brute-Force / Enumeration Attack

- Source IP: 192.168.203.63
- Destination IP: 192.168.229.101
- Method: HEAD
- Status Code: 404 (Not Found)
- User-Agent: DirBuster-0.12 (OWASP DirBuster)

#### Behavior:
- High-volume HEAD requests to random-looking directories.
- All responses returned 404.
- Requests occur within the same second.
- User-Agent explicitly identifies DirBuster tool.

#### Assessment:
This activity is a **directory brute-force / web content discovery scan**, often used during reconnaissance.

---

## Correlation Summary

| Source IP        | Attack Type                | Target              |
|------------------|----------------------------|---------------------|
| 192.168.202.102  | Login brute-force          | /login              |
| 192.168.203.63   | Directory enumeration scan | Web directories     |

No successful authentication or valid directory discovery was observed during the timeframe.

---

## Risk Assessment

- Both activities represent **active web reconnaissance and attack attempts**.
- Indicates potential lateral movement and internal threat actor behavior.
- Could precede exploitation or privilege escalation.

---

## Recommended Actions

- Block both source IPs at firewall/WAF.
- Enable rate limiting on login endpoints.
- Implement account lockout policies.
- Monitor for follow-up exploitation attempts.
- Escalate to Tier 2 SOC for deeper investigation.
