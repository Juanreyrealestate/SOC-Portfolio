# 🛡️ Reporte 09 — Persistence Detection (Detección de Persistencia)

## 🎯 Objetivo
Identificar indicadores de persistencia utilizados por un atacante para mantener acceso continuo a un sistema comprometido.

---

## 🧩 1. Datos del incidente

Máquina afectada: **WIN-233**

Eventos detectados:

| Hora     | Evento |
|----------|--------|
| 03:10 AM | New user created: audit_backup$ (hidden) |
| 03:11 AM | User added to Administrators group |
| 03:15 AM | Scheduled task created: “Windows Update Service Checker” |
| 03:15 AM | Task executes: powershell -enc JAB… (payload) |
| 03:20 AM | Firewall rule created for outbound port 8088 |

---

## 🧠 2. Análisis (razonamiento humano)

- El usuario “audit_backup$” tiene un nombre diseñado para parecer legítimo pero está oculto (“$”).  
- Agregarlo al grupo Administrators permite control completo del sistema.  
- La tarea programada ejecuta PowerShell codificado → indicio claro de malware persistente.  
- Crear una regla de firewall saliente permite comunicación externa continua.
- La actividad ocurre de madrugada, fuera del horario laboral.  

Patrón → **persistencia establecida por atacante**.

---

## 🚨 3. Conclusión
El atacante ha implementado múltiples mecanismos de persistencia en WIN-233, incluyendo cuentas ocultas, tareas programadas y comunicación externa.  
El objetivo es mantener acceso continuo incluso si la sesión original es cerrada.

---

## 🛡️ 4. Acciones recomendadas

1. Aislar inmediatamente WIN-233.  
2. Eliminar cuenta “audit_backup$” y revisar otras cuentas sospechosas.  
3. Eliminar la tarea programada maliciosa.  
4. Bloquear la regla de firewall creada.  
5. Analizar el payload PowerShell.  
6. Revisar otras máquinas por artefactos similares.

---

## 🧭 5. MITRE ATT&CK

- **T1136 — Create Account (Persistence)**  
- **T1053 — Scheduled Task**  
- **T1547 — Boot or Logon Autostart Execution**  
- **T1021 — Remote Services**

---

## 📝 6. Resumen Ejecutivo
Se detectaron mecanismos de persistencia maliciosa creados por un atacante en la máquina WIN-233.  
El objetivo es mantener acceso continuo al sistema mediante cuentas ocultas, tareas programadas y reglas de firewall manipuladas.  
El incidente requiere contención inmediata y análisis forense completo.

