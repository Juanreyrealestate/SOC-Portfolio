# 🛡️ Reporte 03 — Investigación Enriquecida de Fuerza Bruta (Log Enrichment)

## 🎯 Objetivo
Agregar contexto externo a los intentos de login fallidos para determinar si la actividad corresponde a un ataque automatizado, un error humano o un comportamiento esperado.  
Este proceso se conoce como **Log Enrichment**.

---

## 📊 Datos Originales Analizados (Día 2)
| Timestamp  | IP            | Usuario | Resultado |
|------------|--------------|---------|-----------|
| 10:01:01   | 203.0.113.10 | admin   | FAIL      |
| 10:01:17   | 203.0.113.10 | admin   | FAIL      |
| 10:01:32   | 203.0.113.10 | admin   | FAIL      |
| 10:01:46   | 203.0.113.10 | admin   | FAIL      |
| 10:01:57   | 203.0.113.10 | admin   | FAIL      |

Patrón repetitivo → posible ataque automatizado.

---

## 🌍 Enriquecimiento de IP (Simulación Profesional)
**IP:** 203.0.113.10  
**País:** Singapur  
**Proveedor:** DigitalOcean (cloud hosting)  
**Reputación:**  
- 17 reportes de abuso en 30 días  
- 32 intentos anteriores de fuerza bruta (SSH) en honeypots  
- Asociada con actividad automatizada

**Interpretación SOC:**  
Los servidores cloud se usan frecuentemente para lanzar ataques automatizados debido a su bajo costo y facilidad para crear instancias temporales.  
Esto aumenta la probabilidad de actividad maliciosa.

---

## 🧠 Análisis Humano (AI-Proof)
- El patrón de tiempos constantes sugiere un script, no un humano.  
- La IP proviene de cloud hosting → alta probabilidad de automatización.  
- La reputación negativa indica actividad maliciosa previa.  
- El usuario objetivo es “admin”, lo cual incrementa el riesgo.  
- No hay variación en método, velocidad o error → comportamiento de herramienta automatizada.

---

## 🚨 Conclusión
El evento corresponde a un **ataque de fuerza bruta automatizado** proveniente de una IP con historial malicioso.  
No existen indicadores que sugieran error humano.  
La actividad debe considerarse como incidente de seguridad **real**.

---

## 🛡️ Recomendaciones SOC
1. Bloquear temporalmente la IP 203.0.113.10.  
2. Revisar si hubo intentos de login exitosos posteriores.  
3. Revisar tráfico lateral o movimientos sospechosos.  
4. Configurar rate limiting o fail2ban (si aplica).  
5. Habilitar MFA para usuarios administrativos.  
6. Investigar si otras IP de DigitalOcean han atacado el sistema.
