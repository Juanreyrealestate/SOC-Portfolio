# 🛫 Reporte 05 — Impossible Travel Detection

## 🎯 Objetivo
Detectar inicios de sesión imposibles por distancia y tiempo, lo que indica compromiso de cuenta mediante robo de credenciales.

---

## 📊 1. Datos Analizados

Usuario: **Carlos.P**

| Hora  | IP            | Ubicación             | Resultado |
|-------|---------------|------------------------|-----------|
| 10:05 | 45.22.11.9    | Miami, USA            | SUCCESS   |
| 10:28 | 196.44.120.5  | Johannesburgo, Sudáfrica | SUCCESS |

**Distancia aproximada:** 13,000 km  
**Tiempo entre logins:** 23 minutos  
**Velocidad requerida:** físicamente imposible  

---

## 🌍 2. Enriquecimiento de IPs

### IP 45.22.11.9 (Miami, USA)
- Ubicación habitual del usuario  
- Sin historial malicioso  

### IP 196.44.120.5 (Sudáfrica)
- Proveedor: Telco regional  
- Reportes previos de abuso  
- Ubicación totalmente inusual  

---

## 🧠 3. Análisis Humano (AI-Proof)

- El usuario trabaja presencial en Miami  
- No reporta viajes  
- No usa VPN internacional  
- No existen patrones previos de login desde África  
- Dos logins exitosos en menos de 30 minutos → imposibilidad física  
- Alto riesgo de robo de credenciales  

**Conclusión:**  
Compromiso de cuenta por uso malicioso de credenciales.

---

## 🚨 4. Acciones de Contención

1. Forzar cambio de contraseña  
2. Cerrar todas las sesiones activas  
3. Bloquear IP sudafricana  
4. Eliminar reglas de reenvío (si existen)  
5. Revisar actividad entre 10:28 y el momento del bloqueo  

---

## 🛡️ 5. Recomendaciones

- Revisar dispositivos asociados  
- Activar MFA obligatorio  
- Implementar alerta de “Impossible Travel” en el SIEM  
- Entrenamiento anti-phishing al usuario  

---

