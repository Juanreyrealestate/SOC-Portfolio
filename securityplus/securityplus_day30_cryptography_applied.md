# 🔐 Security+ — Día 30  
# Cryptography Applied (Parte 2) — TLS, PKI, Certificates, Hashing, PFS

## 🎯 Objetivo
Entender cómo funciona la criptografía en la vida real: certificados, TLS, PKI, claves, hashing, forward secrecy. Este módulo aparece SIEMPRE en Security+ y es clave en entrevistas SOC / Threat Hunting.

---

# 🟥 1. TLS (Transport Layer Security)

TLS protege conexiones como:
- HTTPS  
- VPN SSL  
- Email seguro  

## 🔸 ¿Qué protege TLS?
- Confidencialidad (cifrado)  
- Integridad (hashes)  
- Autenticidad (certificados)  

---

# 🟧 2. TLS Handshake (explicado fácil)

### Paso 1: ClientHello  
El cliente dice:  
> “Quiero conectarme y aquí están mis algoritmos soportados.”

### Paso 2: ServerHello + Certificado  
El servidor responde con:  
- su certificado digital  
- clave pública  
- suite criptográfica elegida  

### Paso 3: Validación del certificado  
El cliente revisa:  
- ¿El certificado está firmado por una CA confiable?  
- ¿No está expirado?  
- ¿El dominio coincide?

### Paso 4: Intercambio de claves  
Se genera una **session key** (clave simétrica que cifrará la sesión).

### Paso 5: Canal seguro  
Toda la comunicación queda cifrada.

---

# 🟨 3. PKI — Public Key Infrastructure

PKI = sistema que administra certificados y claves públicas.

Componentes:
- **CA (Certificate Authority)**  
- **RA (Registration Authority)**  
- **CRL (Certificate Revocation List)**  
- **OCSP (Online Certificate Status Protocol)**  
- **CSR (Certificate Signing Request)**  

Security+:  
➡️ CA = entidad que firma certificados  
➡️ CSR = solicitud de certificado  
➡️ OCSP = verificar si un certificado sigue válido  

---

# 🟦 4. Certificados Digitales

Incluyen:
- clave pública  
- identidad  
- dominio  
- fecha de expiración  
- algoritmo  
- firma de la CA  

Tipos:
- DV (Domain Validation)  
- OV (Organization Validation)  
- EV (Extended Validation, más estricto)

---

# 🟪 5. Hashing (MUY importante)

Hash = transformación unidireccional.

Usos:
- almacenar contraseñas  
- verificar integridad  
- fingerprinting  

Características:
- unidireccional  
- único  
- determinístico  
- resistente a colisiones  

Buenos hashes:
- SHA-256  
- SHA-3  

Malos hashes:
- MD5  
- SHA-1  

---

# 🟩 6. SALT y PEPPER

### SALT
Datos aleatorios agregados antes de hashear una contraseña.  
Evita ataques con rainbow tables.

### PEPPER
Valor secreto adicional guardado aparte.

Security+:  
➡️ Salt = mitigación para hashing débil.

---

# 🟫 7. Perfect Forward Secrecy (PFS)

Define que:
> Aunque roben la clave privada del servidor, no pueden descifrar sesiones antiguas.

¿Cómo se logra?  
➡️ Usando **Diffie-Hellman Ephemeral (DHE / ECDHE)** para generar claves únicas por sesión.

Security+:  
➡️ PFS = sesiones antiguas protegidas incluso después de un compromiso.

---

# 🟩 8. Symmetric vs Asymmetric (repaso aplicado)

## Simétrico:
- rápido  
- usa UNA sola clave  
Ejemplo: AES

## Asimétrico:
- más lento  
- usa par de claves (pública/privada)  
Ejemplo: RSA, ECC

TLS usa:
- Asimétrico para intercambio de claves  
- Simétrico para cifrar el canal

---

# 🟧 9. Crypto Attacks

- Brute force  
- Dictionary attack  
- Rainbow tables (detenidas con SALT)  
- Downgrade attacks  
- Replay attacks  
- Birthday attacks (contra hashes)

---

# 🟦 10. Mini-Práctica tipo Security+

**1. ¿Qué elemento comprueba la validez de certificados?**  
→ OCSP

**2. ¿Qué propiedad provee PFS?**  
→ Las sesiones antiguas no pueden descifrarse aunque la clave privada sea comprometida.

**3. ¿Qué algoritmo reemplaza MD5/SHA1?**  
→ SHA-256

**4. ¿Qué evita ataques con rainbow tables?**  
→ Salt

**5. ¿Qué tipo de criptografía usa claves pública/privada?**  
→ Asimétrica

---

# ⭐ Resumen Final
Hoy aprendiste:
- TLS handshake  
- Certificados digitales  
- PKI completa  
- Hashing seguro  
- Salt & Pepper  
- Perfect Forward Secrecy  
- Symmetric vs Asymmetric aplicado  
- Ataques criptográficos  

Este módulo te prepara para examen y para entrevistas bien pagadas.

