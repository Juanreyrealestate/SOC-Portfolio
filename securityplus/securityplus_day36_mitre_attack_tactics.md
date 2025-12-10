# 🔐 Security+ — Día 36  
# MITRE ATT&CK — Tácticas, Técnicas y Cómo Detectarlas (explicado fácil)

## 🎯 Objetivo
Aprender a reconocer las tácticas y técnicas MITRE ATT&CK más usadas en ataques reales.  
Esto es CLAVE para:
- entrevistas técnicas
- SOC II
- Threat Hunting Jr
- Detection Engineering Jr
- DFIR Jr

MITRE ATT&CK es el “mapa universal” del comportamiento del atacante.

---

# 🟥 1. ¿Qué es MITRE ATT&CK?

Es una base de datos que describe **cómo atacan los hackers** paso a paso:
- qué hacen primero  
- cómo se mueven  
- cómo obtienen acceso  
- cómo ejecutan malware  
- cómo roban datos  

Se divide en **tácticas** (la intención del atacante) y **técnicas** (cómo lo hace).

---

# 🟧 2. Las 11 tácticas principales (explicación fácil)

Estas son las tácticas que SI o SI debes reconocer:

### 1) **Initial Access** → entrada inicial  
Ejemplos:
- phishing  
- explotación de una vulnerabilidad  
- credenciales robadas  

### 2) **Execution** → ejecutar un comando/programa  
Ejemplos:
- PowerShell malicioso  
- ejecución de malware  
- scripts  

### 3) **Persistence** → permanecer en el sistema  
Ejemplos:
- servicios nuevos  
- claves Run  
- tareas programadas  

### 4) **Privilege Escalation** → obtener permisos más altos  
Ejemplos:
- convertirse en administrador  
- explotación de vulnerabilidad local  

### 5) **Defense Evasion** → esconder actividad  
Ejemplos:
- borrar logs  
- ofuscar PowerShell  
- ejecutar desde TEMP  

### 6) **Credential Access** → robar contraseñas  
Ejemplos:
- LSASS dumping  
- keyloggers  
- phishing  

### 7) **Discovery** → recolectar información del sistema  
Ejemplos:
- listar usuarios  
- descubrir hosts en la red  

### 8) **Lateral Movement** → moverse a otra máquina  
Ejemplos:
- SMB  
- Remote Desktop  
- wmic  
- psexec  

### 9) **Collection** → reunir datos para robar  
Ejemplos:
- screenshots  
- documentos  
- bases de datos  

### 10) **Exfiltration** → sacar datos del sistema  
Ejemplos:
- subir archivos a un servidor C2  
- comprimir `/Documents`  

### 11) **Command and Control (C2)** → comunicarse con el atacante  
Ejemplos:
- conexiones persistentes  
- DNS malicioso  
- malware “phone-home”  

---

# 🟨 3. Técnicas MITRE más importantes para entrevistas

Estas son las técnicas que los reclutadores esperan que sepas:

### 🔸 **T1059 — Command Execution**  
Uso de PowerShell, cmd, bash.  
IOCs:
- `powershell.exe -enc ...`
- `cmd.exe /c whoami`

### 🔸 **T1547 — Persistence (Run Keys)**  
Claves del registro que reinician malware cada vez que inicia Windows.

### 🔸 **T1021 — Remote Services (Lateral Movement)**  
Uso de:
- SMB  
- RDP  
- WinRM  

### 🔸 **T1003 — Credential Dumping**  
Intentos de leer LSASS o usar herramientas como Mimikatz.

### 🔸 **T1078 — Valid Accounts**  
Uso de credenciales robadas (acceso legítimo pero malicioso).

### 🔸 **T1047 — WMI Execution**  
Moverse lateralmente usando WMI.

---

# 🟦 4. ¿Cómo se ven estas técnicas en logs?

Aquí es donde MITRE se vuelve realmente útil:

### Inicial Access → muchos 4625 (fallidos)  
Luego un 4624 (exitoso) → el atacante lo logró.

### Privilege Escalation → evento 4672  
Privilegios asignados.

### Execution → evento 4688  
Nuevo proceso ejecutado.

### Lateral Movement → eventos de autenticación remota  
Ejemplo:  
RDP desde un host al que nunca te conectas normalmente.

### Credential Access  
Alto uso de `lsass.exe` o procesos leyendo memoria.

### Exfiltration  
Conexiones HTTPS fuera de horario a IPs desconocidas.

---

# 🟪 5. Cómo piensa un analista MITRE en entrevistas

Cuando te preguntan un incidente, debes pensar así:

1. ¿Qué táctica representa esto?  
2. ¿Qué técnica MITRE coincide?  
3. ¿Qué eventos debo revisar?  
4. ¿Cómo confirmo o descarto el ataque?  

Ejemplo:

**“Veo muchos 4625 seguido de un 4624.”**  
→ Táctica: Initial Access  
→ Técnica: Valid Accounts (T1078)  
→ Revisar: IP origen, horarios, usuario  
→ Riesgo: Password Spraying

---

# 🟫 6. Preguntas típicas de entrevista (te las harán sí o sí)

### ❓ “¿Qué es MITRE ATT&CK?”
Un marco que describe tácticas y técnicas usadas por atacantes reales.

### ❓ “Dame un ejemplo de técnica de persistencia.”
Claves Run, servicios, tareas programadas.

### ❓ “¿Qué evento indica ejecución de proceso?”
→ 4688

### ❓ “Si ves 4625 → 4624 → 4672 → 4688, ¿qué indica?”
→ Compromiso + escalación + ejecución.

### ❓ “¿Qué es lateral movement?”
Moverse desde una máquina comprometida hacia otra en la red.

---

# ⭐ Resumen del Día 36

Hoy aprendiste:
- las tácticas más importantes de MITRE  
- técnicas críticas usadas en ataques reales  
- cómo mapear eventos a MITRE  
- cómo piensa un analista profesional  
- cómo responder preguntas de entrevistas  

Este módulo es uno de los MÁS valiosos para roles:
- Threat Hunter Jr  
- Detection Engineer Jr  
- SOC II  
- DFIR Jr  

Y te pone a nivel superior inmediatamente.
