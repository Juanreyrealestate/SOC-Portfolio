# 🔐 Security+ — Día 34  
# Event IDs y Logs más importantes (Windows, Linux, Cloud)

## 🎯 Objetivo
Dominar los eventos críticos que aparecen en SOC, Threat Hunting y entrevistas técnicas.  
Saber interpretar estos eventos te hace destacar rápidamente y mejora tus chances para roles de $85k–$140k.

---

# 🟥 1. Windows Event IDs — Los más importantes

Los SOC y Threat Hunters trabajan **constantemente** con estos eventos:

### 🔸 **4624 — Logon exitoso**
Indica que alguien inició sesión correctamente.  
Lo normal:  
- tipo 2 = interactive  
- tipo 3 = network  

Si ves muchos en horarios extraños → sospechoso.

---

### 🔸 **4625 — Logon fallido**
MUY importante para detectar fuerza bruta.  
Si varios intentos vienen de la misma IP → investigar.

---

### 🔸 **4648 — Logon usando credenciales explícitas**
Un atacante suele usarlo al probar credenciales robadas.

---

### 🔸 **4688 — Nuevo proceso creado**
UNO DE LOS EVENTOS MÁS IMPORTANTES EN HUNTING.  
Sirve para detectar:
- malware ejecutándose  
- scripts desconocidos  
- procesos anómalos  

Ejemplos sospechosos:
- `powershell.exe -enc ...`
- `cmd.exe /c whoami`
- procesos desde rutas raras (`AppData`, `Temp`)

---

### 🔸 **4672 — Privilegios especiales asignados**
Indica acciones con privilegios elevados.  
Si un usuario no debería tener admin → alerta.

---

### 🔸 **4776 — Validación de credenciales**
Muestra intentos de autenticación en el dominio.  
Se usa mucho en detección de password spraying.

---

# 🟧 2. Linux Logs — Lo esencial

Linux no usa Event Viewer. Usa archivos de texto.

Los más importantes:

### 🔸 `/var/log/auth.log`
Contiene:
- autenticaciones  
- sudo  
- ssh  
- intentos fallidos  
- escalamiento de privilegios  

Buscar:

    grep -i "failed" /var/log/auth.log
    grep -i "password" /var/log/auth.log

---

### 🔸 `/var/log/syslog` o `/var/log/messages`
Contiene:
- eventos del sistema  
- errores  
- actividad general del OS  

---

### 🔸 `/var/log/secure` (RHEL/CentOS)
Registro de seguridad y autenticación.

---

# 🟦 3. Log Insights para Threat Hunting

### 🔸 Cosas sospechosas que debes reconocer:
- conexiones remotas fuera de horario  
- procesos ejecutados desde carpetas TEMP  
- secuencias raras: logon fallido → logon exitoso → proceso elevado  
- cambios de permisos inesperados  

### 🔸 Patrón típico de ataque:

1. Muchos 4625 (logon fallido)  
2. Un 4624 exitoso  
3. Un 4672 (privilegios)  
4. Un 4688 (nuevo proceso raro)  

Si recuerdas este patrón, ya piensas como hunter.

---

# 🟪 4. Logs de Cloud (introducción esencial)

### 🔸 AWS CloudTrail  
Registra:
- creación de usuarios  
- cambios en roles  
- accesos a buckets  
- actividad anómala desde otros países  

Ejemplo sospechoso:
- `CreateUser` o `AttachPolicy` inesperados  

---

### 🔸 Azure Sign-In Logs  
Útil para ver:
- MFA fallido  
- accesos desde ubicaciones nuevas  
- ataques de password spraying  

---

### 🔸 GCP Audit Logs  
Registra:
- creación de claves  
- permisos añadidos  
- accesos no autorizados  

---

# 🟫 5. Conexión con Security+, SOC y roles mejor pagados

Saber estos eventos te ayuda a:

✔ pasar Security+  
✔ pasar entrevistas técnicas  
✔ pensar como analista real  
✔ aplicar más rápido a SOC II / Threat Hunting Jr  
✔ destacar sobre candidatos que solo “estudian”

Este conocimiento es 100% práctico y aplicable.

---

# ⭐ Resumen del Día 34

Hoy aprendiste:
- los Event IDs más usados profesionalmente  
- los logs clave de Linux  
- la lógica de hunting para detectar ataques  
- qué mirar en logs de cloud  

Este módulo te acerca a roles de:  
➡️ SOC II  
➡️ Threat Hunter Jr  
➡️ DFIR Jr  
➡️ Detection Engineer Jr  

Listo para avanzar hacia tus entrevistas y tu meta salarial de 6 cifras.
