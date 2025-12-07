# 🔐 Security+ — Día 18  
# Secure Application Development, OWASP & SDLC

## 🎯 Objetivo
Aprender cómo se desarrolla software seguro, cuáles son los errores más comunes (OWASP Top 10) y cómo se estructura un ciclo de desarrollo seguro (SDLC). Esto aparece MUCHO en Security+ y es clave en entrevistas SOC.

---

# 🟦 1. Secure Application Development (base fundamental)

## 🔹 Principio de “Secure by Design”
Las aplicaciones deben ser seguras desde el inicio, no como parche al final.

## 🔹 Input Validation
Regla #1: **nunca confíes en la entrada del usuario**.  
Evita:
- inyección SQL  
- inyección de comandos  
- XSS  

## 🔹 Error Handling seguro
Errores detallados = fugas de información.  
Errores correctos:
- genéricos  
- sin rutas internas  
- sin mostrar credenciales  

## 🔹 Logging & Monitoring
Aplicaciones deben registrar eventos críticos:
- logins fallidos  
- cambios de permisos  
- accesos sospechosos  
- errores del sistema  

---

# 🟥 2. OWASP Top 10 (versión simplificada para Security+)

## 1️⃣ Broken Access Control
El más crítico hoy.  
Errores de permisos permiten:
- ver datos ajenos  
- cambiar configuraciones  
- elevar privilegios  

## 2️⃣ Cryptographic Failures
Fallos en cifrado = robo de datos.  
Ejemplos:
- TLS débil  
- claves mal gestionadas  

## 3️⃣ Injection (SQL Injection)
Ejemplo clásico:
SELECT * FROM users WHERE username = '' OR 1=1 --

Super común.

## 4️⃣ Insecure Design
Arquitectura débil → ataques inevitables.

## 5️⃣ Security Misconfiguration
Errores típicos:
- S3 buckets públicos  
- puertos abiertos  
- firewalls desconfigurados  

## 6️⃣ Vulnerable Components
Bibliotecas desactualizadas → exploits.

## 7️⃣ Identification & Authentication Failures
Problemas con:
- MFA  
- sesiones  
- tokens  
- contraseñas débiles  

## 8️⃣ Software Integrity Failures
Ataques supply chain.  

## 9️⃣ Logging & Monitoring Failures
No detectar ataques por falta de registro.  

## 🔟 Server-Side Request Forgery (SSRF)
El servidor hace solicitudes peligrosas en nombre del atacante.

---

# 🟩 3. SDLC (Software Development Life Cycle)

### Fases importantes:

## 1️⃣ Requirements
Definir necesidades de seguridad:
- cifrado  
- autenticación  
- integridad  

## 2️⃣ Design
Modelado de amenazas  
Uso de principios seguros  

## 3️⃣ Development
Codificación segura  
Pruebas unitarias  

## 4️⃣ Testing
- pruebas de seguridad  
- análisis estático (SAST)  
- dinámico (DAST)  
- fuzzing  

## 5️⃣ Deployment
Configurar entorno seguro:
- TLS  
- firewalls  
- permisos mínimos  

## 6️⃣ Maintenance
Parches, monitoreo, logs, actualizaciones.

---

# 🟧 4. Secure Coding & Hardening

## 🔹 Least Privilege
La app solo debe tener permisos necesarios.

## 🔹 Defense in Depth
Capas de seguridad superpuestas.

## 🔹 Secrets Management
Nunca guardar claves en:
- el código  
- archivos de texto  
- repositorios  

Usar:
- vaults  
- AWS Secrets Manager  
- Azure Key Vault  

## 🔹 API Security
Muy importante hoy:
- rate limiting  
- claves rotativas  
- autorización correcta  

---

# 🟥 5. Web Security Essentials (SOC usa esto diario)

## 🔹 XSS (Cross-Site Scripting)
El atacante inyecta JavaScript malicioso.

## 🔹 CSRF (Cross-Site Request Forgery)
El usuario ejecuta acciones sin querer.

## 🔹 SQL Injection
Manipulación directa de bases de datos.

---

# 🧭 6. ¿Qué mira un SOC en aplicaciones?
Aunque SOC no programa apps, sí detecta:

- ataques a APIs  
- tráfico extraño hacia endpoints  
- explotación de inyección  
- actividad anormal en sesiones  
- abuso de tokens  
- brute force a logins  
- errores masivos (error 500, etc.)  

---

# 📝 7. Mini-Práctica

**1. ¿Qué significa Input Validation?**  
➡️ Validar y sanitizar toda entrada del usuario.

**2. ¿Cuál es el riesgo de mostrar errores detallados?**  
➡️ Divulgar información sensible (paths, versiones).

**3. ¿Qué componente del SDLC detecta vulnerabilidades antes del despliegue?**  
➡️ Testing (SAST/DAST).

**4. ¿Cuál es la vulnerabilidad más crítica hoy?**  
➡️ Broken Access Control.

---

# ⭐ Resumen Final
- OWASP Top 10 = las vulnerabilidades más comunes del mundo  
- SDLC = ciclo seguro de desarrollo  
- Hardening → reducir superficie de ataque  
- Aplicaciones inseguras → origen de muchísimos incidentes SOC  
