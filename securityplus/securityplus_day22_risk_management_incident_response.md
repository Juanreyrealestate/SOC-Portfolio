# 🔐 Security+ — Día 22  
# Risk Management, BIA, Incident Response & Disaster Recovery

## 🎯 Objetivo
Dominar la gestión de riesgos, análisis de impacto al negocio, el ciclo completo de respuesta a incidentes y los planes de continuidad. Este contenido es FUNDAMENTAL en Security+ y clave en trabajos SOC.

---

# 🟥 1. Risk Management (gestión de riesgos)

## 🔸 ¿Qué es un riesgo?
Amenaza + vulnerabilidad.

Ejemplo:  
- Amenaza: ransomware  
- Vulnerabilidad: puertos abiertos, RDP expuesto  
- Riesgo: infección total de la empresa  

## 🔸 Controles para reducir riesgo
- Administrativos: políticas, entrenamiento  
- Técnicos: firewalls, MFA, cifrado  
- Físicos: cámaras, cerraduras  

## 🔸 Respuestas al riesgo
1. **Mitigar** (controlarlo)
2. **Transferir** (seguro cibernético)
3. **Aceptar** (si el impacto es bajo)
4. **Evitar** (eliminar actividad riesgosa)

---

# 🟦 2. Risk Assessment (evaluación de riesgo)

## 🔸 Cualitativo
- Basado en probabilidad × impacto  
- Escalas (bajo/medio/alto)

## 🔸 Cuantitativo
Usa métricas:
- SLE (Single Loss Expectancy)  
- ARO (Annual Rate of Occurrence)  
- ALE (Annual Loss Expectancy) = SLE × ARO  

Security+ AMA este tipo de cálculo.

---

# 🟩 3. BIA — Business Impact Analysis

Determina qué tan crítico es cada sistema y cuánto daño ocurre si falla.

Mide:
- impacto financiero  
- legal  
- reputacional  
- operacional  

Componentes clave:

## ✔ RTO (Recovery Time Objective)
Tiempo máximo que un sistema puede estar caído.

## ✔ RPO (Recovery Point Objective)
Cuánta pérdida de datos es aceptable.

## ✔ MTBF (Mean Time Between Failures)
Frecuencia promedio entre fallos.

## ✔ MTTR (Mean Time to Repair)
Tiempo promedio para reparar.

---

# 🟧 4. Incident Response (ciclo completo)

**Security+ y SOC usan este ciclo SIEMPRE.**

## 🔵 1. Preparation
- políticas  
- entrenamiento  
- herramientas SIEM, EDR  
- playbooks  
- backups  

## 🔵 2. Identification
Darse cuenta de que un incidente ocurre:
- alertas SIEM  
- logs  
- actividad anómala  
- reporte del usuario  

## 🔵 3. Containment
Controlar el daño.

### Containment corto plazo:
- aislar host  
- bloquear IP  
- deshabilitar cuenta  

### Containment largo plazo:
- parches  
- segmentación  
- firewalls  

## 🔵 4. Eradication
Eliminar causa raíz:
- borrar malware  
- cerrar vulnerabilidades  
- limpiar persistencias  

## 🔵 5. Recovery
Volver a la normalidad:
- restaurar sistemas  
- verificar integridad  
- monitoreos reforzados  

## 🔵 6. Lessons Learned
Revisar:
- qué falló  
- cómo mejorar  
- actualizar políticas  

SOC escribe un **post-incident report**.

---

# 🟫 5. Disaster Recovery (DR) & Business Continuity (BC)

## 🔸 DRP (Disaster Recovery Plan)
Plan técnico para restaurar sistemas después de un desastre.

Incluye:
- backups  
- replicación  
- procedimientos de restauración  
- sitios alternos (hot/warm/cold site)

## 🔸 BCP (Business Continuity Plan)
Cómo sigue operando la empresa incluso durante el desastre.

---

# 🟨 6. Backup Strategies

## 🔸 Full Backup
Todo cada vez.  
Seguro pero consume tiempo.

## 🔸 Incremental Backup
Guarda cambios *desde el último backup incremental*.  
Rápido → recuperación más lenta.

## 🔸 Differential Backup
Guarda cambios *desde el último full backup*.  
Más grande que incremental → recuperación más rápida.

Security+ ama estas diferencias.

---

# 🟪 7. Hot, Warm, Cold Sites (muy preguntado)

## 🔥 Hot Site
- Equipado  
- Listo para uso inmediato  
- Más caro  
- Menor downtime  

## 🌡 Warm Site
- Equipo parcial  
- Algo preparado  
- Balance entre costo y rapidez  

## ❄️ Cold Site
- Espacio físico vacío  
- Más barato  
- Lento para levantar servicios  

---

# 🔵 8. Qué mira SOC en riesgo e incidentes

- alertas de malware  
- intentos de autenticación anómalos  
- actividad fuera de horario  
- transferencia de datos sospechosa  
- picos de tráfico en firewalls  
- cadenas de ataque mapeadas a MITRE  

SOC participa especialmente en:
- identificación  
- contención  
- erradicación  
- documentación del incidente  

---

# 📝 9. Mini-Práctica

**1. ¿Qué mide RPO?**  
➡️ Cuántos datos puedes perder.

**2. ¿Qué tipo de backup es más rápido de restaurar?**  
➡️ Differential.

**3. ¿Cuál es el primer paso de Incident Response?**  
➡️ Preparation.

**4. ¿Qué tipo de site es el más rápido en activarse?**  
➡️ Hot site.

**5. ¿Qué fórmula se usa en evaluación cuantitativa?**  
➡️ ALE = SLE × ARO.

---

# ⭐ Resumen Final
- Risk = amenaza + vulnerabilidad  
- RTO/RPO son esenciales en continuidad  
- IR cycle = preparación → recuperación → lecciones  
- DRP vs BCP → recuperación vs continuidad  
- Backups: full vs incremental vs differential  
- Esto es núcleo duro de Security+ y SOC  

