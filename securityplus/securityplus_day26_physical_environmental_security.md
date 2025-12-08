# 🔐 Security+ — Día 26  
# Physical Security, Environmental Controls, Hardware Protections & Secure Disposal

## 🎯 Objetivo
Aprender todos los controles físicos y ambientales que protegen infraestructura crítica. Estas preguntas aparecen MUCHO en Security+ y son fáciles puntos si las entiendes con claridad.

---

# 🟥 1. Physical Security Controls

## 🔸 Barreras perimetrales (Perimeter Security)
- Cercas  
- Muros  
- Rejas  
- Iluminación exterior  
- Cámaras exteriores  

Objetivo: evitar acceso físico no autorizado.

---

## 🔸 CCTV (Closed-Circuit Television)
Características de interés:
- Resolución  
- Ángulo de visión  
- IR para visión nocturna  
- Almacenamiento local o NVR  
- Detección de movimiento  

Security+: **IP-based CCTV es más seguro que analógico**.

---

## 🔸 Access Control systems
Métodos de acceso físico:
- Tarjetas RFID / Proximity cards  
- Smart cards  
- Biometrics (huella, iris, rostro)  
- PIN pads  
- Badges  

**Multifactor físico** existe: tarjeta + biometría.

---

## 🔸 Mantraps
Dos puertas secuenciales:  
- La primera no abre hasta que la segunda se cierre.  
Evita tailgating y piggybacking.

---

## 🔸 Turnstiles
Dejan pasar a una sola persona a la vez.  
Evitan entradas en grupo.

---

## 🔸 Guards / Security Personnel
Ventajas:
- evaluación humana  
- flexibilidad  
- prevención  
- verificación adicional  

---

## 🔸 Alarms & Sensors
- Motion detection  
- Heat sensors  
- Glass break sensors  
- Pressure/magnetic sensors  

---

# 🟦 2. Environmental Controls

## 🔸 HVAC (Heating, Ventilation, Air Conditioning)
¿Por qué importa para seguridad?
- Evita sobrecalentamiento de servidores  
- Previene humedad excesiva  
- Mantiene condiciones óptimas de hardware  

---

## 🔸 Fire suppression systems
Tipos:

### ✔ Water-based
- Sprinklers  
- NO se usa cerca de equipos sensibles  

### ✔ Clean agent systems  
- FM-200  
- CO₂  
- Halon (ya casi no se usa por regulación ambiental)  
No dañan equipos electrónicos.

### ✔ Fire extinguishers
Clases:
- Clase A — combustibles sólidos  
- Clase B — líquidos  
- Clase C — eléctricos (importante para data centers)

---

## 🔸 EMI / RFI shielding  
Protección contra interferencias electromagnéticas y radiofrecuencia.

Utilizado en:
- habitaciones sensibles  
- entornos industriales  
- laboratorios  

---

## 🔸 Faraday cages  
Bloquean señales inalámbricas.  
Usos:
- Protección electromagnética  
- Aislamiento de dispositivos comprometidos  
- DFIR (evita que un atacante remoto borre evidencia)

---

# 🟩 3. Hardware-Based Security

## 🔸 TPM (Trusted Platform Module)
Chip especializado que almacena:
- claves criptográficas  
- mediciones de arranque  
- funciones de BitLocker  

---

## 🔸 HSM (Hardware Security Module)
Dispositivo seguro para generar y guardar claves.

Usado en:
- bancos  
- certificados digitales  
- infraestructura crítica  

---

## 🔸 Secure Boot
Verifica que el sistema arranca solo software firmado y legítimo.  
Previene rootkits de arranque.

---

## 🔸 USB blocking / Endpoint control
Evita fugas de datos o malware por USB.

---

# 🟧 4. Secure Disposal (MUY preguntado en Security+)

## 🔸 Shredding (trituración)
Físicamente destruye papel o medios.

---

## 🔸 Degaussing
Campo magnético fuerte que borra discos magnéticos.  
❌ NO funciona en SSD.

---

## 🔸 Incineration
Destrucción total mediante fuego.  
Usado para datos altamente sensibles.

---

## 🔸 Purging / Sanitization
Elimina datos de forma que **no puedan recuperarse**.

---

## 🔸 Wiping
Sobrescribe datos múltiples veces.  
Funciona en HDD, **NO en SSD**.

En Security+:  
➡️ “SSD → usar *crypto erase*”  
➡️ “HDD → wiping / degaussing / shredding”

---

# 🟫 5. Tamper Protection

## 🔸 Tamper-evident seals
Indican si alguien intentó abrir o manipular el equipo.

## 🔸 Tamper-resistant hardware
Dificulta la manipulación física.

## 🔸 Cable locks
Protegen laptops y equipos móviles en oficinas.

## 🔸 Safe rooms / SCIFs
Áreas ultra-seguras con controles estrictos.

---

# 🟨 6. Social Engineering in Physical Context

## 🔸 Tailgating
Entrar detrás de alguien sin permiso.

## 🔸 Piggybacking
La persona con acceso permite entrar a otro.

## 🔸 Dumpster diving
Buscar información en basura.

**Mitigación:**
- Shredding  
- Policies  
- CCTV  
- Guardias  

---

# 📝 7. Mini-Práctica Security+ Style

**1. ¿Qué método bloquea señales inalámbricas?**  
➡️ Faraday cage

**2. ¿Qué método de destrucción NO funciona para SSD?**  
➡️ Degaussing / Wiping

**3. ¿Qué suprime fuego sin dañar electrónicos?**  
➡️ Clean agent (FM-200)

**4. ¿Qué evita tailgating?**  
➡️ Mantrap

**5. ¿Qué componente protege claves criptográficas a nivel hardware?**  
➡️ TPM / HSM

---

# ⭐ Resumen Final
- Physical + Environmental Security = puntos fáciles del examen  
- Recuerda diferencias:  
  - Wiping no sirve para SSD  
  - Clean agent ≠ water-based  
  - Mantrap ≠ turnstile  
  - Faraday ≠ shielding normal  

