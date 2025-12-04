# 🔐 Security+ — Día 4  
# Autenticación, Contraseñas y MFA (Nivel A — Súper Fácil)

---

## 🧠 1. ¿Qué es Autenticación?
Autenticación es simplemente **demostrar quién eres**.

Ejemplos del mundo real:
- Mostrar tu cédula → autenticación  
- Ingresar tu PIN → autenticación  
- FaceID en el iPhone → autenticación  

En ciberseguridad es igual:
> Autenticación = “¿Eres realmente tú?”

---

## 🔢 2. Los 5 factores de autenticación (Security+)
Security+ quiere que conozcas estos CINCO factores:

### 1️⃣ Algo que sabes  
- Contraseña  
- PIN  
- Pregunta secreta  

### 2️⃣ Algo que tienes  
- Tu teléfono (código SMS, app Authenticator)  
- Token físico (YubiKey)  
- Tarjeta inteligente  

### 3️⃣ Algo que eres  
(Biométrico)
- Huella digital  
- Rostro (Face ID)  
- Iris  

### 4️⃣ Lugar donde estás  
- Ubicación GPS  
- IP geográfica  
- País  

### 5️⃣ Algo que haces  
- Tu forma de escribir  
- Tu patrón de movimiento  
- Conducta del usuario  

---

## 🔐 3. ¿Qué es MFA?
MFA = **usar dos o más factores distintos**.

Ejemplo:
- Contraseña (algo que sabes)  
- Código del teléfono (algo que tienes)  

¿Por qué es tan importante?
- Si alguien roba tu contraseña → **no puede entrar sin tu teléfono**.  
- Bloquea fuerza bruta.  
- Bloquea phishing (la mayoría de las veces).  
- Bloquea credential theft.  
- Bloquea impossible travel.

Es el control más simple y más poderoso.

---

## 🔑 4. Contraseñas: lo que Security+ quiere que sepas

### ❌ Contraseñas débiles:
- 123456  
- password  
- qwerty  
- fecha de nacimiento  

### ❌ Reutilizar la misma contraseña en todos lados  
Si una se filtra → se filtran todas tus cuentas.

### ❌ No rotar contraseñas sensibles  
Especialmente cuentas administrativas.

### ✔ Reglas que Security+ recomienda:
- Mínimo 8–12 caracteres  
- Usar passphrases (“gatoscorriendoporlaroom#2024”)  
- Mezclar mayúsculas, minúsculas, números y símbolos  
- Evitar información personal  

---

## 🔒 5. Autenticación vs Autorización (Preguntan MUCHO en el examen)
No es lo mismo:

### ✔ Autenticación  
**¿Quién eres?**  
(Ej: password + MFA)

### ✔ Autorización  
**¿Qué puedes hacer?**  
(Ej: acceso a carpetas, bases de datos, permisos)

Ejemplo real:
- Para entrar al edificio → autenticación  
- Para acceder al piso 8 → autorización  

---

## 🧩 6. Ejemplos SOC para entenderlo mejor

1. *Credential Theft* en tu reporte → autenticación falló.  
2. *Lateral movement* → mala autorización o exceso de permisos.  
3. *Impossible Travel* → autenticación desde ubicación imposible.  
4. *Data exfiltration* → falta de controles + permisos excesivos.  
5. *Brute force* → ataque directo a autenticación.  

Estás viendo que todo conecta.

---

## 📝 7. MINI-PRÁCTICA (sencillísima)

❓ 1. ¿Contraseña + código del teléfono es?  
A) Factor único  
B) MFA  
➡️ **Respuesta: B**

---

❓ 2. La huella digital pertenece a:  
A) Algo que sabes  
B) Algo que eres  
➡️ **Respuesta: B**

---

❓ 3. “¿Qué puedes hacer una vez dentro?” corresponde a:  
A) Autenticación  
B) Autorización  
➡️ **Respuesta: B**

---

# ⭐ 8. RESUMEN FINAL (lo que debes recordar)
- **Autenticación** = demostrar quién eres  
- **Autorización** = qué permisos tienes  
- **MFA** = 2+ factores distintos  
- Factores = sabes / tienes / eres / dónde estás / lo que haces  
- MFA bloquea la mayoría de ataques de credenciales  

