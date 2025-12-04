# 🛡️ Reporte 11 — Beaconing & Command-and-Control (C2) Detection

## 🎯 Objetivo
Identificar patrones de comunicación que indiquen que un malware está contactando a un servidor de comando y control para recibir instrucciones o exfiltrar datos.

---

# 🧠 1. ¿Qué es un C2 (Command-and-Control)?
Es el “centro de mando” del atacante.

Una vez dentro del sistema, el malware:
- se comunica con un servidor externo,
- pide instrucciones,
- descarga payloads,
- envía datos robados.

Esta comunicación es el canal que mantiene vivo el ataque.

---

# 🧠 2. ¿Qué es beaconing?
Beaconing = **señales periódicas enviadas por malware hacia el servidor del atacante**.

Ejemplos:
- Cada 30 segundos → “¿Hay nuevas órdenes?”  
- Cada 2 minutos → “Aquí estoy, sigo vivo.”  
- Cada 10 minutos → “Subo logs robados.”

A diferencia del tráfico normal, el beaconing es:
- **repetitivo**
- **constante**
- **siempre al mismo destino**
- **misma cantidad de bytes**
- **fuera de horario laboral**

---

# 🧩 3. Indicadores clave de beaconing (fáciles de detectar)
1. **Intervalos perfectos**  
   Ejemplo: conexiones exactamente cada 60 segundos.

2. **Mismos tamaños de paquetes**  
   Ejemplo: 512 bytes salientes, siempre iguales.

3. **Destino único sospechoso**  
   Ejemplo: una sola IP en Europa del Este.

4. **Protocolos inusuales**  
   Port 8088, 8443, 1337, 4444, 53 (DNS abuse).

5. **Actividad fuera de horario**  
   Conexiones a las 3 AM.

6. **DNS con patrones raros**  
   Ejemplo:  
   `ajd92kdls99302.xyxcdn.net`

---

# 🧩 4. Caso simulado (para este reporte)

Máquina afectada: **WIN-233**

Logs de red:

| Hora        | Destino           | Puerto | Bytes | Notas |
|-------------|-------------------|--------|-------|-------|
| 02:01:10 AM | 185.77.92.11      | 8088   | 512   | conexión saliente |
| 02:02:10 AM | 185.77.92.11      | 8088   | 512   | patrón repetitivo |
| 02:03:10 AM | 185.77.92.11      | 8088   | 512   | intervalo exacto |
| 02:04:10 AM | 185.77.92.11      | 8088   | 512   | posible beaconing |
| 02:05:10 AM | 185.77.92.11      | 8088   | 512   | persistencia clara |

Características:
- Intervalos exactos de 60 segundos  
- Mismo tamaño de paquete (512 bytes)  
- Puerto sospechoso (8088)  
- Misma IP que apareció en el reporte de exfiltración  
- Actividad repetida en horario no laboral  

Todo apunta a comunicación de malware.

---

# 🧠 5. Análisis (razonamiento humano — AI-proof)

- Ningún proceso legítimo de WIN-233 establece conexiones PERFECTAMENTE periódicas.  
- El tamaño fijo sugiere keep-alive o heartbeat de malware.  
- La IP coincide con actividad maliciosa previa (día de exfiltración).  
- El puerto 8088 no es estándar en servicios del negocio.  
- La consistencia del patrón indica que el atacante mantiene control activo.  

Conclusión del analista:

> “WIN-233 está comprometido y mantiene comunicación activa con un servidor C2.”

---

# 🚨 6. Conclusión del Incidente
Se confirma que **WIN-233** está comunicándose con un servidor de comando y control a intervalos exactos.  
El patrón, horario, tamaño de paquetes y puerto indican **beaconing clásico de malware**.

Este incidente representa **riesgo crítico**, ya que el atacante:
- mantiene acceso  
- puede enviar órdenes  
- puede descargar más payloads  
- puede exfiltrar datos  
- puede activar ransomware en cualquier momento

---

# 🛡️ 7. Acciones recomendadas
1. **Aislar la máquina** inmediatamente.  
2. **Bloquear el dominio/IP** malicioso en firewall.  
3. **Revisar procesos y servicios persistentes**.  
4. **Buscar payloads descargados** previamente.  
5. **Analizar tráfico hacia otros destinos sospechosos**.  
6. **Revisar logs de DNS y Proxy** por actividad similar.  
7. **Ejecutar herramienta forense** para identificar backdoors.  

---

# 🧭 8. MITRE ATT&CK
- **T1071 — Web Protocol Beaconing**  
- **T1095 — Non-Application Layer Protocol**  
- **T1041 — Exfiltration Over C2 Channel**  
- **T1078 — Valid Accounts** (si usan credenciales)

---

# 📝 9. Resumen Ejecutivo
Se identificó tráfico de beaconing desde WIN-233 hacia una IP externa previamente asociada a actividad maliciosa.  
La comunicación periódica, el uso de un puerto no estándar y el tamaño constante de los paquetes indican operación activa de malware y la presencia de un servidor de comando y control.  
Acción urgente es requerida para evitar escalada y despliegue de cargas maliciosas adicionales.

