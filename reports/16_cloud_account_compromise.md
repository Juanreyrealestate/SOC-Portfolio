# 🛡️ Reporte 16 — Cloud Account Compromise (Azure AD / Entra ID)

## 🎯 Objetivo
Detectar señales de que una cuenta corporativa en la nube (Azure AD / Entra ID) ha sido comprometida, utilizando eventos de identidad, MFA, tokens, ubicaciones y políticas de acceso condicional.

---

# 🧠 1. ¿Por qué es tan importante esto?
Hoy, la mayoría de ataques NO comienzan en servidores…  
Comienzan en **identidades en la nube**.

Los atacantes buscan comprometer:
- cuentas de empleados,  
- sesiones de navegador,  
- tokens OAuth,  
- dispositivos no aprobados.

Un solo acceso comprometido puede permitir:
- exfiltrar datos,  
- moverse lateralmente,  
- obtener privilegios elevados,  
- comprometer toda la organización.

---

# 🟦 2. Indicadores típicos de compromiso de cuenta en Azure AD

## 1️⃣ Impossible Travel (viajes imposibles)
Una misma cuenta autenticándose desde:
- Miami a Nueva York en 2 minutos  
- USA → Rusia → USA  

Imposible físicamente.

---

## 2️⃣ Inicios desde ubicaciones inusuales
Ejemplo:
- Rusia  
- China  
- Nigeria  
- VPN comerciales (NordVPN, Mullvad)

---

## 3️⃣ MFA Fatigue Attack
Múltiples solicitudes push de MFA en pocos minutos.

Ejemplo:
- 23 solicitudes en 3 minutos

---

## 4️⃣ Creation of OAuth Tokens from Unknown Device
El atacante obtiene un **refresh token** y mantiene sesión indefinidamente.

---

## 5️⃣ Cambios no autorizados en políticas de acceso
Ejemplo:  
Deshabilitar MFA, agregar excepciones, aprobar dispositivos.

---

## 6️⃣ Consent Grant Attack
El usuario aprueba una aplicación maliciosa que pide permisos elevados.

---

# 🟥 3. Caso simulado para el reporte

Cuenta comprometida: **andres.r@empresa.com**  
Departamento: ventas  
Privilegios: medios

### Eventos registrados:

| Hora        | Evento |
|-------------|--------|
| 01:11 AM | Login successful from Brazil (user normally logs in from Miami) |
| 01:12 AM | Login failed — MFA denied |
| 01:14 AM | MFA push attacks (17 requests in 90 sec) |
| 01:15 AM | User approved MFA (accidental) |
| 01:16 AM | OAuth token issued to unfamiliar device: Chrome/Windows NT |
| 01:18 AM | Activity spike: Access to SharePoint root folders |
| 01:19 AM | Downloaded 1.1GB of files (financials + HR folders) |
| 01:21 AM | New inbox rule created (hide incoming alerts) |

Interpretación:
- No viajó a Brasil → impossible travel  
- Hubo MFA fatigue → compromiso  
- Emisión de OAuth → persistencia  
- Descarga masiva → exfiltración  
- Inbox rule → ocultar rastros  

---

# 🧠 4. Análisis (razonamiento humano — AI-proof)

- El usuario nunca se conecta desde Brasil.  
- La aprobación de MFA tras spam indica ingeniería social.  
- La creación del OAuth token muestra que el atacante estableció persistencia.  
- La descarga de archivos sensibles es clara señal de exfiltración.  
- Las reglas de inbox se usan para ocultar notificaciones de seguridad.

Conclusión:
> “La cuenta de andres.r está totalmente comprometida.  
> Hay evidencia clara de acceso malicioso, exfiltración y persistencia en la nube.”

---

# 🛡️ 5. Acciones recomendadas

1. **Resetear contraseña inmediatamente.**  
2. **Revocar TODOS los tokens de sesión en Azure AD:**  
   - Sign-in logs → Revoke Sessions  
3. **Requerir MFA resistente a phishing (FIDO2, passkeys).**  
4. **Eliminar aplicaciones OAuth no autorizadas.**  
5. **Revisar activity logs de SharePoint/OneDrive.**  
6. **Bloquear IP y rangos utilizados.**  
7. **Revisar otros intentos de compromiso relacionados.**  
8. **Auditar cambios en políticas de seguridad.**

---

# 🧭 6. MITRE ATT&CK Mapping

- **T1078 — Valid Accounts**  
- **T1110 — Credential Access / Brute Force**  
- **T1606.002 — MFA Fatigue Attack**  
- **T1071 — Exfiltration Over Web Services**  
- **T1137 — Email Manipulation**  
- **T1528 — Abuse of Authentication Tokens**

---

# 📝 7. Resumen Ejecutivo

La cuenta “andres.r” fue comprometida a través de un ataque combinado de password spraying y MFA fatigue. El atacante obtuvo un token OAuth, accedió a datos sensibles de la compañía y creó mecanismos de persistencia. La cuenta y sus sesiones deben ser revocadas inmediatamente y se requiere endurecimiento de políticas de autenticación.

