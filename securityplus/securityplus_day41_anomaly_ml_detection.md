# 🔐 Security+ — Día 41  
# Detección de Anomalías + ML en Ciberseguridad (explicado fácil)

## 🎯 Objetivo
Aprender cómo los sistemas modernos detectan comportamiento anormal usando análisis estadístico, comportamiento y machine learning.  
Este módulo es clave para SOC II, Threat Hunter Jr, DFIR Jr y Detection Engineering Jr.

---

# 🟥 1. ¿Qué es una anomalía?

Una **anomalía** es un comportamiento que se sale de lo típico o esperado.

Ejemplos:
- un usuario inicia sesión desde otro país  
- proceso nuevo ejecutado por primera vez  
- Word lanzando PowerShell  
- tráfico de red 10 veces mayor que lo normal  
- actividad a horas extrañas  

Anomalía ≠ Ataque  
Pero una anomalía **puede indicar** un ataque.

---

# 🟧 2. Tipos de detección de anomalías

### 🔸 1) **Detección estadística**
Compara el comportamiento actual con valores normales históricos.

Ejemplos:
- promedio normal de tráfico es 500 MB → hoy 5 GB → anómalo  
- un usuario hace 20 logins al día → hoy hizo 200 → anómalo  

### 🔸 2) **Detección basada en comportamiento**
El sistema aprende lo que *normalmente* hace un usuario o proceso.

Ejemplo:
- El usuario Juan nunca usa RDP → hoy usa RDP → alerta  
- Chrome nunca lanza cmd.exe → hoy sí → alerta  

### 🔸 3) **Detección basada en Machine Learning (ML)**
Identifica patrones complejos que NO se detectan fácilmente por reglas.

Encontrará:
- combinaciones raras de eventos  
- secuencias inusuales  
- “parecidos” a ataques previos  
- actividad que no coincide con ningún perfil normal  

---

# 🟨 3. ¿Qué cosas se consideran anomalías en la práctica?

### ✔ Anomalías de usuario (UEBA — User & Entity Behavior Analytics)
- inicio de sesión desde país distinto  
- aumento repentino de actividad  
- accesos a archivos que nunca usa  
- uso de herramientas de administrador sin ser admin  

### ✔ Anomalías de endpoint (EDR)
- procesos ejecutados desde carpetas raras (TEMP, AppData)  
- PowerShell con parámetros sospechosos  
- procesos que se inyectan en otros  
- secuencia rara: Word → CMD → PowerShell → Download  

### ✔ Anomalías de red
- grandes cantidades de datos saliendo  
- conexiones a IPs de alto riesgo  
- uso de protocolos que nunca usa la empresa  

---

# 🟦 4. ¿Qué hace el ML en ciberseguridad? (explicado fácil)

NO necesitas matemáticas. Debes entender la función:

### ✔ El ML **aprende lo normal**  
El sistema observa:
- qué archivos se ejecutan normalmente  
- qué usuarios trabajan a qué horas  
- qué procesos se comunican con qué IPs  

Luego detecta desviaciones.

### ✔ El ML **compara comportamientos con ataques conocidos**
Ejemplo:
“Esta secuencia se parece a ransomware.”

### ✔ El ML **asigna un riesgo**
Muchos EDR asignan un “score” de riesgo:
- 0–30 → bajo  
- 30–70 → sospechoso  
- 70–100 → probable ataque  

---

# 🟪 5. Casos reales donde anomalía = alerta de ataque

### 🔸 Ejemplo 1 — Ransomware  
Se detecta:
- un proceso que empieza a cifrar muchos archivos muy rápido  
→ comportamiento anómalo de escritura → ML lo detecta

### 🔸 Ejemplo 2 — Un atacante obtuvo credenciales  
Se ve:
- múltiples 4625 → fallidos  
- luego 4624 → éxito desde otro país  
→ anomalía de localización

### 🔸 Ejemplo 3 — Exfiltración  
Se detecta:
- proceso comprimiendo archivos → zip  
- tráfico saliente de gran volumen  
→ anomalía de red + comportamiento

### 🔸 Ejemplo 4 — Persistencia  
Se detecta:
- nueva tarea programada a las 3 AM  
→ anómalo para el usuario  

---

# 🟫 6. Preguntas típicas de entrevista

### ❓ “¿Qué es detección de anomalías?”
Detectar actividad que se desvía de lo normal.

### ❓ “¿Qué diferencia hay entre anomalía y firma?”
- firma → detecta malware conocido  
- anomalía → detecta comportamiento inusual

### ❓ “¿Por qué ML es útil?”
Porque detecta ataques nuevos que NO tienen firma.

### ❓ “¿Qué sería una anomalía de usuario?”
Inicio de sesión desde país nuevo / a hora inusual.

### ❓ “¿Qué sería una anomalía de proceso?”
Word lanzando PowerShell.

---

# ⭐ Resumen del Día 41

Hoy aprendiste:
- qué es una anomalía  
- tipos de detección: estadística, comportamiento, ML  
- ejemplos reales de anomalías usadas por EDR y SIEM  
- cómo se detectan exfiltración, movimiento lateral, ejecución ofensiva  
- contenido exacto de entrevistas para SOC II y Threat Hunting  

Este módulo te pone en terreno profesional: ya estás pensando como un analista real.
