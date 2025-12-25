# SOC Case 09 — Wazuh: Suspicious sudo usage + new user creation (persistence)

## Overview
We simulated a post-compromise scenario where an attacker uses `sudo` to create a new local user and grant elevated privileges.  
Goal: validate Wazuh alerting, confirm evidence in logs, assess impact, and recommend remediation.

## Environment
- OS: Ubuntu lab
- Telemetry: auth logs (sudo/useradd/group changes)
- Detection: Wazuh alerts (agent → manager → dashboard)

## What happened (initial)
A local account executed privileged commands that:
1) created a new user
2) added the user to an admin group (sudo)
This is consistent with persistence / privilege escalation after initial access.

## Evidence Handling (Portfolio Note)
Evidence for this case is captured using:
- Wazuh alert screenshot(s) (recommended)
- Minimal log excerpts (optional)
If screenshots are not available, reproduction steps and expected evidence are documented.

## Next
- Reproduction Steps
- Wazuh Alerts Observed
- Log Validation
- MITRE ATT&CK Mapping
- Severity/Confidence
- Response & Recommendations
- Lessons learned
