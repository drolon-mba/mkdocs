# 00 - Índice General

> Documento vivo de estándares, buenas prácticas y decisiones técnicas del equipo.
>
> Si se encuentra una mejora, ¡se agradece su actualización!
>
> Última actualización: `YYYY-MM-DD`

---

## 📖 Índice General

### 🎯 Fundamentos

- [01 - Fundamentos](./01-fundamentos.md)
  - Niveles de criticidad
  - Reglas generales de código
  - Reglas por lenguaje
  - Reglas por framework
- [02 - Onboarding](./02-onboarding.md)
  - Guía de inicio, Arquitectura, Primer PR

### 🔬 Desarrollo y Testing

- [03 - Disciplinas de Desarrollo](./03-disciplinas-desarrollo.md)
  - TDD, BDD, ATDD, DDD, FDD, MDD, PBT
- [04 - Testing](./04-testing.md)
  - Backend, Frontend, Mobile, Performance, Testing Avanzado
- [05 - Gestión de Calidad](./05-gestion-calidad.md)
  - Code coverage, Static analysis, Linting, Peer review

### 🏗️ Arquitectura y Diseño

- [06 - Arquitectura y Patrones](./06-arquitectura-patrones.md)
  - Arquitecturas de software
  - Patrones de diseño
  - Patrones arquitectónicos avanzados
  - FSM (Finite State Machines)
- [07 - Sesgos Cognitivos, Falacias y Leyes](./07-sesgos-falacias.md)
  - Sesgos cognitivos, Falacias lógicas, Leyes paradójicas, Efectos psicológicos

### 🚀 Operaciones

- [08 - DevOps](./08-devops.md)
  - CI/CD, IaC, Contenedores, Patrones de despliegue
- [09 - Seguridad](./09-seguridad.md)
  - Principios de seguridad, Herramientas, Patrones avanzados
- [10 - Observabilidad y Telemetría](./10-observabilidad.md)
  - Logging, Metrics, Tracing, APM, Alerting, Health checks

### 🛠️ Resolución de Problemas y Mejora

- [11 - Herramientas de Análisis de Problemas](./11-herramientas-problemas.md)
  - Ishikawa, 5 Porqués, Pareto, FTA, 5W2H, Lluvia de ideas
- [12 - Metodologías de Mejora Continua](./12-mejora-continua.md)
  - Six Sigma, Kaizen, Lean, PDCA, 5S, 8D, Kanban, MTBF

### ⚡ Performance y Producción

- [13 - Optimización de Performance](./13-performance.md)
  - Optimización de DB, Frontend, Backend, Caching
- [14 - Checklist de Producción](./14-checklist-produccion.md)
  - Validaciones pre-deploy, Post-deploy verification, Rollback criteria

### 💾 Datos y APIs

- [15 - Bases de Datos](./15-bases-datos.md)
  - SQL, NoSQL, Time Series, Graph, Columnar, In-memory
- [16 - APIs y Protocolos](./16-apis-protocolos.md)
  - REST, GraphQL, gRPC, WebSockets, Event-Driven
  - Documentación por protocolo
  - Patrones de comunicación

### 📱 Interfaces y Experiencia

- [17 - Mobile, UI y UX](./17-mobile-ui-ux.md)
  - Desarrollo móvil, UI, UX, Accesibilidad

### ☁️ Infraestructura y Costos

- [18 - Infraestructura y Cloud](./18-infraestructura-cloud.md)
  - Multi-cloud, Serverless, Containerization, Edge computing
- [19 - Optimización de Costos (FinOps)](./19-cost-optimization.md)
  - FinOps, Right-sizing, Reserved Instances, Cloud cost monitoring

### 🤖 Datos Avanzados

- [20 - Machine Learning y Deep Learning](./20-machine-learning.md)
  - ML supervisado/no supervisado, DL, MLOps, NLP, RL
- [21 - Ciencia de Datos](./21-ciencia-datos.md)
  - Limpieza, Visualización, Reproducibilidad, Modelado
