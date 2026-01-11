#Incident Report: RDP Brute Force Attack
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Incident ID:** IR-2026-001

**Date/Time Detected:** 2026-01-11 19:47:48 UTC

**Reported By:** SOC Team

**Severity:** High

#1. Summary
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

On January 11, 2026, the SOC detected multiple failed Remote Desktop Protocol (RDP) login attempts targeting an internal host (192.168.19.20). The attack originated from source IP 192.168.19.4 and targeted the Administrator(Suraj) account. Immediate alerting and mitigation steps were initiated.

**Type of Attack:** RDP brute-force / credential attack

**Detection Method:** Splunk Security Information and Event Management (SIEM) alert based on Windows EventLog 4625 (failed logon) patterns.

#2. Timeline of Events
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    Time (UTC)   	    |  Event Type	     |  Source IP	|   Target Account         | Host Workstation  |  EventID   |         Notes
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
2026-01-11 19:47:45.999	| Failed RDP login	 | 192.168.19.4	|  Suraj(Administrator)    | 192.168.19.20	   |  4625	    |  First failed login detected
2026-01-11 19:47:45.999	| Failed RDP login	 | 192.168.19.4 |  Suraj(Administrator)    | 192.168.19.20	   |  4625	    |     Second failed login
2026-01-11 19:47:46.021	| Failed RDP login	 | 192.168.19.4	|  Suraj(Administrator)    | 192.168.19.20	   |  4625	    |     Third failed login
2026-01-11 19:47:48.326	| Success RDP login	 | 192.168.19.4	|  Suraj(Administrator)    | 192.168.19.20	   |  4624	    |     Successful login
2026-01-11 19:47:48.326 | SOC Alert Triggered|	N/A	        |      N/A	               |       N/A	       |   N/A	    | Alert triggered after multiple failed attempts
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Note: Additional failed attempts may have occurred; full log review recommended.

#3. Indicators of Compromise (IoCs)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------
   Type	   |    Indicator	        |    Description
--------------------------------------------------------------------------------------
Source IP  |  192.168.19.4	        | Origin of brute-force attempts
Account	   |  Suraj(Administrator)  | Targeted account
Target Host|  192.168.19.20	        | Host being attacked
--------------------------------------------------------------------------------------


#4. Impact Assessment
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Successful login detected from the source IP (192.168.19.4) as of the last review.

Execution of 'calc.exe' using base64 encoded powershell command and after that process creation of 'evil.exe' with sysmon eventid = 1. File needs further investigation.

RDP access for the Administrator account may be under attack along with comproise of internal network.

Note: The source IP( 192.168.19.4 ) is an Internal IP which might be intentional attempt or a compromised host which can be concerning as this indicates compromise of internal network. 


#5. Recommendations / Mitigation
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Immediate Actions:**

Block source IP 192.168.19.4 at firewall or network level until further investigation is made.

Enforce account lockout for repeated failed logins.

Audit Administrator account for unusual activity.

**Long-Term Actions:**

Enable MFA (multi-factor authentication) for RDP access.

Monitor Security EventLog (4625/4624) for repeated attempts.

Educate users to avoid using default or weak credentials.

#6. Evidence / References
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Splunk search query used to detect attack:**

index=main EventCode=4625 OR EventCode=4624
| search Account_Name="Suraj" AND Workstation_Name=DESKTOP-4S6O9OO
| table _time, EventCode, Account_Name, Workstation_Name
| sort - _time


Windows Security Logs (EventID 4625) for failed login attempts.

Network logs showing connection attempts to RDP port (TCP 3389).

#7. Conclusion
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The SOC detected a brute-force RDP attack targeting an internal host from Internal IP 192.168.19.4. Immediate mitigation was applied, including IP blocking and account lockout.
Suspicious '.exe' process creation is detected and alerted by Splunk which needs further investigation. And  also the internal host (192.168.19.4) which was suspected as the attacker might be a internal compromised device which needs a detailed forensic investigation of internal host 192.168.19.4 and log analysis.
