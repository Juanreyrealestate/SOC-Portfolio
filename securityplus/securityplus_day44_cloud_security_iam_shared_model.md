# 🔐 Security+ — Día 44  
# Cloud Security, IAM Avanzado & Shared Responsibility Model (AWS/Azure)

## 🎯 Objetivo
Comprender las bases de seguridad en la nube: IAM (identidad), modelos de responsabilidad compartida, tipos de servicios cloud y riesgos comunes.  
Es un módulo clave en entrevistas y trabajos de seguridad moderna.

---

# 🟥 1. Shared Responsibility Model (modelo clave de la nube)

TODAS las nubes (AWS, Azure, GCP) funcionan así:

### ✔ El proveedor (AWS/Azure) es responsable de:
- la seguridad **DE** la nube  
  (infraestructura física, hardware, red, hipervisores, data centers)

### ✔ El cliente (tú / empresa) es responsable de:
- la seguridad **EN** la nube  
  (configuraciones, usuarios, identidades, permisos, datos, firewalls)

---

# 🟧 2. Modelos de servicio (IaaS, PaaS, SaaS)

### 1) IaaS — Infrastructure as a Service
Ejemplo: AWS EC2, Azure VMs  
Tú administras:
- SO  
- parches  
- firewalls  
- configuraciones  
- identidades  

Proveedor administra el hardware.

---

### 2) PaaS — Platform as a Service  
Ejemplo: AWS Lambda, Azure Functions  
Tú administras:
- código  
- permisos IAM  

Proveedor administra:
- SO  
- infraestructura  
- parches  

---

### 3) SaaS — Software as a Service  
Ejemplo: Gmail, Office 365  
Tú administras:
- usuarios  
- permisos  
- datos  
- MFA  

Proveedor administra todo lo demás.

---

# 🟨 3. IAM (Identity and Access Management)

IAM es el centro de la seguridad cloud.  
Si controlas IAM, controlas el acceso a todo.

### Conceptos clave:

### ✔ Policies
Documentos JSON que definen permisos:
- qué puede hacer un usuario  
- qué recursos puede ver  
- en qué condiciones  

---

### ✔ Roles
Identidades que asumen permisos temporalmente.  
Usados para:
- servidores  
- lambdas  
- servicios automáticos  
- acceso temporal seguro  

---

### ✔ Principle of Least Privilege
A cada identidad → solo los permisos estrictamente necesarios.

---

### ✔ MFA everywhere
Toda cuenta root / admin necesita MFA.

---

### ✔ Access Keys
Son contraseñas para APIs.  
Deben rotarse, protegerse y evitar subirse a GitHub (error muy común).

---

# 🟦 4. Riesgos típicos en AWS/Azure (muy preguntado)

### 1) Buckets S3 o Azure Blobs públicos
Exposición de datos.  
Causa más común de brechas cloud.

### 2) IAM demasiado permisivo
Ejemplo:  
`"Action": "*"` y `"Resource": "*"`

Peligrosísimo.

### 3) Claves de acceso expuestas en GitHub
Atacantes las automatizan.

### 4) Máquinas sin parches o sin SG/NACL correctamente configurados

### 5) Grupos de seguridad abiertos (0.0.0.0/0)
Cualquiera puede entrar.

---

# 🟪 5. Network Security en la nube (explicado simple)

### ✔ Security Groups (SG)
Firewalls virtuales **por instancia**.  
Permiten o bloquean tráfico entrante/saliente.

### ✔ NACLs (Network ACLs)
Firewalls a nivel de subred.  
Reglas de entrada y salida.

### ✔ VPC (Virtual Private Cloud)
Tu red privada dentro del proveedor cloud.

---

# 🟫 6. Preguntas típicas de entrevistas

### ❓ ¿Qué es el shared responsibility model?
Proveedor → seguridad de la nube.  
Cliente → seguridad en la nube.

### ❓ ¿Qué es IaaS vs PaaS vs SaaS?
IaaS → control del SO y red.  
PaaS → solo código.  
SaaS → solo usuarios/datos.

### ❓ ¿Qué es un IAM Role?
Identidad temporal con permisos restringidos.

### ❓ ¿Qué es least privilege?
Solo dar los permisos necesarios, nada más.

### ❓ ¿Qué riesgo cloud es más común?
Buckets públicos + permisos demasiado amplios.

---

# ⭐ Resumen del Día 44

Hoy aprendiste:
- cómo funciona la responsabilidad compartida (clave en trabajo real)  
- diferencias entre IaaS, PaaS, SaaS  
- IAM avanzado (policies, roles, least privilege)  
- riesgos comunes en AWS/Azure  
- firewalls cloud (SG, NACLs)  
- preguntas técnicas de entrevistas  

Este módulo te coloca al nivel requerido para roles **Cloud SOC Analyst** y **Cloud Security Jr**.
