# 🔐 Security+ — Día 43  
# Firewalls, IDS/IPS, Zero Trust & Network Defense (explicación fácil)

## 🎯 Objetivo
Entender cómo funcionan los firewalls modernos, IDS/IPS y Zero Trust de manera simple, práctica y alineada a entrevistas de SOC, Threat Hunting y Cloud Security.

---

# 🟥 1. Firewalls

Un firewall filtra tráﬁco y decide qué entra o sale.

TIPOS:

1) Packet Filtering Firewall  
Mira IP origen, IP destino, puerto y protocolo. Básico.

2) Stateful Firewall  
Entiende el estado de la conexión (si está establecida o no).  
Evita ataques como SYN flood.

3) NGFW (Next-Generation Firewall)  
Incluye inspección profunda, control de aplicaciones, antimalware, bloqueo de C2, filtrado web y análisis de usuario.

Ejemplos: Palo Alto, Fortinet, Cisco Firepower.

---

# 🟧 2. IDS/IPS

IDS = detecta y alerta.  
IPS = detecta y bloquea.

Técnicas de detección:
- Por firmas (ataques ya conocidos).  
- Por anomalías (comportamiento raro).  
- Por comportamiento (secuencias MITRE).

---

# 🟨 3. Detecciones típicas en IDS/IPS

Ejemplos comunes:

1) Port Scan  
Muchos puertos consultados en segundos.

2) SQL Injection  
Patrones como:  
' OR 1=1 --  
(Se deja así, sin formato de bloque, para no romper el editor.)

3) Buffer Overflow  
Peticiones con datos extremadamente grandes.

4) Command & Control  
Conexiones repetidas a una IP desconocida con paquetes pequeños y constantes.

---

# 🟦 4. Zero Trust

Zero Trust = “Nunca confíes, verifica siempre.”

Principios:
- MFA obligatorio.  
- Microsegmentación (dividir la red en zonas pequeñas).  
- Menor privilegio (cada usuario solo lo necesario).  
- Verificación continua (no basta un login).  

Zero Trust evita movimiento lateral y el uso de credenciales robadas.

---

# 🟪 5. Cómo trabajan juntos Firewall + IDS/IPS + Zero Trust

Caso real: Malware con C2  
- NGFW bloquea IP maliciosa.  
- IDS detecta patrón de C2.  
- Zero Trust evita que el atacante acceda a otros sistemas.

Caso real: usuario comprometido  
- MFA bloquea acceso del atacante.  
- IDS detecta comportamiento raro.  
- Zero Trust limita permisos y evita movimiento lateral.

---

# 🟫 6. Preguntas de entrevista típicas

¿Qué es un firewall stateful?  
→ Un firewall que rastrea el estado de las conexiones y permite solo tráfico válido dentro del flujo TCP.

Diferencia entre IDS e IPS:  
→ IDS detecta. IPS detecta y bloquea.

Qué es Zero Trust:  
→ Modelo donde nada se confía por defecto; todo se valida continuamente.

Qué es un NGFW:  
→ Firewall moderno con inspección profunda, control de aplicaciones y protección contra malware/C2.

Cómo evitar movimiento lateral:  
→ Microsegmentación, MFA, firewalls internos, Zero Trust, detección de anomalías.

---

# ⭐ Resumen del Día 43

Aprendiste:
- firewalls clásicos, stateful y NGFW  
- diferencias entre IDS e IPS  
- detecciones típicas (port scan, SQLi, C2, buffer overflow)  
- Zero Trust explicado simple  
- cómo se ven estos conceptos en ataques reales  
- respuestas exactas de entrevista para roles SOC II / Threat Hunter Jr  
