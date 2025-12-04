# 🛡️ PLAYBOOK SOC – Brute Force Attack Against Login Service

## 📌 1. Description
A brute force attack consists of rapid, repeated login attempts from one or multiple IP addresses in an attempt to guess valid credentials.  
This playbook defines the steps to analyze, contain, and remediate such activity.

---

## 📌 2. Detection

### Indicators:
- Many `FAILED LOGIN` events in short time intervals  
- Attempts from the same IP or small IP range  
- Targeting privileged users (e.g., admin, root)  
- Regular timing pattern (e.g., every 10–30 seconds)

### Example logs:
203.0.113.10 → admin → FAIL
203.0.113.10 → admin → FAIL
203.0.113.10 → admin → FAIL


### Automated detection rules:
- More than **5 failed attempts** from same IP in **1 minute**
- More than **3 failed attempts** to any *admin* user

---

## 📌 3. Triage (Quick Assessment)

### Ask:
- Did any attempt eventually succeed?  
- Is the username privileged?  
- Has this IP attacked before?  
- Is the IP from cloud hosting (high risk)?  

### Decide severity:
- **Low:** Single user, few failed attempts, IP internal  
- **Medium:** Multiple attempts, short interval, external IP  
- **High:** Targeting admin, automated pattern, malicious reputation  

---

## 📌 4. Investigation

### Steps:
1. Pull logs for the affected asset (auth log, syslog, Windows security log).  
2. Identify timing pattern (human vs automated).  
3. Enrich the attacking IP:
   - GeoIP  
   - WHOIS  
   - Reputation checks  
4. Check for successful logins after the brute force.  
5. Review adjacent suspicious behavior:
   - Lateral movement  
   - Privileged access  
   - File changes  

---

## 📌 5. Containment

### If automated brute force is confirmed:
- Block offending IP address at firewall  
- Apply rate limiting or fail2ban  
- Disable targeted user temporarily (if needed)  
- Reset passwords for affected accounts  

---

## 📌 6. Eradication

- Ensure MFA is enabled on administrative accounts  
- Review password policy (min length, complexity)  
- Identify and patch weak authentication configurations  

---

## 📌 7. Recovery

- Re-enable accounts once secured  
- Restore normal access  
- Monitor closely for repeated activity  
- Apply additional log alerts or SIEM correlation rules  

---

## 📌 8. Lessons Learned

- Do we need stronger MFA?  
- Should rate limiting thresholds be adjusted?  
- Are admin accounts overly exposed?  
- Should automated detection rules be improved?  

---

## 📌 9. MITRE ATT&CK Mapping

- **T1110 – Brute Force**  
- **T1078 – Valid Accounts (potential next step)**  

---

## 📌 10. Summary (for executives)

A brute force attack was detected against the login service.  
The activity was automated, originating from a cloud-hosted IP with known malicious behavior.  
Containment was applied and no successful compromise was observed.  
Preventive measures were strengthened to reduce future risk.

