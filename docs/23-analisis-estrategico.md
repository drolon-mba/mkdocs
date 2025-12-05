# 23 - Análisis Estratégico y de Negocio

> Frameworks para analizar mercados, competencia, clientes y tomar decisiones estratégicas informadas.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Análisis Estratégico](#analisis-estrategico)
- [🔍 FODA / SWOT](#foda-swot)
- [🎯 CAME](#came)
- [🌍 PESTEL](#pestel)
- [⚔️ 5 Fuerzas de Porter](#5-fuerzas-de-porter)
- [💎 VRIO](#vrio)
- [👤 Buyer Persona](#buyer-persona)
- [🎯 ICP (Ideal Customer Profile)](#icp-ideal-customer-profile)
- [📅 Diagrama de Gantt](#diagrama-de-gantt)
- [🚫 Errores Comunes](#errores-comunes)
- [📚 Recursos](#recursos)
---

## 🎯 Análisis Estratégico

**What:** Herramientas para evaluar situación actual, entorno y definir estrategia.

**Why:** Decisiones basadas en análisis sistemático > intuición.

**Who:** Product Managers, founders, strategy teams, senior leadership.

**When:** Planning anual/trimestral, lanzar producto, pivotar, expansión.

**How much:** 1-4 semanas de análisis, decisiones que afectan años.

---

## 🔍 FODA / SWOT

**What:** Análisis de Fortalezas, Oportunidades, Debilidades y Amenazas.

**Why:** Vista 360° de situación interna y externa.

**When:** Inicio de proyecto, planning estratégico, decisiones importantes.

**How:** Workshop 2-3 horas con stakeholders, matriz 2x2.

| | **Positivo** | **Negativo** |
|:---|:-------------|:-------------|
| **Interno** | **Fortalezas** (Strengths)<br>¿Qué hacemos bien?<br>¿Qué recursos únicos tenemos? | **Debilidades** (Weaknesses)<br>¿Qué podemos mejorar?<br>¿Qué nos falta? |
| **Externo** | **Oportunidades** (Opportunities)<br>¿Qué tendencias favorecen?<br>¿Qué gaps de mercado? | **Amenazas** (Threats)<br>¿Qué competencia?<br>¿Qué riesgos externos? |

**Ejemplo - Startup SaaS B2B:**

**Fortalezas:**
- Equipo técnico senior
- Velocidad de desarrollo
- Producto innovador

**Debilidades:**
- Sin brand recognition
- Presupuesto marketing limitado
- Solo 2 clientes actuales

**Oportunidades:**
- Mercado creciendo 40% anual
- Competidores con UX pobre
- Remote work aumenta demanda

**Amenazas:**
- Competidor grande puede copiar
- Recesión reduce presupuestos B2B
- Regulaciones nuevas posibles

**⚠️ Sesgos Cognitivos a Evitar:**

- **[Confirmation Bias](./07-sesgos-falacias.md#sesgos-de-decision-y-juicio)**: Tendencia a buscar solo información que confirme nuestras creencias. En FODA, esto puede llevar a sobrestimar fortalezas e ignorar debilidades reales. **Mitigación**: Buscar activamente evidencia que contradiga tus suposiciones.

- **[Status Quo Bias](./07-sesgos-falacias.md#sesgos-de-decision-y-juicio)**: Preferencia por mantener el estado actual. Puede impedir identificar oportunidades de cambio necesarias. **Mitigación**: Preguntarse "si empezara de cero hoy, ¿haría esto igual?"

**Siguiente paso:** Usar CAME para convertir insights en acciones.

---

## 🎯 CAME

**What:** Acciones estratégicas derivadas del FODA.

**Why:** FODA sin acción = papel. CAME convierte análisis en plan.

**When:** Inmediatamente después de FODA.

| FODA | CAME | Acción |
|:-----|:-----|:-------|
| **Fortalezas** | **Mantener** (Corregir) | Seguir invirtiendo, defender ventaja | Mantener velocidad: contratar más devs |
| **Oportunidades** | **Explotar** (Afrontar) | Capitalizar, actuar rápido | Lanzar campaña en nicho remote work |
| **Debilidades** | **Corregir** (Mantener) | Mejorar, invertir recursos | Contratar CMO, aumentar budget marketing |
| **Amenazas** | **Afrontar** (Explotar) | Mitigar riesgo, plan contingencia | Diversificar: añadir tier pequeñas empresas |

---

## 🌍 PESTEL

**What:** Análisis de factores macro-ambientales: Político, Económico, Social, Tecnológico, Ecológico, Legal.

**Why:** Entender contexto externo que no controlamos pero nos afecta.

**When:** Estrategia long-term, expansión internacional, nuevos mercados.

**How:** Investigar cada factor, identificar impacto en negocio.

| Factor | What | Preguntas | Ejemplo Tech |
|:-------|:-----|:----------|:-------------|
| **Político** | Estabilidad, políticas, gobierno | ¿Cambios en regulación tech?<br>¿Incentivos fiscales? | Subsidios I+D, restricciones export chips |
| **Económico** | Inflación, tasas, PBI, empleo | ¿Recesión?<br>¿Poder adquisitivo? | Startup funding afectado por tasas altas |
| **Social** | Demografía, cultura, tendencias | ¿Adopción tecnológica?<br>¿Valores? | Remote work normalizado post-COVID |
| **Tecnológico** | Innovación, automatización, I+D | ¿Nuevas tecnologías?<br>¿Obsolescencia? | AI generativa democratiza creación contenido |
| **Ecológico** | Sostenibilidad, clima, recursos | ¿Regulaciones verdes?<br>¿Consumidores eco-conscious? | Data centers eficientes energéticamente |
| **Legal** | Leyes, IP, privacidad | ¿GDPR?<br>¿Copyright AI? | Regulación IA en UE, privacidad datos |

**Ejemplo - SaaS expandiendo a UE:**
- **Legal:** GDPR compliance obligatorio → invertir en infra UE
- **Tecnológico:** Alta adopción cloud → oportunidad
- **Económico:** Euro fuerte → pricing en EUR atractivo

---

## ⚔️ 5 Fuerzas de Porter

**What:** Análisis de competitividad de industria.

**Why:** Entender atractivo de mercado y dinámica competitiva.

**When:** Entrar nuevo mercado, evaluar rentabilidad industria.

**Las 5 Fuerzas:**

```
         [Amenaza Nuevos Entrantes]
                    ↓
[Poder Proveedores] → [Rivalidad Competidores] ← [Poder Compradores]
                    ↑
         [Amenaza Sustitutos]
```

| Fuerza | What | Alta = ⚠️ | Baja = ✅ |
|:-------|:-----|:----------|:---------|
| **Rivalidad entre competidores** | Intensidad competencia actual | Muchos competidores similares, guerra precios | Pocos competidores, diferenciación clara |
| **Amenaza nuevos entrantes** | Facilidad para nuevos competidores | Bajas barreras entrada, capital bajo | Altas barreras (regulación, capital, tech) |
| **Poder de negociación proveedores** | Influencia de proveedores | Pocos proveedores, altos costos cambio | Muchos proveedores, fácil cambiar |
| **Poder de negociación compradores** | Influencia de clientes | Pocos clientes grandes, fácil cambiar | Muchos clientes pequeños, altos switching costs |
| **Amenaza productos sustitutos** | Alternativas al producto | Sustitutos buenos y baratos | Pocos sustitutos, baja performance |

**Ejemplo - Cloud Storage:**
- **Rivalidad:** Alta (AWS, Google, Azure, Dropbox)
- **Nuevos entrantes:** Media (capital alto pero tech disponible)
- **Poder proveedores:** Baja (múltiples datacenter providers)
- **Poder compradores:** Alta (empresas grandes negocian descuentos)
- **Sustitutos:** Media (on-prem, file servers legacy)

**Conclusión:** Industria competitiva, márgenes presionados → diferenciarse o especializarse.

---

## 💎 VRIO

**What:** Framework para evaluar ventaja competitiva sostenible: Valor, Rareza, Imitabilidad, Organización.

**Why:** Identificar qué recursos/capacidades son ventaja real.

**When:** Evaluar fortalezas, decisiones de inversión.

**Preguntas:**

| Pregunta | Resultado |
|:---------|:----------|
| ¿Agrega **Valor**? | No → Desventaja competitiva |
| ¿Es **Raro**? | No → Paridad competitiva |
| ¿Es **Inimitable** (difícil copiar)? | No → Ventaja temporal |
| ¿Está **Organizado** para capturar valor? | Sí → **Ventaja sostenible** ✅ |

**Ejemplo - Tesla:**

| Recurso | Valor | Raro | Inimitable | Organizado | Resultado |
|:--------|:------|:-----|:-----------|:-----------|:----------|
| Marca | ✅ | ✅ | ✅ (reputación construida años) | ✅ | Ventaja sostenible |
| Baterías propias | ✅ | ✅ | ⚠️ (competidores invierten I+D) | ✅ | Ventaja temporal |
| Software OTA | ✅ | ⚠️ (otros adoptan) | ❌ | ✅ | Ventaja temporal |

---

## 👤 Buyer Persona

**What:** Representación semi-ficticia del cliente ideal basada en investigación.

**Why:** Entender profundamente al cliente para mejor producto/marketing.

**When:** Definir producto, crear contenido, segmentar mercado.

**How:** Entrevistas, encuestas, analytics. Crear 2-4 personas clave.

**Template:**

```
Nombre: Laura, la Lead Developer

Demografía:
- 32 años, mujer
- Ingeniería de Software, 8 años experiencia
- Salario: $120k
- Ubicación: Remoto (Argentina)

Psicografía:
- Valora: eficiencia, calidad, aprendizaje
- Frustraciones: reuniones innecesarias, legacy code
- Objetivos: crecer técnicamente, work-life balance

Comportamiento:
- Lee: Dev.to, Hacker News
- Herramientas: VS Code, GitHub, Linear
- Influencers: Kent C. Dodds, Dan Abramov

Necesidades:
- Herramientas que aumenten productividad
- Documentación clara
- Community support

Quote: "Si no puedo configurarlo en 5 minutos, busco alternativa."
```

**Uso:** Validar features ("¿Laura usaría esto?"), escribir copy, priorizar roadmap.

---

## 🎯 ICP (Ideal Customer Profile)

**What:** Descripción de la compañía perfecta para tu producto B2B.

**Why:** Foco en leads de alto potencial, mejor fit product-market.

**When:** B2B sales, marketing campaigns, qualify leads.

**Diferencia con Persona:** ICP = empresa, Persona = individuo dentro de empresa.

**Criterios:**

| Categoría | Ejemplos |
|:----------|:---------|
| **Firmográficos** | Industria (SaaS, Fintech)<br>Tamaño (50-500 empleados)<br>Revenue ($5M-$50M)<br>Ubicación (LATAM, USA) |
| **Tecnográficos** | Stack tech (React, AWS)<br>Herramientas (Salesforce, Slack)<br>Madurez tech (cloud-native) |
| **Comportamiento** | Budget disponible ($50k+/año)<br>Ciclo compra (3-6 meses)<br>Decision makers (CTO, VP Eng) |
| **Pain Points** | Escalabilidad limitada<br>Seguridad preocupante<br>Time-to-market lento |

**Ejemplo ICP - Herramienta DevOps:**
- **Industria:** SaaS, E-commerce
- **Tamaño:** 100-1000 empleados
- **Stack:** Kubernetes, microservicios
- **Madurez:** Usando CI/CD básico, quieren optimizar
- **Budget:** >$100k/año en tooling
- **Pain:** Deploys lentos, rollbacks manuales

---

## 📅 Diagrama de Gantt

**What:** Gráfico de barras que muestra cronograma de proyecto.

**Why:** Visualizar timeline, dependencias, hitos.

**When:** Planning de proyecto, comunicar timeline a stakeholders.

**Componentes:**
- Eje X: Tiempo (días, semanas, meses)
- Eje Y: Tareas
- Barras: Duración de cada tarea
- Flechas: Dependencias

**Ejemplo - Lanzamiento MVP:**
```
Tarea                  | Sem1 | Sem2 | Sem3 | Sem4 |
-----------------------|------|------|------|------|
Diseño UX              | ███  |      |      |      |
Desarrollo Backend     |   ████████  |      |      |
Desarrollo Frontend    |      |  █████████  |      |
Testing                |      |      |  ██  |      |
Deploy                 |      |      |      | █    |
```

**Herramientas:** [Microsoft Project](https://www.microsoft.com/en-us/microsoft-365/project), [TeamGantt](https://www.teamgantt.com/), [GanttProject](https://www.ganttproject.biz/)

---

## 🚫 Errores Comunes

| Error | Problema | Solución |
|:------|:---------|:---------|
| **Análisis sin acción** | Documentos que nadie usa | Derivar OKRs y plan concreto |
| **Assumptions sin validar** | Decisiones basadas en guesses | Customer interviews, MVP |
| **Personas genéricas** | "Todas las empresas" | Segmentar, priorizar ICP |
| **FODA superficial** | Solo lo obvio | Research profundo, data |
| **Ignorar amenazas** | Optimismo sesgado | War gaming, escenarios pesimistas |

---

## 📚 Recursos

- [Blue Ocean Strategy - Kim & Mauborgne](https://www.blueoceanstrategy.com/)
- [Positioning - Al Ries & Jack Trout](https://www.amazon.com/Positioning-Battle-Your-Al-Ries/dp/0071373586)
- [Good Strategy Bad Strategy - Richard Rumelt](https://www.amazon.com/Good-Strategy-Bad-Difference-Matters/dp/0307886239)
- [Harvard Business Review](https://hbr.org/)

---

[⬅️ Anterior: Data Governance](./22-data-governance.md) | [⬆️ Volver arriba](#23-analisis-estrategico-y-de-negocio) | [➡️ Siguiente: Product Management](./24-product-management.md)
