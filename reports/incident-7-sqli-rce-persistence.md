# Incident Report 7 — SQL Injection Leading to RCE and Persistence

## 1. Alert Summary

- **Alert Name:** Suspicious SQL Injection Activity Detected
- **Severity:** Critical
- **Date:** Mar 07, 2024
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to multiple HTTP requests containing SQL injection payloads targeting a web application endpoint.

The payloads indicate automated exploitation attempts using **sqlmap**.

---

## 3. Key Indicators

- **Source IP:** 118.194.247.28
- **Target Server:** WebServer1000 (172.16.20.12)
- **Affected Host:** Atlanta-Server (172.16.20.121)
- **User-Agent:** sqlmap/1.7.2
- **Target Endpoint:** /index.php?id=

---

## 4. Investigation

### 4.1 Web Attack Analysis

- Multiple HTTP requests contain SQL injection payloads:
  - UNION-based injection
  - Time-based injection (`SLEEP`, `WAITFOR DELAY`)
  - Error-based injection (`EXTRACTVALUE`, `XMLType`)

- Automated tool identified:
  - `sqlmap/1.7.2`

---

### 4.2 Exploitation Indicators

- Payload includes:
  - Database enumeration (`information_schema.tables`)
  - Attempted command execution (`xp_cmdshell`)
  - Injection of JavaScript (`<script>alert("XSS")</script>`)

Indicates multi-stage exploitation attempts.

---

### 4.3 Endpoint Activity (Post-Exploitation)

Host: Atlanta-Server (172.16.20.121)

Observed actions:

- Creation of new user:
  - `useradd -m test`

- Password set for new account:
  - `passwd test`

- File manipulation:
  - `proxy.conf` created and modified

- Installation of network tool:
  - `sudo apt-get install iftop`

---

### 4.4 Privilege Escalation

- Use of `sudo` indicates elevated privileges
- Installation of system packages confirms root-level access

---

### 4.5 Persistence & Reconnaissance

- New user account created for persistence
- `iftop` installed for network monitoring
- System and network enumeration commands observed:
  - `whoami`, `netstat`, `ping`

---

### 4.6 Attack Timeline

1. Attacker scans web application
2. Automated SQL injection initiated via sqlmap
3. Database enumeration performed
4. Command execution attempted via SQL injection
5. Server compromised (RCE achieved)
6. Attacker gains elevated privileges
7. Persistence established via new user account
8. Reconnaissance tools installed (`iftop`)

---

## 5. Findings

- Successful SQL injection exploitation
- Remote code execution achieved
- Root-level access obtained
- Persistence established via user account
- Reconnaissance activity initiated

---

## 6. Verdict

**True Positive**

The attack resulted in full system compromise, including remote code execution, privilege escalation, and persistence.

---

## 7. MITRE ATT&CK Mapping

- **T1190** — Exploit Public-Facing Application
- **T1059** — Command Execution
- **T1078** — Valid Accounts (Persistence)
- **T1068** — Privilege Escalation
- **T1046** — Network Discovery

---

## 8. Response Actions

- Immediate escalation to Tier 2
- Compromised host identified for containment

---

## 9. Recommended Actions

- Isolate affected server immediately
- Remove unauthorized user accounts
- Reimage system
- Patch web application vulnerabilities
- Disable dangerous functions (e.g., `xp_cmdshell`)
- Implement Web Application Firewall (WAF)
- Enforce input validation and parameterized queries

---

## 10. Conclusion

An automated SQL injection attack successfully compromised the target web server, leading to remote code execution, privilege escalation, and persistence. The attacker established a foothold and began reconnaissance activities. Immediate containment and full remediation are required.