- [22 - Data Governance](./22-data-governance.md)
  - Data Lineage, Data Quality, MDM, Privacy by Design

### 📊 Estrategia y Negocio

- [23 - Análisis Estratégico](./23-analisis-estrategico.md)
  - FODA, PESTEL, Porter, VRIO, CAME, Buyer Persona, ICP
- [24 - Product Management](./24-product-management.md)
  - JTBD, User Story Mapping, OKRs, North Star Metric
- [25 - Métricas y KPIs](./25-metricas-kpis.md)
  - HEART, AARRR, DORA, NPS, SLIs/SLOs/SLAs

### 👥 Roles y Cultura

- [26 - Roles y Responsabilidades](./26-roles-responsabilidades.md)
  - Roles técnicos, Producto y negocio, Calidad, Operaciones, Datos, RACI Matrix
- [27 - Colaboración y Cultura](./27-colaboracion-cultura.md)
  - Pair Programming, Code Review, Postmortems, Escalation

### 📝 Documentación y Convenciones

- [28 - Documentación y Diagramas](./28-documentacion-diagramas.md)
  - Markdown, Mermaid, LaTeX, PlantUML, C4, ER, UML
  - Tipos de diagramas: flujo, secuencia, clases, estado
- [29 - Convenciones](./29-convenciones.md)
  - Nomenclatura, Git/GitOps, i18n/l10n, Configuración, Dependencias

### 🤖 AI y Automatización

- [30 - Prompts y Agentes de IA](./30-prompts-agentes.md)
  - The Gentleman (agente principal), 57 Agentes especializados, Prompt engineering
- [31 - Estrategia de IA y Automatización](./31-estrategia-ia-automatizacion.md)
  - Casos de uso prácticos, Límites de la IA, Integración en CI/CD

### ⚖️ Ética y Gobernanza

- [32 - Ética y Gobernanza de IA](./32-etica-gobernanza-ia.md)
  - Bias en ML, Fairness metrics, Explicabilidad (XAI), Privacy, Gobernanza

### 📝 Comunicación y Artefactos

- [33 - Comunicación y Contenido Técnico](./33-comunicacion-contenido.md)
  - Escritura para diferentes audiencias, Storytelling técnico, Content repurposing, SEO
- [34 - Plantillas y Artefactos](./34-plantillas-artefactos.md)
  - Decision Journal, Pre-Mortem, Runbook, Incident Response Playbook, ADR

### 🔧 Gestión Técnica

- [35 - Gestión de Dependencias y Deuda Técnica](./35-dependencias-deuda-tecnica.md)
  - Dependency management, Technical debt tracking, Refactoring strategies, Breaking changes
- [36 - Priorización y Roadmapping](./36-priorizacion-roadmapping.md)
  - RICE Framework, MoSCoW, Kano Model, Value vs Effort Matrix, Roadmapping
- [37 - Gestión de Secretos](./37-gestion-secretos.md)
  - Secret management tools, Secret rotation, Least privilege, Secrets en CI/CD, Detección

### 🛡️ Resiliencia y Datos

- [38 - Chaos Engineering y Resiliencia](./38-chaos-engineering.md)
  - Chaos Engineering principles, Failure injection, Game Days, Resiliencia patterns
- [39 - Data Literacy](./39-data-literacy.md)
  - Data literacy fundamentals, Self-service analytics, Data storytelling, Data quality

### 📝 Gobernanza Low-Code/No-Code (LCNC)

- [40 - Gobernanza Low-Code/No-Code (LCNC)](./40-lowcode-nocode.md)
  - ¿Qué es LCNC Governance?, Riesgos Clave de LCNC, Políticas de Seguridad y Acceso, Data Governance para LCNC, Ciclo de Vida y Auditoría, Roles y Accountability, Anti-patrones, Recursos.

### 📝 Recursos de práctica de código y preparación para entrevistas

- [98 - Recursos de práctica de código y preparación para entrevistas](./98-recursos-entrevistas.md)
  - Coding interview questions, Coding interview preparation, Coding interview tips, Coding interview resources.

