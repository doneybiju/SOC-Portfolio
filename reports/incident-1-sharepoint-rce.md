# Incident Report 1 — SharePoint RCE (CVE-2025-53770)

## 1. Alert Summary

* **Alert Name:** SOC342 - SharePoint ToolShell Auth Bypass and RCE
* **Severity:** Critical
* **Date:** Jul 22, 2025, 01:07 PM
* **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to a suspicious unauthenticated POST request targeting a SharePoint endpoint (`ToolPane.aspx`) with a large payload and spoofed referer.

Initial assessment indicates potential exploitation of a known SharePoint vulnerability.

---

## 3. Key Indicators

* **Source IP:** 107.191.58.76
* **Destination IP:** 172.16.20.17
* **Hostname:** SharePoint01
* **URL:** /_layouts/15/ToolPane.aspx
* **User-Agent:** Firefox (Windows 10)

---

## 4. Investigation

### 4.1 Log Analysis

* Unauthenticated POST request observed
* Large payload size (7699 bytes)
* Suspicious referer (`SignOut.aspx`) used for spoofing
* Activity matches exploitation pattern of CVE-2025-53770

---

### 4.2 Threat Intelligence

* **VirusTotal:** 11/94 vendors flagged IP as malicious
* **Reputation:** Associated with malware and phishing activity
* **Hosting:** Data center (Vultr) — commonly used by attackers

---

### 4.3 Attack Behavior

Post-exploitation activity confirmed:

* PowerShell execution used to extract sensitive MachineKeys
* Web shell (`spinstall0.aspx`) deployed for persistence
* `csc.exe` used to compile malicious payload in Temp directory

---

### 4.4 Timeline of Events

1. Attacker sends crafted POST request to SharePoint endpoint
2. Authentication bypass achieved
3. Remote Code Execution triggered
4. PowerShell used to extract sensitive keys
5. Web shell deployed for persistence
6. Additional payload compiled using `csc.exe`

---

## 5. Findings

* Successful exploitation of SharePoint vulnerability
* Attacker gained remote code execution
* Persistence established via web shell
* Sensitive cryptographic material (MachineKeys) targeted

---

## 6. Verdict

**True Positive**

The observed activity matches a confirmed exploitation pattern of CVE-2025-53770 with successful execution and persistence.

---

## 7. MITRE ATT&CK Mapping

* **T1190** — Exploit Public-Facing Application
* **T1059.001** — PowerShell Execution
* **T1505.003** — Web Shell
* **T1105** — Ingress Tool Transfer

---

## 8. Recommended Actions

* Immediately isolate affected host
* Remove web shell and malicious payloads
* Rotate SharePoint MachineKeys
* Patch SharePoint vulnerability
* Conduct full system integrity check

---

## 9. Conclusion

A critical SharePoint vulnerability was successfully exploited, leading to remote code execution and persistence. Immediate containment and remediation actions are required to prevent further compromise.
