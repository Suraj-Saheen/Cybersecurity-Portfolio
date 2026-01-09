Headers
======================================
Date: Mon, 31 Oct 2022 07:03:57 +0000

Subject: FWD: All unverified accounts will be suspended on 10/30/2022.
 2hwpexn64bmc7qrzvo0kyduajlgf3598

To: emily.jenkins@potentialsecurity.net

From: 7wq1vg3kn9woejk4@emails.gorgias.com

Reply-To: 7wq1vg3kn9woejk4@emails.gorgias.com

Return-Path: bounce+31a2a2.6303d-emily.jenkins=potentialsecurity.net@gorgias.io

Sender IP: 143.55.227.147

Originating Mail Server: emails.gorgias.com via mailgun.net

Message-ID: <166719983695.1603003.167987655214941784.10334148-20347658@helpdesk-rules-worker-7d6b9ff7cb-hbpzp>

URLs
======================================
hxxps[://]usertest[.]sciquest[.]com/apps/Router/ExternalSiteTransition?url=hxxps[://]drop-coin-availablenow[.]site44[.]com/


Attachments
======================================
No Attachments


Description
======================================
This email is a suspected phishing email impersonating "trustwallet.com" (a popular, non-custodial (self-custody) mobile and browser extension crypto wallet), claiming that the user's Trust Wallet has not been verified and warns that failure to complete verification will result in account suspension, an urgency and fear is created to lure the recipient into clicking the link. The email uses spoofed sender details with no link to Trust Wallet.

Attacker are abusing a legitimate customer-support platform "gorgias.com" to pass SPF and DKIM , pass filters and appear more legitimate.But the email fails DMARC due to domain mismatch an indication of impersonation.

Moreover the email contains grammatical errors, unstructured and unprofessional wordings which is a big red flag for emails form companies like trustwallet.com


Artifact Analysis
======================================
**Sender Analysis:**
The sender passed SPF and DKIM due to the use of legitimate third-party platform (gorgias/mailgun) but failed DMARC which is an indication of impersonation.

The IP address(143.55.227.147) used is not associated with Trust Wallet. According to DomainTools the IP is associated with "a227-147.mailgun.net" an US based enterprise-grade email delivery platform (DomainTools website screenshot provided in 'screenshots' directory).

The sender and bounce domain used 7wq1vg3kn9woejk4@emails.gorgias.com is from a legitimate domain (gorgias.com) but it is not associated with Trust Wallet. 

The domains used is legitimate which is being abused by the attacker to impersonate Trust Wallet and deliver phishing emails.

**URL Analysis:**
The "Confirm my wallet" button redirects to the URL- hxxps[://]usertest[.]sciquest[.]com/apps/Router/ExternalSiteTransition?url=hxxps[://]drop-coin-availablenow[.]site44[.]com/

The first part of the URL is a legitimate service redirector  often used by companies to safely redirect users to external links.
But the second part of the URL- hxxps[://]drop-coin-availablenow[.]site44[.]com/ is flagged as malicious and phishing by Virustotal (screeshot of the virustotal findigs is provided on the screenshots directory). Moreover "site44.com" is a free hosting service often abused for phishing,scams, or malware distribution.


Impact Level
======================================
High- This phishing email impersonates a trusted crypto wallet platform "trustwallet.com" and attempts to collect credentials. Users clicking the link may have their account compromised, leading to potential financial loss.


Verdict
======================================
**Confirmed Phishing Email**
The email is not legitimate,impersonating "trustwallet.com". A clear indication of domainspoofing and impersonation of legitimate service and platform is detected. Further investigation and checks must be done to see for other users that got similar emails.

Defense Actions
======================================
-Block Sending Domain and domains associated with the emails.

-Enforce DMARC = reject

-Report to email provider and https://support.trustwallet.com

-Inform the user and check for any compromised crypto wallets.

