# 🔐 Security+ — Día 11  
# PKI, Certificados, OCSP, CRL — (Nivel A)

---

# 🧠 1. ¿Qué es PKI?
PKI = Public Key Infrastructure  
Es el sistema que administra:

- certificados digitales  
- llaves públicas y privadas  
- confianza entre usuarios/servidores  
- validación de identidad  

Es lo que hace posible HTTPS, SSO, VPN, firmas digitales, email seguro.

---

# 🟦 2. Certificados Digitales (explicación simple)
Un certificado es como un **pasaporte digital**.

Incluye:
- la identidad del dueño (ej: google.com)  
- la clave pública  
- la firma de una autoridad confiable (CA)  
- fecha de expiración  

Si el certificado es válido → tu navegador lo confía.  
Si no → alerta roja.

---

# 🟩 3. Componentes de PKI

## 1️⃣ CA — Certificate Authority
La "autoridad" que firma certificados.  
Ejemplo: DigiCert, GlobalSign, Let’s Encrypt.

---

## 2️⃣ RA — Registration Authority
Verifica identidades antes de emitir certificados.

---

## 3️⃣ CSR — Certificate Signing Request
Solicitud que envía un servidor para obtener su certificado.

Incluye:  
- clave pública  
- nombre del servidor  
- información de identidad  

---

## 4️⃣ Private Key / Public Key
- La clave **privada** se queda en el servidor.  
- La clave **pública** se incluye en el certificado.  

**Nunca compartas la clave privada.**

---

# 🟥 4. Validación de Certificados (OCSP y CRL)

Cuando un cliente quiere saber si un certificado sigue siendo válido, usa:

---

## 🔹 CRL — Certificate Revocation List  
Una lista pública de certificados revocados.

Problema:
- No es en tiempo real  
- Puede demorar en actualizarse

---

## 🔹 OCSP — Online Certificate Status Protocol  
Es una **consulta en vivo** a la CA para saber si el certificado sigue válido.

OCSP es:
- rápido  
- moderno  
- usado en la mayoría de servicios

---

# 🟫 5. Tipos de certificados (Security+)

## 1️⃣ Certificado de Servidor (más común)
Usado para HTTPS.  
Ejemplo: google.com

---

## 2️⃣ Certificado de Cliente  
Autentica usuarios, no servidores.  
Usado en empresas + EAP-TLS.

---

## 3️⃣ Certificado de Email (S/MIME)  
Protege correo:  
- Cifrado  
- Firma digital  

---

## 4️⃣ Certificados de Firma de Código  
Garantizan que el software no ha sido alterado.  
Ejemplo: actualizaciones de Windows.

---

# 🟪 6. Firmas digitales vs cifrado

❗ Importante para el examen:

### 🔸 La firma digital garantiza:
- integridad  
- autenticidad  
- no repudio  

### 🔸 El cifrado garantiza:
- confidencialidad  

Son cosas distintas.

---

# 🧠 7. ¿Cómo usa esto un SOC?

Un SOC debe detectar:

- certificados expirados  
- certificados falsificados  
- anomalías en TLS  
- intentos de downgrade a protocolos inseguros  
- uso de certificados autofirmados en servidores sensibles  
- exfiltración vía HTTPS malicioso  

Es crítico en:
- C2 detection  
- MITM detection  
- Zero Trust  
- Cloud identity

---

# 📝 8. Mini-práctica (Security+ Style)

**1. ¿Qué verifica si un certificado sigue válido en tiempo real?**  
➡️ OCSP

---

**2. ¿Qué garantiza la firma digital?**  
➡️ Integridad, autenticidad, no repudio

---

**3. ¿Qué archivo envía un servidor para obtener un certificado?**  
➡️ CSR

---

**4. ¿Qué componente firma el certificado?**  
➡️ CA

---

# ⭐ 9. Resumen Final  
- PKI administra llaves y certificados  
- CA firma → RA valida identidades  
- CSR = solicitud de certificado  
- OCSP = verificación en tiempo real  
- CRL = lista de revocados  
- Firma digital = autenticidad + integridad  
- Cifrado = confidencialidad  

