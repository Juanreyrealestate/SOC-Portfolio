# 🔐 Security+ — Día 20  
# Network Security: Firewalls, VPN, NAC, Zero Trust, Segmentation

## 🎯 Objetivo
Dominar los conceptos de seguridad en redes que aparecen en Security+, entrevistas SOC y en prácticamente todas las infraestructuras modernas: firewalls, VPNs, Zero Trust, Network Access Control, segmentación y más.

---

# 🟥 1. Firewalls (core de seguridad en red)

## 🔸 Firewall básico (packet filtering)
- Revisa direcciones IP, puertos, protocolos  
- Muy rápido  
- Poco inteligente  

## 🔸 Stateful Firewall
- Mantiene estado de conexiones  
- Verifica que el tráfico sea esperado  
- Mucho más seguro que el básico  

## 🔸 Next-Generation Firewall (NGFW)
El estándar actual. Incluye:
- inspección profunda (DPI)  
- detección de aplicaciones  
- prevención de intrusiones (IPS)  
- filtrado por usuario/identidad  
- integración con nube  

Es el firewall que la mayoría de empresas usa hoy.

---

# 🟦 2. IDS vs IPS

## IDS (Intrusion Detection System)
- Detecta tráfico malicioso  
- No bloquea, solo alerta  

## IPS (Intrusion Prevention System)
- Detecta y BLOQUEA  
- Suele integrarse en NGFW  

---

# 🟩 3. VPN (Virtual Private Network)

## 🔸 VPN basada en SSL/TLS
La más común hoy.  
Se accede mediante navegador.

## 🔸 VPN IPSec
Más segura para conexiones entre sitios.

## Modos IPSec:
- Transport Mode → cifra carga útil  
- Tunnel Mode → cifra TODO el paquete  

**Tunnel Mode = usado en VPN site-to-site.**

---

# 🟧 4. NAC (Network Access Control)

Controla quién puede entrar a la red.

## 🔸 Métodos:
- **802.1X** (muy usado en empresas)  
- certificados  
- posture assessment  
- validar si el equipo está sano:
  - antivirus activado  
  - parches al día  
  - sin malware  
  - configuración correcta  

Si no cumple → se envía a VLAN de cuarentena.

---

# 🟫 5. Segmentation & Isolation

## 🔸 VLANs
Separan tráfico en “islas lógicas”.  
Evitan que toda la red esté expuesta.

Ejemplos:
- VLAN de invitados  
- VLAN de servidores  
- VLAN de IoT  
- VLAN de usuarios internos  

## 🔸 DMZ
Zona aislada para servicios públicos:
- web server  
- mail server  
- DNS  
Protege la red interna.

## 🔸 Air Gap
Aislamiento físico total (e.g., sistemas críticos industriales).

---

# 🟨 6. Zero Trust (arquitectura moderna)

Principio fundamental:

> **“Nunca confíes, siempre verifica.”**

Características:
- autenticación continua  
- acceso mínimo necesario  
- segmentación estricta  
- monitoreo constante  
- no se confía en la red interna  

Usado en Google BeyondCorp, Microsoft, Okta, etc.

Zero Trust hoy es estándar de seguridad empresarial.

---

# 🟪 7. Load Balancers (Security+ Tested)

Funciones:
- distribuyen tráfico  
- previenen sobrecarga  
- permiten alta disponibilidad  

Tipos:
- **L3/L4**: IP y puertos  
- **L7**: nivel aplicación (más inteligente)  

---

# 🟦 8. Network Appliances (dispositivos clave)

## 🔸 Proxy
Filtra tráfico web  
Controla acceso  
Oculta IP interna  

## 🔸 Reverse Proxy
Protege servidores internos  
Usado para balanceo y seguridad  

## 🔸 WAF (Web Application Firewall)
Protege aplicaciones web de:
- SQLi  
- XSS  
- CSRF  
- ataques OWASP Top 10  

Muy usado en:
- Cloudflare  
- AWS  
- Azure  

---

# 🔵 9. Network Monitoring (lo que ve un SOC)

SOC analiza:
- tráfico inusual  
- escaneo de puertos  
- conexiones repetidas  
- exfiltración  
- beaconing  
- intentos de bypass de firewall  
- conexiones no autorizadas a puertos sensibles  

Puertos críticos:
- 22 SSH  
- 23 Telnet (inseguro)  
- 80 HTTP  
- 443 HTTPS  
- 3389 RDP  
- 445 SMB  
- 5900 VNC  

---

# 📝 10. Mini-Práctica

**1. ¿Qué firewall es estándar moderno?**  
➡️ NGFW (Next-Generation Firewall)

**2. ¿Qué modo IPSec cifra TODO el paquete?**  
➡️ Tunnel Mode

**3. ¿Qué herramienta bloquea y detecta intrusiones?**  
➡️ IPS

**4. ¿Qué modelo dice “nunca confíes, siempre verifica”?**  
➡️ Zero Trust

**5. ¿Qué tecnología controla acceso a la red según postura del dispositivo?**  
➡️ NAC

---

# ⭐ Resumen Final
- NGFW = firewall moderno por excelencia  
- IDS detecta, IPS bloquea  
- VPN puede ser SSL o IPSec  
- NAC evalúa dispositivos  
- Zero Trust es estándar actual de arquitectura  
- Segmentación y DMZ reducen superficie de ataque  
- Conocer puertos y dispositivos es esencial para SOC  

