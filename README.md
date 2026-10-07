# Firewall-Alert-Investigation-L1
# Incident Report: Access to Blacklisted External URL Blocked by Firewall

## Overview
This document provides a detailed SOC Tier 1 analysis and escalation report for Event ID **8816**. The alert was triggered by an internal host attempting to establish an outbound TCP connection to a known malicious shortened URL.

---

## 1. Alert Summary & Metadata

| Field | Value |
| :--- | :--- |
| **Event ID** | 8816 |
| **Alert Name** | Access to Blacklisted External URL Blocked by Firewall |
| **Severity** | High |
| **Category** | Firewall / Network Security |
| **Timestamp** | 10/07/2026 10:51:58.031 |
| **Source IP** | 10.20.2.17 |
| **Source Port** | 34257 |
| **Destination IP** | 67.199.248.11 |
| **Destination Port** | 80 (HTTP) |
| **Requested URL** | `http://bit.ly/3sHkX3da12340` |
| **Protocol** | TCP |
| **Action Taken** | Blocked by Firewall Rule |

---

## 2. Investigation & Findings

- **URL Analysis:** The requested short URL (`http://bit.ly/3sHkX3da12340`) belongs to a blacklisted domain associated with potential phishing or malicious redirect activities.
- **Firewall Rule:** The connection attempt was intercepted and blocked successfully by edge firewall policies prior to establishing data exchange.
- **Impact Assessment:** Although the traffic was blocked at the perimeter, the outbound initiation confirms that host `10.20.2.17` initiated the request (either via user interaction or background process/malware).

---

## 3. Incident Classification & Resolution

* **Alert Classification:** `True Positive`
* **Escalated to Tier 2:** `Yes`

### Analyst Final Notes
> On Oct 7th, 2026 at 12:54, the internal host (IP: 10.20.2.17) attempted to access a blacklisted external URL (`http://bit.ly/3sHkX3da12340`) over TCP protocol (Source Port: 34257, Destination IP: 67.199.248.11, Destination Port: 80).
> 
> Upon analysis, the URL was confirmed to be malicious and was successfully blocked by the firewall's blacklisting rules. 
> 
> Since an outbound connection attempt was initiated, further investigation is required to determine the root cause, check for potential machine compromise, and identify the user/process responsible. Therefore, the alert has been escalated to Tier 2 for deep-dive investigation.

---

## 4. Evidence & Screenshots

* **Alert Details & Summary:**
<img width="994" alt="details2" src="https://github.com/user-attachments/assets/fc9d6e71-12c5-4282-9c56-4ff192579567"/>

* **SIEM / Log Investigation:**
<img width="1281" alt="url" src="https://github.com/user-attachments/assets/5c2f079e-a444-43e5-aa0a-99e054e2eb4f"/>

* **Incident Decision & Escalation Form:**
<img width="1001" alt="report" src="https://github.com/user-attachments/assets/d7638b8d-13ea-4371-99fd-a86030b73419"/>
---

## 5. Recommended Tier 2 Follow-Up Actions

1. Check endpoint process history on host `10.20.2.17` around `10/07/2026 10:51:58` to identify the browser or executable that issued the HTTP request.
2. Inspect web browser history and email logs on `10.20.2.17` to verify if this was triggered by a user clicking a phishing link.
3. Perform an EDR/Antivirus scan on host `10.20.2.17` to rule out active local persistence or malware execution.
