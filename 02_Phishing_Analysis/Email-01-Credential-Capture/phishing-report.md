Headers
======================================
Date: Tue, 1 Aug 2023 21:22:47 +0000

Subject: Microsoft account unusual signin activity September 16, 2022 #[636274168]
To: phishing@pot

From: Microsoft account team ,_<no-reply@access-accsecurity.com>

Reply-To: solutionteamrecognizd03@gmail.com

Return-Path:bounce@providentusezn.co.uk

Sender IP: 89.144.44.4

Originating Mail Server: providentusezn.co.uk

Message-ID: <191ad2cb-9324-4167-9e8b-30a60c49d341@DB3EUR04FT008.eop-eur04.prod.protection.outlook.com>

URLs
======================================
hxxps[://]mc4-two[.]vercel[.]app


Attachments
======================================
None


Description
======================================
This email is a suspected phishing email impersonating the Microsoft Account Team, claiming suspicious account login activity. The email uses spoofed sender details with no link to the Microsoft Account Teams and Unauthorized mail infrastructure with failed authentication mechanisms(SPF, DKIM and DMARC). The message attempts to lure the recipient into interacting with a malicious link.


Artifact Analysis
======================================
**Sender Analysis:**
The sender failed crucial security check like SPF, DKIM and DMARC.

The IP address(89.144.44.4) used is not associated with Microsoft. According to DomainTools the IP is associated with "GHOSTNET-FRA"(DomainTools website screenshot provided in 'screenshots' directory).

The sender and bounce domains used like no-reply@access-accsecurity.com, bounce@providentusezn.co.uk are not legitimate Microsoft domains and are used for mass phishing campaigns without caring about the failed email authentication. 

The Reply-To address (solutionteamrecognizd03@gmail.com) is likely the attacker-controlled mailbox, intended to collect responses or credentials. Further investigation is recommended.

**URL Analysis:**
The "view activity" button redirects to the URL- hxxps[://]mc4-two[.]vercel[.]app
VirusTotal flagged the URL as phishing (screenshot provided in the 'screenshot' directory).The target brand identified is "Microsoft" which is true in our case.



Verdict
======================================
**Confirmed Phishing Email**
The email is not legitimate, fails all authentication checks , and impersonating a trusted brand(Microsoft). Further investigation and check must be done to see for other users that got similar emails.

Defense Actions
======================================
-Block Sending Domain and domains associated with the emails.

-Enforce DMARC = reject

-Report to email provider

