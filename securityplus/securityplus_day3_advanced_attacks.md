# 🔐 Security+ — Día 3  
# Ataques Avanzados (Nivel A — Explicado Súper Fácil)

---

## 🧠 1. SQL Injection (Inyección SQL)
El atacante escribe código malicioso donde debería ir texto normal.

Ejemplo simple:
- Caja de login: el atacante escribe un comando en vez de usuario.

Esto puede:
- Dar acceso no autorizado
- Extraer datos
- Modificar información

Ejemplo de la vida real:
- “Entré al sistema porque la página no limpiaba lo que yo escribía.”

SOC connection:
Actividades inusuales en base de datos → alertas.

---

## 🧠 2. XSS (Cross-Site Scripting)
El atacante inserta código en una página web que otros usuarios ven.

Ejemplo:
- Comentas en un foro:  
  `<script>robaCookies()</script>`

Afecta a:
- usuarios, no al servidor.

SOC connection:
Usuarios infectados → sesión robada → actividad rara.

---

## 🧠 3. Directory Traversal
El atacante accede a archivos donde no debería.

Ejemplo cotidiano:
- Entras a una web:  
  `website.com/images/`  
  → y pruebas  
  `../../../etc/passwd`

Si no está protegido, lo muestra.

SOC connection:
Accesos a rutas sensibles → alarma.

---

## 🧠 4. Man-in-the-Middle (MITM)
El atacante “escucha” entre tú y el servidor.

Ejemplo:
- Un WiFi falso llamado “Starbucks_Free”.

SOC connection:
Certificados raros, tráfico sospechoso.

---

## 🧠 5. Replay Attack
El atacante captura tráfico legítimo y lo “repite”.

Ejemplo simple:
- Capturo tu “token de acceso”  
- Lo uso otra vez aunque no tenga tu contraseña

SOC connection:
Tokens viejos usados → alerta.

---

## 🧠 6. Session Hijacking
El atacante roba tu “cookie de sesión” y entra como si fueras tú.

Ejemplo:
- Entras a Facebook  
- Atacante roba tu cookie → entra sin contraseña

---

## 🧠 7. Zero-Day Attack
Ataque que ocurre el MISMO día en que la vulnerabilidad se descubre.

Ejemplo:
- Apple anuncia un fallo en iPhone  
- Ese mismo día hay ataques porque no hay parche aún

SOC connection:
Tráfico raro después de anuncio de vulnerabilidad.

---

## 🧠 8. Supply Chain Attack
El atacante NO ataca a la empresa grande.  
Ataca a un proveedor MÁS débil.

Ejemplo real:
- SolarWinds  
- Su proveedor fue hackeado → todas las empresas clientes comprometidas

SOC connection:
Infecciones que vienen de actualizaciones legítimas.

---

# 📝 MINI-PRÁCTICA

**1. Un WiFi falso que roba tráfico es un ataque:**  
A) Replay  
B) MITM  
C) SQL Injection  
➡️ **Respuesta: B**

---

**2. Insertar código en un formulario para engañar la base de datos es:**  
A) Zero-Day  
B) SQL Injection  
C) XSS  
➡️ **Respuesta: B**

---

**3. Un ataque que se aprovecha de un proveedor débil se llama:**  
A) Supply Chain Attack  
B) Session Hijacking  
C) Directory Traversal  
➡️ **Respuesta: A**

---

# ⭐ RESUMEN FINAL (lo que importa en entrevistas y examen)

- **SQL Injection** → atacar bases de datos  
- **XSS** → robar datos de usuarios  
- **MITM** → interceptar tráfico  
- **Replay** → repetir mensajes capturados  
- **Session Hijacking** → robar sesión  
- **Directory Traversal** → acceder a archivos prohibidos  
- **Zero-Day** → ataque antes de haber parche  
- **Supply Chain** → atacar proveedores  

