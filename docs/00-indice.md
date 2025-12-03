# 00 - Indice General

> Documento vivo de estándares, buenas prácticas y decisiones técnicas del equipo.
>
> Si encontrás una mejora, ¡actualizalo!
>
> Última actualización: `YYYY-MM-DD`

---

## 📋 Índice Rápido

- [📖 Índice General](#indice-general)
- [🎯 Cómo usar esta guía](#como-usar-esta-guia)
- [📋 Niveles de Criticidad](#niveles-de-criticidad)
- [🤝 Contribuciones](#contribuciones)
- [📚 Recursos Adicionales](#recursos-adicionales)
---

## 📖 Índice General

### 🎯 Fundamentos
- [01 - Fundamentos](./01-fundamentos.md)
  - Niveles de criticidad
  - Reglas generales de código
  - Reglas por lenguaje
  - Reglas por framework

### 🔬 Desarrollo y Testing
- [02 - Disciplinas de Desarrollo](./02-disciplinas-desarrollo.md)
  - TDD, BDD, ATDD, DDD, FDD, MDD, PBT
- [03 - Testing](./03-testing.md)
  - Backend, Frontend, Mobile, Performance, Testing Avanzado

### 🏗️ Arquitectura y Diseño
- [04 - Arquitectura y Patrones](./04-arquitectura-patrones.md)
  - Arquitecturas de software
  - Patrones de diseño
  - Patrones arquitectónicos avanzados
  - FSM (Finite State Machines)

### 🚀 Operaciones
- [05 - DevOps](./05-devops.md)
  - CI/CD, IaC, Contenedores, Patrones de despliegue
- [06 - Seguridad](./06-seguridad.md)
  - Principios de seguridad, Herramientas, Patrones avanzados
- [07 - Observabilidad y Telemetría](./07-observabilidad.md)
  - Logging, Metrics, Tracing, APM, Alerting, Health checks
- [08 - Optimización de Performance](./08-performance.md)
  - Optimización de DB, Frontend, Backend, Caching

### 💾 Datos y APIs
- [09 - Bases de Datos](./09-bases-datos.md)
  - SQL, NoSQL, Time Series, Graph, Columnar, In-memory
- [10 - APIs y Protocolos](./10-apis-protocolos.md)
  - REST, GraphQL, gRPC, WebSockets, Event-Driven
  - Documentación por protocolo
  - Patrones de comunicación

### 📱 Interfaces y Experiencia
- [11 - Mobile, UI y UX](./11-mobile-ui-ux.md)
  - Desarrollo móvil, UI, UX, Accesibilidad

### ☁️ Infraestructura
- [12 - Infraestructura y Cloud](./12-infraestructura-cloud.md)
  - Multi-cloud, Serverless, Containerization, Edge computing

### 🤖 Datos Avanzados
- [13 - Machine Learning y Deep Learning](./13-machine-learning.md)
  - ML supervisado/no supervisado, DL, MLOps, NLP, RL
- [14 - Ciencia de Datos](./14-ciencia-datos.md)
  - Limpieza, Visualización, Reproducibilidad, Modelado

### ✅ Calidad y Gestión
- [15 - Gestión de Calidad](./15-gestion-calidad.md)
  - Code coverage, Static analysis, Linting, Peer review

### 🛠️ Resolución de Problemas y Mejora
- [16 - Herramientas de Solución de Problemas](./16-herramientas-problemas.md)
  - Ishikawa, 5 Porqués, Pareto, FTA, 5W2H, Lluvia de ideas
- [17 - Metodologías de Mejora Continua](./17-mejora-continua.md)
  - Six Sigma, Kaizen, Lean, PDCA, 5S, 8D, Kanban, MTBF

### 📊 Estrategia y Negocio
- [18 - Análisis Estratégico](./18-analisis-estrategico.md)
  - FODA, PESTEL, Porter, VRIO, CAME, Buyer Persona, ICP
- [19 - Product Management](./19-product-management.md)
  - JTBD, User Story Mapping, OKRs, North Star Metric
- [20 - Métricas y KPIs](./20-metricas-kpis.md)
  - HEART, AARRR, DORA, NPS, SLIs/SLOs/SLAs

### 👥 Cultura y Colaboración
- [21 - Colaboración y Cultura](./21-colaboracion-cultura.md)
  - Pair Programming, Code Review, Postmortems, Escalation
- [22 - Optimización de Costos](./22-cost-optimization.md)
  - FinOps, Right-sizing, Reserved Instances, Cloud cost monitoring
- [23 - Data Governance](./23-data-governance.md)
  - Data Lineage, Data Quality, MDM, Privacy by Design

### 📝 Documentación y Convenciones
- [24 - Documentación y Diagramas](./24-documentacion-diagramas.md)
  - Markdown, Mermaid, LaTeX, PlantUML, C4, ER, UML
  - Tipos de diagramas: flujo, secuencia, clases, estado
- [25 - Convenciones](./25-convenciones.md)
  - Nomenclatura, Git/GitOps, i18n/l10n, Configuración, Dependencias

### 🎓 Onboarding y Criterios
- [26 - Onboarding](./26-onboarding.md)
  - Guía de inicio, Arquitectura, Primer PR
- [27 - Checklist de Producción](./27-checklist-produccion.md)
  - Validaciones pre-deploy
- [28 - Sesgos Cognitivos, Falacias y Leyes](./28-sesgos-falacias.md)
  - Sesgos cognitivos, Falacias lógicas, Leyes paradójicas, Efectos psicológicos


### 🤖 AI y Automatización
- [29 - Prompts y Agentes de IA](./29-prompts-agentes.md)
  - The Gentleman (agente principal), Agentes especializados, Prompt engineering
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
2. Leer [Disciplinas de Desarrollo](./02-disciplinas-desarrollo.md)
3. Consultar [Onboarding](./26-onboarding.md)
4. Revisar convenciones del lenguaje/framework que usarás

### Para arquitectos
1. Revisar [Arquitectura y Patrones](./04-arquitectura-patrones.md)
2. Consultar [Infraestructura y Cloud](./12-infraestructura-cloud.md)
3. Validar contra [Seguridad](./06-seguridad.md)
4. Implementar [Observabilidad](./07-observabilidad.md)

### Para product managers
1. Estudiar [Product Management](./19-product-management.md)
2. Definir [Métricas y KPIs](./20-metricas-kpis.md)
3. Usar [Análisis Estratégico](./18-analisis-estrategico.md)
4. Aplicar [Herramientas de Problemas](./16-herramientas-problemas.md)

### Para DevOps/SRE
1. Implementar [DevOps](./05-devops.md)
2. Configurar [Observabilidad](./07-observabilidad.md)
3. Optimizar [Performance](./08-performance.md)
4. Gestionar [Infraestructura Cloud](./12-infraestructura-cloud.md)

### Para resolución de problemas
1. Aplicar [Herramientas de Problemas](./16-herramientas-problemas.md)
2. Usar [Mejora Continua](./17-mejora-continua.md)
3. Consultar [Testing](./03-testing.md)
4. Revisar [Observabilidad](./07-observabilidad.md)

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

**Mantenedores**: David Rolón (https://github.com/davichuder)