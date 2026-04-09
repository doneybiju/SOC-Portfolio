# Incident Report 2 — Phishing Attack Leading to Lumma Stealer Infection

## 1. Alert Summary

- **Alert Name:** Suspicious Email with Malicious Redirect (Lumma Stealer Distribution)
- **Severity:** High
- **Date:** Mar 13, 2025
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to an email containing a malicious link associated with a click-fix script used to distribute Lumma Stealer malware.

Initial assessment indicates a phishing attempt targeting the end user.

---

## 3. Key Indicators

- **Source Email:** [update@windows-update.site](mailto:update@windows-update.site)
- **Recipient:** [dylan@letsdefend.io](mailto:dylan@letsdefend.io)
- **Source IP:** 132.232.40.201
- **User Host IP:** 172.16.17.216
- **Malicious URL:** https://windows-update.site/
- **Payload URL:** https://overcoatpassably.shop/Z8UZbPyVpGfdRS/maloy.mp4

---

## 4. Investigation

### 4.1 Email Analysis

- Email impersonates a legitimate Windows update notification
- Sender domain is not an official Microsoft domain
- Contains a malicious link designed to lure user interaction

---

### 4.2 Endpoint Activity

- User accessed the phishing URL via browser
- Browser history confirms visit to malicious site
- Terminal history shows execution of PowerShell commands

---

### 4.3 Command Execution

Observed commands:

- PowerShell used to execute obfuscated command
- `mshta.exe` leveraged to fetch remote payload

Example behavior:

- Obfuscated PowerShell command reconstructing `mshta.exe` execution
- Download and execution of remote file (`maloy.mp4`)

---

### 4.4 Network Activity

- Outbound connection from 172.16.17.216 to 172.67.139.19 (HTTPS)
- GET request to malicious payload URL
- Traffic allowed through firewall

---

### 4.5 Threat Intelligence

- Phishing domain flagged as malicious in VirusTotal (11/95 detections)
- Payload domain (`overcoatpassably.shop`) confirmed malicious
- Attack pattern consistent with Lumma Stealer distribution

---

### 4.6 Attack Timeline

1. Phishing email delivered to user
2. User clicks malicious link
3. Fake CAPTCHA page displayed
4. User executes malicious PowerShell command
5. `mshta.exe` downloads payload
6. Malicious payload executed on host
7. Outbound connection established to attacker infrastructure

---

## 5. Findings

- Successful phishing attack via social engineering
- User executed malicious PowerShell command
- Payload downloaded and executed using `mshta.exe`
- System compromised with Lumma Stealer malware

---

## 6. Verdict

**True Positive**

The attack resulted in successful execution of a malicious payload and system compromise.

---

## 7. MITRE ATT&CK Mapping

- **T1566.002** — Phishing: Link
- **T1204.002** — User Execution: Malicious File
- **T1059.001** — PowerShell
- **T1218.005** — mshta (Signed Binary Proxy Execution)
- **T1105** — Ingress Tool Transfer

---

## 8. Response Actions

- Infected host isolated (172.16.17.216)
- Malicious domains identified and flagged
- Further spread prevented

---

## 9. Recommended Actions

- Reset user credentials
- Run full malware scan and system reimage if needed
- Block malicious domains/IPs at firewall
- Conduct phishing awareness training
- Monitor for potential data exfiltration

---

## 10. Conclusion

A successful phishing attack led to the execution of Lumma Stealer malware via social engineering and PowerShell abuse. Prompt containment limited further impact, but remediation and monitoring are required to ensure full recovery.
