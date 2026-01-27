# Analysis Notes – DNS Log Investigation

## Date  
2026-01-18

## Analyst  
Suraj

---

## Log Source Details
- **Log Type:** DNS 
- **File Name:** dns.log.gz 
- **Time Range Analyzed:** All available logs 
- **Total Events:** ~422,000 

---

## Initial Observations

1. A single internal host (**192.168.202.83**) generated an unusually high volume of DNS queries (**1,000+ within one hour**).
2. Multiple **NXDOMAIN** responses were observed from the same host.
3. Repeated **reverse DNS lookup** requests for the same IP address 
   (`44.206.168.192.in-addr.arpa` → 192.168.206.44).

---

## Behavioral Analysis

- Query patterns demonstrate **consistent, automated beaconing behavior**, primarily occurring during the time window of **18:00 to 04:00**.

---

## Preliminary Assessment

The observed activity strongly suggests:
- **Malware command-and-control (C2) communication**
- Potential **malware beaconing** or **Domain Generation Algorithm (DGA)** usage

---

## Recommended Actions

- **Isolate** the affected host immediately.
- Perform a **full malware scan** and **memory analysis**.
- **Block** all identified suspicious domains and IP addresses.
- **Escalate** the incident to **Tier 2 SOC** for deeper investigation.

