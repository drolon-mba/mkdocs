# 11 - Herramientas de Análisis de Problemas

> Técnicas estructuradas para identificar causas raíz, analizar problemas y encontrar soluciones efectivas.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🌳 Issue Trees (Árbol de Problemas)](#issue-trees-arbol-de-problemas)
- [🔍 MECE Principle](#mece-principle)
- [✅ Phoenix Checklist](#phoenix-checklist)
- [⚠️ AMFE (Análisis de Modos de Fallo y Efectos)](#amfe-analisis-de-modos-de-fallo-y-efectos)
- [🎯 ¿Por qué usar herramientas estructuradas?](#por-que-usar-herramientas-estructuradas)
- [🐟 Diagrama de Ishikawa (Espina de Pescado)](#diagrama-de-ishikawa-espina-de-pescado)
- [❓ 5 Porqués](#5-porques)
- [📊 Diagrama de Pareto (Regla 80/20)](#diagrama-de-pareto-regla-8020)
- [💡 Lluvia de Ideas (Brainstorming)](#lluvia-de-ideas-brainstorming)
- [🌳 Árbol Lógico de Fallos (FTA)](#arbol-logico-de-fallos-fta-fault-tree-analysis)
- [📈 Diagrama de Flujo](#diagrama-de-flujo)
- [🔍 5W2H](#5w2h)
- [🔄 PDCA (Plan-Do-Check-Act)](#pdca-plan-do-check-act)
- [🎯 Matriz de Decisión](#matriz-de-decision)
- [🚫 Errores Comunes](#errores-comunes)
- [📚 Recursos](#recursos)

---

## 🌳 Issue Trees (Árbol de Problemas)

**What:** Descomposición estructurada de problema en sub-problemas mutuamente excluyentes.

**Why:** Evitar análisis caótico, asegurar exhaustividad, priorizar mejor.

**When:** Problemas complejos, consultancy, análisis de causa raíz.

**Where:** Whiteboards, Miro, papel.

**How:**
1. Definir problema en la raíz (root)
2. Descomponer en categorías MECE (ver abajo)
3. Sub-dividir cada categoría hasta llegar a causas accionables
4. Priorizar ramas por impacto/factibilidad

**Ejemplo - "Performance del sistema es lenta":**
```
           [Performance Lenta]
                  |
      ┌──────────┼──────────┐
      |          |          |
  [Backend]  [Frontend]  [Network]
      |          |          |
  ┌───┼───┐  ┌──┼──┐   ┌───┼───┐
  |   |   |  |  |  |   |   |   |
 DB  API Code CSS JS HTML CDN Latency Bandwidth
```

**Reglas:**
- Cada nivel debe ser MECE (Mutually Exclusive, Collectively Exhaustive)
- Profundizar solo ramas relevantes
- Usar datos para priorizar ramas

**Diferencia con Ishikawa:** Issue Tree es más estructurado y cuantificable, Ishikawa es brainstorming.

---

## 🔍 MECE Principle

**What:** Mutually Exclusive, Collectively Exhaustive (Mutuamente Excluyente, Colectivamente Exhaustivo).

**Why:** Evitar overlaps y gaps en análisis, claridad en categorización.

**When:** Segmentar mercados, organizar análisis, estructurar presentaciones.

**Reglas:**
- **Mutually Exclusive:** Sin overlap entre categorías
- **Collectively Exhaustive:** Cubre todos los casos posibles

**Ejemplo - Segmentar usuarios:**

❌ **No MECE:**
- Usuarios nuevos
- Usuarios pagos
- Usuarios activos
(Problema: Un usuario puede ser nuevo Y pago Y activo = overlap)

✅ **MECE:**
- Por antigüedad: Nuevo (< 30 días) / Establecido (≥ 30 días)
- Por pago: Free / Pago
- Por actividad: Activo (login última semana) / Inactivo

**Frameworks MECE comunes:**
- Tiempo: Pasado / Presente / Futuro
- Geográfico: Region A / Region B / Region C
- Tipo de cliente: B2B / B2C
- Funnel: Awareness / Consideration / Purchase / Retention

---

## ✅ Phoenix Checklist

**What:** Lista de preguntas desarrollada por la CIA para resolver problemas complejos.

**Why:** Fuerza pensar desde múltiples ángulos, evita soluciones superficiales.

**When:** Problemas críticos, decisiones estratégicas, brainstorming estructurado.

**Categorías de Preguntas:**

### 1. El Problema
- ¿Por qué es necesario resolver este problema?
- ¿Cuáles son los beneficios de resolverlo?
- ¿Qué pasa si no lo resolvemos?
- ¿Quién decide si está resuelto?

### 2. Definición
- ¿Cómo lo explicarías a un niño de 10 años?
- ¿Qué palabras clave describen el problema?
- ¿Qué analogías aplican?
- ¿Puedes dibujarlo?

### 3. Soluciones
- ¿Cómo lo resolverían expertos de otros campos?
- ¿Qué haría [persona admirable]?
- ¿Y si tuvieras recursos ilimitados?
- ¿Y si tuvieras que resolver en 1 hora?
- ¿Cuál es la solución opuesta/inversa?

### 4. Plan
- ¿Qué información necesitas?
- ¿Qué no sabes que necesitas saber?
- ¿Dónde está la información?
- ¿Qué asunciones estás haciendo?

### 5. Revisión
- ¿Hay un patrón en soluciones anteriores?
- ¿Qué puedes generalizar?
- ¿Cómo esto se relaciona con otros problemas?
- ¿Qué aprendiste?

**Ejemplo de uso:**
Problema: "Churn alto de usuarios"
- **Definición:** "Usuarios dejan de usar el producto después de 2 meses"
- **Analogía:** "Como un gimnasio donde la gente paga pero no va"
- **¿Qué haría Netflix?** Personalización, contenido constante, recordatorios
- **Solución inversa:** En vez de retener, ¿y si hacemos más fácil volver?

---

## ⚠️ AMFE (Análisis de Modos de Fallo y Efectos)

**What:** Método sistemático para identificar fallos potenciales y su impacto.

**Why:** Prevención proactiva, priorizar riesgos por severidad.

**When:** Diseño de sistemas críticos, nuevas features riesgosas, compliance.

**Componentes:**

| Componente | What | Escala |
|:-----------|:-----|:-------|
| **Modo de Fallo** | ¿Cómo puede fallar? | N/A |
| **Efecto** | ¿Qué pasa si falla? | N/A |
| **Severidad (S)** | Impacto del fallo | 1-10 (10=catastrófico) |
| **Ocurrencia (O)** | Probabilidad | 1-10 (10=muy frecuente) |
| **Detección (D)** | ¿Qué tan difícil detectar? | 1-10 (10=imposible detectar) |
| **RPN** | Risk Priority Number | S × O × D |

**Proceso:**
1. Identificar componente/proceso
2. Listar modos de fallo posibles
3. Analizar efectos
4. Calcular RPN
5. Priorizar acciones para RPN > 100

**Ejemplo - Sistema de pagos:**

| Modo Fallo | Efecto | S | O | D | RPN | Acción |
|:-----------|:-------|:--|:--|:--|:----|:-------|
| DB caída | No se procesan pagos | 9 | 2 | 2 | 36 | Redundancia DB |
| API timeout | Usuario ve error | 5 | 6 | 3 | 90 | Retry logic + circuit breaker |
| Doble cobro | Usuario cobra 2x | 10 | 4 | 7 | 280 🔴 | **Idempotency keys obligatorios** |
| Webhook falla | Merchant no notificado | 8 | 5 | 4 | 160 🔴 | **Queue + retry exponencial** |

**Acciones según RPN:**
- **> 200:** Crítico, actuar inmediatamente
- **100-200:** Alto riesgo, priorizar
- **< 100:** Monitorear

**Herramientas:** Excel, Google Sheets, software específico FMEA.

---

## 🎯 ¿Por qué usar herramientas estructuradas?

**What:** Frameworks probados para resolver problemas de forma sistemática.

**Why:** Evitar soluciones superficiales (tratar síntomas en vez de causas), tomar decisiones basadas en datos.

**Who:** Todo el equipo - developers, PMs, QAs, managers.

**When:** Cuando hay un problema recurrente, incident post-mortem, planning de features.

**How much:** Inversión 30min-2h por sesión, previene semanas de trabajo en dirección incorrecta.

---

## 🐟 Diagrama de Ishikawa (Espina de Pescado)

**What:** Diagrama causa-efecto que identifica múltiples causas potenciales de un problema.

**Why:** Visualiza relaciones entre causas y efecto, pensamiento estructurado.

**When:** Problemas complejos con múltiples causas posibles, post-mortems.

**Where:** Whiteboards, Miro, FigJam, papel.

**How:** 
1. Dibujar línea horizontal (espina) con problema en la derecha
2. Dibujar espinas principales (categorías): Personas, Procesos, Tecnología, Ambiente, Métodos, Materiales
3. Para cada categoría, hacer brainstorming de causas
4. Agregar sub-causas (espinas secundarias)
5. Analizar e investigar causas más probables

**Ejemplo:**
```
              Personas          Procesos
                 |                 |
                 |                 |
        ---------+-----------------+--------- [Bug en Producción]
                 |                 |
                 |                 |
            Tecnología         Ambiente
```

**Caso de uso real:** Sistema lento en producción
- **Personas:** Falta capacitación en optimización, equipo nuevo
- **Procesos:** Sin code review de performance, no hay load testing
- **Tecnología:** DB sin índices, queries N+1, instancias pequeñas
- **Ambiente:** Alto tráfico inesperado, región lejana de usuarios

---

## ❓ 5 Porqués

**What:** Preguntar "¿Por qué?" 5 veces consecutivas para llegar a la causa raíz.

**Why:** Profundizar más allá del síntoma obvio.

**When:** Problemas con causa no clara, post-mortems, retrospectivas.

**How:**
1. Definir problema claramente
2. Preguntar "¿Por qué ocurrió?"
3. Responder basándose en hechos
4. Preguntar "¿Por qué?" a esa respuesta
5. Repetir hasta llegar a causa raíz (típicamente 5 veces)

**Ejemplo - Deploy fallido:**
1. **Problema:** Deploy a producción falló
2. **¿Por qué?** → Tests E2E fallaron
3. **¿Por qué?** → Endpoint /users retorna 500
4. **¿Por qué?** → DB migration no corrió
5. **¿Por qué?** → Script de deploy no ejecuta migrations
6. **¿Por qué?** → Migrations fueron agregadas pero script no actualizado

**Causa raíz:** Proceso de deploy no incluye checklist de migrations.

**Solución:** Agregar migrations al pipeline automático + checklist.

**Tip:** No siempre son exactamente 5. Puede ser 3 o 7 según complejidad.

---

## 📊 Diagrama de Pareto (Regla 80/20)

**What:** Principio que dice que 80% de los efectos vienen de 20% de las causas.

**Why:** Priorizar esfuerzos en lo que más impacta.

**When:** Múltiples problemas, priorizar bugs, optimizar performance.

**How:**
1. Listar todos los problemas/causas
2. Medir frecuencia o impacto de cada uno
3. Ordenar de mayor a menor
4. Calcular % acumulado
5. Identificar el 20% que causa el 80% del problema

**Ejemplo - Bugs en producción (último mes):**

| Tipo Bug | Cantidad | % Acumulado |
|:---------|:---------|:------------|
| Validación inputs | 45 | 45% |
| Timeouts API | 30 | 75% |
| UI responsive | 15 | 90% |
| Otros | 10 | 100% |

**Insight:** Enfocarse en validación de inputs (45%) y timeouts (30%) resuelve el 75% de bugs.

**Herramientas:** Excel, Google Sheets, Python (matplotlib).

---

## 💡 Lluvia de Ideas (Brainstorming)

**What:** Generación libre de ideas sin juicio inicial.

**Why:** Explorar todas las posibilidades, creatividad colectiva.

**When:** Buscar soluciones, diseño de features, naming, arquitectura.

**How:**
1. Definir problema/objetivo claramente
2. Timeboxear (15-30 min)
3. Reglas: No juzgar, todas las ideas valen, cantidad > calidad
4. Una persona modera, otra anota todo
5. Agrupar ideas similares
6. Votar o priorizar después

**Variantes:**
- **Brainwriting:** Escribir ideas en post-its en silencio (mejor para introverts)
- **Round Robin:** Cada persona aporta una idea por turno
- **Starbursting:** Generar preguntas en vez de respuestas

**Herramientas:** Miro, FigJam, post-its físicos.

---

## 🌳 Árbol Lógico de Fallos (FTA - Fault Tree Analysis)

**What:** Diagrama top-down que descompone un fallo en causas más básicas.

**Why:** Analizar fallos críticos de forma exhaustiva, encontrar puntos únicos de falla.

**When:** Sistemas críticos (salud, finanzas, aeroespacial), análisis de riesgo.

**How:**
1. Identificar evento no deseado (top)
2. Preguntar: "¿Qué puede causar esto?"
3. Usar compuertas lógicas:
   - **AND:** Todas las causas deben ocurrir
   - **OR:** Cualquiera de las causas es suficiente
4. Descomponer hasta eventos básicos
5. Calcular probabilidades si se tienen datos

**Ejemplo - Sistema caído:**
```
          [Sistema Caído]
                |
          ----- OR -----
          |            |
   [App crashea]  [DB no responde]
          |            |
    ----- OR ----  --- OR ---
    |          |   |        |
[Memory]  [Bug]  [Disco] [Network]
```

**Uso en software:** Identificar single points of failure, diseñar redundancia.

---

## 📈 Diagrama de Flujo

**What:** Representación gráfica de proceso paso a paso.

**Why:** Visualizar proceso completo, identificar cuellos de botella, documentar.

**When:** Diseñar algoritmos, documentar procesos, onboarding.

**Símbolos:**
- **Óvalo:** Inicio/Fin
- **Rectángulo:** Proceso/Acción
- **Rombo:** Decisión (if)
- **Paralelogramo:** Input/Output
- **Flecha:** Flujo

**Ejemplo - Proceso de login:**
```
(Inicio) → [Ingresar credenciales] → <¿Válidas?> 
                                          |
                                    No ----+---- Sí
                                    |            |
                            [Mostrar error]   [Login exitoso]
                                    |            |
                                    +------------+
                                          |
                                        (Fin)
```

**Herramientas:** [draw.io](https://www.draw.io/), [Lucidchart](https://www.lucidchart.com/), [Mermaid](https://mermaid.js.org/).

---

## 🔍 5W2H

**What:** Framework de 7 preguntas para definir problema/solución completamente.

**Why:** Asegurar que se consideraron todos los aspectos importantes.

**When:** Planning de features, escribir user stories, post-mortems.

**Las 7 preguntas:**
1. **What** (Qué): ¿Qué es el problema/solución?
2. **Why** (Por qué): ¿Por qué es importante resolverlo?
3. **Who** (Quién): ¿Quién está involucrado/afectado?
4. **When** (Cuándo): ¿Cuándo ocurre? ¿Deadline?
5. **Where** (Dónde): ¿Dónde ocurre? (Sistema, módulo, geografía)
6. **How** (Cómo): ¿Cómo lo resolveremos?
7. **How much** (Cuánto): ¿Cuánto costará en tiempo/dinero/esfuerzo?

**Ejemplo - Feature: Export de reportes:**
- **What:** Permitir exportar dashboard a PDF
- **Why:** Clientes necesitan compartir reportes con stakeholders
- **Who:** Usuarios premium, equipo de analytics (desarrollo)
- **When:** Sprint actual, crítico para Q1
- **Where:** Módulo de reportes, botón en toolbar
- **How:** Librería Puppeteer para generar PDF, queue para async
- **How much:** 3 días desarrollo, 1 día QA, gratis para usuarios

---

## 🔄 PDCA (Plan-Do-Check-Act)

**What:** Ciclo iterativo de mejora continua.

**Why:** Mejora incremental basada en datos.

**When:** Implementar mejoras, optimizar procesos.

**Fases:**
1. **Plan:** Identificar problema, analizar, planear solución
2. **Do:** Implementar solución en pequeña escala (piloto)
3. **Check:** Medir resultados, comparar con objetivo
4. **Act:** Si funciona → estandarizar. Si no → ajustar y repetir

**Ejemplo:**
- **Plan:** Reducir bugs en producción
- **Do:** Implementar pre-commit hooks + code review obligatorio
- **Check:** Medir bugs/semana durante 1 mes: -40%
- **Act:** Estandarizar en todos los repos, documentar proceso

---

## 🎯 Matriz de Decisión

**What:** Tabla para comparar opciones según criterios ponderados.

**Why:** Decisiones objetivas, transparentes.

**When:** Elegir tecnología, priorizar features, seleccionar vendor.

**How:**
1. Listar opciones (columnas)
2. Listar criterios (filas)
3. Asignar peso a cada criterio (1-5)
4. Calificar cada opción en cada criterio (1-10)
5. Multiplicar peso × calificación
6. Sumar total por opción
7. Mayor puntaje = mejor opción

**Ejemplo - Elegir framework frontend:**

| Criterio | Peso | React | Vue | Angular |
|:---------|:-----|:------|:----|:--------|
| Performance | 5 | 8×5=40 | 9×5=45 | 7×5=35 |
| Curva aprendizaje | 3 | 7×3=21 | 9×3=27 | 5×3=15 |
| Ecosistema | 4 | 10×4=40 | 7×4=28 | 8×4=32 |
| **Total** | - | **101** | **100** | **82** |

**Resultado:** React ligeramente mejor que Vue, Angular tercero.

---

## 🚫 Errores Comunes

| Error | Problema | Solución |
|:------|:---------|:---------|
| **Saltar al "cómo" sin el "por qué"** | Resolver síntoma, no causa | Usar 5 Porqués primero |
| **Análisis parálisis** | Sobre-analizar sin actuar | Timeboxear, decidir con datos disponibles |
| **Sesgo de confirmación** | Buscar solo evidencia que confirme hipótesis | Buscar activamente evidencia contraria |
| **Soluciones sin medir** | No saber si funcionó | Definir métricas de éxito antes |
| **No documentar aprendizajes** | Repetir mismos errores | Post-mortem blameless, runbooks |

---

## 📚 Recursos

- [The 5 Whys - Toyota Production System](https://en.wikipedia.org/wiki/Five_whys)
- [Ishikawa Diagram - ASQ](https://asq.org/quality-resources/fishbone)
- [Root Cause Analysis Handbook](https://www.amazon.com/Root-Cause-Analysis-Handbook-Effective/dp/1563273494)
- [Miro Templates](https://miro.com/templates/)

---

[⬅️ Anterior: Observabilidad](./10-observabilidad.md) | [⬆️ Volver arriba](#11-herramientas-de-analisis-de-problemas) | [➡️ Siguiente: Mejora Continua](./12-mejora-continua.md)