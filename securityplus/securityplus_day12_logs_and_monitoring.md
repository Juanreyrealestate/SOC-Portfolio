# 🔐 Security+ — Día 12  
# Logs & Monitoring (SIEM, UEBA, DLP, Alerts) — Nivel A

---

# 🧠 1. ¿Qué son los logs?

Los **logs** son registros de todo lo que hace un sistema.

Ejemplos:
- “Usuario juan.r inició sesión”
- “Se creó un nuevo archivo”
- “Servicio X falló”
- “Se hizo una conexión desde IP 10.0.0.5 al puerto 443”

Tipos de logs:
- Logs de sistema (Windows, Linux)
- Logs de red (firewalls, routers)
- Logs de aplicaciones (web, bases de datos)
- Logs de seguridad (antivirus, EDR, DLP, IAM)

Sin logs → no puedes investigar NADA.

---

# 🟦 2. ¿Qué es un SIEM?

SIEM = **Security Information and Event Management**

Es una plataforma que:
1. Recibe logs de muchas fuentes  
2. Los normaliza (los hace entendibles)  
3. Aplica reglas y correlación  
4. Genera alertas  
5. Permite investigar incidentes

Ejemplos de SIEM:
- Splunk
- Microsoft Sentinel
- QRadar
- Elastic SIEM

En un SOC tú:
- miras alertas en el SIEM  
- filtras  
- investigas  
- creas reportes (como los de tu portafolio)

---

# 🟩 3. Qué es “correlación” en el SIEM

Ya lo has hecho en tus reportes SOC.

Correlación = juntar múltiples eventos para ver si forman un ataque.

Ejemplo:
- login raro  
- ejecución de PowerShell  
- conexión a IP maliciosa  
- descarga de payload  

Individualmente son “ruido”.  
Juntos = incidente serio.

---

# 🟧 4. UEBA — User and Entity Behavior Analytics

UEBA = sistema que analiza el **comportamiento** de:
- usuarios  
- máquinas  
- aplicaciones  

Y busca:
- cosas fuera de lo normal para ese usuario  
- patrones de insider threat  
- compromiso de cuentas

Ejemplos:
- Usuario que nunca accede de madrugada → hoy sí, y descarga 3GB.  
- Empleado de marketing leyendo carpetas de finanzas.  
- Inicios de sesión desde países nuevos.

UEBA asigna **riesgo** al comportamiento.

---

# 🟥 5. DLP (Data Loss Prevention) en monitoreo

DLP monitorea:
- archivos  
- emails  
- subidas a la nube  
- copias a USB  

Busca:
- números de tarjeta
- datos personales (PII)
- registros médicos
- archivos confidenciales

Si ve algo raro:
- alerta  
- bloquea  
- registra evento  

Se integra con el SIEM para ver exfiltración y abuso de datos.

---

# 🟫 6. Tipos de alertas en un entorno real

Ejemplos de alertas que vería un analista SOC:

- “Multiple failed logins for user X”  
- “Suspicious PowerShell execution detected”  
- “Large data transfer to external IP”  
- “New admin account created”  
- “Unusual sign-in location (impossible travel)”  
- “DLP: uploaded sensitive data to Dropbox”  
- “UEBA: risk score for user increased from 10 → 90”

Tú ya has trabajado con casi todos estos escenarios.

---

# 🧠 7. Buenas prácticas de logging y monitoreo

- Activar logs donde importan (servidores, AD, cloud, endpoints, firewalls)  
- Enviar todos al SIEM  
- No guardar logs inútiles (ruido excesivo)  
- Retención adecuada (mínimo 90 días, ideal 1 año o más)  
- Tener reglas de correlación basadas en MITRE ATT&CK  
- Revisar y afinar alertas (evitar demasiados falsos positivos)

---

# 📝 8. Mini-práctica (Estilo Security+)

**1. ¿Qué hace un SIEM?**  
A) Solo almacena logs  
B) Recolecta, normaliza, correlaciona y alerta  
➡️ **Respuesta: B**

---

**2. UEBA se enfoca en:**  
A) Comportamiento de usuarios y entidades  
B) Cifrar tráfico web  
➡️ **Respuesta: A**

---

**3. DLP está diseñado para:**  
A) Evitar fuga de datos sensibles  
B) Bloquear todas las conexiones a internet  
➡️ **Respuesta: A**

---

**4. ¿Qué necesitas para investigar un incidente?**  
A) Logs  
B) Solo firewall  
➡️ **Respuesta: A**

---

# ⭐ 9. Resumen Final

- **Logs** = registro de todo lo que pasa.  
- **SIEM** = junta logs, correlaciona y alerta.  
- **UEBA** = analiza comportamiento de usuarios/entidades.  
- **DLP** = evita fuga de datos.  
- Sin logs, no hay investigación ni detección efectiva.

