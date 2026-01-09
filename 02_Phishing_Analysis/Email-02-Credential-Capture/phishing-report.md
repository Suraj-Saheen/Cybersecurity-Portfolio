Headers
======================================
Date: Wed, 10 Apr 2019 11:46:37 -0600

Subject: You've got 1 new message [REF: 8]

To: jsmith@technicalsolutions.com

From: CIBC-Banking.Service.Email.8@caib.com

Reply-To: Absent

Return-Path: meztaz.logocec8@caib.com

Sender IP: 190.6.201.67

Originating Mail Server: 96-91-136-70-static.hfc.comcastbusiness.net

Message-ID: <i7g9MMh5NtErtaOzQZEp3D-i-u3FWwdo0wY5mhD8Q1vIvv1yeLj-jMWPAn-HP3FugKsucesWSubO0Vns8GRFYG0aH4MyU2paqP6yUnRcgaU=@protonmail.com>

URLs
======================================
hxxp[://]app[.]e[.]royalmail[.]com/e/es?s=451761973&e=102011&elqTrackId=78D8A052C380BCBFF284D754BEBE9730&elq=29631e61f5464684a81212b3091d9419&elqaid=494&elqat=1


Attachments
======================================
No Attachments


Description
======================================
This email is a suspected phishing email impersonating the CIBC Bank (A Canadian Multinational banking and financial service company), claiming suspicious account login using incorrect password which lead to account deactivation. The email uses spoofed sender details with no link to the CIBC bank and Unauthorized mail infrastructure with failed authentication mechanisms(SPF, DKIM and DMARC). The message attempts to lure the recipient into interacting with a malicious link and potentially a credential capture page.


Artifact Analysis
======================================
**Sender Analysis:**
The sender failed crucial security check like SPF, DKIM and DMARC.

The IP address(190.6.201.67) used is not associated with CIBC. According to DomainTools the IP is associated with "CABLECOLOR" a Honduras based company (DomainTools website screenshot provided in 'screenshots' directory).

The sender and bounce domains used like CIBC-Banking.Service.Email.8@caib.com, meztaz.logocec8@caib.com are not legitimate CIBC domains. Domain spoofing and typosquatting is observed here **caib.com** which is similar to **cibc(the actual bank name)**

Both the domains are likely the attacker-controlled mailbox, intended to collect responses or credentials. Further investigation is recommended.

**URL Analysis:**
The "Activate my account" button redirects to the URL- hxxp[://]app[.]e[.]royalmail[.]com/e/es?s=451761973&e=102011&elqTrackId=78D8A052C380BCBFF284D754BEBE9730&elq=29631e61f5464684a81212b3091d9419&elqaid=494&elqat=1

This url is claiming to be of "royalmail.com" which is a legitimate main service used by banks and governments but due to the failed cryptographic  authentication , the url cannot be trusted and needs further investigation. VirusTotal and other similar tools show the url to be clean(no sure).


Impact Level
======================================
High- This phishing email is impersonates a trusted bank(CIBC) and attempts to collect credentials. Users clicking the link may have their account compromised, leading to potential financial loss.


Verdict
======================================
**Potential Phishing Email**
The email is not legitimate, fails all authentication checks , and impersonating a trusted bank(CIBC). A clear indication of domainspoofing and impersonation is detected. Further investigation and checks must be done to see for other users that got similar emails.

Defense Actions
======================================
-Block Sending Domain and domains associated with the emails.

-Enforce DMARC = reject

-Report to email provider and the associated bank

-Check for compromised account info of the user and contact the bank immediately.

