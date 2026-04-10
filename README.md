# SOC Analyst Portfolio

## Objective

Aspiring Security Operations Center (SOC) Analyst with hands-on experience in alert triage, incident investigation, and detection engineering.

This repository documents practical SOC investigations performed in a simulated environment, focusing on real-world attack scenarios, log analysis, and incident response workflows.

The goal is to demonstrate the ability to:

- Analyze security alerts and determine their validity
- Investigate incidents using logs and threat intelligence
- Document findings in a structured, professional format
- Develop detection ideas based on observed attack patterns

---

## Skills Demonstrated

- Alert Triage & Incident Analysis
- Log Analysis (Authentication, Web, System Logs)
- Threat Intelligence Enrichment (IP, Hash, URL analysis)
- Phishing & Malware Investigation
- SOC Workflow (Detection → Investigation → Response)
- Basic Detection Rule Development

---

## Tools & Technologies

- SIEM & Monitoring:
  - LetsDefend (SOC Monitoring Lab)
  - Wazuh SIEM

- Analysis Tools:
  - VirusTotal
  - Wireshark
  - Sysmon

- Security Tools:
  - Nmap
  - Burp Suite

- Environment:
  - Windows / Linux
  - VirtualBox / VMware

---

## Repository Structure

```
SOC-Portfolio/
│
├── reports/        # Incident investigation reports
├── detections/     # Detection rules and ideas
├── notes/          # Learning notes and attack patterns
└── README.md       # Portfolio overview
```

---

## Incident Reports

Each report includes:

- Alert Description
- Investigation Steps
- Evidence & Log Analysis
- Threat Intelligence Findings
- Final Verdict (True Positive / False Positive)
- Recommended Actions

Reports are located in the `/reports` directory.

---

## Featured Incident Reports

- **SharePoint RCE Attack (CVE-2025-53770)**
  Critical vulnerability exploitation leading to remote code execution and persistence.
  [View Report](./reports/incident-1-sharepoint-rce.md)

- **Phishing Attack Leading to Malware (Lumma Stealer)**  
  Social engineering attack resulting in payload execution via mshta and system compromise.  
  [View Report](./reports/incident-2-phishing-lumma-stealer.md)

- **Zero-Click RTF Exploit (CVE-2025-21298)**  
  Critical exploitation using regsvr32 (Squiblydoo) for remote payload execution.  
  [View Report](./reports/incident-3-ole-rce-regsvr32.md)

- **Typosquatting Phishing Attack (MX Record Abuse)**  
  Domain impersonation attack leveraging MX record changes to deliver phishing emails.  
  [View Report](./reports/incident-4-typosquatting-phishing-mx-change.md)

---

## Detection Engineering

The `/detections` folder contains:

- Custom detection ideas
- Basic correlation rules
- Observed attack patterns mapped to MITRE ATT&CK

---

## Learning Approach

This portfolio follows a hands-on methodology:

1. Investigate real SOC alerts using LetsDefend
2. Analyze logs and identify indicators of compromise
3. Validate findings using threat intelligence
4. Document the investigation in a structured format
5. Improve detection based on findings

---

## Background

- Cybersecurity Intern experience (phishing investigation, vulnerability assessment)
- Experience with SIEM tools and SOC workflows
- Academic background in Information Systems & Cyber Security

---

## Goal

To secure a Junior SOC Analyst role and contribute to real-world security operations by detecting, analyzing, and responding to cyber threats.

---
