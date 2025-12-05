# 20 - Metodologías de Mejora Continua

> Frameworks sistemáticos para optimizar procesos, eliminar desperdicios y mejorar calidad de forma sostenida.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Mejora Continua](#mejora-continua)
- [📊 Six Sigma](#six-sigma)
- [🔄 Kaizen (改善)](#kaizen)
- [🏭 Lean Manufacturing](#lean-manufacturing)
- [🔄 Ciclo PDCA (Plan-Do-Check-Act)](#ciclo-pdca-plan-do-check-act)
- [🧹 5S (5 Eses)](#5s-5-eses)
- [🔧 8D (Eight Disciplines)](#8d-eight-disciplines)
- [📋 Kanban](#kanban)
- [⚙️ MTBF y MTTR](#mtbf-y-mttr)
- [📊 Comparación de Metodologías](#comparacion-de-metodologias)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 Mejora Continua

**What:** Filosofía de optimización incremental constante en procesos y productos.

**Why:** Pequeñas mejoras sostenidas > grandes cambios esporádicos. Cultura de excelencia.

**Who:** Todo el equipo, liderado por management.

**When:** Siempre, como parte de la cultura organizacional.

**How much:** Inversión en tiempo y cambio cultural, ROI acumulativo a largo plazo.

---

## 📊 Six Sigma

**What:** Metodología estadística para reducir defectos a 3.4 por millón de oportunidades.

**Why:** Calidad extrema, reducción de variabilidad, decisiones basadas en datos.

**When:** Procesos con alta variabilidad, manufactura, servicios críticos.

### DMAIC (Metodología Six Sigma)

| Fase | What | How | Herramientas |
|:-----|:-----|:----|:-------------|
| **Define** (Definir) | Identificar problema y objetivo | Project charter, VOC (Voice of Customer) | Diagrama Ishikawa, 5W2H |
| **Measure** (Medir) | Recopilar datos actuales | Métricas baseline, capability analysis | Control charts, histogramas |
| **Analyze** (Analizar) | Encontrar causas raíz | Análisis estadístico, correlaciones | 5 Porqués, Pareto, scatter plots |
| **Improve** (Mejorar) | Implementar soluciones | Pilotos, experimentos | DOE (Design of Experiments) |
| **Control** (Controlar) | Sostener mejoras | SOP, monitoreo continuo | Control charts, auditorías |

**Ejemplo en software:** Reducir bugs en producción
- **Define:** Meta = reducir 50% bugs críticos en 3 meses
- **Measure:** Actual = 20 bugs/mes, 60% en validaciones
- **Analyze:** Causa = falta de validación backend, tests insuficientes
- **Improve:** Implementar validación en 3 capas, aumentar coverage a 85%
- **Control:** Dashboard bugs, alertas si >10/mes

**Niveles de certificación:** Yellow Belt → Green Belt → Black Belt → Master Black Belt

---

## 🔄 Kaizen (改善)

**What:** Filosofía japonesa de "mejora continua" mediante pequeños cambios incrementales.

**Why:** Involucra a todos, cambios pequeños = menos resistencia, mejora sostenida.

**When:** Siempre, como cultura organizacional.

### Principios Kaizen

1. **Buenos procesos = buenos resultados**
2. **Ve y observa (Gemba)** - ir al lugar real
3. **Habla con datos**
4. **Toma acción para contener y corregir causas raíz**
5. **Trabaja en equipo**
6. **Kaizen es de todos**

**Kaizen Event:** Workshop de 3-5 días para mejorar un proceso específico.

**Aplicación en software:**
- Daily standups enfocados en mejoras
- Retrospectivas con acción concreta
- Sugerencias de mejora siempre bienvenidas
- Métricas visibles (dashboards)

**Ejemplo:** Cada sprint, equipo identifica 1 mejora pequeña (automatizar test, mejorar doc, refactor).

---

## 🏭 Lean Manufacturing

**What:** Filosofía de eliminación de desperdicios (Muda) y maximización de valor.

**Why:** Hacer más con menos, enfocarse en lo que agrega valor al cliente.

**When:** Procesos con desperdicio evidente, optimización de flujo.

### 8 Tipos de Desperdicio (DOWNTIME)

| Desperdicio | What | Ejemplo Software |
|:------------|:-----|:-----------------|
| **Defects** | Errores, retrabajos | Bugs, hotfixes |
| **Overproduction** | Producir más de lo necesario | Features no usadas |
| **Waiting** | Tiempo ocioso | Esperar code review, deploys |
| **Non-utilized talent** | No usar habilidades del equipo | Seniors haciendo tareas junior |
| **Transportation** | Movimiento innecesario | Múltiples handoffs entre equipos |
| **Inventory** | Work in progress excesivo | 20 PRs abiertos |
| **Motion** | Movimiento innecesario | Cambiar entre 10 herramientas |
| **Extra processing** | Trabajo que no agrega valor | Documentación que nadie lee |

**Herramientas Lean:**
- **Value Stream Mapping:** Visualizar flujo de valor
- **5S:** Ver abajo
- **Pull System:** Producir solo cuando hay demanda (Kanban)
- **Jidoka:** Autonomation, detectar problemas temprano

---

## 🔄 Ciclo PDCA (Plan-Do-Check-Act)

**What:** Ciclo iterativo de mejora continua (también conocido como Deming Cycle).

**Why:** Estructura para implementar mejoras de forma controlada.

**When:** Implementar cualquier mejora, resolver problemas.

| Fase | What | How | Output |
|:-----|:-----|:----|:-------|
| **Plan** | Identificar oportunidad, planear cambio | Análisis causa raíz, definir objetivo SMART | Plan de acción |
| **Do** | Ejecutar plan en pequeña escala | Piloto, experimento controlado | Datos de prueba |
| **Check** | Medir resultados vs objetivo | Comparar métricas antes/después | Learnings |
| **Act** | Estandarizar si funciona, ajustar si no | Documentar, entrenar, escalar | Nueva baseline |

**Ejemplo:** Reducir tiempo de deploy
- **Plan:** Objetivo = deploy en <5 min (actual: 20 min). Cambio: paralelizar tests
- **Do:** Implementar en 1 repo piloto durante 1 semana
- **Check:** Tiempo promedio = 4.5 min ✅
- **Act:** Aplicar a todos los repos, documentar en runbook

**Diferencia con DMAIC:** PDCA es más simple y rápido, DMAIC más riguroso y estadístico.

---

## 🧹 5S (5 Eses)

**What:** Metodología japonesa para organizar y mantener un espacio de trabajo.

**Why:** Eficiencia, calidad, seguridad mediante orden y limpieza.

**When:** Organizar codebase, repos, herramientas, espacios físicos.

| Fase | Japonés | Español | What | How (Software) |
|:-----|:--------|:--------|:-----|:---------------|
| **1** | Seiri | **Clasificar** | Separar necesario de innecesario | Borrar código muerto, deps sin usar |
| **2** | Seiton | **Ordenar** | Un lugar para cada cosa | Estructura de carpetas lógica, naming conventions |
| **3** | Seiso | **Limpiar** | Mantener limpio | Formateo automático, linting, refactoring |
| **4** | Seiketsu | **Estandarizar** | Crear estándares | Style guides, templates, convenciones |
| **5** | Shitsuke | **Sostener** | Disciplina para mantener | Code reviews, auditorías, cultura |

**Beneficios en software:**
- Onboarding más rápido
- Menos bugs por confusión
- Búsqueda más eficiente
- Mantenimiento simplificado

---

## 🔧 8D (Eight Disciplines)

**What:** Metodología de 8 pasos para resolver problemas complejos en equipo.

**Why:** Enfoque estructurado que asegura solución definitiva.

**When:** Problemas críticos recurrentes, post-mortems importantes.

| Disciplina | What | Output |
|:-----------|:-----|:-------|
| **D0** | Preparar | Reconocer problema, decidir usar 8D |
| **D1** | Formar equipo | Equipo multifuncional con conocimiento relevante |
| **D2** | Describir problema | Descripción detallada con datos (5W2H) |
| **D3** | Contención | Acción inmediata para proteger cliente |
| **D4** | Causa raíz | Identificar todas las causas (5 Porqués, Ishikawa) |
| **D5** | Solución permanente | Elegir e implementar correcciones |
| **D6** | Implementar | Validar efectividad, eliminar causa raíz |
| **D7** | Prevenir recurrencia | Actualizar procesos, entrenar |
| **D8** | Felicitar equipo | Reconocer contribuciones, celebrar |

**Ejemplo - Outage en producción:**
- **D1:** Equipo: 2 devs, 1 SRE, 1 PM
- **D2:** Outage 45 min, afectó 10k usuarios, pérdida $5k
- **D3:** Rollback inmediato, comunicar a clientes
- **D4:** Causa raíz: migration sin rollback plan
- **D5:** Solución: añadir rollback automático, staging obligatorio
- **D6:** Implementado, testeado en staging
- **D7:** Checklist pre-deploy actualizado, training equipo
- **D8:** Shoutout en all-hands, mejora documentada

---

## 📋 Kanban

**What:** Sistema visual de gestión de flujo basado en pull.

**Why:** Visualizar trabajo, limitar WIP, optimizar throughput.

**When:** Gestión de tareas, workflow continuo sin sprints.

### Principios Kanban

1. **Visualizar trabajo:** Tablero con columnas (To Do, In Progress, Done)
2. **Limitar WIP:** Máximo X tareas en progreso simultáneamente
3. **Gestionar flujo:** Medir tiempo por columna, eliminar cuellos de botella
4. **Hacer políticas explícitas:** Definition of Done claro
5. **Feedback loops:** Retrospectivas, métricas
6. **Mejorar colaborativamente:** Kaizen

**Métricas Kanban:**
- **Lead Time:** Tiempo desde request hasta entrega
- **Cycle Time:** Tiempo desde inicio hasta completado
- **Throughput:** Items completados por periodo
- **WIP:** Work In Progress actual

**Herramientas:** [Jira](https://www.atlassian.com/software/jira), [Trello](https://trello.com/), [Azure Boards](https://azure.microsoft.com/en-us/products/devops/boards)

---

## ⚙️ MTBF y MTTR

**What:** Métricas de confiabilidad y mantenibilidad de sistemas.

| Métrica | What | Fórmula | Objetivo |
|:--------|:-----|:--------|:---------|
| **MTBF** (Mean Time Between Failures) | Tiempo promedio entre fallos | Tiempo operativo / # de fallos | ↑ Maximizar |
| **MTTR** (Mean Time To Repair) | Tiempo promedio para reparar | Tiempo downtime / # de incidents | ↓ Minimizar |
| **MTTF** (Mean Time To Failure) | Tiempo hasta primer fallo | - | ↑ Maximizar |
| **MTTA** (Mean Time To Acknowledge) | Tiempo hasta reconocer incident | - | ↓ Minimizar |

**Ejemplo:**
- Sistema operó 720 horas en un mes
- Tuvo 3 fallos de 2h, 1h, 3h
- **MTBF** = 720 / 3 = 240 horas
- **MTTR** = (2+1+3) / 3 = 2 horas

**Cómo mejorar:**
- **MTBF:** Mejor testing, code reviews, monitoring
- **MTTR:** Runbooks, alertas, rollback automático

---

## 📊 Comparación de Metodologías

| Metodología | Enfoque | Duración | Complejidad | Mejor Para |
|:------------|:--------|:---------|:------------|:-----------|
| **Six Sigma** | Reducir variabilidad | 3-6 meses | Alta | Procesos críticos, manufactura |
| **Kaizen** | Mejora incremental | Continuo | Baja | Cultura diaria |
| **Lean** | Eliminar desperdicio | Continuo | Media | Optimizar flujo |
| **PDCA** | Ciclo mejora | 1-4 semanas | Baja | Cualquier mejora |
| **5S** | Organización | 1-2 semanas | Baja | Workspace, codebase |
| **8D** | Resolución problemas | 2-8 semanas | Alta | Problemas complejos |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Mejora sin métricas** | No saber si funcionó | Definir baseline y target |
| **Iniciativas sin seguimiento** | Se abandonan | Ownership claro, reviews periódicas |
| **Cambios enormes** | Alta resistencia | Pequeños cambios incrementales |
| **Blame culture** | Miedo a reportar problemas | Blameless post-mortems |
| **Documentar sin aplicar** | Trabajo en vano | Implementar y auditar |

---

## 📚 Recursos

- [The Lean Startup - Eric Ries](http://theleanstartup.com/)
- [Kaizen Institute](https://www.kaizen.com/)
- [iSixSigma](https://www.isixsigma.com/)
- [Toyota Production System](https://global.toyota/en/company/vision-and-philosophy/production-system/)

---

[⬅️ Anterior: Herramientas de Problemas](./19-herramientas-problemas.md) | [⬆️ Volver arriba](#20-metodologias-de-mejora-continua) | [➡️ Siguiente: Análisis Estratégico](./21-analisis-estrategico.md)