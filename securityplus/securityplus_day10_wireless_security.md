# 🔐 Security+ — Día 10  
# Wireless Security (WPA3, EAP, Ataques Wireless) — Nivel A

---

# 🧠 1. Seguridad Wireless: lo esencial
Las redes inalámbricas son uno de los vectores de ataque más fáciles.  
Security+ se enfoca en:

- protocolos de autenticación  
- cifrado  
- ataques comunes  
- protección de redes Wi-Fi corporativas  

---

# 🟩 2. WPA, WPA2, WPA3 (los protocolos de Wi-Fi)

## 🔸 WEP (NO seguro)
- Muy antiguo  
- Se rompe en segundos  
- NO se usa nunca  

---

## 🔸 WPA
- Mejor que WEP, pero ya viejo  

---

## 🔸 WPA2 (Aún común)
- Usa **AES**  
- Requiere clave precompartida (PSK) en redes básicas  
- Más seguro que WPA, pero ya no perfecto

---

## 🔸 WPA3 (El estándar moderno)
🔐 Mucho más seguro  
🔐 Protege contra ataques de diccionario  
🔐 Usa “SAE” (Simultaneous Authentication of Equals)

**Si te preguntan: “¿Cuál es el protocolo Wi-Fi más seguro?” → WPA3.**

---

# 🟦 3. EAP (Extensible Authentication Protocol)

EAP se usa en redes empresariales (WPA2-Enterprise, WPA3-Enterprise).

Tipos importantes:

## 🔹 EAP-TLS (EL MÁS SEGURO)
- Usa certificados  
- Muy difícil de romper  
- Muy recomendado por Security+

## 🔹 PEAP
- Usa túnel TLS  
- Más fácil de implementar  
- Seguridad buena

## 🔹 EAP-TTLS
- Similar a PEAP  
- También usa túnel seguro

**TIP:** Si ves algo relacionado con empresas o alta seguridad → **EAP-TLS**.

---

# 🟫 4. Ataques Wireless Comunes

## 1️⃣ Evil Twin
Un atacante crea un Wi-Fi falso con el mismo nombre (SSID).  
La gente se conecta pensando que es legítimo.

El atacante puede:
- capturar tráfico  
- robar credenciales  
- hacer MITM  

Protección:
- WPA3  
- detección de APs falsos  
- certificados

---

## 2️⃣ Deauthentication Attack
El atacante “expulsa” a los usuarios del Wi-Fi para obligarlos a reconectarse.

Usado para:
- capturar handshakes  
- ataques de cracking

WPA3 reduce este riesgo.

---

## 3️⃣ Rogue Access Point
Punto de acceso Wi-Fi NO autorizado dentro de la empresa.

---

## 4️⃣ WPS Attack
WPS (el botón de “Press to connect”)  
Se rompe muy fácil → NO usar nunca.

---

# 🟧 5. Seguridad Wireless Requerida en Empresas

- WPA3 siempre que sea posible  
- Desactivar WPS  
- EAP-TLS en entornos corporativos  
- Segmentar la red Wi-Fi de invitados  
- Filtrar MAC (solo como apoyo, NO como seguridad real)  
- Usar 802.1X (control de acceso enterprise)  
- Detectar rogue APs

---

# 🧠 6. ¿Cómo usa esto un SOC?

SOC ve:

- conexiones sospechosas a APs desconocidos  
- dispositivos no autorizados en la red  
- fallos repetidos de autenticación  
- cambios de SSID  
- alertas de WIPS (Wireless Intrusion Prevention)  

Importante para:
- insider threat  
- ataques de proximidad  
- robar credenciales Wi-Fi  

---

# 📝 7. Mini-práctica (Security+ Style)

**1. ¿Cuál es el protocolo Wi-Fi más seguro hoy?**  
➡️ WPA3

---

**2. ¿Qué EAP es el más seguro?**  
➡️ EAP-TLS

---

**3. ¿Cómo se llama el ataque donde crean un Wi-Fi falso?**  
➡️ Evil Twin

---

**4. ¿Qué protocolo NO se debe usar nunca?**  
➡️ WEP o WPS

---

# ⭐ 8. Resumen Final  
- **WPA3 = seguridad moderna**  
- **EAP-TLS = autenticación empresarial top**  
- **Evil Twin = Wi-Fi falso malicioso**  
- **WPS = inseguro**  
- **SOC monitorea redes wireless corporativas**  

