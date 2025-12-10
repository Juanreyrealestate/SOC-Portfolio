# 🔐 Security+ — Día 39  
# Detecciones Avanzadas con MITRE + Técnicas de Correlación Real

## 🎯 Objetivo
Aprender a construir detecciones reales basadas en técnicas MITRE, patrones de ataque y correlaciones entre logs.  
Este día te enseña lo que hacen:
- Threat Hunters Jr  
- Detection Engineers Jr  
- SOC II  
- DFIR Jr  

Esto te pone en posición de aplicar a roles mejor pagados.

---

# 🟥 1. Detecciones basadas en MITRE (explicación simple)

Una detección basada en MITRE responde a:

1. ¿Qué técnica está intentando usar el atacante?  
2. ¿Qué logs evidencian esa técnica?  
3. ¿Cómo puedo detectar o alertar ese comportamiento?

Por ejemplo:

### Técnica T1059 — Command Execution  
Detectable con:
- Evento 4688 (procesos)  
- Comandos sospechosos (`powershell.exe`, `cmd.exe /c`)  
- Script execution desde TEMP  

---

# 🟧 2. Detecciones reales que construyen los analistas

Aquí tienes **detecciones reales** que se crean en empresas (CrowdStrike, Microsoft, Palo Alto, etc.) y que TÚ podrás entender después de este módulo.

---

## 🔸 **Detección 1 — PowerShell codificado (Execution | T1059)**

¿Por qué importa?  
Los atacantes usan PowerShell con Base64 para ocultar comandos maliciosos.

### ¿Qué buscamos?

- `powershell.exe -enc`
- `powershell.exe -EncodedCommand`
- procesos creados desde rutas sospechosas

### Evidencia en logs:
- **4688** → proceso PowerShell con argumentos raros  
- **4104** (PowerShell ScriptBlock) → comando malicioso  

---

## 🔸 **Detección 2 — Uso de `cmd.exe` para acciones administrativas (Execution)**

Síntoma típico de ataque:

- `cmd.exe` lanzado por un usuario NO administrador  
- ejecución de comandos como:
    - `whoami /priv`
    - `net user`
    - `ipconfig /all`
    - `net localgroup administrators`

### Logs:
- 4688  
- 4648 si hubo credenciales explícitas  
- 4672 si obtuvo privilegios especiales  

---

## 🔸 **Detección 3 — Persistence por Run Keys (T1547)**

El atacante trata de quedarse en el sistema.

### Indicadores:
- creación de claves:
    - `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`
    - `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

### Logs relevantes:
- Sysmon Event ID 13 → Registry value set  
- 4688 (si el proceso creó la persistencia)  

---

## 🔸 **Detección 4 — Movimiento lateral sospechoso (T1021, T1047)**

### Indicadores:
- uso de:
    - `wmic`
    - `psexec`
    - `winrm`
- autenticaciones remotas fuera de horario

### Logs:
- 4624 (logon tipo 10 = remote)  
- 4625 fallidos previos  
- 4672 (privilegios especiales)  

---

## 🔸 **Detección 5 — Credential Dumping (T1003)**

El atacante intenta robar contraseñas de la memoria.

### Señales:
- Proceso accediendo a `lsass.exe`  
- Uso de herramientas como Mimikatz  
- Lectura de memoria sospechosa

### Logs:
- Sysmon 10 (Process Access)  
- Eventos de privilegio inusual  

---

# 🟨 3. Correlaciones avanzadas (Kill Chain + MITRE)

Estas correlaciones se consideran “oro puro” en entrevistas:

---

### **Patrón A — Acceso indebido + escalación + ejecución**

1. 4625 → fallidos repetidos  
2. 4624 → éxito  
3. 4672 → privilegios  
4. 4688 → ejecución de comando sospechoso  

Interpretación:  
**Compromiso + escalación + acción maliciosa.**

---

### **Patrón B — Persistencia después de ejecución**

1. 4688 ejecuta script  
2. Sysmon 13 modifica Run Keys  
3. Reinicio → persistencia activa  

Interpretación:  
**El atacante dejó una puerta trasera.**

---

### **Patrón C — Reconnaissance + Movement + Spread**

1. Enumeración:
    - `net user`
    - `net localgroup administrators`
    - `arp -a`
2. Movimiento lateral:
    - RDP  
    - WMI  
3. Nuevos procesos en máquinas remotas

Interpretación:  
**El atacante está extendiéndose por la red.**

---

### **Patrón D — Exfiltración**

1. Comprimir archivos (4688 ejecutando zip/rar)  
2. Conexiones salientes a IP rara  
3. Tráfico persistente fuera de horario  

Interpretación:  
**Intento de robar datos.**

---

# 🟦 4. ¿Qué preguntas de entrevista salen de aquí?

### ❓ “¿Cómo detectarías ejecución maliciosa de PowerShell?”
- buscar `-enc`, `DownloadString`, `Invoke-WebRequest`
- eventos 4688, 4104

### ❓ “¿Cómo sabes si hubo lateral movement?”
- logon tipo 10  
- uso de WMI, PSExec  
- máquinas remotas ejecutando procesos sospechosos  

### ❓ “¿Qué evento te muestra un nuevo proceso?”  
→ 4688

### ❓ “¿Cómo detectar persistencia?”
- Run Keys  
- servicios nuevos  
- tareas programadas  

### ❓ “¿Cómo correlacionas un ataque exitoso?”
4625 → 4624 → 4672 → 4688

---

# ⭐ Resumen del Día 39

Hoy aprendiste:
- detecciones reales basadas en MITRE  
- cómo se ven en logs  
- patrones avanzados de correlación  
- comportamiento de ataques reales  
- cómo pensar como un hunter profesional  
- preguntas que SI salen en entrevistas  

Este día te mueve de “entry-level” a **nivel profesional JR real**.
