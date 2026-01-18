# Incident Report – Suspicious DNS Activity

## Incident Summary

Suspicious DNS activity was detected from an internal host (**IP: 192.168.202.83**) exhibiting high **NXDOMAIN** response rates, long and randomly generated domain queries, and beaconing behavior. This activity is consistent with **malware beaconing** or **DNS tunneling**.

## Detection Method

The incident was detected using Splunk threshold-based alerts for:
- High **NXDOMAIN** response rates
- Unusual activity timeframe (**18:00:00 – 04:00:00**)
- High request volume (**1,000+ per hour**), indicating automated behavior (suspected malware activity)
- Long and anomalous domain name queries

## Timeline

- **First suspicious event:** 2016-03-12 19:30:54 IST 
- **Last suspicious event:** 2016-03-13 03:30:00 IST 

## Affected Assets

- **Host IP:** 192.168.202.83 
- **User Account:** workstation-user 
- **Network Segment:** Internal LAN 

## Indicators of Compromise (IOCs)

- **Domains:**
  - `44.206.168.192.in-addr.arpa`
  - Multiple randomly generated domain names (limited in number)

- **IP Addresses:**
  - `192.168.202.83`

## Analysis

The affected host generated over **1,000 DNS queries per hour**, with more than **95% resulting in NXDOMAIN** responses during nighttime hours, and also the presence of randomly generated domain names indicates **malware beaconing** and potential **Domain Generation Algorithm (DGA)** activity. The unusually high query volume further suggests the malware may be **stuck in a loop**, possibly due to failed C2 resolution or aggressive retry behavior. No legitimate business justification was identified.

## Root Cause

The most likely cause is a **malware infection**, potentially originating from phishing email execution or access to malicious or compromised websites, resulting in outbound command-and-control communication using DNS as the transport layer.

## Impact

There is a potential risk of data exfiltration and internal system compromise. No confirmed data loss was identified at this time; however, the risk remains high.

## Recommendations

- Immediately isolate the affected host.
- Conduct full malware scanning and forensic analysis.
- Block all identified IOCs at firewall and DNS levels.
- Reset affected user credentials.
- Implement stricter DNS monitoring and alerting thresholds.

## Evidence

- Screenshots of Splunk dashboards showing elevated **NXDOMAIN** counts from `192.168.202.83`.
- Screenshots of repeated reverse DNS lookup activity during non-business hours.
- Detection queries used for identification.

