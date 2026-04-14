# Incident Report 5 — VPN Access Attempt from Unauthorized Country

## 1. Alert Summary

- **Alert Name:** VPN Connection Detected from Unauthorized Country
- **Severity:** Low
- **Date:** Feb 13, 2024
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to a VPN access attempt from an unauthorized country (Vietnam) using valid user credentials.

Initial assessment indicates potential credential compromise.

---

## 3. Key Indicators

- **User:** [monica@letsdefend.io](mailto:monica@letsdefend.io)
- **Source IP:** 113.161.158.12
- **Location:** Vietnam
- **Target:** vpn-letsdefend.io
- **User Host IP:** 33.33.33.33

---

## 4. Investigation

### 4.1 VPN Access Attempt

- Request to VPN portal returned HTTP 200 (successful connection to service)
- Indicates attacker reached login interface

---

### 4.2 Authentication Behavior

- Correct password entered for user account
- MFA (OTP) triggered
- OTP entered incorrectly multiple times
- Authentication ultimately failed

---

### 4.3 Email Evidence

- Multiple OTP emails sent to user at:
  - 02:01 AM
  - 02:02 AM
  - 02:03 AM

- Confirms MFA challenge was triggered

---

### 4.4 Network Activity

- Source IP identified as external (Vietnam)
- Associated with suspicious activity (reported for brute force and malicious behavior)

---

### 4.5 Additional Activity

- Logs show port scanning behavior targeting internal IP
- Indicates reconnaissance attempt following failed login

---

### 4.6 Attack Timeline

1. Attacker attempts VPN login using stolen credentials
2. Correct password entered
3. MFA challenge triggered (OTP sent)
4. Attacker fails to provide correct OTP
5. Multiple login attempts observed
6. Reconnaissance activity (port scanning) detected

---

## 5. Findings

- User credentials were compromised (password known to attacker)
- MFA successfully prevented full account access
- Suspicious reconnaissance activity detected
- No confirmed system access or lateral movement

---

## 6. Verdict

**True Positive**

This is a confirmed unauthorized access attempt using valid credentials. However, MFA prevented successful login.

---

## 7. MITRE ATT&CK Mapping

- **T1133** — External Remote Services (VPN)
- **T1110** — Brute Force / Credential Access
- **T1046** — Network Service Discovery (Port Scanning)

---

## 8. Response Actions

- No host isolation required (no successful login)
- Incident monitored

---

## 9. Recommended Actions

- Reset user password immediately
- Enforce strong password policy
- Enable account lockout after failed attempts
- Restrict VPN access by geographic region
- Monitor account for further suspicious activity

---

## 10. Conclusion

An attacker attempted to access the VPN using valid credentials from an unauthorized country. While MFA successfully blocked access, the correct password entry confirms credential compromise. Immediate credential reset and monitoring are required.
