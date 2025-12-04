# 🔐 Security+ — Día 1  
# Introducción a Amenazas y Tipos de Ataques (Nivel A — súper fácil)

---

## 🧠 1. ¿Qué es una “amenaza” en ciberseguridad?  
Una *amenaza* es simplemente **algo que puede causar daño** a:

- un sistema  
- una cuenta  
- una empresa  
- una persona  

Es como dejar la puerta abierta de tu casa:  
la *amenaza* no es el ladrón.  
La amenaza es **la posibilidad de que alguien entre**.

En Security+ lo verás así:  
- amenazas → cosas que pueden ocurrir  
- vulnerabilidades → debilidades  
- ataques → cuando el atacante aprovecha la debilidad  

---

## 🛑 2. Tipos de ataques principales (Security+ explicado simple)

### 1️⃣ **Phishing**  
Ataque donde te engañan para que des tu contraseña o información.

Ejemplo real:  
Correo falso de “Microsoft” → tú entras → pones contraseña → atacante entra a tu cuenta.

SOC connection:  
Tú ya analizaste un caso real (Reporte 04).

---

### 2️⃣ **Malware**  
Software malicioso. Puede ser:

- virus  
- spyware  
- troyano  
- keylogger  

Ejemplo simple:  
Descargas un “programa gratis” → te instala un espía.

SOC connection:  
Analistas revisan procesos sospechosos, conexiones raras, descargas no autorizadas.

---

### 3️⃣ **Ransomware**  
Secuestra tus archivos y pide dinero para liberarlos.

Ejemplo real:  
Hospitales bloqueados hasta pagar.

SOC connection:  
Se detecta por actividad anormal, encriptaciones masivas o conexiones sospechosas.

---

### 4️⃣ **Fuerza bruta (Brute Force)**  
Intentar miles de contraseñas hasta adivinar la correcta.

Ejemplo simple:  
Probar 0000 → 0001 → 0002 → … en una caja fuerte.

SOC connection:  
Tus reportes 01, 02, 03 y tu playbook cubren este ataque a nivel profesional.

---

### 5️⃣ **DoS / DDoS (Denial of Service)**  
Ataque que **satura un servidor** para que deje de funcionar.

Ejemplo simple:  
Miles de personas llamando al mismo número al mismo tiempo → colapsa.

SOC connection:  
El SIEM detecta tráfico masivo desde muchas IP al mismo servicio.

---

### 6️⃣ **MITM (Man-In-The-Middle)**  
El atacante se mete entre tú y el servidor, y ve lo que haces.

Ejemplo simple:  
WiFi público falso llamado “Starbucks Free WiFi”.

SOC connection:  
Comportamientos sospechosos, certificados extraños, redirecciones HTTP → HTTPS fallidas.

---

### 7️⃣ **Ingeniería social**  
Atacan a la persona, no a la tecnología.

Ejemplos:
- “Soy del soporte técnico, dame tu contraseña.”  
- “Tienes un paquete detenido, ingresa tus datos.”  

SOC connection:  
Incidentes como phishing → exposición de credenciales.

---

# 🧩 3. ¿Qué quiere Security+ que entiendas aquí?

Solo esto:

👉 Saber **qué es cada ataque**  
👉 Saber **cómo reconocerlo**  
👉 Saber **cómo protegerte** (ej. MFA, entrenamiento, firewalls, etc.)

NO necesitas saber cómo programar malware.  
NO necesitas hacer hacking.  
NO necesitas fórmulas.

---

# 🧠 4. Ejemplos del mundo real (para que no memorices, lo entiendas)

### 🔹 Phishing  
Tu banco te pide “confirmar tu cuenta”.  
Falso → robo de credenciales.

### 🔹 Ransomware  
Abres un archivo “factura.pdf” → en realidad es malware.

### 🔹 Brute Force  
Alguien intenta adivinar tu contraseña de Instagram.

### 🔹 MITM  
Alguien crea un WiFi falso y ve tu tráfico.

---

# 🛡️ 5. ¿Cómo lo ve un SOC Analyst?

**Tu trabajo en el SOC consiste en:**

- detectar cuándo ocurre  
- identificar el patrón en logs  
- confirmar si es real o falso positivo  
- reportarlo  
- recomendar acciones  

Todo lo que ya estás haciendo en CYBERSCHOOL.

---

# 📝 6. MINI-PRÁCTICA (estilo Security+)  
Responde mentalmente (muy fácil):

**1. Si un usuario cae en un correo falso y entrega su contraseña, ¿qué tipo de ataque es?**  
A) Malware  
B) Phishing  
C) DoS  

**Respuesta:** B

---

**2. Si un atacante intenta adivinar contraseñas muchas veces seguidas, ¿qué ataque es?**  
A) Brute Force  
B) MITM  
C) Ingeniería social  

**Respuesta:** A

---

**3. Si los archivos de una empresa se bloquean y aparece un mensaje pidiendo dinero, ¿qué ataque es?**  
A) Ransomware  
B) DoS  
C) Phishing  

**Respuesta:** A

---

# ⭐ 7. RESUMEN FINAL (lo que debes recordar sí o sí)

- Phishing → te engañan  
- Malware → software malo  
- Ransomware → secuestran tus archivos  
- Brute Force → probar contraseñas sin parar  
- DoS/DDoS → saturar un servidor  
- MITM → interceptar tráfico  
- Ingeniería social → atacar a la persona  

¡Listo!  
Aprendiste lo que otros tardan horas en entender.

---

