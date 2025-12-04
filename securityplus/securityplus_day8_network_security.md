# 🔐 Security+ — Día 8  
# Network Security (Firewalls, IDS/IPS, VPN, Zero Trust) — Nivel A

---

## 🧠 1. ¿Qué es seguridad de red?

Es todo lo que usamos para **proteger el tráfico** que va:

- entre computadoras  
- entre servidores  
- hacia internet  

Incluye:
- firewalls  
- IDS/IPS  
- VPN  
- segmentación  
- proxies  
- Zero Trust  

---

# 🟥 2. Firewalls (el guardia de la puerta)

Un firewall decide **qué tráfico entra y qué tráfico sale** según reglas.

Piensa en:

> Un guardia en la puerta del edificio que deja pasar a algunos y a otros no.

Puede filtrar por:
- IP  
- puerto  
- protocolo  
- aplicación  

### Tipos importantes para Security+:

- **Firewall de red** → protege segmentos enteros.  
- **Firewall de host** → en la máquina (Windows Firewall, etc.).  
- **Next-Gen Firewall (NGFW)** → entiende aplicaciones (HTTP, DNS, SSL, etc.).

Ejemplo:
- Bloquear todo excepto puertos 80/443 (web).  
- Bloquear IP maliciosa específica.

---

# 🟦 3. IDS e IPS

## IDS — Intrusion Detection System
- Solo **detecta**.  
- Genera alertas cuando el tráfico parece ataque.  
- No bloquea por sí solo.

## IPS — Intrusion Prevention System
- **Detecta y BLOQUEA**.  
- Está en línea (inline).  
- Puede cortar la conexión.

Ejemplo:
- Detecta SQL injection → alerta (IDS).  
- Detecta SQL injection y lo bloquea → IPS.

---

# 🟩 4. VPN (Virtual Private Network)

La VPN crea un **túnel cifrado** entre tu equipo y otra red.

Sirve para:
- conectarse a la red de la empresa desde casa, de forma segura.  
- proteger tu tráfico en WiFi públicos.  

Importante:
- Usa **cifrado** (IPSec, SSL/TLS, etc.).  
- Hace que tu tráfico parezca venir desde la red remota.

En Security+:
- Se asocia con “túnel seguro sobre red insegura”.

---

# 🟨 5. Segmentación de red y VLANs

En vez de tener una sola red enorme, se divide en pedazos más pequeños.

Ejemplo:
- Red de Finanzas  
- Red de Recursos Humanos  
- Red de Invitados  

Beneficios:
- Si alguien compromete un segmento, no controla todo.  
- Menos lateral movement.  
- Mejor control de tráfico.

VLAN = Virtual LAN → segmentación lógica dentro de la red.

---

# 🟫 6. Proxy y Web Filtering

Un proxy está “en el medio” entre los usuarios e internet.

Sirve para:
- filtrar contenido (bloquear sitios peligrosos).  
- registrar qué webs visitan los usuarios.  
- aplicar políticas (no redes sociales, no porno, etc. en horario laboral).  

También ayuda a:
- ocultar IP interna.  
- mejorar cacheo de contenido.

---

# 🟪 7. Zero Trust (muy importante y moderno)

**Zero Trust** = “Nunca confíes por defecto, siempre verifica.”

Antes:
- “Dentro de la red todo es confiable.”

Ahora:
- Cada petición → verifica identidad, dispositivo, ubicación, riesgo.

Principios:
- Identity first (prioridad a la identidad).  
- Least Privilege.  
- Microsegmentación.  
- MFA en todas partes.

Esto está MUY de moda y lo aman en entrevistas.

---

# 🧠 8. ¿Cómo usa esto un SOC Analyst?

En un SOC tú:

- Ves logs de firewall (bloqueos, conexiones, puertos raros).  
- Ves alertas de IDS/IPS (intentos de ataque).  
- Ves eventos de VPN (logins, ubicaciones, horarios raros).  
- Ves tráfico entre segmentos (movimiento lateral).  
- Ves acceso a sitios maliciosos desde proxies.  

Muchos de tus reportes ya implican:
- bloqueos de IP  
- reglas de firewall  
- tráfico sospechoso saliente  
- conexiones internas raras

---

# 📝 9. Mini–Práctica (Estilo Security+)

**1. Un sistema que solo detecta pero no bloquea es:**  
A) Firewall  
B) IDS  
C) IPS  
➡️ **Respuesta: B**

---

**2. Un túnel cifrado sobre internet se llama:**  
A) Proxy  
B) VLAN  
C) VPN  
➡️ **Respuesta: C**

---

**3. “Nunca confiar por defecto, siempre verificar” corresponde a:**  
A) Zero Trust  
B) IDS  
C) Proxy  
➡️ **Respuesta: A**

---

**4. Diferencia principal entre IDS e IPS:**  
A) El IDS bloquea y el IPS no.  
B) El IPS bloquea y el IDS no.  
➡️ **Respuesta: B**

---

# ⭐ 10. Resumen en una línea

- **Firewall** → decide qué entra/sale.  
- **IDS/IPS** → detecta (IDS) / detecta y bloquea (IPS).  
- **VPN** → túnel cifrado seguro.  
- **Segmentación/VLAN** → separar redes para más seguridad.  
- **Proxy** → intermediario para filtrar y registrar.  
- **Zero Trust** → nunca confiar por defecto, siempre verificar.

