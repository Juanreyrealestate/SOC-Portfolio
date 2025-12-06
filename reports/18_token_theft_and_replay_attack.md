# 🛡️ Reporte 18 — Token Theft & Replay Attacks (Cloud Identity Compromise)

## 🎯 Objetivo
Explicar cómo funciona el robo de tokens en la nube, cómo un atacante los reutiliza (replay attack), cómo detectarlo desde un SOC y qué acciones de respuesta son necesarias.

---

# 🧠 1. ¿Qué es un token?
Después de iniciar sesión, el usuario recibe:
- **Access Token** (permite acceso a recursos)  
- **Refresh Token** (permite obtener nuevos tokens sin volver a iniciar sesión)

Estos tokens viven en:
- el navegador  
- cookies  
- storage local  
- aplicaciones móviles  
- clientes de escritorio

Si un atacante roba el token → **no necesita contraseña ni MFA**.

---

# 🟥 2. Token Replay Attack (explicación simple)

Es cuando un atacante roba el token de un usuario legítimo  
y lo “reproduce” (replay) desde su propio dispositivo.

Ejemplo real:
1. Usuario inicia sesión correctamente.  
2. Su navegador guarda un token válido.  
3. Un malware o extensión maliciosa roba ese token.  
4. El atacante lo carga en su navegador.  
5. El servidor piensa que el atacante **es** el usuario real.

Resultado:
- acceso total  
- sin MFA  
- sin contraseña  
- persistencia prolongada  

---

# 🟧 3. Formas comunes de robo de tokens

## 1️⃣ Malware en el navegador  
Los infostealers (RedLine, Raccoon, Vidar, Lumma) roban cookies y tokens.

---

## 2️⃣ Ataques XSS (Cross-Site Scripting)
Scripts maliciosos roban tokens directamente del local storage.

---

## 3️⃣ Sesiones en dispositivos comprometidos  
Si la laptop está comprometida, el token puede ser extraído fácilmente.

---

## 4️⃣ MitM / Reverse proxies maliciosos  
Ejemplo: Evilginx  
Captura:
- contraseña  
- MFA  
- token  
→ bypass total de autenticación

---

## 5️⃣ Token hijacking via OAuth consent grant  
Una aplicación maliciosa obtiene un refresh token del usuario.

---

# 🟫 4. Señales de token theft en entornos cloud (lo que ve un SOC)

### 🔹 Inicio de sesión SIN evento de autenticación
El token hace login sin registrar contraseña o MFA.

### 🔹 Inicios desde nuevos dispositivos pero con tokens válidos  
Ejemplo:
- Access token created in Miami  
- Replay from Poland

### 🔹 Múltiples sesiones con el mismo token fingerprint  
El servidor detecta uso simultáneo desde distintos lugares.

### 🔹 Token válido usado DESPUÉS de cierre de sesión del usuario  
Indica que el atacante conservó una copia.

### 🔹 Actividad anómala después de inactivity period  
El usuario no está activo → pero su token sí.

---

# 🟥 5. Caso simulado (cloud identity incident)

Usuario: **monica.s@empresa.com**  
Rol: Analista  
Sistema: Azure AD

### Eventos:

| Hora        | Evento |
|-------------|--------|
| 09:12 AM | User authenticates successfully from Miami |
| 09:13 AM | Access token issued (Chrome, Windows 10) |
| 09:40 AM | Token replay detected from Sweden — no MFA |  
| 09:40 AM | Device fingerprint mismatch |
| 09:41 AM | Downloaded 2.3GB from OneDrive shared folders |
| 09:42 AM | OAuth app registered: “DataSyncPro” — suspicious |
| 09:44 AM | Refresh token granted to malicious app |
| 09:45 AM | Conditional Access: impossible travel detected |

Interpretación:
- Token original fue robado del navegador  
- Atacante lo usó desde otro país  
- Se creó una aplicación OAuth para persistencia  
- Descarga masiva indica exfiltración  

---

# 🧠 6. Análisis (razonamiento humano — AI-proof)

1. No hubo autenticación antes del acceso desde Suecia → uso de token replay.  
2. Fingerprint distinto = otro dispositivo.  
3. La creación de una app OAuth es táctica común para persistencia.  
4. Descarga masiva de datos indica objetivo exfiltración.  
5. No hay MFA → porque el atacante usó el token válido original.

Conclusión:
> “La identidad de monica.s fue comprometida mediante robo de token y replay attack. Hubo exfiltración de datos y establecimiento de persistencia OAuth.”

---

# 🛡️ 7. Acciones recomendadas

1. **Revocar TODOS los tokens de sesión**  
   Azure AD → “Invalidate Refresh Tokens”

2. **Eliminar todas las aplicaciones OAuth no autorizadas**

3. **Resetear contraseña**  
   (no es suficiente, pero ayuda)

4. **Forzar reautenticación en todos los dispositivos**

5. **Revisar actividad en OneDrive/SharePoint**

6. **Habilitar MFA resistente a phishing (FIDO2 / Passkeys)**

7. **Bloquear direcciones IP involucradas**

---

# 🧭 8. MITRE ATT&CK Mapping

- **T1539 — Steal Web Session Cookie**  
- **T1550.004 — Web Session Cookie Replay**  
- **T1528 — Abuse of Authentication Tokens**  
- **T1110 — Credential Access**  
- **T1020 — Exfiltration Over Cloud Services**

---

# 📝 9. Resumen Ejecutivo

Se detectó un ataque de robo de token contra la cuenta “monica.s”. El atacante utilizó el token legítimo para acceder sin MFA desde otro país, descargó grandes cantidades de datos y creó una aplicación OAuth maliciosa para persistencia. Se recomienda revocar tokens, eliminar apps OAuth y activar MFA resistente a phishing.

