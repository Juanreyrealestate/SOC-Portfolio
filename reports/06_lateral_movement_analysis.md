# 🛡️ Reporte 06 — Lateral Movement (Movimiento Lateral)

## 🎯 Objetivo
Detectar si un atacante comprometió una cuenta y luego se movió entre sistemas internos para acceder a información más sensible.

---

## 🧩 1. Datos del incidente (caso simulado)

Usuario afectado: **Carlos.P**  
Acceso normal esperado: solo desde su laptop **WIN-102**

Eventos observados:

| Hora  | Origen    | Usuario  | Acción                                 |
|-------|-----------|----------|----------------------------------------|
| 15:04 | WIN-102   | Carlos.P | LOGIN SUCCESS                          |
| 15:09 | WIN-233   | Carlos.P | LOGIN SUCCESS                          |
| 15:11 | WIN-FIN01 | Carlos.P | LOGIN FAILED                           |
| 15:12 | WIN-FIN01 | Carlos.P | LOGIN FAILED                           |
| 15:13 | WIN-FIN01 | Carlos.P | LOGIN SUCCESS                          |
| 15:16 | WIN-FIN01 | Carlos.P | Access to \\FINANCE\\Payroll.xlsx      |

---

## 🧠 2. Análisis (razonamiento humano)

- Carlos normalmente **solo** inicia sesión desde **WIN-102** (su laptop).
- Aparece login desde **WIN-233**, una máquina interna donde nunca debería entrar.
- Luego intenta varias veces entrar a **WIN-FIN01** (servidor financiero).
- Finalmente **logra entrar** y accede a un archivo sensible (`Payroll.xlsx`).

Eso NO es comportamiento normal de un usuario común.  
Parece alguien usando su cuenta para moverse por la red y buscar información valiosa.

> Esto encaja con **lateral movement**: el atacante ya está dentro y va saltando entre sistemas.

---

## 🧭 3. Interpretación

Probable secuencia:

1. La cuenta de **Carlos.P** fue comprometida (por ejemplo, phishing).
2. El atacante usa esa cuenta para iniciar sesión en otra máquina interna (**WIN-233**).
3. Desde ahí intenta acceder al servidor financiero (**WIN-FIN01**).
4. Tras algunos intentos fallidos, logra entrar.
5. Accede a información de nómina (alta sensibilidad).

Esto corresponde a la técnica MITRE ATT&CK:

- **T1021 – Remote Services (Lateral Movement)**

---

## 🚨 4. Acciones recomendadas (SOC)

1. **Resetear la contraseña** de Carlos.P.
2. **Cerrar todas las sesiones activas** de esa cuenta.
3. **Aislar** las máquinas WIN-233 y WIN-FIN01 para análisis.
4. Revisar:
   - qué otros archivos se abrieron,
   - si hubo descargas,
   - si hubo movimientos hacia otros servidores.
5. Buscar otros logins inusuales de la misma cuenta.

---

## 🛡️ 5. Recomendaciones a futuro

- Activar **MFA** para cuentas que acceden a servidores críticos.
- Alertar cuando un usuario se conecta a máquinas donde nunca ha trabajado.
- Implementar segmentación de red (no todas las máquinas pueden ver todos los servidores).
- Dar entrenamiento de phishing al usuario si el origen fue un correo malicioso.

---

## 📝 6. Resumen corto

Se observó que la cuenta de un usuario legítimo fue utilizada para iniciar sesión en máquinas donde normalmente no tiene actividad, incluyendo un servidor financiero.  
El patrón indica **movimiento lateral** dentro de la red para alcanzar información sensible, lo que sugiere compromiso de cuenta y requiere respuesta inmediata.
