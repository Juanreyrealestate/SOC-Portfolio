# 🔐 Security+ — Día 6  
# Criptografía (Nivel A — Explicación Simple y Clara)

---

## 🧠 1. ¿Qué es criptografía?
Criptografía es convertir información legible en algo que nadie pueda entender, a menos que tenga la clave correcta.

Sirve para:
- proteger datos  
- evitar espionaje  
- validar integridad  
- asegurar conexiones  

---

# 🟦 2. Conceptos Fundamentales

## 1️⃣ Hashing  
- Crea una “huella digital” del dato.  
- **No se puede revertir.**  
- Si cambias una letra, el hash cambia totalmente.  
- Se usa para contraseñas y verificar integridad.

Ejemplos de algoritmos:  
- MD5 (no seguro)  
- SHA-1 (no seguro)  
- SHA-256 (seguro)

---

## 2️⃣ Salting  
- Añade datos aleatorios a una contraseña ANTES de hacerle hash.  
- Evita que dos contraseñas iguales tengan el mismo hash.  
- Protege contra ataques de diccionario y rainbow tables.

---

## 3️⃣ Encryption (Encriptación)  
Convierte datos en ilegibles, pero **sí** se pueden volver a convertir al original.

### 🔹 Encriptación Simétrica  
- Una sola clave para cifrar y descifrar.  
- Rápida y eficiente.  
- Ejemplo: **AES-256** (muy seguro).

### 🔹 Encriptación Asimétrica  
- Usa **dos claves**: pública y privada.  
- Cualquiera puede cifrar con la pública.  
- Solo el dueño puede descifrar con la privada.  
- Ejemplo: **RSA**.

---

# 🟩 3. TLS / SSL (Seguridad en Internet)
TLS protege todo tu tráfico web.

HTTPS = HTTP + TLS

TLS asegura:
- cifrado  
- autenticación del servidor  
- integridad de datos  

**Dato de examen:**  
TLS es el estándar actual (NO digas SSL).

---

# 🟫 4. Certificados Digitales
Un certificado es como un pasaporte digital.

Incluye:
- identidad del sitio  
- llave pública  
- firma de una Autoridad de Certificación (CA)  

Si el certificado es válido → el navegador confía.  
Si es falso o inválido → alerta.

---

# 🧠 5. Cómo usa esto un SOC Analyst
- Verificar hashes de archivos (malware).  
- Confirmar tráfico HTTPS legítimo vs sospechoso.  
- Revisar certificados falsificados.  
- Detectar C2 oculto dentro de tráfico cifrado.  
- Identificar downgrade attacks (forzar protocolos débiles).

---

# 📝 6. Mini-Práctica (Estilo Security+)

**1. ¿Qué NO se puede revertir?**  
A) Hashing  
B) Cifrado  
➡️ **A**

**2. HTTPS se asegura con:**  
A) SSL  
B) TLS  
➡️ **B**

**3. ¿Qué usa dos claves (pública y privada)?**  
A) Simétrica  
B) Asimétrica  
➡️ **B**

**4. ¿Para qué sirve el salting?**  
A) Cifrar datos  
B) Fortalecer hashes de contraseñas  
➡️ **B**

---

# ⭐ 7. Resumen en una línea
- **Hash:** irreversible.  
- **Salting:** protege contraseñas.  
- **Simétrica:** 1 clave (AES).  
- **Asimétrica:** 2 claves (RSA).  
- **TLS:** protege tráfico web.  
- **Certificados:** identidad + llave pública.  

