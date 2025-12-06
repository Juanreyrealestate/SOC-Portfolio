# 🔐 Security+ — Día 13  
# Secure Network Design (DMZ, VLANs, NAC, Proxy, Reverse Proxy)

---

# 🧠 1. ¿Qué es “diseño seguro de red”?

Es la forma en que las empresas organizan sus redes para que:
- los atacantes no puedan entrar fácilmente  
- se limite el daño si logran entrar  
- los servicios públicos estén aislados  
- los usuarios internos no tengan acceso a todo  

Diseñar bien la red = aumentar seguridad sin complicar el negocio.

---

# 🟦 2. DMZ (Zona Desmilitarizada)

Una **DMZ** es una red intermedia entre internet y la red interna.

Aquí se colocan servidores accesibles desde internet, por ejemplo:
- servidores web  
- servidores DNS  
- portales públicos  
- APIs expuestas  

¿Por qué?

Porque si alguien compromete un servidor en la DMZ,  
**no puede entrar directamente a la red interna**.

La DMZ es protección + contención.

---

# 🟩 3. VLANs (Virtual LANs)

Son segmentos virtuales dentro de la red para separar tráfico.

Ejemplos:
- VLAN de empleados  
- VLAN de invitados  
- VLAN de finanzas  
- VLAN de servidores  

Ventajas:
- reduce impacto del movimiento lateral  
- limita acceso  
- mejora visibilidad para SOC  
- facilita políticas de segmentación  

---

# 🟧 4. NAC — Network Access Control (control de acceso a la red)

NAC decide **quién puede entrar** a la red y bajo qué condiciones.

Ejemplos:
- “Solo laptops corporativos pueden conectarse”  
- “Si no tienes antivirus → no entras”  
- “Invitados van a la VLAN de invitados”  

Dos tipos:
- **Pre-admission** → antes de entrar  
- **Post-admission** → monitoreo continuo después de entrar  

---

# 🟥 5. Reverse Proxy (muy importante en empresas modernas)

Un reverse proxy está **frente a los servidores**,  
recibe el tráfico y se lo pasa a los servidores internos.

Beneficios:
- oculta la red interna  
- protege servidores  
- balancea carga  
- cachea contenido  
- agrega autenticación adicional  
- permite filtrar tráfico malicioso  

Ejemplos:
- NGINX reverse proxy  
- Cloudflare  
- AWS CloudFront  

Para SOC:
- fácil detectar tráfico malicioso  
- muy útil para detección de C2 y bots

---

# 🟫 6. Proxies (Forward Proxy)

Un forward proxy actúa entre los usuarios y el internet.

Sirve para:
- bloquear sitios  
- registrar actividad  
- proteger IP real  
- filtrar descargas peligrosas

El reverse proxy protege servidores.  
El forward proxy protege usuarios.

---

# 🟪 7. VPN (Virtual Private Network)

La VPN crea un **túnel cifrado** a través de internet.

Usos:
- empleados se conectan a la red de la empresa  
- proteger tráfico en redes públicas  
- acceso remoto seguro  

Protocolos:
- IPSec  
- SSL/TLS  
- WireGuard  

---

# 🟫 8. Secure Network Zoning (zonificación por seguridad)

Técnica para dividir la red en niveles de sensibilidad:

Ejemplo:

| Zona | Contenido | Seguridad |
|------|-----------|-----------|
| Pública | servidores web | media |
| Interna | usuarios regulares | alta |
| Segura | finanzas, HR, credenciales | muy alta |

A los atacantes se les dificulta avanzar entre zonas.

---

# 🧠 9. ¿Cómo usa esto un SOC Analyst?

TÚ usarás esta información para:

- saber dónde se generan los logs,  
- entender por qué ciertos accesos son sospechosos,  
- detectar movimiento lateral prohibido,  
- analizar tráfico que intenta cruzar zonas,  
- ver cuándo un atacante intenta saltar VLANs,  
- revisar tráfico hacia/desde DMZ,  
- entender patrones anómalos en redes segmentadas,  
- detectar C2 escondido detrás de reverse proxies.

Ejemplos reales:
- tráfico interno tocando la DMZ = sospechoso  
- tráfico de invitados accediendo finanzas = imposible  
- intento de cross-VLAN = lateral movement  
- conexiones inusuales hacia proxies = posible exfiltración  

---

# 📝 10. Mini-práctica (Security+ Style)

**1. ¿Qué es una DMZ?**  
➡️ Una red intermedia que protege la red interna de servidores expuestos.

---

**2. ¿Qué separan las VLANs?**  
➡️ Segmentos de red para limitar acceso y movimiento lateral.

---

**3. ¿Qué hace un reverse proxy?**  
➡️ Protege y oculta servidores internos.

---

**4. ¿Qué hace NAC?**  
➡️ Decide quién entra a la red y en qué condiciones.

---

# ⭐ 11. Resumen Final  
- DMZ = aislar servidores expuestos  
- VLANs = segmentar la red para seguridad  
- NAC = control de acceso a red  
- Reverse Proxy = protege servidores internos  
- VPN = túnel cifrado  
- Forward Proxy = filtro entre usuarios e internet  
- SOC usa todo esto para entender tráfico normal vs malicioso

