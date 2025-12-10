# 🔐 Security+ — Día 35  
# Indicadores de Compromiso (IOCs) & Artefactos de Ataque

## 🎯 Objetivo
Aprender a identificar IOCs y artefactos de ataque en logs, endpoints y redes.  
Este skill es fundamental para SOC, Threat Hunting y DFIR, y aparece en todas las entrevistas técnicas bien pagadas.

---

# 🟥 1. ¿Qué es un IOC?

Un **IOC (Indicator of Compromise)** es una señal de que un sistema puede haber sido comprometido.

Ejemplos típicos:
- IPs maliciosas  
- dominios usados en phishing  
- hashes de malware  
- procesos anómalos  
- archivos creados por malware  
- logs que muestran accesos sospechosos  

En una investigación real, los IOCs son lo primero que se busca.

---

# 🟧 2. Tipos de IOCs más comunes

### 🔸 1) IPs sospechosas
Ejemplo:
- conexiones desde Rusia/China a las 3 AM  
- la misma IP intentando múltiples logins  

### 🔸 2) Dominios maliciosos
Usados para:
- phishing  
- command & control (C2)  
- descarga de payloads  

### 🔸 3) Hashes de archivos
Un hash identifica si un archivo:
- es malware conocido  
- fue modificado por un atacante  

Hashes comunes:
- MD5  
- SHA1  
- SHA256  

### 🔸 4) Procesos anómalos
Ejemplos reales:
- `powershell.exe -enc ...`  
- `cmd.exe /c whoami`  
- `regsvr32.exe /s /u`  
- procesos desde AppData o Temp  

Si un atacante ejecuta malware, normalmente aparece en **4688** (Windows).

### 🔸 5) Archivos sospechosos
Incluye:
- scripts `.ps1` desconocidos  
- ejecutables en carpetas raras  
- archivos persistentes (Run keys, servicios)

---

# 🟨 3. Artefactos de ataque (lo que dejan los hackers)

Un artefacto es **cualquier evidencia física** que queda tras un ataque.

Los más comunes:

### 🔸 Persistence (persistencia)
Cómo se asegura el atacante de volver a entrar:
- claves de registro Run  
- servicios nuevos  
- tareas programadas  
- scripts de inicio  

### 🔸 Execution (ejecución)
El malware o comando que se ejecuta:
- proceso nuevo  
- script descargado  
- payload cifrado  

### 🔸 Lateral Movement
Cuando el atacante intenta pasar a otra máquina:
- intentos de autenticación remota  
- uso de `wmic`, `psexec`, `smb`  

### 🔸 Credential Access
Intentos de obtener credenciales:
- lectura del LSASS  
- ejecución de herramientas como Mimikatz  

### 🔸 Collection & Exfiltration
Exfiltración = robo de datos.
Artefactos:
- archivos comprimidos  
- conexiones salientes a IPs desconocidas  
- tráfico HTTPS voluminoso a hosts raros  

---

# 🟦 4. Detección básica de IOCs en logs

### 🔸 Windows (Event Viewer)
- **4625** → intentos fallidos (bruteforce)  
- **4624** → logon exitoso sospechoso  
- **4672** → privilegios elevados  
- **4688** → procesos nuevos (puede indicar ejecución de malware)  

### 🔸 Linux
Buscar en `/var/log/auth.log`:

    grep -i "failed" /var/log/auth.log
    grep -i "invalid" /var/log/auth.log
    grep -i "sudo" /var/log/auth.log

### 🔸 Red
IOCs típicos de red:
- picos de tráfico  
- conexiones persistentes a un solo IP  
- DNS hacia dominios recién creados  

---

# 🟪 5. Cómo piensa un Threat Hunter cuando ve un IOC

Un hunter sigue este flujo mental:

1. **¿Este evento es normal para este usuario/sistema?**  
2. **¿Esto aparece en horarios raros?**  
3. **¿Es un proceso legítimo, pero usado de forma maliciosa?**  
4. **¿Hay secuencia correlacionada?**  
   (fallidos → éxito → privilegios → proceso)  
5. **¿Coincide con MITRE ATT&CK?**  

Si se cumplen varios puntos: investigar.

---

# 🟫 6. Lo que más preguntan en entrevistas sobre IOCs

### ❓ “¿Qué es un IOC?”
Una señal observable que indica un posible compromiso.

### ❓ “Dame ejemplos de IOCs.”
IPs maliciosas, hashes, procesos inusuales, eventos 4625 repetidos, archivos en carpetas sospechosas.

### ❓ “¿Qué evento indica creación de proceso en Windows?”
→ 4688

### ❓ “¿Qué buscarías en un ataque de fuerza bruta?”
→ múltiples 4625 desde la misma IP

### ❓ “¿Cómo detectas persistencia?”
→ nuevos servicios, claves Run, tareas programadas

---

# ⭐ Resumen del Día 35

Hoy aprendiste:
- qué es un IOC  
- los tipos más importantes  
- artefactos de ataque que dejan los hackers  
- cómo se ven los IOCs en logs reales  
- cómo piensa un Threat Hunter cuando analiza evidencia  

Este módulo te acerca directamente a roles de:
- Threat Hunting Jr  
- SOC II  
- DFIR Jr  
- Detection Engineer Jr  

y cubre contenido MUY común en entrevistas de $90k–$140k.
