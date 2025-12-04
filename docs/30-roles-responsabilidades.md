# 30 - Roles y Responsabilidades

> Definición clara de roles en equipos de software, responsabilidades, skills requeridos e interacciones clave.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎭 Introducción](#introduccion)
- [👨‍💻 Roles Técnicos](#roles-tecnicos)
- [📊 Roles de Producto y Negocio](#roles-de-producto-y-negocio)
- [🧪 Roles de Calidad](#roles-de-calidad)
- [🔧 Roles de Operaciones](#roles-de-operaciones)
- [📊 Roles de Datos](#roles-de-datos)
- [📋 Artefactos](#artefactos)

---

## 🎭 Introducción

**What:** Definición de roles, responsabilidades y cómo interactúan en equipos de software modernos.

**Why:** Claridad en roles evita overlaps, gaps y conflictos. Equipos que escalan necesitan roles bien definidos.

**How:** Definir responsabilidades, skills requeridos, interacciones clave y anti-patterns comunes para cada rol.

---

## 👨‍💻 Roles Técnicos

### Tech Lead

**Responsabilidades:**
- Decisiones técnicas de alto nivel (arquitectura, stack, patterns)
- Mentoring técnico del equipo
- Code reviews críticos
- Unblocking técnico
- Balance entre deuda técnica y features

**Skills requeridos:**
- 🔴 Expertise técnico profundo en el stack del equipo
- 🔴 Capacidad de tomar decisiones arquitectónicas
- 🟠 Comunicación técnica efectiva
- 🟠 Mentoring y coaching

**Interacciones clave:**
- Con Engineering Manager: Alineación en prioridades técnicas vs negocio
- Con Product Manager: Traducir requisitos a soluciones técnicas
- Con equipo: Guiar, desbloquear, revisar código

**Anti-patterns:**
- ❌ Convertirse en bottleneck (revisar todo el código)
- ❌ Tomar todas las decisiones sin involucrar al equipo
- ❌ Escribir todo el código crítico personalmente

---

### Engineering Manager (EM)

**Responsabilidades:**
- Gestión de personas (1-on-1s, performance reviews, career development)
- Hiring y onboarding
- Remover impedimentos organizacionales
- Alineación entre equipos
- Métricas de equipo (velocity, quality, happiness)

**Skills requeridos:**
- 🔴 People management
- 🔴 Comunicación y negociación
- 🟠 Background técnico (no necesita ser el más senior)
- 🟠 Gestión de conflictos

**Interacciones clave:**
- Con Tech Lead: Complementarse (EM → people, Tech Lead → tech)
- Con Product Manager: Alineación en roadmap y capacidad
- Con equipo: 1-on-1s, feedback, desarrollo de carrera

**Anti-patterns:**
- ❌ Micromanagement
- ❌ No delegar decisiones técnicas al Tech Lead
- ❌ Ignorar señales de burnout o conflictos

---

### Software Architect

**Responsabilidades:**
- Diseño de arquitectura de sistemas complejos
- ADRs (Architecture Decision Records)
- Evaluación de trade-offs arquitectónicos
- Definir estándares y patterns
- Architectural reviews

**Skills requeridos:**
- 🔴 Conocimiento profundo de patterns arquitectónicos
- 🔴 Experiencia en sistemas distribuidos
- 🟠 Comunicación (explicar decisiones complejas)
- 🟠 Visión de negocio (arquitectura alineada a objetivos)

**Interacciones clave:**
- Con Tech Leads: Alineación en decisiones arquitectónicas
- Con Product: Entender requisitos no funcionales (escalabilidad, performance)
- Con equipos: Evangelizar arquitectura, revisar implementaciones

**Anti-patterns:**
- ❌ Ivory tower architect (diseñar sin implementar)
- ❌ Over-engineering
- ❌ No documentar decisiones (ADRs)

---

### Frontend Developer

**Responsabilidades:**
- Implementar UI/UX
- Optimización de performance frontend
- Accesibilidad (WCAG)
- Integración con APIs
- Testing de componentes

**Skills requeridos:**
- 🔴 HTML, CSS, JavaScript/TypeScript
- 🔴 Framework moderno (React, Angular, Vue)
- 🟠 Design systems y component libraries
- 🟠 Performance optimization (lazy loading, code splitting)

**Especialización vs Generalización:**
- **Especialista**: Experto en un framework, performance, accesibilidad
- **Generalista (Full-Stack)**: Puede hacer frontend + backend, menos profundidad

---

### Backend Developer

**Responsabilidades:**
- Diseño e implementación de APIs
- Lógica de negocio
- Integración con bases de datos
- Performance y escalabilidad backend
- Testing (unit, integration)

**Skills requeridos:**
- 🔴 Lenguaje backend (Java, Python, Node.js, etc.)
- 🔴 Frameworks (Spring, FastAPI, Express, Django)
- 🟠 Bases de datos (SQL, NoSQL)
- 🟠 Arquitectura de microservicios

**Especialización vs Generalización:**
- **Especialista**: Experto en un stack, performance, arquitectura distribuida
- **Generalista (Full-Stack)**: Puede hacer backend + frontend, menos profundidad

---

### Full-Stack Developer

**Responsabilidades:**
- Implementar features end-to-end (frontend + backend)
- Integración completa (UI → API → DB)
- Versatilidad en diferentes capas

**Trade-offs:**
- ✅ **Ventajas**: Autonomía, visión completa, menos handoffs
- ❌ **Desventajas**: Menos profundidad en cada área, riesgo de ser "jack of all trades, master of none"

**Cuándo usar:**
- Equipos pequeños o startups
- Features end-to-end con poco acoplamiento
- Cuando la velocidad es más importante que la especialización

---

## 📊 Roles de Producto y Negocio

### Product Manager (PM)

**Responsabilidades:**
- Visión y estrategia de producto
- Roadmap de producto
- Priorización de features (RICE, MoSCoW)
- Análisis de mercado y competencia
- Métricas de producto (adoption, retention, NPS)

**Skills requeridos:**
- 🔴 Product strategy
- 🔴 Data-driven decision making
- 🟠 Comunicación con stakeholders
- 🟠 Understanding técnico (no necesita codear)

**PM vs PO:**
- **PM**: Estrategia, visión, mercado, roadmap de largo plazo
- **PO**: Ejecución, backlog, user stories, priorización táctica

---

### Product Owner (PO)

**Responsabilidades:**
- Gestión de backlog
- Definir user stories y acceptance criteria
- Priorización sprint a sprint
- Clarificar requisitos al equipo
- Aceptar o rechazar features implementadas

**Skills requeridos:**
- 🔴 Conocimiento del dominio de negocio
- 🔴 Escribir user stories efectivas
- 🟠 Comunicación con equipo técnico
- 🟠 Priorización táctica

**PO vs PM:**
- **PO**: Táctico, día a día, backlog, sprint planning
- **PM**: Estratégico, visión, roadmap, mercado

---

## 🧪 Roles de Calidad

### QA Engineer (Manual)

**Responsabilidades:**
- Testing manual exploratorio
- Validación de acceptance criteria
- Reportar bugs con reproducción clara
- Testing de regresión manual
- Validación de UX/UI

**Skills requeridos:**
- 🔴 Pensamiento crítico y atención al detalle
- 🔴 Conocimiento del dominio de negocio
- 🟠 Comunicación (reportar bugs claros)
- 🟠 Nociones de SQL (para validar datos)

---

### QA Automation Engineer

**Responsabilidades:**
- Automatizar test cases
- Mantener suites de tests automatizados
- Integrar tests en CI/CD
- Reducir testing manual repetitivo

**Skills requeridos:**
- 🔴 Programación (Python, JavaScript, Java)
- 🔴 Frameworks de testing (Selenium, Cypress, Playwright)
- 🟠 CI/CD (GitHub Actions, Jenkins)
- 🟠 Page Object Model y patterns de testing

---

### SDET (Software Development Engineer in Test)

**Responsabilidades:**
- Desarrollar frameworks de testing custom
- Tooling para testing (mocks, test data generators)
- Performance testing (JMeter, k6)
- Testing de infraestructura (chaos engineering)

**Skills requeridos:**
- 🔴 Desarrollo de software (igual que un developer)
- 🔴 Expertise en testing (unit, integration, E2E, performance)
- 🟠 Arquitectura de sistemas de testing
- 🟠 Observability y debugging

**QA vs QA Automation vs SDET:**
- **QA**: Manual, exploratorio, validación de UX
- **QA Automation**: Automatiza tests existentes, mantiene suites
- **SDET**: Desarrolla frameworks, tooling, testing avanzado

---

## 🔧 Roles de Operaciones

### DevOps Engineer

**Responsabilidades:**
- CI/CD pipelines
- Automatización de deployments
- IaC (Terraform, CloudFormation)
- Monitoring y alerting
- Colaboración entre Dev y Ops

**Skills requeridos:**
- 🔴 Scripting (Bash, Python)
- 🔴 CI/CD (GitHub Actions, GitLab CI, Jenkins)
- 🟠 Cloud (AWS, Azure, GCP)
- 🟠 Containers (Docker, Kubernetes)

---

### SRE (Site Reliability Engineer)

**Responsabilidades:**
- Garantizar reliability (SLIs, SLOs, SLAs)
- Incident response y on-call
- Post-mortems y RCA
- Toil reduction (automatización)
- Capacity planning

**Skills requeridos:**
- 🔴 Desarrollo de software (50% coding)
- 🔴 Operaciones (monitoring, alerting, incident response)
- 🟠 Distributed systems
- 🟠 Performance tuning

**DevOps vs SRE:**
- **DevOps**: Cultura, automatización, CI/CD, colaboración Dev-Ops
- **SRE**: Reliability, SLOs, incident response, on-call, toil reduction

---

### Platform Engineer

**Responsabilidades:**
- Construir plataformas internas (developer experience)
- Self-service tooling (deploy, monitoring, logs)
- Abstracciones sobre cloud (internal PaaS)
- Developer productivity

**Skills requeridos:**
- 🔴 Desarrollo de software
- 🔴 Cloud y Kubernetes
- 🟠 Product thinking (internal customers = developers)
- 🟠 APIs y abstracciones

**Platform vs DevOps vs SRE:**
- **Platform**: Construir herramientas para developers (internal products)
- **DevOps**: Automatización, CI/CD, cultura
- **SRE**: Reliability, incident response

---

## 📊 Roles de Datos

### Data Engineer

**Responsabilidades:**
- Construir data pipelines (ETL/ELT)
- Data warehousing (Snowflake, BigQuery, Redshift)
- Data quality y validación
- Optimización de queries y performance

**Skills requeridos:**
- 🔴 SQL avanzado
- 🔴 Python (pandas, PySpark)
- 🟠 Cloud data tools (Airflow, dbt, Fivetran)
- 🟠 Distributed computing (Spark)

---

### Data Scientist

**Responsabilidades:**
- Análisis exploratorio (EDA)
- Feature engineering
- Modelado estadístico y ML
- Experimentos y A/B testing
- Comunicar insights a stakeholders

**Skills requeridos:**
- 🔴 Estadística y matemáticas
- 🔴 Python (pandas, scikit-learn, matplotlib)
- 🟠 ML frameworks (TensorFlow, PyTorch)
- 🟠 Storytelling con datos

---

### ML Engineer

**Responsabilidades:**
- Deployment de modelos ML a producción
- MLOps (versionado, monitoring, retraining)
- Optimización de modelos (latency, throughput)
- Feature stores y serving infrastructure

**Skills requeridos:**
- 🔴 Software engineering
- 🔴 ML frameworks (TensorFlow, PyTorch)
- 🟠 MLOps tools (MLflow, Kubeflow, SageMaker)
- 🟠 Distributed systems

**Data Engineer vs Data Scientist vs ML Engineer:**
- **Data Engineer**: Pipelines, infraestructura de datos, ETL
- **Data Scientist**: Análisis, modelado, experimentos, insights
- **ML Engineer**: Deployment, MLOps, productionización de modelos

---

## 📋 Artefactos

### RACI Matrix Template

Matriz para definir responsabilidades en proyectos:

| Tarea / Decisión | Tech Lead | EM | PM | Frontend | Backend | QA |
|:-----------------|:---------:|:--:|:--:|:--------:|:-------:|:--:|
| Decisión arquitectónica | **A** | C | I | C | C | I |
| Priorización de features | C | C | **A** | I | I | I |
| Code review | **R** | I | I | R | R | I |
| Hiring técnico | C | **A** | I | I | I | I |
| Definir acceptance criteria | I | I | **A** | C | C | R |
| Incident response | C | I | I | R | **R** | I |

**Leyenda:**
- **R** (Responsible): Ejecuta la tarea
- **A** (Accountable): Responsable final, toma la decisión
- **C** (Consulted): Se le consulta antes de decidir
- **I** (Informed): Se le informa después de decidir

---

### Role Definition Card Template

```markdown
## [Nombre del Rol]

**Responsabilidades principales:**
1. [Responsabilidad 1]
2. [Responsabilidad 2]
3. [Responsabilidad 3]

**Skills requeridos:**
- 🔴 [Skill crítico 1]
- 🔴 [Skill crítico 2]
- 🟠 [Skill importante 1]
- 🟢 [Skill deseable 1]

**Interacciones clave:**
- Con [Rol X]: [Tipo de interacción]
- Con [Rol Y]: [Tipo de interacción]

**Anti-patterns comunes:**
- ❌ [Anti-pattern 1]
- ❌ [Anti-pattern 2]

**Métricas de éxito:**
- [Métrica 1]
- [Métrica 2]
```

---

### Team Topology Canvas

Basado en el libro "Team Topologies" de Matthew Skelton y Manuel Pais.

**Tipos de equipos:**

| Tipo | Propósito | Ejemplos |
|:-----|:----------|:---------|
| **Stream-Aligned** | Entregar valor end-to-end para un flujo de negocio | Equipo de Checkout, Equipo de Payments |
| **Enabling** | Ayudar a otros equipos a adoptar nuevas tecnologías | Platform Adoption Team, Security Champions |
| **Complicated Subsystem** | Construir y mantener subsistemas complejos | ML Platform Team, Video Processing Team |
| **Platform** | Proveer servicios internos (internal products) | Cloud Platform Team, Data Platform Team |

**Modos de interacción:**

| Modo | Descripción | Cuándo usar |
|:-----|:------------|:------------|
| **Collaboration** | Dos equipos trabajan juntos temporalmente | Adopción de nueva tecnología, migración compleja |
| **X-as-a-Service** | Un equipo consume servicios de otro | Platform team provee APIs a stream-aligned teams |
| **Facilitating** | Un equipo ayuda a otro a mejorar capacidades | Enabling team ayuda a adoptar nuevas prácticas |

---

## 📚 Recursos

- [Team Topologies - Matthew Skelton & Manuel Pais](https://teamtopologies.com/)
- [The Manager's Path - Camille Fournier](https://www.oreilly.com/library/view/the-managers-path/9781491973882/)
- [Staff Engineer - Will Larson](https://staffeng.com/)
- [Google SRE Book](https://sre.google/books/)

---

[⬅️ Anterior: Prompts y Agentes](./29-prompts-agentes.md) | [➡️ Siguiente: Estrategia de IA](./31-estrategia-ia-automatizacion.md) | [⬆️ Volver arriba](#30-roles-y-responsabilidades)
