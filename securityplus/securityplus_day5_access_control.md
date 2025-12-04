# 🔐 Security+ — Día 5  
# Modelos de Control de Acceso (DAC, RBAC, MAC) — Nivel A

---

## 🧠 1. ¿Qué es el control de acceso?
Control de acceso es simplemente **decidir quién puede acceder a qué**.

Ejemplos del mundo real:
- No todos pueden entrar a todos los pisos de un edificio.  
- No todos pueden ver los mismos archivos en un computador.  

En ciberseguridad:
> El control de acceso determina quién puede leer, modificar, ejecutar o eliminar un recurso.

---

# 🟩 2. Modelo DAC — Discretionary Access Control  
**El dueño del recurso decide quién tiene acceso.**

Es el modelo más flexible, pero también el menos estricto.

Ejemplos:
- Tienes un archivo en tu laptop y tú eliges quién puede verlo.  
- En Windows, cuando haces “Compartir carpeta” y das permisos manualmente.  

Características:
- El **propietario** controla los permisos.  
- Fácil de usar.  
- Menos seguro en grandes organizaciones.

DAC = *“Yo decido quién entra a mi cuarto.”*

---

# 🟦 3. Modelo RBAC — Role Based Access Control  
**Los permisos se asignan según el rol (posición, departamento, función).**

Este es el modelo más usado en empresas modernas.

Ejemplos:
- Empleado de Finanzas → acceso a nómina.  
- Empleado de Recursos Humanos → acceso a datos de empleados.  
- Ingeniero → acceso a servidores técnicos.

Características:
- Ordenado  
- Escalable  
- Se usa en Active Directory, Azure, AWS, Google Cloud  

RBAC = *“No importa quién seas, importa tu rol.”*

---

# 🟥 4. Modelo MAC — Mandatory Access Control  
**El sistema impone las reglas y el usuario NO puede cambiarlas.**

Se usa en ambientes donde la seguridad es crítica.

Ejemplos:
- Gobierno  
- Militar  
- Documentos clasificados (“Confidential”, “Secret”, “Top Secret”)

Características:
- Muy seguro  
- Muy rígido  
- Control estricto basado en niveles de clasificación  

MAC = *“Solo los que tienen nivel suficiente pueden entrar.”*

---

# 🧩 5. Comparación simple

| Modelo | Quién decide | Ejemplo |
|--------|--------------|---------|
| **DAC** | El dueño | Tú compartiendo una carpeta |
| **RBAC** | El rol | Finanzas puede ver nómina |
| **MAC** | El sistema | Documentos clasificados |

---

# 🧠 6. Ejemplos para memorizarlo fácil

- **DAC →** Tú decides quién puede entrar.  
- **RBAC →** Tu puesto define tus permisos.  
- **MAC →** Clasificación militar; el sistema manda.  

---

# 📝 7. Mini-Práctica (Preguntas tipo Security+)

❓ 1. “El dueño del archivo decide a quién darle acceso” corresponde a:  
A) RBAC  
B) DAC  
C) MAC  
➡️ **Respuesta: B**

---

❓ 2. “Permisos basados en departamento (Finanzas, HR, IT)” corresponde a:  
A) DAC  
B) RBAC  
C) MAC  
➡️ **Respuesta: B**

---

❓ 3. “Secret / Top Secret / Confidential” corresponde a:  
A) DAC  
B) RBAC  
C) MAC  
➡️ **Respuesta: C**

---

# ⭐ 8. Resumen final
- **DAC** — el dueño controla el acceso.  
- **RBAC** — los permisos dependen del rol.  
- **MAC** — el sistema dicta los permisos; máxima seguridad.  

Si recuerdas estas tres frases, ya dominas el tema.

