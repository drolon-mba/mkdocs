# 40 - Gobernanza Low-Code/No-Code (LCNC)

Abordar el riesgo y la seguridad de la proliferación de herramientas *Low-Code/No-Code* en la organización para asegurar cumplimiento, seguridad y calidad de datos.  
🏠 [Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 ¿Qué es LCNC Governance?](#que-es-lcnc-governance)
- [⚠️ Riesgos Clave de LCNC](#riesgos-clave-de-lcnc)
- [🔒 Políticas de Seguridad y Acceso](#politicas-de-seguridad-y-acceso)
- [📊 Data Governance para LCNC](#data-governance-para-lcnc)
- [🔄 Ciclo de Vida y Auditoría](#ciclo-de-vida-y-auditoria)
- [👥 Roles y Accountability](#roles-y-accountability)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)

---

## 🎯 ¿Qué es LCNC Governance?

**Qué:** Marco de trabajo que define políticas, estándares y supervisión para aplicaciones creadas con plataformas *Low-Code/No-Code* (LCNC), muchas veces por *Citizen Developers* fuera de TI.  
**Por qué:** Sin gobernanza, LCNC deriva en **Shadow IT**, vulnerabilidades, inconsistencias de datos y pérdida de trazabilidad. La gobernanza busca equilibrar **velocidad** con **integridad** y **control**.  
**Quién:** Data Stewards, Platform Engineers, Security Experts, Business Owners.  
**Esfuerzo:** Inversión inicial en tooling y políticas que evita costos exponenciales por brechas o incumplimientos.

---

## ⚠️ Riesgos Clave de LCNC

| Riesgo | Problema | Impacto |
|:-------|:---------|:--------|
| **Shadow IT** | Apps sin supervisión TI | Falta de seguridad y observabilidad |
| **Configuración insegura** | Endpoints expuestos, defaults inseguros | Vulnerabilidades críticas |
| **Data Leakage/Integridad** | Manejo incorrecto de PII o datos maestros | Filtración, duplicados, pérdida de unicidad |
| **Vendor Lock-in** | Dependencia de plataformas propietarias | Costos altos, migración difícil |
| **Cumplimiento regulatorio** | GDPR, HIPAA, SOX | Multas y sanciones |
| **AI copilots integrados** | Generación automática sin control | Riesgo de lógica insegura o sesgada |

---

## 🔒 Políticas de Seguridad y Acceso

| Principio | Aplicación en LCNC | Referencia |
|:----------|:-------------------|:-----------|
| **Least Privilege** | Acceso mínimo a DB/APIs, granular por filas/columnas | Seguridad de acceso |
| **Zero Trust** | Autenticación/autorización explícita en cada conexión | Zero Trust |
| **Secrets Management** | Claves gestionadas en Vault/Secrets Manager, nunca hardcodeadas | Gestión de secretos |
| **Input Validation** | Validación en backend además del builder | Validación de entradas |
| **Secure Defaults** | Plantillas seguras preconfiguradas en la plataforma | Insecure Design |

---

## 📊 Data Governance para LCNC

| Práctica | Qué | Cómo |
|:---------|:----|:-----|
| **Data Lineage** | Mapear origen/consumo de datos | Catalogar campos creados/modificados |
| **Data Contracts** | Cumplir schema y calidad | Rechazo o DLQ si falla |
| **Data Quality Monitoring** | Monitorear freshness, volumen, null rate, duplicados | Alertas y dashboards |
| **Master Data Integration** | LCNC no debe crear “nuevos maestros” sin aprobación | Integración controlada |

---

## 🔄 Ciclo de Vida y Auditoría

- **Registro obligatorio:** catálogo central con owner, dominio, criticidad.  
- **ALM completo:** ambientes separados (Dev, Staging, Prod).  
- **Audit Logging inmutable:** quién cambió qué y cuándo.  
- **Security Testing periódico:** SAST/DAST sobre conectores y configuraciones.  
- **Center of Excellence (CoE):** equipo que define estándares, plantillas seguras y revisa apps LCNC.  

---

## 👥 Roles y Accountability

| Rol | Responsabilidad |
|:----|:----------------|
| **Platform Owner** | Mantener infraestructura LCNC, definir plantillas seguras |
| **Citizen Developer** | Crear apps cumpliendo reglas de negocio y convenciones |
| **Data Steward** | Responsable final del dato, valida calidad y privacidad |
| **Security Officer** | Revisión periódica de apps LCNC, cumplimiento regulatorio |
| **Business Owner** | Define requerimientos, asegura alineación con objetivos |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Hardcoded Secrets** | Credenciales en app/config | Secrets Manager + rotación |
| **Access Wildcard** | Permisos totales (“SELECT *”) | RBAC granular |
| **No Testing** | Asumir que builder = producción | Staging + smoke tests |
| **Sin Owner** | App huérfana | Registro obligatorio en catálogo |
| **Duplicación de datos maestros** | Nuevos “clientes” fuera del MDM | Integración con Data Governance |

---

## 📚 Recursos

- [OWASP Top 10 – Insecure Design](https://owasp.org/Top10/A04_2021-Insecure_Design/)  
- [Gartner LCNC Governance Framework](https://www.gartner.com/en/documents/3980469)  
- [Microsoft Power Platform Governance Guide](https://learn.microsoft.com/en-us/power-platform/admin/governance)  
- [OutSystems Security Best Practices](https://www.outsystems.com/security/)  
- [Mendix Governance & Compliance](https://docs.mendix.com/developerportal/deploy/governance/)  

---

[⬅️ Anterior: Capítulo 39 - Data Literacy](./39-data-literacy.md) | ⬆️ [Volver arriba](#40-gobernanza-low-codeno-code-lcnc) | [➡️ Siguiente: Casos de Estudio](./97-casos-estudio.md)
