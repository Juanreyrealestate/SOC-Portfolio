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

## Lab Notes — Why I only got 3 password prompts (and why Fail2ban didn't ban)

### 1) Why SSH asked for only **3 passwords**
When you run `ssh user@host`, the SSH **client** (your terminal) typically allows only a limited number of password prompts.
- Most OpenSSH clients default to **3 password prompts** (`NumberOfPasswordPrompts 3`).
- So you see: password → wrong → password → wrong → password → wrong → then **Permission denied**.
This is normal and does **not** mean Fail2ban is blocking you yet. It just means the SSH client stopped trying.

**Mental model:**  
- SSH **client limit** = how many times your terminal will ask you for a password.  
- Fail2ban **maxretry** = how many failed events are allowed **in the logs** within a time window before banning an IP.

---

### 2) Why Fail2ban showed 0 banned (and the "Ignore 127.0.0.1" message)
Fail2ban bans IPs based on **log events**. In lab testing, two common reasons prevent bans:

#### A) You were testing from localhost (127.0.0.1)
When you do `ssh fakeuser@localhost`, the source IP is **127.0.0.1** (your own machine).
Fail2ban often ignores your own host by default (to avoid locking yourself out).
That’s why you saw log lines like:
- `Ignore 127.0.0.1 by ignoreself rule`

✅ Meaning: Fail2ban is working, but it is **refusing to ban your own machine**.

#### B) Your test IP is in `ignoreip` / local ranges
If your attack source is from a “local” network (example: Docker bridge networks), Fail2ban may ignore it depending on config.
In Docker default bridge mode:
- Container IP is usually like `172.17.0.2`
- Host (Docker bridge gateway) is usually `172.17.0.1`

If `ignoreip` includes local ranges, you may never see bans.

---

### 3) How to correctly test Fail2ban in a lab (safe approach)
Goal: generate failed SSH attempts from a source IP that Fail2ban is allowed to ban.

**Best lab approach:**
- Generate attempts from a Docker container (source = container IP, e.g., `172.17.0.2`)
- Ensure `ignoreip` does **not** include `172.17.0.0/16`
- Confirm the jail is enabled (`sshd`) and reading SSH logs correctly

**Expected outcome:**
- After `maxretry` failures within `findtime`, Fail2ban should ban the container IP.


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

