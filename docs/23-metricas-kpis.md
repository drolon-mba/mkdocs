# 23 - Métricas y KPIs

> Indicadores clave para medir salud del producto, negocio y experiencia de usuario.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Métricas vs KPIs](#metricas-vs-kpis)
- [❤️ HEART Framework (Google)](#heart-framework-google)
- [🏴‍☠️ AARRR (Pirate Metrics)](#aarrr-pirate-metrics)
- [📊 Métricas DORA (DevOps)](#metricas-dora-devops)
- [🎯 NPS, CSAT, CES](#nps-csat-ces)
- [💰 Métricas de Negocio](#metricas-de-negocio)
- [📈 Métricas de Engagement](#metricas-de-engagement)
- [🔄 Retention Cohorts](#retention-cohorts)
- [⚠️ Vanity Metrics vs Actionable Metrics](#vanity-metrics-vs-actionable-metrics)
- [🎯 North Star + Supporting Metrics](#north-star-supporting-metrics)
- [🔬 A/B Testing Metrics](#ab-testing-metrics)
- [📊 Dashboards](#dashboards)
- [🚫 Errores Comunes](#errores-comunes)
- [📚 Recursos](#recursos)
---

## 🎯 Métricas vs KPIs

**What:** Métricas = cualquier dato medible. KPIs = métricas críticas para objetivos estratégicos.

**Why:** Enfoque en lo que importa. "What gets measured gets managed."

**Who:** PMs, founders, data analysts, leadership.

**When:** Definir al lanzar producto, revisar mensual/trimestral.

**How much:** 5-7 KPIs máximo por producto. Menos es más.

---

## ❤️ HEART Framework (Google)

**What:** Framework de Google para medir UX y engagement.

**Why:** Estructura completa para product health.

**When:** Definir métricas de producto, dashboards.

| Dimensión | What | Métricas Ejemplo | Cuándo usar |
|:----------|:-----|:-----------------|:------------|
| **Happiness** | Satisfacción y actitud | NPS, CSAT, app store rating | Productos consumer, SaaS |
| **Engagement** | Nivel de actividad | DAU/MAU, sesiones/usuario, tiempo en app | Apps sociales, contenido |
| **Adoption** | Nuevos usuarios usando feature | % usuarios activos usando feature X | Lanzar features |
| **Retention** | Usuarios que regresan | D1/D7/D30 retention, churn rate | Todo producto |
| **Task Success** | Eficiencia completando tareas | Tasa completación, tiempo por tarea, error rate | Herramientas, utilities |

**Ejemplo - App de Fitness:**
- **Happiness:** App store rating 4.5★, NPS 45
- **Engagement:** 3.5 workouts/semana, 25 min/sesión
- **Adoption:** 60% usuarios probaron feature "Challenges"
- **Retention:** 40% D30 retention
- **Task Success:** 85% completan workout sin saltar

---

## 🏴‍☠️ AARRR (Pirate Metrics)

**What:** Framework de Dave McClure para medir funnel de producto.

**Why:** Optimizar cada etapa del customer journey.

**When:** Startups growth, optimización conversión.

| Etapa | What | Métricas | Optimizar |
|:------|:-----|:---------|:----------|
| **Acquisition** | Cómo llegan usuarios | Tráfico, cost per acquisition (CPA), canales | SEO, ads, referrals |
| **Activation** | Primera experiencia positiva | % completan onboarding, time to value | Onboarding, aha moment |
| **Retention** | Usuarios regresan | D7/D30 retention, churn rate | Engagement loops, notifs |
| **Revenue** | Monetización | MRR, ARPU, LTV | Pricing, upsells |
| **Referral** | Usuarios invitan otros | Referral rate, K-factor, viral coefficient | Sharing, incentivos |

**Funnel típico:**
```
1000 visitantes
  ↓ 20% signup
200 usuarios
  ↓ 50% activan
100 activos
  ↓ 40% retención D30
40 retained
  ↓ 25% convierten pago
10 pagos
  ↓ 20% refieren
2 referrals
```

**Acción:** Identificar mayor drop-off y optimizar ahí primero.

---

## 📊 Métricas DORA (DevOps)

**What:** Métricas para evaluar performance de engineering teams.

**Why:** Correlación demostrada con business outcomes.

**When:** Evaluar madurez DevOps, benchmarking.

| Métrica | What | Elite | High | Medium | Low |
|:--------|:-----|:------|:-----|:-------|:----|
| **Deployment Frequency** | Frecuencia de deploys a prod | On-demand | Semanal-mensual | Mensual-semestral | < Semestral |
| **Lead Time for Changes** | Commit → producción | < 1 hora | < 1 día | < 1 semana | > 1 semana |
| **Change Failure Rate** | % deploys que fallan | 0-15% | 16-30% | 31-45% | > 45% |
| **MTTR** | Mean Time To Recover | < 1 hora | < 1 día | < 1 semana | > 1 semana |

**Cómo mejorar:**
- **Deployment Frequency:** CI/CD automático, feature flags
- **Lead Time:** Trunk-based development, automatización
- **Change Failure Rate:** Tests, code review, staging
- **MTTR:** Monitoring, runbooks, rollback automático

---

## 🎯 NPS, CSAT, CES

### NPS (Net Promoter Score)

**What:** "¿Qué tan probable recomendarías [producto] a un amigo?" (0-10)

**Cálculo:** % Promotores (9-10) - % Detractores (0-6)

**Interpretación:**
- **> 50:** Excelente
- **30-50:** Bueno
- **0-30:** Mejorar
- **< 0:** Problema serio

**Cuándo:** Trimestral, post-interacción importante

### CSAT (Customer Satisfaction)

**What:** "¿Qué tan satisfecho estás con [experiencia]?" (1-5)

**Cálculo:** (Respuestas 4-5 / Total) × 100

**Cuándo:** Post-support ticket, post-compra

### CES (Customer Effort Score)

**What:** "¿Qué tan fácil fue resolver tu problema?" (1-7)

**Cálculo:** Promedio de respuestas (menor = mejor)

**Cuándo:** Post-tarea compleja, onboarding

**Comparación:**

| Métrica | Predice | Cuándo |
|:--------|:--------|:-------|
| **NPS** | Loyalty, growth | Long-term health |
| **CSAT** | Satisfacción momento | Experiencia específica |
| **CES** | Retention | Esfuerzo usuario |

---

## 💰 Métricas de Negocio

### SaaS Metrics

| Métrica | What | Fórmula | Target |
|:--------|:-----|:--------|:-------|
| **MRR** | Monthly Recurring Revenue | Suma suscripciones mensuales | Crecimiento 10%+ MoM |
| **ARR** | Annual Recurring Revenue | MRR × 12 | - |
| **ARPU** | Average Revenue Per User | MRR / Total usuarios | ↑ Over time |
| **LTV** | Lifetime Value | ARPU × (1 / Churn rate) | LTV > 3× CAC |
| **CAC** | Customer Acquisition Cost | Sales+Marketing / Nuevos clientes | ↓ Over time |
| **Churn Rate** | % clientes que cancelan | Cancelaciones / Total usuarios | < 5% mensual |
| **CAC Payback** | Meses para recuperar CAC | CAC / (ARPU × Margen bruto) | < 12 meses |

**Ejemplo:**
- MRR: $100k
- ARPU: $50/mes
- Churn: 5%/mes
- LTV: $50 / 0.05 = $1,000
- CAC: $300
- **LTV/CAC = 3.33** ✅ (target: >3)

### E-commerce

| Métrica | What | Fórmula |
|:--------|:-----|:--------|
| **Conversion Rate** | % visitantes que compran | Compras / Visitantes × 100 |
| **AOV** | Average Order Value | Revenue / # Órdenes |
| **Cart Abandonment** | % carritos no completados | Carritos abandonados / Carritos iniciados |
| **ROAS** | Return on Ad Spend | Revenue ads / Gasto ads |

---

## 📈 Métricas de Engagement

| Métrica | What | Cálculo | Interpretación |
|:--------|:-----|:--------|:---------------|
| **DAU/MAU** | Daily/Monthly Active Users | Ratio DAU/MAU | >20% = sticky product |
| **Sessions/User** | Frecuencia de uso | Sesiones totales / Usuarios | Engagement alto |
| **Session Duration** | Tiempo por visita | Avg tiempo sesión | Depende producto |
| **Feature Adoption** | % usando feature | Usuarios feature / Total activos | >70% = feature exitosa |
| **Stickiness** | Hábito de uso | DAU / MAU | >0.2 = sticky |

**DAU/MAU Benchmark:**
- **>40%:** Redes sociales top (Facebook, Instagram)
- **20-40%:** Productos con buen engagement
- **<20%:** Engagement débil

---

## 🔄 Retention Cohorts

**What:** Tabla que muestra % usuarios activos por cohorte en el tiempo.

**Why:** Identificar si retention mejora con cambios de producto.

**Ejemplo:**

| Cohort | Week 0 | Week 1 | Week 2 | Week 3 | Week 4 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| Jan W1 | 100% | 40% | 30% | 25% | 23% |
| Jan W2 | 100% | 45% | 35% | 30% | 28% |
| Jan W3 | 100% | 50% | 40% | 35% | 33% |

**Insight:** Retention mejorando (cohorts nuevos retienen mejor). Cambios recientes funcionan.

**Buena retention curve:** Se aplana (no llega a 0%)

---

## ⚠️ Vanity Metrics vs Actionable Metrics

| Vanity (Evitar) | Por qué engañosa | Actionable (Preferir) |
|:----------------|:-----------------|:----------------------|
| Total usuarios registrados | No dice cuántos activos | MAU, DAU |
| Page views | No refleja engagement real | Tiempo en página, conversión |
| Followers sociales | Pueden ser bots, inactivos | Engagement rate, clicks |
| Total downloads | No dice cuántos usan | D7/D30 retention |
| Revenue absoluto | Sin contexto de costo | MRR growth rate, LTV/CAC |

**Principio:** Métrica accionable = si sube/baja, sabes qué hacer.

---

## 🎯 North Star + Supporting Metrics

**Estructura:**

```
        [North Star Metric]
         /      |      \
    Input 1  Input 2  Input 3
     /  \      /  \      /  \
   M1  M2    M3  M4    M5  M6
```

**Ejemplo - Spotify:**
- **North Star:** Tiempo escuchando música
- **Input Metrics:**
  - Frecuencia uso (sesiones/semana)
  - Engagement con playlists (saves, shares)
  - Discovery (nuevas canciones/artistas)
- **Supporting:**
  - % usuarios usando Discover Weekly
  - Avg canciones por playlist
  - % sesiones completas (no skip)

---

## 🔬 A/B Testing Metrics

| Concepto | What | Ejemplo |
|:---------|:-----|:--------|
| **Primary Metric** | Métrica principal a mover | Conversion rate |
| **Secondary Metrics** | Otras métricas a monitorear | AOV, retention |
| **Guardrail Metrics** | No deben empeorar | Load time, error rate |
| **Statistical Significance** | p-value < 0.05 | Confianza 95% |
| **Minimum Detectable Effect** | Cambio mínimo a detectar | +5% conversion |

**Evitar:** Múltiples comparaciones sin corrección (p-hacking).

---

## 📊 Dashboards

### Dashboard de Producto

**Sección 1: Health Overview**
- MAU, DAU, DAU/MAU
- Churn rate
- NPS

**Sección 2: Engagement**
- Sesiones/usuario
- Session duration
- Feature adoption

**Sección 3: Growth**
- New users
- Activation rate
- Retention cohorts

**Sección 4: Business**
- MRR, ARR
- LTV, CAC
- Conversion funnel

**Herramientas:** [Amplitude](https://amplitude.com/), [Mixpanel](https://mixpanel.com/), [Looker](https://cloud.google.com/looker), [Metabase](https://www.metabase.com/)

---

## 🚫 Errores Comunes

| Error | Problema | Solución |
|:------|:---------|:---------|
| **Demasiadas métricas** | Parálisis, falta foco | 5-7 KPIs máximo |
| **Métricas sin ownership** | Nadie responsable | Asignar owner por métrica |
| **No segmentar** | Promedios esconden insights | Segmentar por persona, feature, cohorte |
| **Optimizar métrica equivocada** | Goodhart's Law | Validar que métrica refleja valor real |
| **Ignorar leading indicators** | Solo mirar lagging | Balancear ambos |

---

## 📚 Recursos

- [Lean Analytics - Alistair Croll](https://leananalyticsbook.com/)
- [Measuring Success - Kerry Rodden (Google)](https://www.interaction-design.org/literature/article/measuring-success-with-the-heart-framework)
- [SaaS Metrics 2.0 - David Skok](https://www.forentrepreneurs.com/saas-metrics-2/)
- [Amplitude Blog](https://amplitude.com/blog)

---

[⬅️ Anterior: Product Management](./22-product-management.md) | [⬆️ Volver arriba](#23-metricas-y-kpis) | [➡️ Siguiente: Roles y Responsabilidades](./24-roles-responsabilidades.md)