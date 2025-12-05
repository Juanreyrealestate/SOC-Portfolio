# 🛡️ Reporte 14 — Insider Threat Detection

## 🎯 Objetivo
Identificar comportamientos anómalos de empleados o usuarios internos que puedan indicar robo de datos, abuso de privilegios o acciones maliciosas dentro de la organización.

---

# 🧠 1. ¿Qué es un Insider Threat?
Es una amenaza que proviene **desde dentro de la empresa**, por ejemplo:

- un empleado molesto  
- un usuario comprometido  
- alguien robando información  
- un contratista abusando de accesos  
- cuenta tomada por un atacante externo  

Lo peligroso:  
Insiders ya tienen **credenciales legítimas**.

---

# 🟦 2. Tipos de Insider Threat

## 1️⃣ Negligente  
Usuarios descuidados:
- comparten contraseñas  
- hacen clic en phishing  
- suben datos a sitios no autorizados  

---

## 2️⃣ Malicioso  
Usuarios con intención de dañar:
- roban información  
- venden secretos  
- sabotean sistemas  
- exfiltran datos  

---

## 3️⃣ Comprometido  
Usuarios cuyas credenciales fueron robadas:
- keylogger  
- phishing  
- token comprometido  

---

# 🟥 3. Indicadores típicos de un Insider Threat

## 🔹 Comportamiento anómalo
- iniciar sesión fuera de horario  
- inicios desde ubicaciones inusuales  
- accesos repetidos a datos sensibles  

## 🔹 Exfiltración de datos
- subida masiva a Google Drive, Dropbox, etc.  
- copia masiva a USB  
- envío de archivos grandes por email  
- uso de herramientas no aprobadas  
- tráfico saliente inusual  

## 🔹 Uso abusivo de privilegios
- alguien de marketing leyendo carpetas de Finanzas  
- creación de cuentas sin autorización  
- extraer bases de datos completas  

## 🔹 Señales de UEBA (User & Entity Behavior Analytics)
- comportamiento diferente al historial del usuario  
- acceso a sistemas nunca usados antes  
- descarga masiva de archivos  

---

# 🟫 4. Caso simulado (para el reporte)

Empleado: **Alicia R.**  
Departamento: Finanzas  
Rol: Analista de cuentas

Eventos registrados:

### 🔹 1. Actividad fuera de horario
Login successful — 03:14 AM
Source: home IP

### 🔹 2. Acceso a carpetas no relacionadas con su rol
Accessed folder: /HR/Employee_Records

### 🔹 3. Descarga masiva de datos
Downloaded 4.7GB from /FIN/2024_Q4_Reports

### 🔹 4. Subida de datos a un servicio externo no permitido
Upload: 4.7GB to dropbox.com

### 🔹 5. Conexiones a un dispositivo USB desconocido
USB device connected: VendorUnknown
Files transferred: 1832

Interpretación inicial:  
Comportamiento altamente sospechoso de **exfiltración interna**.

---

# 🧠 5. Análisis (razonamiento humano — AI-proof)

- Alicia no debería acceder a HR.  
- No hay razón legítima para trabajar a las 3 AM.  
- Volumen de 4.7GB es inusual para sus tareas.  
- Dropbox NO está permitido por políticas corporativas.  
- El uso de USB desconocido sugiere copia local.  

Todo apunta a:
> “Posible insider malicioso, exfiltración de datos financieros y HR.”

---

# 🚨 6. Acciones recomendadas (SOC Playbook)

1. Suspender la cuenta de Alicia temporalmente.  
2. Aislar su dispositivo de la red.  
3. Revisar logs de exfiltración adicionales.  
4. Analizar actividad USB completa.  
5. Coordinar con Recursos Humanos.  
6. Investigar si sus credenciales fueron comprometidas.  
7. Revisar accesos de los últimos 90 días.  
8. Activar procedimientos legales/disciplinarios si corresponde.

---

# 🧭 7. Mapeo MITRE ATT&CK

- **T1567 — Exfiltration to Cloud Storage**  
- **T1078 — Valid Accounts**  
- **T1020 — Automated Exfiltration**  
- **T1056 — Input Capture (credenciales robadas)**  
- **T1530 — Data from Cloud Storage**  

---

# 📝 8. Resumen Ejecutivo
El usuario interno “Alicia R.” mostró comportamientos de alto riesgo, incluyendo accesos no autorizados, exfiltración masiva a Dropbox, y uso de USB desconocido.  
Los patrones sugieren posible actividad maliciosa o credenciales comprometidas.  
Se recomienda suspender acceso y comenzar investigación formal.

