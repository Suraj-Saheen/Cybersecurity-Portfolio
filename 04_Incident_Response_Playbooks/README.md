# Incident Response Playbooks

## Overview
This project contains incident response playbooks designed to demonstrate **Security Operations Center (SOC) operational readiness**. The playbooks align with the **NIST Incident Response Lifecycle (SP 800-61)** and the **MITRE ATT&CK framework**, providing structured, repeatable response procedures for common enterprise security incidents.

## Included Playbooks
- **Phishing Incident Response Playbook**
- **Malware Incident Response Playbook**
- **Account Compromise Incident Response Playbook**

Each playbook follows a consistent format covering detection, triage, investigation, containment, recovery, and escalation.



## Incident Scope
The playbooks address common security incidents that impact:
- End users and email systems
- Endpoints and servers
- Identity and access management systems

They are written to reflect **real-world SOC workflows** and decision-making processes.


## NIST Incident Response Lifecycle Alignment
These playbooks align with the phases defined in **NIST SP 800-61**:

1. **Preparation**
2. **Detection & Analysis**
3. **Containment**
4. **Eradication & Recovery**
5. **Post-Incident Activity**



## Response Flow (High-Level)
1. Alert Detection or User Report 
2. Initial Analysis and Validation 
3. Triage and Severity Classification 
4. Investigation and Scoping 
5. Containment Actions 
6. Eradication and Recovery 
7. Lessons Learned and Documentation 



## Incident Response Flowchart

```text
[ Alert / User Report ]
           |
           v
[ Detection & Analysis ]
           |
           v
[ Triage & Severity Assessment ]
           |
     +-----+-----+
     |           |
     v           v
[ Low / Medium ] [ High / Critical ]
     |           |
     v           v
[ Containment ] [ Escalation to IR Team ]
     |           |
     v           v
[ Recovery ]   [ Executive Notification ]
     |
     v
[ Lessons Learned ]
```

## Escalation Matrix

| Severity | Description                                      | Escalation Level            |
|:-------- :|:------------------------------------------------:|:---------------------------:|
| Low      | Single user affected, no confirmed impact        | Tier 1 SOC                  |
| Medium   | Multiple users or systems impacted               | Tier 2 SOC                  |
| High     | Privileged access, malware spread, or ransomware | Tier 3 / IR Team            |
| Critical | Business-wide impact or data breach              | CISO / Executive Management |


## Frameworks Used
- NIST SP 800-61 - Computer Security Incident Handling Guide
- MITRE ATT&CK - Adversary Tactics, Techniques, and Procedures

---

## Author

**Name:** Suraj Saheen 
**Role:** Cybersecurity | SOC Analyst (Aspiring)
**Email:** surajsaheen@gmail.com
**GitHub:** https://github.com/Suraj-Saheen
**LinkedIn:** https://www.linkedin.com/in/suraj-saheen-a0912a394

This repository was created to demonstrate practical SOC operational knowledge, structured incident response methodologies, and alignment with industry standards such as **NIST SP 800-61** and **MITRE ATT&CK**.

