# SOC Case 08 — Wazuh Detection of SSH Brute Force Attempts (Ubuntu)

## Overview
This case documents the detection, investigation, and assessment of repeated SSH authentication failures observed on a Linux host. The activity was detected via Wazuh SIEM and correlated with raw system logs to determine whether a compromise occurred.

---

## Environment
Host: Ubuntu-lab  
OS: Ubuntu Linux  
Analyst user: analyst  
Log source: /var/log/auth.log  
Monitored service: SSH  
SIEM / Platform: Wazuh (manager, agent, dashboard)

---

## Detection

### Linux log detection
Repeated SSH authentication failures were observed in /var/log/auth.log, including attempts against non-existent users.

Command used:
sudo grep -E "Failed password|Invalid user|authentication failure" /var/log/auth.log

Observed indicators:
- High frequency of failed SSH attempts in a short time window
- Attempts against non-existent usernames (e.g. fakeuser)
- PAM authentication failures
- Connection closed after repeated failures

Example log entries:
Dec 23 20:53:44 Ubuntu-lab sshd[5056]: Failed password for invalid user fakeuser from 127.0.0.1
Dec 23 20:53:46 Ubuntu-lab sshd[5056]: Failed password for invalid user fakeuser from 127.0.0.1
Dec 23 20:53:57 Ubuntu-lab sshd[5056]: Connection closed by invalid user fakeuser

---

## Wazuh Detection
Wazuh surfaced related alerts in:
- Threat Hunting overview (events + MITRE ATT&CK mapping)
- Security Alerts table for the Ubuntu-lab agent

Key observation:
Alerts were generated, but no very high-severity levels were observed in the dashboard.

---

## Investigation

1) Confirm affected host and analyst context
hostname  
whoami  
id analyst  

Result:
Host confirmed as Ubuntu-lab. Analyst user context validated.

## Supporting Evidence

Relevant log excerpts used during this investigation are documented here:

- [Log Evidence – Case 08](../logs/case-08-log-snippets.md)

Logs were reviewed manually to validate:
- SSH authentication failures
- Absence of successful compromise
- Correct Fail2ban behavior


---

2) Confirm brute-force pattern in auth log
sudo grep -E "Failed password|Invalid user|authentication failure" /var/log/auth.log

What to look for:
Multiple authentication failures clustered closely in time.

---

3) Identify targeted usernames (possible user enumeration)
sudo grep "Invalid user" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr

Interpretation:
Repeated "Invalid user X" suggests automated guessing of usernames.

---

4) Identify source IP(s)
sudo grep "Failed password|Invalid user" /var/log/auth.log | grep -oE "from ([0-9]{1,3}\.){3}[0-9]{1,3}" | awk '{print $2}' | sort | uniq -c | sort -nr | head

Result in this lab:
127.0.0.1 (localhost), consistent with a controlled simulation.

---

5) Check for successful authentication (compromise validation)
sudo grep -E "Accepted password|Accepted publickey" /var/log/auth.log | tail -n 50

Result:
No successful authentication events during the attack window.

---

6) Check for suspicious privilege escalation after SSH activity
sudo grep -E "sudo: session opened for user root|COMMAND=" /var/log/auth.log | tail -n 80

Result:
No suspicious sudo or root sessions following the SSH failures.

---

## MITRE ATT&CK Mapping
T1110 — Brute Force: repeated SSH authentication failures  
T1078 — Valid Accounts (Attempted): credential guessing against potential accounts

---

## Assessment

What happened?
Repeated SSH authentication failures consistent with a brute-force attempt (or simulated brute-force) against the SSH service on Ubuntu-lab.

Was the host compromised?
No evidence of compromise:
- No accepted password or public key events
- No privilege escalation
- Activity originated from localhost in a lab environment

Severity:
Low (Lab / Simulated)

---

## Response & Recommendations

Immediate actions (production scenario):
- Block offending IP(s)
- Enable brute-force protections (Fail2ban / rate limiting)
- Increase monitoring sensitivity

SSH hardening:
- Disable password authentication; use SSH keys only
- Disable root SSH login
- Restrict SSH access (VPN / allowlist / bastion)
- Enforce strong passwords and MFA where applicable

Wazuh improvements:
- Tune rules for N failed attempts in X minutes
- Dashboards for:
  - Invalid user attempts
  - Failed passwords
  - Accepted logins after failures
  - Sudo escalation after SSH login

---

## Lessons Learned (Interview-ready)
- Always validate SIEM alerts against raw logs
- Confirm source, target, success vs failure, and post-auth behavior
- Document timeline, MITRE mapping, severity, and remediation clearly

---

## Appendix — Commands Used
hostname  
whoami  
id analyst  

sudo grep -E "Failed password|Invalid user|authentication failure" /var/log/auth.log  

sudo grep "Invalid user" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr  

sudo grep "Failed password|Invalid user" /var/log/auth.log | grep -oE "from ([0-9]{1,3}\.){3}[0-9]{1,3}" | awk '{print $2}' | sort | uniq -c | sort -nr | head  

sudo grep -E "Accepted password|Accepted publickey" /var/log/auth.log | tail -n 50  

sudo grep -E "sudo: session opened for user root|COMMAND=" /var/log/auth.log | tail -n 80

