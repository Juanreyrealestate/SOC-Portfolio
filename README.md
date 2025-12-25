# SOC Analyst Portfolio — Juan Rey

Hands-on SOC portfolio focused on **detection, investigation, and documentation** using real logs, Linux, and SIEM workflows.  
This repository is built to be **recruiter-friendly**: quick overview + direct access to case studies, reports, playbooks, and evidence.

---

## What you’ll find here

- **SOC Case Studies** (end-to-end): detection → investigation → evidence → MITRE mapping → response recommendations  
- **Incident-style Reports** (structured writeups)
- **Playbooks** (repeatable procedures)
- **Logs & Evidence** (supporting artifacts where applicable)
- **Security+ Notes** (learning track and applied concepts)

---

## Highlights (start here)

- **Case 08 — Wazuh Detection of SSH Brute Force Attempts (Ubuntu)**
  - Validated SIEM alerts against raw logs (`auth.log`)
  - Confirmed no successful authentication / no compromise
  - Configured and tested Fail2ban behavior (lab simulation + local traffic handling)
  - MITRE ATT&CK mapping + remediation guidance  
  ➜ Read: [Case 08](./soc-cases/case-08-wazuh-ssh-bruteforce-detection.md)

> More cases are available in the folder below.

---

## Repository Map (fast navigation)

- ## Start Here
- **SOC Cases (Index):** [Open the case studies folder](./soc-cases/)
- **Latest case:** [Case 08 — Wazuh SSH Brute Force Detection (Ubuntu)](./soc-cases/case-08-wazuh-ssh-bruteforce-detection.md)

- **SOC Case Studies:** `./soc-cases/`
- **Reports:** `./reports/`
- **Playbooks:** `./playbooks/`
- **Logs / Evidence:** `./logs/`
- **Notes / Learning:** `./notes/`
- **Security+ track:** `./securityplus/`
- **Archive:** `./archive/`
- SOC Cases Index: Open soc-cases/

---

## Core Skills Demonstrated

- **Alert triage & investigation** (validate SIEM alerts with source logs)
- **Linux log analysis** (`auth.log`, systemd journal, filtering, timelines)
- **SIEM workflow thinking** (what happened, impact, evidence, next steps)
- **MITRE ATT&CK mapping** (technique-level reasoning)
- **Practical hardening recommendations** (SSH + brute-force protections)
- **Clear documentation** (incident-style reporting)

---

## Tooling / Tech Used (varies by case)

- Linux (Ubuntu), SSH, system logs
- Wazuh (SIEM / agent / manager)
- Fail2ban (brute-force mitigation)
- Docker (controlled simulation environments)
- GitHub documentation workflows (Markdown reporting)

---

## How I build each SOC case (my standard)

Each case study follows a consistent structure:

1. **Overview** (what triggered the alert)
2. **Environment** (host, log source, tooling)
3. **Detection** (what was observed)
4. **Investigation** (commands/queries + interpretation)
5. **Assessment** (was it malicious? compromised?)
6. **MITRE ATT&CK mapping**
7. **Response & Recommendations**
8. **Evidence references** (logs/screens where relevant)
9. **Lessons learned** (interview-ready)

---

## Contact

If you’d like to discuss my SOC workflow or any case study:
- LinkedIn: (https://www.linkedin.com/in/juanrey-cyber)
- Email: (juanreycyber@gmail.com)

