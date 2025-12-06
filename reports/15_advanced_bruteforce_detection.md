# 🛡️ Reporte 15 — Advanced Brute Force Detection

## 🎯 Objetivo
Detectar variantes modernas de ataques de fuerza bruta, incluyendo password spraying, credential stuffing, MFA fatigue attacks y ataques lentos distribuidos, tal como se observan hoy en entornos cloud y empresariales.

---

# 🧠 1. ¿Qué es un Brute Force moderno?
Un brute force ya no es solo “intentos repetidos de login”.

Hoy los atacantes usan:

- ataques lentos para no disparar alertas  
- múltiples IPs (ataque distribuido)  
- spraying (mismo password para muchos usuarios)  
- credential stuffing (credenciales filtradas)  
- MFA fatigue attacks  
- bots automáticos con rotación de agentes  
- proxys y VPN comerciales  

Por eso requieren detección más avanzada.

---

# 🟦 2. Tipos de Brute Force modernos

## 1️⃣ Password Spraying  
Usar **UNA contraseña contra MUCHOS usuarios**.

Ejemplo:
- Password utilizado: `Welcome123!`  
- Usuarios atacados: `ana.p`, `juan.r`, `admin.hr`, `cfo.m`, etc.

👉 Evita bloquear cuentas y evita detecciones simples.

---

## 2️⃣ Credential Stuffing  
Usar credenciales filtradas de breaches anteriores.

Ejemplo:
- usuario: `juan@example.com`  
- pass: `password123`  
(viene de un leak)

Los atacantes prueban millones de estas.

---

## 3️⃣ Distributed Brute Force  
Ataque desde muchas IPs diferentes para no activar alertas de rate limiting.

---

## 4️⃣ Low-and-Slow Brute Force  
Intentos **espaciados** en el tiempo (cada 10–20 min) para evitar alarmas.

---

## 5️⃣ MFA Fatigue Attack  
El atacante obtiene la contraseña, pero no el segundo factor.  
Entonces envía miles de solicitudes push para cansar al usuario.

Si el usuario presiona “approve” → compromiso total.

---

# 🟥 3. Caso simulado (para este reporte)

Servicio atacado: **Azure AD / Entra ID**  
Usuario objetivo: `maria.c`

### 🔹 Eventos registrados:

| Hora        | Evento |
|-------------|--------|
| 01:11 AM | 42 attempts from 17 IPs — password spraying pattern |
| 01:12 AM | Password tested: "Welcome2024!" |  
| 01:14 AM | Login attempted for 14 different users with same password |
| 01:16 AM | 6 IPs flagged as previously malicious (TI data) |
| 01:18 AM | User maria.c targeted for MFA push 27 times in 3 min |
| 01:19 AM | User accidentally approved push request |
| 01:19 AM | Successful login from attacker IP (Russia) |
| 01:20 AM | OAuth token issued — attacker session established |

---

Interpretación inmediata:
- Hay un claro **password spraying attack**.  
- Uso de múltiples IPs → distributed brute force.  
- Posterior **MFA fatigue attack**.  
- Usuario aprobó → **cuenta comprometida**.  

---

# 🧠 4. Análisis (razonamiento humano — AI-proof)

- 42 intentos desde 17 IPs elimina la posibilidad de “usuario equivocándose”.  
- Misma contraseña usada para múltiples usuarios = spraying.  
- IPs con mala reputación validan actividad maliciosa.  
- 27 solicitudes MFA en 3 minutos = ataque de fatiga manual o automatizado.  
- Aprobación accidental indica un vector de ingeniería social.

Conclusión:
> “Cuenta maria.c está totalmente comprometida por un atacante externo vía spraying + MFA fatigue.”

---

# 🛡️ 5. Acciones recomendadas

1. Resetear contraseña de `maria.c`.  
2. Revocar todos los tokens activos (Azure AD).  
3. Habilitar **MFA resistente a phishing** (FIDO2, Passkeys).  
4. Habilitar detección de password spraying en el SIEM.  
5. Bloquear IPs involucradas via firewall/conditional access.  
6. Habilitar políticas de **Smart Lockout**.  
7. Revisar acceso a datos reciente del usuario.  
8. Revisar si hay otras cuentas atacadas con el mismo password pattern.

---

# 🧭 6. Mapeo MITRE ATT&CK
- **T1110 — Brute Force**  
- **T1110.003 — Password Spraying**  
- **T1110.004 — Credential Stuffing**  
- **T1621 — Multi-Factor Authentication Request Generation (MFA Fatigue)**  
- **T1078 — Valid Accounts**  

---

# 📝 7. Resumen Ejecutivo

Se detectó un ataque moderno de fuerza bruta contra múltiples usuarios utilizando password spraying, seguido de un ataque MFA fatigue. La usuaria `maria.c` aprobó una solicitud push, dando acceso al atacante. Se considera un compromiso total de la cuenta, requiriendo respuesta inmediata y endurecimiento de políticas de autenticación.

