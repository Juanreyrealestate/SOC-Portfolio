# SOC Case 02 – SSH Brute Force: Severity, Confidence & Escalation Analysis

## Purpose of This Case

This case focuses on decision-making and incident handling judgment rather than raw detection.
The objective is to demonstrate how a SOC Analyst evaluates severity, confidence, business impact,
and determines appropriate escalation actions after detecting a known attack pattern.

This case builds on SOC Case 01 (SSH Brute Force Detection & Investigation) and simulates
a real-world SOC workflow beyond initial alert triage.

---

## Incident Summary

- Attack Type: SSH Brute Force Authentication Attempts
- Target System: Linux host (Ubuntu)
- Log Source: /var/log/auth.log
- Access Vector: SSH (TCP/22)
- Detection Method: Manual log analysis using grep and journalctl
- Timeframe: Short burst of repeated failed authentication attempts

---

## Observed Indicators

- High volume of failed SSH login attempts
- Repeated attempts against the same user accounts
- Source IP address external to the internal network
- Activity occurring outside normal business hours
- No successful authentication observed

---

## Severity Assessment

**Assigned Severity: MEDIUM**

### Rationale

- The attack is external and automated in nature (common brute force behavior)
- No confirmed successful login or system compromise
- No evidence of privilege escalation or lateral movement
- Targeted a single host, not multiple assets

### Why Not LOW?

- External threat actor activity
- Repeated authentication attempts indicate malicious intent
- SSH is a critical service that can lead to full system compromise if breached

### Why Not HIGH?

- No successful authentication
- No malware execution
- No persistence mechanisms identified
- No confirmed impact to confidentiality, integrity, or availability

---

## Confidence Assessment

**Assigned Confidence: HIGH**

### Rationale

- Log entries clearly show repeated "Failed password" events
- Pattern matches known brute-force authentication behavior
- Source IP consistency supports automated attack hypothesis
- Low likelihood of false positive (not user error or internal admin activity)

---

## Business Impact Assessment

**Current Impact: LOW**

- No service disruption observed
- No data exposure detected
- No system downtime
- Attack blocked at authentication layer

**Potential Impact if Successful: HIGH**

- Full system compromise
- Credential theft
- Possible lateral movement
- Reputational and operational risk

---

## Escalation Decision

**Escalation Level: Tier 1 → Tier 2 SOC**

### Actions Taken

- Incident documented and categorized
- Source IP flagged for monitoring
- Recommendation provided for defensive hardening

### Actions NOT Required at This Stage

- Incident Response (IR) activation
- Executive notification
- Law enforcement involvement

---

## Recommended Mitigations

- Implement SSH rate limiting (e.g., Fail2Ban)
- Enforce key-based authentication
- Disable root login over SSH
- Restrict SSH access by IP where possible
- Monitor for repeat activity from same source IP

---

## What I Would Do Next in a Production Environment

If this system were part of a production environment, the following actions would be taken:

1. Correlate SSH logs with SIEM data across other hosts
2. Check for similar attempts against other assets
3. Validate firewall and IDS/IPS logs
4. Add detection rule for excessive SSH failures
5. Review IAM and access policies
6. Document lessons learned for SOC playbooks

---

## SOC Analyst Value Demonstrated

This case demonstrates:

- Ability to assess risk beyond detection
- Proper severity and confidence classification
- Business-aware decision making
- Appropriate escalation judgment
- Clear documentation suitable for handoff and reporting

---

## Final Assessment

This incident represents a **common but meaningful external threat** that requires
monitoring, documentation, and preventive hardening rather than emergency response.

Correct handling avoids alert fatigue while maintaining security posture.

