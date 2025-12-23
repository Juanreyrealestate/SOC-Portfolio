# SOC Case 04 — Suspicious PowerShell Encoded Command Execution

## Overview

This case documents the detection and investigation of suspicious PowerShell activity involving the use of encoded commands. Encoded PowerShell execution is a common technique used by threat actors to obfuscate malicious intent, evade detection, and deliver payloads. The objective of this investigation was to identify whether the activity was legitimate administrative behavior or indicative of malicious execution.

---

## Environment

- Operating System: Windows
- Affected User: Standard user account (non-administrative)
- Execution Tool: PowerShell
- Log Sources:
  - Windows Security Logs
  - PowerShell Operational Logs (conceptual)
- Investigation Context: SOC alert triage and investigation

---

## Detection

The activity was flagged due to the execution of PowerShell with suspicious command-line arguments commonly associated with malicious behavior.

Indicators observed:
- Use of `-EncodedCommand`
- Use of `-NoProfile`
- Use of `-WindowStyle Hidden`
- Execution outside of normal business hours
- No documented administrative or operational justification

These indicators strongly suggested intentional obfuscation and potential malicious execution.

---

## Investigation

### Encoded Command Analysis

PowerShell supports Base64-encoded command execution using the `-EncodedCommand` flag. Attackers frequently abuse this functionality to hide malicious instructions.

The investigation focused on:
- Identifying the encoded PowerShell command
- Decoding the Base64 payload
- Determining the true behavior of the script

Potential malicious outcomes after decoding include:
- Downloading payloads from external hosts
- Establishing command-and-control (C2) communication
- Creating persistence mechanisms
- Executing lateral movement techniques

---

## Indicators of Compromise (IOCs)

Key indicators identified:
- Obfuscated PowerShell execution
- Encoded command usage without clear business purpose
- Suspicious execution flags
- Potential execution from non-standard directories (TEMP / AppData)
- Possible outbound network connections following execution

---

## MITRE ATT&CK Mapping

The observed behavior maps to the following MITRE ATT&CK techniques:

- T1059.001 — Command and Scripting Interpreter: PowerShell
- T1027 — Obfuscated / Encrypted Payloads
- T1105 — Ingress Tool Transfer (if payload download occurred)
- T1053 — Scheduled Task (if persistence was established)

---

## Severity and Confidence Assessment

**Severity: High**  
**Confidence: High**

Rationale:
- Encoded PowerShell execution is a known malicious technique
- Obfuscation indicates intent to evade detection
- Execution context lacked legitimate justification
- Potential for payload delivery and further compromise

---

## Response and Next Steps

Recommended actions:
1. Confirm the affected host and user account
2. Decode and analyze the PowerShell encoded payload
3. Review outbound network connections from the host
4. Inspect the system for persistence mechanisms
5. Check for signs of lateral movement
6. Escalate to Incident Response if malicious behavior is confirmed

---

## Analyst Conclusion

The use of encoded PowerShell commands combined with obfuscation techniques represents a high-risk event. Without clear administrative justification, this activity should be treated as potentially malicious and escalated for deeper forensic analysis and containment actions.
