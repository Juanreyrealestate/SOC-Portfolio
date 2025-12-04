Reporte 01 – Primer vistazo a conexiones y logs

Objetivo
Hoy intenté ver quién se conecta a la máquina y si hay intentos fallidos de acceso, para empezar a pensar como un analista SOC.
 
Comandos usados
who → resultado resumido
last | head -n 10 → resultado o error. Ver quien se conectó ultimo.
ls /var/log → qué pasó.  Intentar ver “logs” (la caja negra de lo que pasó)
sudo tail -n 50 /var/log/auth.log → qué pasó.
•  sudo → pedir privilegios de administrador
•  tail -n 50 → ver las últimas 50 líneas
•  /var/log/auth.log → archivo donde se guardan cosas de autenticación

 
Observaciones
•	En mi sistema no aparece /var/log/auth.log
•	No pude ver intentos de login, pero entendí qué se buscaría.
•	Me di cuenta que muchos comandos pueden fallar y es normal.
 
 
Conclusión
Hoy no encontré un ataque real, pero aprendí dónde buscaría evidencia de accesos fallidos y empecé a diferenciar en mi cabeza qué podría ser un error humano vs. un ataque intencional.

