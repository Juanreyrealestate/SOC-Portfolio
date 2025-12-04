# 🛡️ Reporte 10 — Privilege Escalation Detection (Escalada de Privilegios)

## 🎯 Objetivo
Detectar eventos que indiquen que un atacante obtuvo permisos más altos dentro de un sistema, comprometiendo su seguridad.

---

## 🧩 1. Datos del incidente

Máquina afectada: **WIN-FIN01**

Eventos observados:

| Hora     | Evento |
|----------|--------|
| 04:42 AM | Unauthorized modification attempt on service: BackupService |
| 04:43 AM | Service restarted running as NT AUTHORITY\SYSTEM |
| 04:45 AM | Process executed: cmd.exe → whoami |
| 04:45 AM | Result: NT AUTHORITY\SYSTEM |
| 04:48 AM | New admin account created: sys_maint$ |
| 04:50 AM | Registry key modified for elevated startup |

---

## 🧠 2. Análisis (razonamiento humano)

- La modificación del servicio “BackupService” sugiere explotación para elevar permisos.  
- Reiniciar el servicio bajo SYSTEM da control total del equipo.  
- El comando `whoami` es típico tras obtener privilegios elevados para verificar el nivel.  
- La creación de un usuario admin oculto asegura acceso continuo.  
- Modificar el registro con privilegios elevados indica persistencia avanzada.

La combinación de estos eventos confirma una **escalada de privilegios exitosa**.

---

## 🚨 3. Conclusión
El atacante ha elevado sus privilegios hasta nivel SYSTEM y ha establecido persistencia mediante una cuenta oculta y cambios en el registro.  
Esto representa un compromiso completo del servidor financiero.

---

## 🛡️ 4. Acciones de respuesta recomendadas

1. Aislar inmediatamente WIN-FIN01.  
2. Eliminar usuario `sys_maint$` y revisar otras cuentas ocultas.  
3. Restaurar configuración del servicio “BackupService”.  
4. Revisar claves de registro modificadas.  
5. Revocar credenciales posiblemente comprometidas.  
6. Revisar logs para identificar vector inicial de escalada.  
7. Investigar posible exfiltración adicional.

---

## 🧭 5. MITRE ATT&CK
- **T1068 — Exploitation for Privilege Escalation**  
- **T1543 — Create or Modify System Process**  
- **T1136 — Create Account**  
- **T1547 — Boot or Logon Autostart Execution**

---

## 📝 6. Resumen Ejecutivo
Se identificó un conjunto de eventos que indican que el atacante escaló privilegios en el servidor financiero WIN-FIN01, tomando control total del sistema y creando mecanismos de persistencia.  
El incidente requiere respuesta inmediata y análisis forense completo.