### 📝 Glosario

- [99 - Glosario](./99-glosario.md)
  - Glosario de términos técnicos y conceptos.

### 📝 Reportes y Templates

| Tipo de Reporte | Template | Ejemplo |
|:----------------|:---------|:--------|
| **Bug Report** | [📄 Ver Template](./reports/templates/bug-report-template.md) | [🐛 Ver Ejemplo](./reports/examples/bug-report-example.md) |
| **Feature Request** | [📄 Ver Template](./reports/templates/feature-request-template.md) | [💡 Ver Ejemplo](./reports/examples/feature-request-example.md) |
| **Post-Mortem** | [📄 Ver Template](./reports/templates/post-mortem-template.md) | [💀 Ver Ejemplo](./reports/examples/post-mortem-example.md) |
| **RFC** | [📄 Ver Template](./reports/templates/rfc-template.md) | [📝 Ver Ejemplo](./reports/examples/rfc-example.md) |

---

## 🎯 Cómo usar esta guía

### Para nuevos desarrolladores

1. Comenzar por [Fundamentos](./01-fundamentos.md)
2. Leer [Onboarding](./02-onboarding.md)
3. Consultar [Disciplinas de Desarrollo](./03-disciplinas-desarrollo.md)
4. Revisar convenciones del lenguaje/framework que usarás

### Para arquitectos

1. Revisar [Arquitectura y Patrones](./06-arquitectura-patrones.md)
2. Consultar [Infraestructura y Cloud](./18-infraestructura-cloud.md)
3. Validar contra [Seguridad](./09-seguridad.md)
4. Implementar [Observabilidad](./10-observabilidad.md)

### Para product managers

1. Estudiar [Product Management](./24-product-management.md)
2. Definir [Métricas y KPIs](./25-metricas-kpis.md)
3. Usar [Análisis Estratégico](./23-analisis-estrategico.md)
4. Aplicar [Herramientas de Problemas](./11-herramientas-problemas.md)

### Para DevOps/SRE

1. Implementar [DevOps](./08-devops.md)
2. Configurar [Observabilidad](./10-observabilidad.md)
3. Optimizar [Performance](./13-performance.md)
4. Gestionar [Infraestructura Cloud](./18-infraestructura-cloud.md)

### Para resolución de problemas

1. Aplicar [Herramientas de Problemas](./11-herramientas-problemas.md)
2. Usar [Mejora Continua](./12-mejora-continua.md)
3. Consultar [Testing](./04-testing.md)
4. Revisar [Observabilidad](./10-observabilidad.md)

---

## 📋 Niveles de Criticidad

| Criticidad | Abrev. | Explicación                                  |
| ---------- | ------ | -------------------------------------------- |
| Crítico    | 🔴     | Incumplimiento = bug de seguridad o caída.   |
| Alto       | 🟠     | Afecta mantenibilidad o rendimiento.         |
| Estilo     | 🟢     | Preferencia de equipo, sin impacto funcional.|

---

## 🤝 Contribuciones

Este documento es vivo y colaborativo:

1. **Proponer mejoras**: Abrir PR con cambios sugeridos
2. **Reportar errores**: Issues con etiqueta `docs`
3. **Agregar ejemplos**: Ejemplos concisos con enlaces
4. **Actualizar herramientas**: Mantener versiones y links actualizados

---

## 📚 Recursos Adicionales

- [Refactoring Guru - Patrones de Diseño](https://refactoring.guru/design-patterns)
- [Martin Fowler - Architecture](https://martinfowler.com/architecture/)
- [OWASP - Security](https://owasp.org/)
- [12 Factor App](https://12factor.net/)
- [Google SRE Book](https://sre.google/books/)

---

**Mantenedores**: David Rolón (<https://github.com/davichuder>)

---

[⬆️ Volver arriba](#00-indice-general) | [➡️ Siguiente: Fundamentos](./01-fundamentos.md)
