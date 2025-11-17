LOG ANALYSIS — FOUNDATIONAL SKILLS (USA Remote)
Juan Rey — SOC Analyst (Entry Level)

(Bilingual EN/ES)

🟦 1. Overview / Resumen General

This document summarizes my first hands-on log analysis exercises as part of my SOC Analyst learning path.
All logs were manually parsed using Linux command-line tools to identify authentication failures, suspicious IP activity, IOC patterns, and brute-force attack indicators.

Este documento resume mis primeras prácticas reales de análisis de logs como parte de mi ruta SOC Analyst.
Todos los logs fueron analizados usando herramientas de línea de comando en Linux para identificar fallas de autenticación, actividad sospechosa, patrones de IOCs y señales de ataques de fuerza bruta.

🟧 2. Skills Demonstrated / Habilidades Demostradas
✔ Linux log analysis (grep, sort, wc, uniq, cut)
✔ Failed login detection
✔ Identification of malicious external IPs
✔ IOC detection & correlation
✔ Pattern frequency counting
✔ Separation between internal vs external IP ranges
✔ Creating/organizing SOC evidence folders
✔ Writing structured SOC findings
✔ Git/GitHub repository management
🟩 3. Logs Analysed / Logs Analizados
servidor.log

Authentication activity including OK events, failed login attempts, and suspicious IP access.

frecuencia.log

Large number of repeated failed attempts, ideal for brute-force pattern detection.

🟦 4. Key Linux Commands Used (Explained Simply)
grep — search
grep "ERROR" archivo.log


Busca líneas que contienen la palabra ERROR.

wc -l — count
grep "ERROR" archivo.log | wc -l


Cuenta cuántos errores hubo.

sort — order
sort archivo.log

uniq -c — group + count duplicates
sort archivo.log | uniq -c

cut — extract fields
cut -d " " -f 7


Extrae un campo específico (ej: la IP).

🟥 5. Findings / Hallazgos SOC
5.1 Detection of Brute-Force Pattern

Using:

grep "ERROR" frecuencia.log | wc -l


→ 16 failed logins detected.

Then:

grep "ERROR" frecuencia.log | cut -d " " -f 7 | sort | uniq -c

Result (example):
11 203.0.113.10   (external malicious source)
5  192.168.1.50   (internal source)


Interpretation:

203.0.113.10 → repeated failed logins from a malicious external IP

Likely brute-force attack attempt

🟫 5.2 Suspicious External Connections

From servidor.log:

Multiple failed logins from 203.0.113.10

Classified as external public IP

Potential indication of:

Credential stuffing

Password guessing

Bot traffic

🟪 6. Classification: Internal vs External IPs
Internal IP ranges (RFC1918)

10.x.x.x

192.168.x.x

172.16 – 172.31.x.x

External IPs (Internet):

Any IP outside those ranges → potentially attacker.

🟩 7. Takeaways / Conclusiones

You can already analyze logs at a real SOC Tier 1 level.

You know how to detect brute-force attacks.

You understand IOC recurrence.

You know how to classify suspicious IP sources.

You're building professional, real evidence for your portfolio.

🟦 8. Next Steps / Próximos Pasos
✔ Add big.log
✔ Add ioc.log
✔ Add lateral.log
✔ Write Investigation #6 (Lateral Movement)
✔ Add dashboards (matplotlib → PDF ready)
✔ Add TryHackMe progress badge
✔ Apply for SOC Analyst roles
🟩 9. Why This Matters

This page demonstrates real, practical, hands-on knowledge.
Not theory. Not copy/paste.
Actual SOC analysis.

Recruiters LOVE this.

🟧 10. End of Notes / Fin de Notas
