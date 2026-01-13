# Phishing Incident Response Playbook

## 1. Overview
This playbook outlines the response procedures for phishing incidents involving malicious emails, credential harvesting, or social engineering attempts.

## 2. Incident Scope
- Suspicious or malicious emails reported by users
- Emails containing malicious links or attachments
- Credential harvesting attempts

## 3. Detection
- User-reported phishing emails via security mailbox or ticketing system
- Email security gateway alerts (e.g., malicious links, attachments, spoofed domains)
- SIEM alerts for suspicious email activity

### Phishing Email Analysis (SOC Analyst Actions)
- Review email headers for sender authenticity and routing anomalies
- Analyze sender domain and check for spoofing or lookalike domains
- Inspect URLs using URL analysis tools (sandbox, reputation services)
- Detonate attachments in a sandbox environment
- Identify indicators of compromise (IOCs):
  - Malicious IP addresses
  - Domains
  - URLs
  - File hashes
- Determine phishing type:
  - Credential harvesting
  - Malware delivery
  - Business Email Compromise (BEC)


## 4. Triage
- Validate whether the email is malicious
- Determine user interaction (clicked link, opened attachment, submitted credentials)
- Assess scope (single user vs multiple recipients)
- Assign severity level (Low / Medium / High)
   - Low: Generic phishing attempt with no user interaction
   - Medium: User clicked link or downloaded attachment
   - High: Credentials submitted or malware executed
- Decide escalation path

## 5. Phishing Investigation Checklist

### Email Analysis
- [ ] Capture original email (EML or headers)
- [ ] Verify sender domain and display name
- [ ] Check for domain spoofing or lookalike domains
- [ ] Analyze email headers for anomalies

### URL and Attachment Analysis
- [ ] Inspect embedded URLs using reputation tools
- [ ] Detonate attachments in sandbox
- [ ] Identify malware or credential harvesting behavior
- [ ] Extract IOCs (URLs, IPs, domains, file hashes)

### User Impact Assessment
- [ ] Identify recipients of the phishing email
- [ ] Confirm whether links were clicked
- [ ] Confirm whether credentials were submitted
- [ ] Identify affected endpoints or accounts

### Scope and Severity
- [ ] Determine if incident is isolated or widespread
- [ ] Assign severity level (Low / Medium / High)
- [ ] Decide if escalation is required


## 6. Containment
- Quarantine malicious emails across all mailboxes using the email security platform
- Block malicious sender domains, IP addresses, and URLs at:
  - Email gateway
  - Secure web gateway / proxy
  - Firewall (if applicable)
- Disable or temporarily suspend affected user accounts if credential compromise is confirmed
- Revoke active sessions and OAuth tokens for impacted accounts
- Prevent further delivery by creating email filtering rules based on identified IOCs


## 7. Eradication & Recovery
- Force password resets for affected users
- Re-enable multi-factor authentication (MFA) where applicable
- Remove malicious files or artifacts from endpoints
- Conduct endpoint scans using EDR or antivirus tools
- Restore systems from known-good backups if malware execution occurred
- Monitor affected accounts for signs of continued suspicious activity


## 8. Post-Incident Actions
- Conduct a post-incident review to identify root cause
- Update phishing detection rules and SIEM correlation logic
- Add new indicators of compromise (IOCs) to threat intelligence feeds
- Provide targeted security awareness training to affected users
- Document incident details, actions taken, and lessons learned

## 9. Escalation Criteria
- Phishing email delivered to multiple users or departments
- Credentials entered into a malicious site
- Privileged, executive, or administrator accounts targeted
- Evidence of mailbox access, forwarding rules, or lateral movement
- Indicators of data access or exfiltration


## 10. MITRE ATT&CK Mapping
- T1566: Phishing
- T1566.001: Spearphishing Attachment
- T1566.002: Spearphishing Link
- T1056: Input Capture (Credential Harvesting)
- T1078: Valid Accounts

