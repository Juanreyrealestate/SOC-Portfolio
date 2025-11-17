🔵 LOG ANALYSIS — FOUNDATIONAL NOTES (SOC Analyst)
Juan Rey — USA Remote | Bilingual EN/ES

Estilo Moderno Azul — Portafolio SOC

🔷 1. Overview / Resumen General

This report summarizes the foundational log analysis skills developed during my SOC Analyst training path.
All logs were created, parsed, and analyzed manually using Linux command-line tools, simulating real-world SOC Tier 1 tasks.

Este reporte resume las habilidades de análisis de logs desarrolladas durante mi ruta de entrenamiento como SOC Analyst.
Todos los logs fueron creados, analizados y correlacionados manualmente usando herramientas de línea de comando en Linux.

🔷 2. Skills Demonstrated / Habilidades Demostradas
✅ Linux Log Analysis

grep

wc -l

sort

uniq -c

cut

head / tail

✅ SOC Fundamentals

Identificación de fuerza bruta

Clasificación de IP interna vs externa

Reconocimiento de IOCs

Patrones en múltiples fallos de autenticación

Actividad sospechosa repetida

Correlación de logs con timestamps

✅ Git & Documentation

GitHub portfolio structure

Evidence logging

Organized SOC folder system

Structured report writing

🔷 3. Logs Analysed / Logs Analizados
✔ servidor.log

Authentication flow: OK events, failed logins, suspicious events.

✔ frecuencia.log

High repetition failed attempts → ideal brute-force pattern.

✔ big.log (500 lines)

Large-scale brute-force, multiple IOCs, port scanning, outbound connections, and recon patterns.

🔷 4. Key Linux Commands (Explained Simply)
grep

Search for patterns in a file.

grep "ERROR" archivo.log

wc -l

Count lines (useful for count of attacks).

grep "ERROR" archivo.log | wc -l

sort

Order lines alphabetically or by numeric value.

uniq -c

Count unique repeated patterns.

grep "ERROR" big.log | cut -d " " -f 7 | sort | uniq -c

cut

Extract specific fields (example: extract IP from logs).

cut -d " " -f 7

🔷 5. SOC Findings / Hallazgos
🔹 5.1 Brute-Force Detection

Patterns show multiple failed authentication attempts from external IPs:

203.0.113.10 → High-frequency fail attempts

198.51.100.50 → Secondary attacker

185.231.45.90 → Scanning behavior

Conclusion:
Clear brute-force and credential stuffing patterns.

🔹 5.2 IOC Detection

Domains detected:

malware-check.evil-domain.com

suspicious-update.evil-domain.com

backup-sync.evil-domain.com

Repeated outbound calls indicate possible malware or botnet callbacks.

🔹 5.3 Internal vs External IP Classification
Internal (RFC1918)

10.x.x.x

192.168.x.x

172.16.x.x – 172.31.x.x

External

Anything outside internal ranges → potential attacker

🔷 6. Summary of Attack Pattern Identified

1. Reconnaissance (port scans)
185.231.45.90 repeatedly scans ports.

2. Brute Force Attempts
203.0.113.10 → repeated authentication failures.

3. Credential Stuffing
198.51.100.50 → multiple attempt clusters.

4. Outbound connections to suspicious domains
Possible C2 (Command & Control) indicators.

🔷 7. Impact Assessment

If real, these events would indicate:

High likelihood of password spraying

Attempted unauthorized access

Potential compromised system beaconing out

Need for immediate firewall action

🔷 8. Recommendations

✔ Block IP range 203.0.113.0/24
✔ Implement MFA for all accounts
✔ Quarantine machine showing outbound connections
✔ Enhance detection rules for repeated failed logins
✔ Add alert for specific IOCs detected
✔ Enable logging of east-west internal movement

🔷 9. Tools Used

macOS Terminal

Linux CLI suite (grep, sort, uniq, cut, wc)

GitHub (evidence storage)

Manual log creation / simulation

🔷 10. Conclusion

These foundational exercises demonstrate the core capabilities required for a SOC Tier 1 Analyst.
They show practical, hands-on detection of brute-force attacks, IOC correlation, suspicious outbound behavior, and structured reporting.

🔵 END OF REPORT
