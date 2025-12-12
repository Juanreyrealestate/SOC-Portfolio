# 🔐 Security+ — Día 49  
# SIEM Fundamentals (Splunk, Sentinel, Elastic) — Versión Clara y Estética

============================================================
🎯 OBJETIVO
============================================================
Entender qué es un SIEM, cómo trabaja, qué logs procesa, qué alertas genera y cómo investiga un analista SOC.  
Esto es fundamental para entrevistas y para roles SOC I, SOC II y Threat Hunter Jr.

============================================================
1) ¿QUÉ ES UN SIEM?
============================================================
Un SIEM es una plataforma central que:
• Recolecta logs  
• Normaliza datos  
• Correlaciona eventos  
• Detecta actividad sospechosa  
• Genera alertas  
• Permite investigar incidentes  

Ejemplos reales usados por empresas:
• Splunk  
• Microsoft Sentinel  
• Elastic SIEM  
• QRadar  
• ArcSight  

============================================================
2) ¿QUÉ FUNCIONES REALIZA UN SIEM?
============================================================
• Recolección de logs desde Windows, Linux, firewalls, cloud y EDR  
• Correlación de eventos entre múltiples fuentes  
• Análisis de comportamiento  
• Generación automática de alertas  
• Dashboards para investigación  
• Reporting para cumplimiento  

============================================================
3) LOGS MÁS IMPORTANTES ENVIADOS AL SIEM
============================================================
WINDOWS:  
• 4624 (login exitoso)  
• 4625 (login fallido)  
• 4672 (privilegios especiales)  
• PowerShell 4103 / 4104  
• Sysmon (procesos, conexiones, hashes)  

LINUX:  
• auth.log (SSH, sudo, login)  
• syslog (sistema, servicios)  

FIREWALL:  
• tráfico permitido/denegado  
• puertos y direcciones  

CLOUD:  
• Cambios en IAM, buckets, permisos, roles  

EDR:  
• detecciones de malware  
• actividad sospechosa  
• comunicación con C2  

============================================================
4) ¿CÓMO SE VEN ALERTAS REALES EN EL SIEM?
============================================================
Alerta típica de fuerza bruta:
• Múltiples intentos fallidos de login para un usuario  
• Misma IP intentando repetidamente  
Interpretación: posible ataque automatizado

Alerta de PowerShell sospechoso:
• Uso de comandos codificados  
• Lanzado por procesos inusuales como Office  
Interpretación: posible macro maliciosa

Alerta de C2 (Command and Control):
• Conexiones periódicas a IP desconocida  
• Proceso extraño comunicándose hacia afuera  
Interpretación: beaconing de malware

============================================================
5) CÓMO INVESTIGA UN ANALISTA SOC EN EL SIEM
============================================================
1. Revisar la alerta  
2. Confirmar usuario, host, horario  
3. Revisar logs relacionados (Windows, Sysmon, firewall)  
4. Correlacionar actividad antes y después  
5. Determinar si es falso positivo o incidente real  
6. Escalar si corresponde  

============================================================
6) DETECCIONES SOC MÁS COMUNES
============================================================
• Fuerza bruta → muchos 4625 seguidos, luego 4624  
• RDP sospechoso → logon type 10 desde IP inusual  
• PowerShell peligroso → comandos codificados  
• Persistencia → creación de usuarios o servicios nuevos  
• C2 → conexiones repetidas a IP desconocida  
• SSH brute force en Linux  

============================================================
7) PREGUNTAS DE ENTREVISTA
============================================================
• ¿Qué es un SIEM?  
  Plataforma que recolecta, correlaciona y alerta sobre eventos.

• ¿Qué logs entran?  
  Windows, Linux, firewall, EDR, cloud.

• ¿Cómo detectas fuerza bruta?  
  Secuencia de múltiples intentos fallidos seguida por uno exitoso.

• ¿Cómo detectas PowerShell malicioso?  
  Comandos codificados o procesos parent sospechosos.

• ¿Por qué Sysmon es tan importante?  
  Porque revela procesos, conexiones, parent-child processes y hashes.

============================================================
⭐ RESUMEN DEL DÍA 49
============================================================
Hoy aprendiste:  
• Cómo funciona un SIEM  
• Qué logs procesa  
• Cómo se ven alertas reales  
• Cómo investiga un SOC  
• Cuáles son las detecciones más comunes  
• Qué suelen preguntar en entrevistas  
