# Account Compromise Incident Response Playbook

## 1. Overview
This playbook outlines response procedures for incidents involving compromised user or privileged accounts.

## 2. Incident Scope
- Unauthorized login attempts
- Suspicious account activity
- Privilege misuse or escalation

## 3. Detection
- SIEM alerts for anomalous authentication activity
- Impossible travel alerts
- MFA bypass or failure alerts
- Identity provider (IdP) alerts

### Account Activity Analysis (SOC Analyst Actions)
- Review authentication logs for suspicious login patterns
- Identify source IPs, locations, and devices
- Review MFA usage and failures
- Identify abnormal account behavior or access attempts
- Identify indicators of compromise (IOCs):
  - IP addresses
  - Devices
  - Locations

## 4. Triage
- Validate suspicious authentication activity
- Identify affected account(s)
- Determine account privilege level
- Assess scope (single account vs multiple accounts)
- Assign severity level (Low / Medium / High)
  - Low: Failed login attempts only
  - Medium: Successful login from suspicious source
  - High: Privileged account or evidence of misuse
- Decide escalation path

## 5. Account Compromise Investigation Checklist

### Authentication Review
- [ ] Review login timestamps and source IPs
- [ ] Identify impossible travel or unusual locations
- [ ] Review MFA status and bypass attempts

### Account Activity
- [ ] Review mailbox rules and forwarding settings
- [ ] Check for privilege changes or role assignments
- [ ] Review access to sensitive systems or data

### Scope Assessment
- [ ] Identify other potentially compromised accounts
- [ ] Check for shared or reused credentials
- [ ] Review logs for lateral movement

### Severity and Escalation
- [ ] Determine if account is privileged
- [ ] Assess risk of data access or exfiltration
- [ ] Decide if escalation is required

## 6. Containment
- Disable or lock compromised accounts
- Revoke active sessions and authentication tokens
- Force password resets
- Enforce or re-enable MFA
- Block malicious IP addresses if applicable

## 7. Eradication & Recovery
- Restore account access securely
- Review and correct account permissions
- Remove unauthorized mailbox rules or access changes
- Monitor account for continued suspicious activity

## 8. Post-Incident Actions
- Conduct access and authentication audits
- Update identity and access management (IAM) policies
- Improve authentication monitoring and alerts
- Document incident details and lessons learned

## 9. Escalation Criteria
- Privileged or administrator account compromised
- Evidence of data access or exfiltration
- Multiple accounts affected
- Signs of lateral movement or persistence

## 10. MITRE ATT&CK Mapping
- T1078: Valid Accounts
- T1110: Brute Force
- T1021: Remote Services
- T1556: Modify Authentication Process

