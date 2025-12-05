# 22 - Product Management

> Frameworks y técnicas para descubrir, priorizar y entregar productos que usuarios amen y negocio necesite.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 SMART Goals](#smart-goals)
- [📊 Goal Pyramid](#goal-pyramid)
- [🎯 BHAG (Big Hairy Audacious Goal)](#bhag-big-hairy-audacious-goal)
- [📋 SCQA Framework](#scqa-framework)
- [🔍 CIRCLES Method](#circles-method)
- [📊 Lean Canvas](#lean-canvas)
- [🧠 Mapa de Empatía](#mapa-de-empatia)
- [🎯 Product Management](#product-management)
- [💡 JTBD (Jobs To Be Done)](#jtbd-jobs-to-be-done)
- [🗺️ User Story Mapping](#user-story-mapping)
- [🎯 OKRs (Objectives & Key Results)](#okrs-objectives-key-results)
- [⭐ North Star Metric](#north-star-metric)
- [📊 Product-Market Fit](#product-market-fit)
- [🔄 Build-Measure-Learn](#build-measure-learn)
- [📋 Priorización](#priorizacion)
- [📝 Product Requirements](#product-requirements)
- [🔍 Discovery Techniques](#discovery-techniques)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 SMART Goals

**What:** Criterio para definir objetivos efectivos.

**Why:** Objetivos vagos = no accionables. SMART = claridad y medición.

**When:** Definir OKRs, roadmaps, user stories.

**Criterios:**
- **S**pecific (Específico): Claro y concreto
- **M**easurable (Medible): Con métrica cuantificable
- **A**chievable (Alcanzable): Desafiante pero posible
- **R**elevant (Relevante): Alineado con objetivos mayores
- **T**ime-bound (Con plazo): Deadline definido

**Ejemplo:**
- ❌ Vago: "Mejorar performance"
- ✅ SMART: "Reducir p95 latency de 800ms a 300ms en APIs críticas para fin de Q2"

---

## 📊 Goal Pyramid

**What:** Estructura jerárquica de objetivos desde visión hasta hábitos diarios.

**Why:** Conectar visión long-term con acciones daily.

**Niveles:**
```
        [Goal]
     Big Goal / BHAG
          ↓
   [Intermediate Goals]
     Quarterly OKRs
          ↓
   [Short-term Goals]
     Sprint goals
          ↓
    [Sub-tasks]
   Daily habits/tasks
```

**Ejemplo:**
- **BHAG:** Ser el CRM #1 para startups tech en 5 años
- **Intermediate:** 100k usuarios activos en 18 meses
- **Short-term:** Lanzar onboarding simplificado este quarter
- **Daily:** Hacer 3 user interviews/semana

---

## 🎯 BHAG (Big Hairy Audacious Goal)

**What:** Objetivo grande, descabellado y audaz (10-30 años).

**Why:** Inspira, motiva, da dirección long-term.

**When:** Definir visión de compañía, norte estratégico.

**Características:**
- Claro y convincente
- Ambicioso (50-70% probabilidad)
- Timeframe: 10-30 años
- Tangible, no aspiracional vago

**Ejemplos reales:**
- Google (1990s): "Organizar la información del mundo"
- SpaceX: "Hacer la humanidad multi-planetaria"
- Amazon (1990s): "Ser la tienda más customer-centric"

---

## 📋 SCQA Framework

**What:** Estructura narrativa para presentar problemas/soluciones: Situation, Complication, Question, Answer.

**Why:** Comunicación clara con stakeholders, alineación rápida.

**When:** PRDs, presentaciones a liderazgo, pitches.

**Estructura:**
1. **Situation:** Contexto actual (hechos, sin juicio)
2. **Complication:** Problema, tensión, oportunidad
3. **Question:** Pregunta clave a responder
4. **Answer:** Solución propuesta

**Ejemplo:**
- **S:** Tenemos 50k usuarios pero NPS es 25 (bajo)
- **C:** Onboarding actual tarda 10 pasos, 60% abandonan
- **Q:** ¿Cómo reducir fricción en onboarding?
- **A:** Simplificar a 3 pasos + wizard guiado

---

## 🔍 CIRCLES Method

**What:** Framework para product design interviews/features: Comprehend, Identify, Report, Cut, List, Evaluate, Summarize.

**Why:** Estructura para diseñar productos/features sistemáticamente.

**When:** Discovery, design de features, entrevistas PM.

**Pasos:**
1. **Comprehend:** Entender situación (What? Why? Who? How?)
2. **Identify:** Identificar el customer específico
3. **Report:** Reportar necesidades del customer
4. **Cut:** Priorizar (through trade-offs)
5. **List:** Listar soluciones posibles
6. **Evaluate:** Evaluar trade-offs de cada solución
7. **Summarize:** Resumir recomendación

**Ejemplo - Diseñar feature de notificaciones:**
1. **Comprehend:** Sistema actual sin notificaciones, usuarios piden updates
2. **Identify:** Power users que revisan app 5+ veces/día
3. **Report:** Quieren saber de updates sin revisar manualmente
4. **Cut:** Priorizar notificaciones críticas (no todo)
5. **List:** Push, email, in-app, SMS
6. **Evaluate:** Push = mejor engagement, email = fallback
7. **Summarize:** Implementar push con opt-in, email como backup

---

## 📊 Lean Canvas

**What:** Adaptación de Business Model Canvas para startups/productos.

**Why:** Capturar modelo de negocio en 1 página, iterable.

**When:** Validar idea, pivots, comunicar a inversionistas.

**9 Bloques:**

| | | |
|:---|:---|:---|
| **Problema**<br>Top 3 problemas | **Solución**<br>Top 3 features | **Propuesta de Valor Única**<br>Mensaje claro y convincente |
| **Ventaja Especial**<br>No se puede copiar fácil | **Segmento de Clientes**<br>Target users | |
| **Métricas Clave**<br>KPIs críticos | **Canales**<br>Path to customers | |
| **Estructura de Costes**<br>Fixed + variable costs | **Flujo de Ingresos**<br>Revenue streams | |

**Ejemplo - SaaS para equipos remotos:**
- **Problema:** Comunicación async ineficiente, context switching
- **Solución:** Workspace unificado, async-first, deep work
- **Propuesta:** "Slack para deep work"
- **Ventaja:** AI que resume threads automáticamente
- **Clientes:** Equipos remotos 10-50 personas
- **Métricas:** DAU/MAU, messages/user, retention D30
- **Canales:** Product Hunt, content marketing, referrals
- **Costes:** Infra cloud, salarios, marketing
- **Ingresos:** SaaS $15/user/mes

---

## 🧠 Mapa de Empatía

**What:** Herramienta visual para entender profundamente al usuario.

**Why:** Diseñar productos que resuenan con necesidades reales.

**When:** Discovery, crear personas, validar assumptions.

**6 Cuadrantes:**

```
        [Usuario: Laura, Lead Developer]
                    
    ┌──────────────────┬──────────────────┐
    │   QUÉ PIENSA     │    QUÉ OYE       │
    │   Y SIENTE       │                  │
    │ "Necesito más    │ Manager: "ship   │
    │  tiempo focus"   │  faster"         │
    │ "Impostor syn"   │ Peers: "burnt    │
    │                  │  out"            │
    ├──────────────────┼──────────────────┤
    │    QUÉ VE        │  QUÉ DICE Y HACE │
    │                  │                  │
    │ Slack con 50     │ "Sí puedo hacer  │
    │ notificaciones   │  eso" (overcom)  │
    │ Jira con 20      │ Trabaja hasta    │
    │ tickets          │ las 10pm         │
    ├──────────────────┴──────────────────┤
    │         ESFUERZOS (Pains)            │
    │ • Interrupciones constantes          │
    │ • Reuniones innecesarias             │
    │ • Expectations poco claras           │
    │ • Legacy code sin docs               │
    ├──────────────────────────────────────┤
    │        RESULTADOS (Gains)            │
    │ • Completar feature de impacto       │
    │ • Aprender tecnología nueva          │
    │ • Reconocimiento del equipo          │
    │ • Work-life balance                  │
    └──────────────────────────────────────┘
```

**Cómo usarlo:**
1. Definir usuario específico (persona)
2. Llenar cada cuadrante con research (entrevistas, observación)
3. Identificar contradicciones (dice vs hace)
4. Diseñar soluciones que alivien pains y maximicen gains

---

## 🎯 Product Management

**What:** Disciplina que conecta negocio, tecnología y UX para crear productos exitosos.

**Why:** Productos sin PM = features aleatorias sin estrategia. PM asegura value delivery.

**Who:** Product Managers, Product Owners, founders.

**When:** Desde ideación hasta sunset del producto.

**How much:** PM típicamente gestiona $1M-$10M+ en inversión anual de desarrollo.

---

## 💡 JTBD (Jobs To Be Done)

**What:** Framework que dice que clientes "contratan" productos para hacer un "trabajo".

**Why:** Entender el trabajo real (no features) que cliente necesita.

**When:** Discovery, definir producto, entender competencia.

**Formato:** "Cuando [situación], quiero [motivación], para que [outcome esperado]"

**Ejemplo:**
- ❌ "Quiero taladro de 1/4 pulgada"
- ✅ "Cuando quiero colgar un cuadro, necesito hacer un agujero, para que el cuadro quede en la pared"

**Insights:**
- El "trabajo" es colgar cuadro, no el taladro
- Competidores: cinta adhesiva, clavos sin agujero, servicios de instalación

**Aplicación:**
1. Identificar el Job principal
2. Entender contexto (cuándo, dónde)
3. Identificar pain points del job actual
4. Diseñar solución que haga el job mejor

**Ejemplo real - Milkshake (Clayton Christensen):**
- **Job:** Hacer commute menos aburrido y llenar estómago hasta almuerzo
- **"Competidores":** Bagels (dejan manos sucias), bananas (no duran), café (termina rápido)
- **Solución:** Milkshake espeso que dura 20min conduciendo

---

## 🗺️ User Story Mapping

**What:** Técnica visual para planear releases organizando user stories en mapa 2D.

**Why:** Vista holística del journey del usuario, priorización colaborativa.

**When:** Planning de MVP, roadmap, sprint planning.

**Ejes:**
- **Horizontal:** Journey del usuario (izq → der)
- **Vertical:** Prioridad (arriba → abajo)

**Estructura:**
```
[Activities] →  Login    →  Browse  →  Purchase  →  Track
                  |           |          |           |
[Tasks]      Autenticar   Buscar     Pagar      Ver status
                  |           |          |           |
[Stories]    Crear cuenta  Filtrar   Tarjeta   Email notif
             Social login  Ordenar   PayPal    Push notif
             2FA           Favoritos Crypto    Tracking map
```

**Releases:**
- **MVP (línea 1):** Login básico, búsqueda simple, pago tarjeta, email
- **V2 (línea 2):** Social login, filtros, PayPal, push
- **V3 (línea 3):** 2FA, favoritos, crypto, tracking map

**Herramientas:** [Miro](https://miro.com/), [Mural](https://www.mural.co/), post-its físicos.

---

## 🎯 OKRs (Objectives & Key Results)

**What:** Framework de goal-setting usado por Google, LinkedIn, Twitter.

**Why:** Alinear equipo, medir progreso, foco en outcomes no outputs.

**When:** Planning trimestral, anual.

**Estructura:**
- **Objective:** Qué queremos lograr (cualitativo, inspiracional)
- **Key Results:** Cómo medimos éxito (cuantitativo, 2-5 por objetivo)

**Características:**
- Ambiciosos (70% logro = éxito)
- Temporales (típicamente trimestre)
- Transparentes (públicos en org)

**Ejemplo - Startup SaaS:**

**Objective:** Convertirnos en la herramienta #1 para equipos remotos

**Key Results:**
1. Crecer usuarios activos mensuales de 10k a 50k
2. Aumentar NPS de 30 a 50
3. Lograr 80% de equipos usen feature colaborativa
4. Reducir churn de 10% a 5%

**Diferencia con KPIs:** OKRs cambian cada quarter, KPIs son permanentes.

---

## ⭐ North Star Metric

**What:** LA métrica que mejor predice éxito long-term del producto.

**Why:** Foco singular, alinea todos los equipos.

**When:** Definir estrategia producto, medir product-market fit.

**Criterios buena North Star:**
- Refleja value entregado al cliente
- Mide progreso hacia visión
- Leading indicator (predice revenue futuro)
- Accionable por equipo

**Ejemplos:**

| Producto | North Star | Por qué |
|:---------|:-----------|:--------|
| **Airbnb** | Noches reservadas | Refleja value para host y guest |
| **Spotify** | Tiempo escuchando | Engagement = retención = suscripciones |
| **Slack** | Mensajes enviados | Core value = comunicación |
| **Medium** | Tiempo leyendo | Value = contenido de calidad consumido |
| **Uber** | Viajes completados | Core transaction |

**Supporting Metrics:** Métricas que influencian la North Star
- Para "Noches reservadas": Listings activos, tasa conversión búsqueda, reviews positivas

---

## 📊 Product-Market Fit

**What:** Grado en que un producto satisface demanda de mercado.

**Why:** Sin PMF, scaling = desperdicio. Con PMF, crecer es más fácil.

**When:** Validar antes de escalar marketing/ventas.

**Cómo medir:**

### 1. Sean Ellis Test
Pregunta a usuarios: "¿Qué tan decepcionado estarías si ya no pudieras usar este producto?"
- **>40% responden "muy decepcionado"** → PMF ✅
- <40% → seguir iterando

### 2. Retention Cohorts
- Gráfico de retención por cohorte
- Si curva se aplana (no llega a 0) → PMF
- Si sigue bajendo → leaky bucket, no PMF

### 3. Organic Growth
- % usuarios que vienen por referral/word-of-mouth
- >40% → señal fuerte de PMF

### 4. Sales Velocity
- Si cierras deals rápido sin convencer mucho → PMF
- Si cada deal requiere custom pitch → no PMF

**Pre-PMF:** Focus en learning y iteración rápida  
**Post-PMF:** Focus en scaling y optimización

---

## 🔄 Build-Measure-Learn

**What:** Ciclo de Lean Startup para validar hipótesis rápidamente.

**Why:** Reducir desperdicio, aprender rápido, pivotar si necesario.

**When:** Incertidumbre alta, nuevos productos/features.

**Ciclo:**
```
1. Build (MVP)
   ↓
2. Measure (Datos)
   ↓
3. Learn (Insights)
   ↓
4. Pivot or Persevere
   ↓
(Repeat)
```

**Ejemplo:**
- **Hipótesis:** "Usuarios pagarían por export a PDF"
- **Build:** Botón "Export PDF" que manda email pidiendo upgrade
- **Measure:** 200 clicks en 1 semana, 30 respondieron email
- **Learn:** 15% interesados → vale la pena construir
- **Persevere:** Construir feature real

**Tipo de MVPs:**
- Landing page con signup
- Wizard of Oz (manual behind scenes)
- Concierge (servicio personalizado)
- Prototype (Figma clickeable)

---

## 📋 Priorización

### RICE Framework

**What:** Modelo para priorizar features: Reach × Impact × Confidence / Effort

| Factor | What | Escala |
|:-------|:-----|:-------|
| **Reach** | ¿Cuántos usuarios afecta? | Usuarios/trimestre |
| **Impact** | ¿Qué tanto ayuda? | 3=Massive, 2=High, 1=Medium, 0.5=Low, 0.25=Minimal |
| **Confidence** | ¿Qué tan seguros? | 100%=High data, 80%=Medium, 50%=Low |
| **Effort** | ¿Cuánto trabajo? | Person-months |

**Fórmula:** `Score = (Reach × Impact × Confidence) / Effort`

**Ejemplo:**

| Feature | Reach | Impact | Confidence | Effort | Score |
|:--------|:------|:-------|:-----------|:-------|:------|
| Dark mode | 10k | 1 | 80% | 0.5 | 16 |
| AI suggestions | 50k | 3 | 50% | 4 | 18.75 ⭐ |
| Export PDF | 5k | 2 | 100% | 1 | 10 |

**Resultado:** Priorizar AI suggestions.

**⚠️ Sesgos Cognitivos a Evitar:**

- **[Planning Fallacy](./29-sesgos-falacias.md#sesgos-de-decision-y-juicio)**: Tendencia a subestimar el tiempo necesario para completar tareas. Al estimar "Effort" en RICE, considera agregar un buffer del 30-50%. **Mitigación**: Usar estimaciones de 3 puntos (optimista, realista, pesimista) y revisar estimaciones históricas.

- **[Sunk Cost Fallacy](./29-sesgos-falacias.md#sesgos-de-decision-y-juicio)**: Continuar invirtiendo en algo porque ya invertiste mucho. No dejes que el trabajo previo influya en la priorización actual. **Mitigación**: Evaluar cada feature como si fuera nueva, ignorando el esfuerzo ya invertido.

### Value vs Effort Matrix

| | **High Value** | **Low Value** |
|:---|:--------------|:--------------|
| **Low Effort** | 🚀 **Quick Wins** - Hacer primero | 💤 **Fill-ins** - Cuando hay tiempo |
| **High Effort** | 🎯 **Big Bets** - Planear bien | ❌ **Money Pit** - Evitar |

---

## 📝 Product Requirements

### PRD (Product Requirements Document)

**What:** Documento que define qué construir y por qué.

**When:** Antes de iniciar desarrollo de features grandes.

**Secciones:**
1. **Resumen ejecutivo:** One-pager
2. **Problema:** JTBD, pain points, quotes usuarios
3. **Objetivos:** OKRs, success metrics
4. **Usuarios:** Personas afectadas
5. **Solución propuesta:** Features, flows, mocks
6. **Scope:** In/Out, MVPs fases
7. **Dependencias:** APIs, teams, integraciones
8. **Riesgos:** Technical, market, regulatory
9. **Timeline:** Estimaciones, hitos

**Tip:** Usar template, iterar con stakeholders.

---

## 🔍 Discovery Techniques

| Técnica | What | When |
|:--------|:-----|:-----|
| **User Interviews** | Conversaciones 1:1 | Entender problemas profundos |
| **Surveys** | Cuestionarios masivos | Validar cuantitativamente |
| **Usability Testing** | Observar usuarios usando producto | Identificar fricciones |
| **Analytics** | Behavioral data | Encontrar patrones uso real |
| **A/B Testing** | Experimentos controlados | Validar cambios |
| **Competitor Analysis** | Estudiar competencia | Identificar gaps, best practices |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **HiPPO decisions** | Highest Paid Person's Opinion | User research, data-driven |
| **Feature factory** | Construir sin strategy | OKRs, JTBD, medir outcomes |
| **Build it they will come** | No validar demanda | Discovery, MVPs, pre-sales |
| **One size fits all** | No segmentar | Personas, ICP, priorizar |
| **Analysis paralysis** | Investigar sin decidir | Timeboxear, suficientemente bueno |

---

## 📚 Recursos

- [Inspired - Marty Cagan](https://www.svpg.com/books/inspired/)
- [The Lean Startup - Eric Ries](http://theleanstartup.com/)
- [Crossing the Chasm - Geoffrey Moore](https://www.amazon.com/Crossing-Chasm-3rd-Disruptive-Mainstream/dp/0062292986)
- [Product School](https://productschool.com/)

---

[⬅️ Anterior: Análisis Estratégico](./21-analisis-estrategico.md) | [⬆️ Volver arriba](#product-management) | [➡️ Siguiente: Métricas y KPIs](./23-metricas-kpis.md)
