# SOC Case 06 — Lateral Movement via RDP, SMB, and WMI

## Overview

This case documents the investigation of potential lateral movement within a network following an initial system compromise. Lateral movement refers to techniques used by attackers to move from one compromised host to other systems in the environment in order to expand access, escalate privileges, and reach high-value assets such as servers or domain controllers.

This investigation focuses on three common lateral movement techniques: Remote Desktop Protocol (RDP), Server Message Block (SMB), and Windows Management Instrumentation (WMI).

---

## Environment

- Operating System: Windows
- Investigation Context: Post-compromise SOC investigation
- Affected Assets: Multiple internal hosts
- Log Sources:
  - Windows Security Event Logs
  - Authentication logs
  - Network connection telemetry (conceptual)

---

## What Is Lateral Movement (Explained Simply)

After gaining access to one system, attackers rarely stop there. Their goal is to move sideways across the network to reach more valuable systems.

Lateral movement allows attackers to:
- Access additional machines
- Reuse stolen credentials
- Escalate privileges
- Reach sensitive data or infrastructure

Lateral movement is a strong indicator that an incident is no longer limited to a single host.

---

## Detection

Suspicious activity was identified based on authentication events and network behavior inconsistent with normal user activity.

Indicators included:
- Successful logins from one internal host to multiple other hosts
- Authentication attempts using administrative accounts
- Access occurring outside normal business hours
- Use of protocols commonly abused for lateral movement

---

## Lateral Movement Techniques Investigated

### RDP (Remote Desktop Protocol)

RDP allows users to remotely access another Windows system.

Suspicious RDP indicators:
- RDP logins from a workstation to servers
- RDP activity outside business hours
- RDP access using accounts that do not normally use remote desktop
- Multiple RDP logins to different hosts in a short time frame

---

### SMB (Server Message Block)

SMB is commonly used for file sharing and remote execution.

Suspicious SMB indicators:
- Access to administrative shares (C$, ADMIN$)
- Authentication attempts to multiple hosts
- Use of SMB for remote command execution
- File transfers involving unknown executables or scripts

---

### WMI (Windows Management Instrumentation)

WMI allows remote system management and execution of commands.

Suspicious WMI indicators:
- Remote process creation using WMI
- Execution of PowerShell or cmd.exe via WMI
- WMI activity from non-administrative workstations
- Lack of legitimate IT administrative justification

---

## Indicators of Compromise (IOCs)

Potential indicators observed:
- Repeated authentication events across multiple hosts
- Lateral authentication using the same credentials
- RDP, SMB, or WMI usage from unexpected source systems
- Access patterns inconsistent with normal user behavior

---

## MITRE ATT&CK Mapping

The activity observed maps to the following MITRE ATT&CK techniques:

- T1021.001 — Remote Services: RDP
- T1021.002 — Remote Services: SMB
- T1047 — Windows Management Instrumentation
- T1078 — Valid Accounts

---

## Severity and Confidence Assessment

**Severity: High**  
**Confidence: High**

Rationale:
- Lateral movement indicates an expanded compromise
- Use of legitimate credentials increases impact
- Multiple systems potentially affected
- High risk of data access or privilege escalation

---

## Response and Next Steps

Recommended SOC actions:
1. Identify all affected hosts
2. Disable or reset compromised credentials
3. Review authentication logs for additional lateral movement
4. Contain impacted systems
5. Escalate to Incident Response
6. Conduct full scope assessment to identify further compromise

---

## Analyst Conclusion

The observed RDP, SMB, and WMI activity strongly indicates lateral movement following an initial compromise. This behavior represents a critical escalation in the incident lifecycle and requires immediate containment and response to prevent further spread and data exposure.
