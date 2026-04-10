# Incident Report 4 — Typosquatting Phishing Attack via MX Record Change

## 1. Alert Summary

- **Alert Name:** Impersonating Domain MX Record Change Detected
- **Severity:** Medium
- **Date:** Sep 17, 2024
- **Source:** LetsDefend SIEM

---

## 2. Initial Triage

The alert was triggered due to a suspicious MX record change on the domain `letsdefwnd.io`, indicating potential phishing infrastructure setup.

The domain closely resembles the legitimate domain `letsdefend.io`, suggesting a typosquatting attack.

---

## 3. Key Indicators

- **Suspicious Domain:** letsdefwnd.io
- **MX Record:** mail.mailerhost.net
- **Sender Email:** [voucher@letsdefwnd.io](mailto:voucher@letsdefwnd.io)
- **Recipient:** [mateo@letsdefend.io](mailto:mateo@letsdefend.io)
- **User Host IP:** 172.16.17.162
- **Associated IP:** 45.33.23.183

---

## 4. Investigation

### 4.1 Domain Analysis

- Domain `letsdefwnd.io` is a typosquatted version of `letsdefend.io`
- MX record configured to external mail server (`mailerhost.net`)
- Indicates setup for phishing email delivery

---

### 4.2 Email Analysis

- Phishing email sent from `voucher@letsdefwnd.io`
- Subject: “Congratulations! You've Won a Voucher”
- Social engineering tactic to lure user interaction
- Email successfully delivered (Action: Allowed)

---

### 4.3 Endpoint Activity

- User: Mateo (172.16.17.162)
- Browser history confirms access to:
  - http://www.letsdefwnd.io/

- Indicates user interaction with phishing content

---

### 4.4 Network Activity

- Outbound request from 172.16.17.162 to 45.33.23.183
- URL accessed: https://letsdefwnd.io
- Same IP associated with email source infrastructure

---

### 4.5 Infrastructure Correlation

- Email source and web hosting share the same IP (45.33.23.183)
- Confirms attacker-controlled phishing infrastructure

---

### 4.6 Attack Timeline

1. Attacker registers typosquatted domain (`letsdefwnd.io`)
2. MX record configured for phishing email delivery
3. Phishing email sent to target user
4. User receives and opens email
5. User clicks link and visits malicious domain
6. Connection established to attacker infrastructure

---

## 5. Findings

- Typosquatted domain used to impersonate legitimate service
- Phishing email successfully delivered and opened
- User interacted with malicious domain
- Attacker infrastructure confirmed via IP correlation

---

## 6. Verdict

**True Positive**

Confirmed phishing attack using domain impersonation and social engineering.

---

## 7. MITRE ATT&CK Mapping

- **T1566.002** — Phishing: Link
- **T1583.001** — Acquire Infrastructure: Domains
- **T1584.001** — Compromise Infrastructure: Domains

---

## 8. Response Actions

- Affected host isolated (172.16.17.162)
- Malicious domain blocked at firewall and email gateway

---

## 9. Recommended Actions

- Reset user credentials (Mateo)
- Block domain and associated IP across all systems
- Monitor for additional phishing emails
- Conduct user awareness training on phishing attacks

---

## 10. Conclusion

A typosquatting-based phishing attack was conducted using a look-alike domain and modified MX records. The attack successfully reached the target user and resulted in interaction with attacker-controlled infrastructure. Prompt containment actions reduced further risk.
