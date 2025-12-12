# 🔐 Security+ — Día 49  
# SIEM Fundamentals (Splunk, Sentinel, Elastic) — explicado fácil

## 🎯 Objetivo
Entender qué es un SIEM, qué hace, qué logs procesa, cómo genera alertas y cómo lo usa un analista SOC/Threat Hunter.  
Este tema es clave en entrevistas y en el trabajo diario.

---

## 🟥 1. ¿Qué es un SIEM?

SIEM = *Security Information and Event Management*.

En palabras simples, un SIEM es una plataforma que:

- **Recolecta** logs de muchos sistemas distintos  
- **Normaliza** la información para que tenga un formato similar  
- **Correlaciona** eventos para encontrar patrones sospechosos  
- **Genera alertas** cuando detecta posibles ataques  
- **Permite investigar** incidentes con búsquedas y dashboards  

Ejemplos de SIEM que se usan en empresas:

- Splunk  
- Microsoft Sentinel  
- Elastic SIEM  
- IBM QRadar  
- ArcSight  

---

## 🟧 2. ¿Qué funciones realiza un SIEM?

Un SIEM típico hace:

1. **Ingesta de logs**  
   - Windows (Event Logs, Sysmon)  
   - Linux (auth.log, syslog)  
   - Firewalls  
   - EDR/antivirus  
   - Cloud (AWS, Azure, GCP)  
   - Aplicaciones y bases de datos  

2. **Normalización**  
   Convierte formatos distintos a un modelo común (por ejemplo, siempre tener campos como `user`, `host`, `ip`, `action`).

3. **Correlación**  
   Junta eventos relacionados para detectar ataques completos, no solo eventos aislados.

4. **Alerting**  
   Crea alertas cuando las reglas o detecciones encuentran algo sospechoso.

5. **Dashboards e investigación**  
   Permite a los analistas buscar por usuario, IP, hostname, evento, tiempo, etc., y reconstruir lo que pasó.

---

## 🟨 3. Logs más importantes que entran al SIEM

### 🔹 Windows

- **4624** → logon exitoso  
- **4625** → logon fallido  
- **4672** → privilegios especiales asignados  
- **4103 / 4104** → comandos y scripts de PowerShell  
- **Sysmon** → creación de procesos, conexiones de red, hashes, acceso a procesos, archivos creados, etc.

### 🔹 Linux

- **auth.log / secure** → logins, SSH, sudo  
- **syslog / messages** → eventos del sistema, servicios, errores  

### 🔹 Firewall / red

- tráfico permitido y bloqueado  
- puertos origen/destino  
- IP origen/destino  

### 🔹 Cloud

- cambios en IAM (usuarios, roles, policies)  
- configuración de buckets/almacenamiento  
- cambios de seguridad en recursos cloud  

### 🔹 EDR

- detección de malware  
- comportamiento de procesos  
- conexiones a posibles C2  

---

## 🟦 4. ¿Cómo se ve una alerta dentro de un SIEM?

### ⚠ Ejemplo 1 — Fuerza bruta

Regla típica:

- muchos eventos **4625** (fallidos) para el mismo usuario  
- desde la misma IP  
- en poco tiempo  

Interpretación SOC:

- intento de fuerza bruta  
- revisar si luego hay un **4624** (login exitoso) para el mismo usuario  

---

### ⚠ Ejemplo 2 — PowerShell sospechoso

Alerta:

- PowerShell con parámetros raros o codificados  
- parent process inusual (por ejemplo, Word o Excel)  

Interpretación:

- posible macro maliciosa  
- posible script de ataque (living off the land)  

---

### ⚠ Ejemplo 3 — C2 (Command and Control)

Alerta:

- proceso desconocido conectándose repetidamente a la misma IP externa  
- paquetes pequeños y frecuentes (beaconing)  

Interpretación:

- posible malware comunicándose con servidor de comando y control  

---

## 🟪 5. Flujo de investigación en un SIEM (cómo trabaja un SOC)

1. **Revisar la alerta primaria**  
   - tipo de alerta  
   - usuario  
   - host  
   - IP  
   - hora  

2. **Buscar eventos relacionados**  
   - logons (4624, 4625)  
   - creación de procesos (Sysmon 1)  
   - conexiones de red (Sysmon 3, firewall)  
   - eventos de PowerShell (4103, 4104)  

3. **Contextualizar**  
   - ¿El usuario suele conectarse a esa hora?  
   - ¿La IP es interna, externa o de otro país?  
   - ¿El proceso es legítimo o raro?  

4. **Clasificar**  
   - benigno  
   - falso positivo  
   - incidente real  

5. **Escalar o cerrar**  
   - si es real, se escala a IR (Incident Response)  
   - si es falso positivo, se ajustan reglas y umbrales  

---

## 🟫 6. Detecciones comunes que debes conocer

- **Fuerza bruta:**  
  muchos 4625 seguidos, luego 4624 para el mismo usuario/IP.

- **RDP sospechoso:**  
  4624 con logon type 10 desde IP inusual o fuera de horario.

- **PowerShell malicioso:**  
  comandos codificados, uso de `ExecutionPolicy Bypass`, llamado desde Office.

- **Persistencia:**  
  creación de nuevas cuentas, servicios, tareas programadas.

- **C2:**  
  conexiones periódicas desde un proceso raro a una IP desconocida.

- **SSH brute force (Linux):**  
  muchas líneas de “Failed password” en auth.log.

---

## 🟩 7. Preguntas típicas de entrevista sobre SIEM

- **¿Qué es un SIEM?**  
  Plataforma que recolecta, normaliza, correlaciona y alerta sobre eventos de seguridad.

- **¿Qué tipo de logs entran a un SIEM?**  
  Windows, Linux, firewall, EDR, cloud, aplicaciones.

- **¿Cómo detectar fuerza bruta en un SIEM?**  
  múltiples intentos de logon fallidos seguidos por un logon exitoso.

- **¿Cómo detectar PowerShell sospechoso?**  
  comandos codificados o lanzados por procesos como Word/Excel.

- **¿Por qué Sysmon es tan valioso en un SIEM?**  
  porque da contexto profundo: procesos, parent/child, conexiones de red, hashes, acceso a procesos y archivos.

---

## ⭐ Resumen del Día 49

Hoy aprendiste:

- qué es un SIEM y qué hace  
- qué fuentes de logs alimentan al SIEM  
- cómo se ven alertas típicas (fuerza bruta, PowerShell, C2)  
- cómo investiga un SOC un incidente dentro del SIEM  
- detecciones básicas que debes reconocer  
- preguntas de entrevista relacionadas con SIEM  

Este módulo te acerca directamente al tipo de trabajo que hace un **SOC Analyst II / Threat Hunter Jr** en el día a día.

