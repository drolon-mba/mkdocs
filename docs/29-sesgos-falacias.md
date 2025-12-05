# 29 - Sesgos Cognitivos, Falacias y Leyes a Evitar

> Trampas mentales, errores de razonamiento y leyes que impactan toma de decisiones en tecnología, producto y negocio.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🧠 ¿Por qué importan los Sesgos?](#por-que-importan-los-sesgos)
- [📐 Leyes Fundamentales en Tecnología](#leyes-fundamentales-en-tecnologia)
- [🎯 Sesgos de Decisión y Juicio](#sesgos-de-decision-y-juicio)
- [📊 Sesgos en Datos y Análisis](#sesgos-en-datos-y-analisis)
- [👥 Sesgos Sociales y de Grupo](#sesgos-sociales-y-de-grupo)
- [🔍 Sesgos Perceptuales y de Evaluación](#sesgos-perceptuales-y-de-evaluacion)
- [⚖️ Falacias Lógicas Críticas](#falacias-logicas-criticas)
- [⚠️ Leyes y Efectos Paradójicos](#leyes-y-efectos-paradojicos)
- [📊 Sesgos en Data Science y ML](#sesgos-en-data-science-y-ml)
- [🛡️ Estrategias de Mitigación](#estrategias-de-mitigacion)
- [🚫 Señales de Alerta: Cómo Reconocer Estás Sesgado](#senales-de-alerta-como-reconocer-estas-sesgado)
- [✅ Checklist Anti-Sesgos](#checklist-anti-sesgos)
- [🎯 Template para RFCs Anti-Sesgo](#template-para-rfcs-anti-sesgo)
- [🎯 Casos Prácticos en Tecnología](#casos-practicos-en-tecnologia)
- [📚 Recursos](#recursos)
- [💡 Clave para Semi-Seniors](#clave-para-semi-seniors)
---

## 🧠 ¿Por qué importan los Sesgos?

**What:** Atajos mentales (heurísticos) que sistemáticamente desvían el juicio de la racionalidad.

**Why:** Todos tenemos sesgos. Reconocerlos previene malas decisiones en producto, inversión, arquitectura y management.

**Who:** Product Managers, founders, investors, developers, leaders.

**When:** Diseño de producto, decisiones de inversión, evaluación de performance, priorización.

**How:** Awareness, procesos estructurados, devil's advocate, datos sobre intuición.

**How much:** Un sesgo no detectado puede costar millones en producto fallido o inversión perdida.

---

## 📐 Leyes Fundamentales en Tecnología

| Ley | Definición | Aplicación en Tech/Negocio | Ejemplo Real |
|:----|:-----------|:---------------------------|:-------------|
| **Ley de Murphy** | "Si algo puede salir mal, saldrá mal" | Siempre tener plan B, runbooks, rollback plan | Deploy sin rollback → caída total del sistema |
| **Ley de Kiddlin** | "Si escribes el problema con suficiente claridad, ya tienes la mitad de la solución" | 5W2H, SCQA framework, documentar problemas claramente | Documentar bug con contexto completo acelera resolución |
| **Ley de Gilbert** | "Cuando actúas, el éxito no está garantizado. Pero cuando no actúas, el fracaso sí lo está" | Bias to action, MVPs, fail fast | No lanzar MVP por miedo = oportunidad perdida |
| **Ley de Wilson** | "Si priorizas el conocimiento sobre la sabiduría, el progreso te hará más estúpido" | Balance entre learning y wisdom, senior judgement | Adoptar frameworks sin criterio de cuándo usarlos |
| **Ley de Faulkland** | "Cuando no necesites tomar una decisión, no la tomes" | Reversible decisions, defer until necessary | Decisiones de arquitectura: esperar hasta tener más información |
| **Primera Ley de Newton** | "Un objeto en movimiento permanece en movimiento" | Momentum matters, consistency beats intensity | Daily commits consistentes > sprints intensos esporádicos |
| **Principio de Pareto (80/20)** | 80% resultados de 20% esfuerzo | Identificar y optimizar el 20% crítico | 20% de features generan 80% del valor |
| **Ley de Parkinson** | "El trabajo se expande para llenar el tiempo disponible" | Timeboxing, sprints cortos (1-2 semanas) | Sprint de 4 semanas → scope creep inevitable |
| **Ley de Hick** | "Tiempo de decisión aumenta logarítmicamente con opciones" | Limitar opciones en UI, simplificar decisiones | Dropdown con 50 opciones vs búsqueda con autocompletado |
| **Navaja de Ockham** | "La explicación más simple suele ser la correcta" | KISS principle, evitar over-engineering | Debugging: buscar causas simples primero |
| **Ley de Conway** | "Sistemas reflejan estructura de comunicación organizacional" | Diseñar equipos y comunicación antes que arquitectura | Equipos aislados → arquitectura monolítica |
| **Goodhart's Law** | "Cuando una medida se convierte en objetivo, deja de ser buena medida" | Medir múltiples dimensiones, cambiar métricas | Optimizar lines of code → código inflado |
| **Cobra Effect** | "Solución al problema empeora el problema" | Anticipar incentivos perversos | Pagar por bugs reportados → crear bugs ficticios |

> 💡 **Patrón anti-sesgo:** Implementar "pre-mortem" antes de cada release: *"Es 3 meses después, el feature falló. ¿Por qué?"*

---

## 🎯 Sesgos de Decisión y Juicio

| Sesgo | What | Why ocurre | When aparece | Impacto | Cómo Mitigar |
|:------|:-----|:-----------|:-------------|:--------|:-------------|
| **Confirmation Bias (Confirmación)** | Buscar solo evidencia que confirme creencias pre-existentes | Cerebro busca coherencia y evita disonancia cognitiva | Evaluar nuevas tecnologías, revisar métricas, code review | Ignorar señales de que el producto no funciona, mantener código legacy innecesariamente | Pre-mortem: "¿Por qué podría fallar esto?", buscar evidencia contradictoria activamente |
| **Anchoring Bias (Anclaje)** | Sobre-ponderar la primera información recibida | La información inicial establece un punto de referencia mental | Estimaciones de tiempo, negociaciones salariales, planning de sprints | Estimaciones sesgadas por número inicial, presupuestos irreales | Múltiples estimaciones independientes, usar base rates históricos |
| **Availability Bias (Disponibilidad)** | Sobrevalorar información fácilmente recordable (reciente, dramática) | Memoria privilegia eventos vívidos y recientes | Evaluar riesgos después de un incidente, priorizar features | Temer riesgos raros pero visibles, ignorar problemas comunes pero menos dramáticos | Datos estadísticos en lugar de anécdotas, mantener registros históricos |
| **Recency Bias (Actualidad)** | Ponderar más eventos recientes | Memoria de trabajo tiene capacidad limitada | Después de un deploy fallido, evaluación trimestral | "Última release falló" → evitar deploys por miedo injustificado | Analizar tendencias a largo plazo, no eventos aislados |
| **Hindsight Bias (Retrospectiva)** | "Yo lo sabía desde el principio" después del hecho | Cerebro reescribe recuerdos para ser consistente | Post-mortems, revisiones de decisiones pasadas | No aprender de errores reales, sobrestimar capacidad predictiva | Documentar predicciones antes de conocer resultados, blameless postmortems |
| **Overconfidence Bias (Exceso de confianza)** | Sobreestimar habilidades y probabilidad de éxito | Falta de feedback inmediato sobre errores de juicio | Estimaciones de proyectos, evaluación de habilidades técnicas | Estimaciones optimistas, no preparar contingencias, bugs en producción | Calibración con track record histórico, revisiones por pares |
| **Planning Fallacy** | Subestimar tiempo/costo, sobrestimar beneficios | Enfoque en escenario ideal sin considerar imprevistos | Planning de sprints, roadmap de producto | Proyectos tarde y sobre presupuesto, equipos sobrecargados | Reference class forecasting, buffer time basado en histórico (25%) |
| **Sunk Cost Fallacy (Costo hundido)** | Continuar invirtiendo porque ya invertiste mucho | Aversión a admitir pérdidas, deseo de justificar decisiones pasadas | Mantener proyectos fallidos, seguir con tecnología obsoleta | Mantener proyectos fallidos mucho tiempo, waste de recursos | Decisiones basadas en valor futuro, no pasado; kill criteria definidas |
| **Status Quo Bias** | Preferir estado actual, resistir cambio | Conservación de energía mental, miedo a lo desconocido | Adopción de nuevas tecnologías, cambios de proceso | No adoptar mejores tecnologías/procesos, estancamiento técnico | Forzar justificación del status quo también, experimentos controlados |
| **Loss Aversion (Aversión a pérdida)** | Pérdidas duelen 2x más que ganancias equivalentes | Mecanismo evolutivo de supervivencia | Decisiones de refactoring, inversión en tech debt | Evitar riesgos necesarios, no innovar, acumulación de tech debt | Enmarcar como pérdida de oportunidad si no actúas, dividir en pasos pequeños |
| **Regret Aversion (Aversión al arrepentimiento)** | Evitar decisiones que podrían causar arrepentimiento | Miedo a consecuencias emocionales de errores | Cambios arquitectónicos grandes, hiring/firing | Parálisis por análisis, no tomar decisiones reversibles | Distinguir decisiones reversibles vs irreversibles, timeboxing de decisiones |

---

## 📊 Sesgos en Datos y Análisis

| Sesgo | What | Why ocurre | Impacto | Ejemplo | Cómo Mitigar |
|:------|:-----|:-----------|:--------|:--------|:-------------|
| **Survivorship Bias (Supervivencia)** | Analizar solo lo que "sobrevivió", ignorar lo que falló | Los fracasos son menos visibles y se olvidan | Conclusiones erróneas sobre causas de éxito | Estudiar startups exitosas sin analizar las que fallaron | Incluir data de failures, buscar casos de estudio negativos |
| **Selection Bias (Selección)** | Muestra no representativa de población | Acceso limitado a ciertos grupos de datos | Decisiones basadas en data sesgada | User surveys solo responden los muy satisfechos/insatisfechos | Random sampling, analizar non-responders, múltiples fuentes |
| **Cherry Picking** | Seleccionar data que apoya tu argumento | Sesgo de confirmación en análisis de datos | Validar hipótesis falsas | Mostrar solo trimestres de crecimiento, ocultar los malos | Pre-registrar análisis, third-party review, análisis ciego |
| **Sampling Bias** | Muestra no aleatoria de la población | Métodos de recolección imperfectos | Resultados no generalizables | A/B test solo en power users, ignorando nuevos usuarios | Stratified sampling, randomización, tamaño muestral adecuado |
| **Response Bias** | Respondientes difieren de no-respondientes | Características que afectan disposición a responder | Survey results sesgados | Solo usuarios muy engaged responden NPS | Follow-up con non-responders, incentivos balanceados |
| **Base Rate Neglect (Negación ratio base)** | Ignorar probabilidades base, foco en caso específico | Casos específicos son más memorables | Sobreestimar probabilidad de eventos raros | "Este startup es el próximo Google" (ignorando que 90% fallan) | Siempre empezar con base rates, usar estadística bayesiana |
| **Volatility Bias** | Confundir volatilidad con riesgo | Aversión a variabilidad sin analizar dirección | Evitar inversiones volátiles pero rentables | Evitar crypto por volatilidad, no por fundamentos | Separar volatilidad de riesgo direccional |
| **Evaluator Bias (Del evaluador)** | Quien evalúa afecta resultado | Diferentes estándares entre evaluadores | Performance reviews inconsistentes | Manager laxo vs estricto | Calibración, múltiples evaluadores |

---

## 👥 Sesgos Sociales y de Grupo

| Sesgo | What | Why ocurre | Impacto | Cómo Mitigar |
|:------|:-----|:-----------|:--------|:-------------|
| **Authority Bias (Autoridad)** | Confiar excesivamente en "expertos" | Estructura social jerárquica, deferencia a experiencia | Seguir malas ideas de seniors, falta de pensamiento crítico | Question everything, "disagree and commit", meritocracia de ideas |
| **Halo Effect (Efecto halo)** | Atributo positivo influye juicio general | Generalización de impresiones | Sobrevalorar a persona por un logro aislado | Evaluar dimensiones independientemente, rubricas estructuradas |
| **Horn Effect (Efecto cuerno)** | Atributo negativo contamina todo | Generalización negativa por primera impresión | Subestimar por error pasado, oportunidades perdidas | Separar evaluaciones, fresh start mentality, focus en mejora |
| **False Consensus (Falso consenso)** | Asumir que otros piensan como tú | Proyección de propias creencias | Diseñar para ti, no para usuarios, features no usadas | User research, diverse team, testing con usuarios reales |
| **Similarity Bias (Afinidad)** | Favorecer personas similares a ti | Comfort con lo familiar, validación social | Homogeneidad en contratación, groupthink | Structured interviews, diverse panels, criterios objetivos |
| **Contrast Effect (Contraste)** | Juzgar por comparación reciente, no absoluto | Procesamiento relativo vs absoluto | Candidato mediocre después de malo parece excelente | Rubric de evaluación absoluto |
| **Social Proof (Prueba social)** | Hacer lo que otros hacen | Validación social, miedo a perderse oportunidades (FOMO) | Adoptar tech hype sin evaluar, arquitectura de rebaño | Evaluate technical fit, no popularity; proof of concepts |
| **Framing Effect (Enmarcado)** | Decisión cambia según cómo se presente | Procesamiento emocional de información | "90% sobrevive" vs "10% muere" generan decisiones diferentes | Present both frames, analizar desde múltiples perspectivas |
| **Bandwagon Effect (Arrastre)** | "Todos lo hacen, debe ser correcto" | Presión social, validación grupal | Adoptar tecnologías sin evaluar fit | Revisar fit con contexto específico, no popularidad |
| **Efecto Espectador** | No actuar cuando hay más gente | Difusión de responsabilidad | "Alguien más lo reportará" → bugs no reportados | Asignar responsabilidades explícitas |

---

## 🔍 Sesgos Perceptuales y de Evaluación

| Sesgo | What | Why ocurre | Impacto | Cómo Mitigar |
|:------|:-----|:-----------|:--------|:-------------|
| **Dunning-Kruger Effect** | Incompetentes sobrestiman habilidad, expertos subestiman | Falta de metacognición en novatos, conciencia de complejidad en expertos | Juniors overconfident, seniors con impostor syndrome | Calibración con feedback objetivo, rubricas de evaluación claras |
| **Observer-Expectancy Effect** | Expectativas influencian observación | Profecía autocumplida, procesamiento selectivo | Self-fulfilling prophecies en testing y métricas | Blind testing, double-blind reviews, procesos estandarizados |
| **Outcome Bias (Por resultados)** | Juzgar decisión por resultado, no por proceso | Atajo mental para evaluar calidad decisión | Validar mal proceso porque tuvo suerte, castigar buena decisión con mal resultado | Evaluar decisión con info disponible en momento, análisis de proceso |
| **Focus Effect (Efecto foco)** | Sobre-ponderar un aspecto, ignorar el resto | Atención limitada, saliencia de ciertas métricas | Obsesionarse con una métrica, optimización local vs global | Scorecards balanceadas, múltiples métricas, perspectiva sistémica |
| **Apophenia** | Ver patrones donde no existen | Cerebro busca patrones incluso en ruido | Trading en ruido random, ver "señal" en chart patterns aleatorios | Análisis estadístico riguroso, tests de significancia |
| **Representativeness Bias (Representatividad)** | Juzgar probabilidad por similitud con estereotipo | Atajos mentales basados en prototipos | Ignorar base rates, "Parece fundador exitoso" → invertir sin due diligence | Siempre empezar con base rates, no con similitudes |
| **Illusion of Control (Ilusión de control)** | Sobrestimar capacidad de controlar eventos | Necesidad psicológica de control | Tomar riesgos excesivos, "Puedo time el mercado" | Reconocer límites de control, focus en lo controlable |
| **Optimism Bias (Optimismo)** | Sobrestimar probabilidad de eventos positivos | Mecanismo de protección psicológica | Underestimate riesgos, "A nosotros no nos pasará" | Reference class forecasting, análisis de riesgos sistemático |
| **Negativity Bias (Negatividad)** | Ponderar más eventos negativos | Mecanismo evolutivo de supervivencia | Evitar riesgos necesarios, un review malo pesa más que 10 buenos | Análisis balanceado, métricas objetivas |
| **Denomination Effect** | Menos dispuesto a gastar billetes grandes vs pequeños | Percepción psicológica del valor | Subestimar gastos pequeños recurrentes, $5/mes parece barato, $60/año parece caro | Analizar en términos anuales o lifetime value |

### Sesgos Adicionales de Percepción y Memoria

| Sesgo | What | Ejemplo | Mitigación |
|:------|:-----|:--------|:-----------|
| **Sesgo de Atención** | Atender selectivamente a ciertos estímulos | Notar solo bugs en framework que no te gusta | Systematic observation, checklists |
| **Sesgo de Distinción** | Valorar más cuando comparamos opciones lado a lado | Feature parece mejor en comparación directa | Evaluar absolutamente también |
| **Sesgo Egocéntrico** | Sobrevalorar propio rol en eventos | "El proyecto fue exitoso gracias a mí" | Reconocer contribuciones del equipo |
| **Efecto de Primacía** | Recordar más lo primero | Primera impresión en entrevista domina evaluación | Tomar notas, evaluar al final |
| **Efecto de Retrospección "Color de Rosa"** | Recordar pasado mejor de lo que fue | "Los viejos tiempos eran mejores" | Consultar registros históricos |
| **Sesgo de Punto Ciego** | No ver propios sesgos | "Yo soy objetivo, los demás están sesgados" | Humildad intelectual, feedback externo |
| **Efecto del Lago Wobegon** | Creer que estás por encima del promedio | "Soy mejor developer que la media" (todos creen eso) | Calibración con métricas objetivas |

---

## ⚖️ Falacias Lógicas Críticas

| Falacia | What | Ejemplo en Tech | Por qué es problema | Cómo Refutar |
|:--------|:-----|:----------------|:-------------------|:-------------|
| **Straw Man (Hombre de paja)** | Distorsionar argumento del oponente para refutarlo fácil | "¿Quieres microservicios? ¿Quieres 100 repos imposibles de mantener?" | Evita discusión real, crea conflictos artificiales | "Estoy proponiendo servicios bounded context, no microservicios extremos" |
| **Ad Hominem** | Atacar a la persona, no al argumento | "No le hagas caso, es junior/no tiene experiencia" | Ignora méritos del argumento | "Evaluemos la idea por sus méritos técnicos" |
| **Appeal to Authority (Verecundiam)** | "X lo dice, debe ser verdad" | "Google usa microservicios, nosotros también debemos" | Ignora contexto específico | "Context matters, evaluemos fit con nuestras necesidades" |
| **False Dichotomy (Falso dilema)** | Presentar solo 2 opciones cuando hay más | "O usamos Agile o Waterfall" | Limita opciones creativas, fuerza elecciones subóptimas | "Hay múltiples enfoques: híbridos, ScrumBan, enfoques adaptativos" |
| **Slippery Slope (Pendiente resbaladiza)** | "Si hacemos A, inevitablemente pasará Z" | "Si permitimos TypeScript, pronto usaremos 10 lenguajes" | Paraliza progreso con miedos exagerados | "Podemos establecer governance y criterios para adopción controlada" |
| **Post Hoc Ergo Propter Hoc** | "Después de esto, entonces a causa de esto" | "Deploy en viernes → incidente, entonces no deployar viernes" | Atribución incorrecta de causas, correlación ≠ causación | Analizar causas reales con datos |
| **Red Herring (Pista falsa)** | Desviar la atención con tema irrelevante | "Sí, el código tiene bugs, pero mira esta nueva feature" | Evita resolver problemas reales | Volver a tópico original |
| **Begging the Question (Petición de principio)** | Razonamiento circular, conclusión asumida en premisa | "Este framework es mejor porque es superior" | Falta de evidencia real | Proveer evidencia externa, benchmarks |
| **False Analogy (Falsa analogía)** | Comparación engañosa entre cosas no comparables | "Construir software es como construir un edificio" | Modelos mentales incorrectos | "Software se re-construye constantemente, edificios no" |
| **Tu Quoque** | "Tú también lo haces" | "Me dices que no copie código, pero tú lo haces" | Evita responsabilidad personal | "Hipocresía no invalida el argumento" |
| **Appeal to Emotion (Patético)** | Apelar a emociones en lugar de razón | "Si no hacemos esto, la empresa quebrará" | Decide por miedo, no por datos | Evaluar lógica y datos objetivamente |
| **Appeal to Tradition** | "Siempre se ha hecho así" | "Siempre usamos MySQL, no necesitamos evaluar otras DB" | Impide innovación y mejora continua | "Las necesidades evolucionan, debemos evaluar según requisitos actuales" |
| **Hasty Generalization (Generalización precipitada)** | Generalización apresurada con muestra pequeña | "Los dos primeros usuarios se quejaron, entonces a todos les disgusta" | Decisiones basadas en data insuficiente | "Necesitamos muestra estadísticamente significativa" |
| **Bandwagon (Carro)** | "Todos lo hacen, debe ser correcto" | Adoptar hype sin evaluar | Seguir modas sin análisis | Revisar fit con negocio específico |
| **Carga de la Prueba** | Invertir quien debe probar | "Demuestra que NO funciona" | Evita responsabilidad de probar afirmaciones | "Quien afirma debe probar" |
| **Appeal to Ignorance (Ignorantiam)** | "No se probó falso → es verdadero" | "No hay evidencia contra esta arquitectura → debe ser buena" | Carga de prueba invertida | Ausencia de evidencia ≠ evidencia de ausencia |
| **Envenenar el Pozo** | Descalificar antes de hablar | "Todo lo que dice X es mentira" | Pre-emptive ad hominem | Evaluar cada argumento por mérito |
| **Equívoco** | Cambiar significado de término en argumento | "Banco" (institución vs asiento) en diferentes premisas | Confusión conceptual | Definiciones consistentes |
| **Non Sequitur** | Conclusión no sigue de premisas | "Es martes → debemos usar Python" | No hay conexión lógica | Mostrar falta de conexión |
| **Afirmación del Consecuente** | "Si llueve, hay nubes. Hay nubes → llueve" | Confundir suficiente con necesario | Lógica inválida | Mostrar contraejemplos |
| **Negación del Antecedente** | "Si llueve, uso paraguas. No llueve → no uso paraguas" | Confundir necesario con suficiente | Lógica inválida | Mostrar contraejemplos |

---

## ⚠️ Leyes y Efectos Paradójicos

| Efecto/Ley | What | Por qué es paradójico | Ejemplo en Tech | Mitigación |
|:-----------|:-----|:---------------------|:----------------|:-----------|
| **Goodhart's Law** | "Cuando una medida se convierte en objetivo, deja de ser buena medida" | Optimizar métricas corrompe su validez | Optimizar lines of code → código inflado | Métricas múltiples, auditorías, qualitative + quantitative |
| **Campbell's Law** | Similar a Goodhart: indicador social bajo presión corrompe procesos | Medición bajo presión se corrompe | Teaching to the test, gaming de KPIs | Auditorías, métricas difíciles de gamear |
| **Cobra Effect** | Solución al problema empeora el problema | Incentivos mal diseñados crean comportamientos no deseados | Pagar por bugs reportados → crear bugs ficticios | Diseñar incentivos alineados, métricas balanceadas |
| **Streisand Effect** | Intentar suprimir información la hace más popular | Censura atrae atención | Ocultar security issues → mayor escrutinio cuando se descubren | Transparencia controlada, comunicación proactiva |
| **Peter Principle** | "En jerarquía, cada empleado tiende a ascender hasta su nivel de incompetencia" | Promoción basada en performance actual, no en habilidades para nuevo rol | Excelente IC → mal manager | Dual track (IC y management), evaluar habilidades específicas |
| **Iron Law of Bureaucracy** | Burocracia crece independientemente de su utilidad | Procesos se vuelven fines en sí mismos | Process overload en grandes organizaciones | Regular review de procesos, eliminar redundancias |
| **Efecto de Sobrejustificación** | Motivación externa reduce intrínseca | Recompensas externas matan motivación interna | "Pagar por hobby lo vuelve trabajo" | Preservar motivación intrínseca |
| **Efecto de Polarización** | Evidencia fortalece creencias opuestas | Backfire effect | Datos que contradicen creencias las refuerzan | Presentar info de forma no amenazante |
| **Profecía Autocumplida (Pigmalión)** | Expectativas influyen resultado | Creencias crean realidad | Esperar que feature falle → no promoverla → falla | Awareness de expectativas, testing objetivo |

---

## 📊 Sesgos en Data Science y ML

| Sesgo | What | Fase del proceso | Impacto | Mitigación |
|:------|:-----|:-----------------|:--------|:-----------|
| **Training Data Bias** | Data no representa población real | Data collection | Modelo discrimina grupos subrepresentados | Audit datasets, fairness metrics, data augmentation |
| **Label Bias** | Labels incorrectos o sesgados | Data labeling | Modelo aprende sesgos humanos | Multiple labelers, blind labeling, consensus protocols |
| **Confirmation in EDA** | Buscar patrones que confirman hipótesis | Exploratory analysis | Overfitting a narrativa preexistente | Pre-register hypotheses, análisis ciego |
| **P-hacking** | Probar hasta encontrar p<0.05 | Statistical testing | False positives, resultados no reproducibles | Bonferroni correction, pre-registration, replication |

### Ejemplo de Código Anti-Sesgo en ML

```python
# Mitigación de sesgos en pipeline de ML

# 1. Survivorship Bias: Incluir usuarios churned
df = load_full_cohort(include_churned=True)

# 2. Base Rate: Siempre reportar métricas por clase
from sklearn.metrics import classification_report
print(classification_report(y_true, y_pred))

# 3. Fairness Audits pre-deploy
from aif360 import metrics
fairness_metric = metrics.ClassificationMetric(
    dataset_true, dataset_pred,
    unprivileged_groups=[{'gender': 0}],
    privileged_groups=[{'gender': 1}]
)
print(f"Disparate Impact: {fairness_metric.disparate_impact()}")

# 4. Selection Bias: Muestreo estratificado
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, stratify=y, test_size=0.2
)
```

---

## 🛡️ Estrategias de Mitigación

### 1. Pre-Mortem
**What:** Antes de decidir, asumir que falló y explicar por qué.

**When:** Planning de proyectos, decisiones arquitectónicas grandes.

**How:**
1. "Es un año después, el proyecto falló. ¿Por qué?"
2. Equipo genera razones de fallo
3. Mitigar top 3 razones identificadas

### 2. Red Team / Devil's Advocate
**What:** Asignar persona/equipo para atacar plan.

**When:** Decisiones críticas, cambios arquitectónicos.

**How:** Rotar rol, requiere argumentos contra con evidencia, no solo opinión.

### 3. Decision Journal
**What:** Documentar decisiones antes de conocer outcomes.

**How:** Registrar:
- Decisión tomada
- Razones y contexto
- Expectativas y predicciones
- Alternativas consideradas
- Métricas de éxito

### 4. Checklists Anti-sesgos
**What:** Forzar considerar múltiples factores antes de decidir.

**How:** Checklist pre-decisión con preguntas desafiantes (ver abajo).

### 5. Diverse Teams
**What:** Equipos heterogéneos cuestionan assumptions.

**How:** Diversidad cognitiva, backgrounds, experiencias, perspectivas.

### 6. Base Rates First
**What:** Siempre empezar con probabilidad base.

**How:** "De 100 startups similares, ¿cuántos tienen éxito?" antes de evaluar caso específico.

### 7. Prospective Hindsight
**What:** Imaginar futuro como si fuera pasado.

**How:** "Es 2026, ¿cómo llegamos aquí?" más concreto que "¿Qué haremos?"

### 8. Blind Reviews
**What:** Evaluaciones sin conocer identidad del autor.

**How:** Anonymous RFCs, code reviews ciegos, evaluaciones de candidatos sin CV.

### 9. Calibration Sessions
**What:** Comparar predicciones con resultados reales.

**How:** Mensual, comparar estimaciones vs real en retrospectivas.

### 10. Multiple Perspectives
**What:** Analizar desde diferentes ángulos.

**How:** Framing positivo y negativo, diferentes stakeholders, múltiples métricas.

---

## 🚫 Señales de Alerta: Cómo Reconocer Estás Sesgado

### Red Flags Cognitivas (Individual)
- ❌ Buscar solo evidencia que confirme tu creencia
- ❌ Justificar decisión post-hoc (racionalizando)
- ❌ "Todos piensan como yo" (sin verificar)
- ❌ Decisión rápida sin considerar alternativas
- ❌ Emocional ante cuestionamiento de idea
- ❌ "Esto es diferente" (special pleading)
- ❌ Ignorar base rates históricos
- ❌ No documentar predicciones antes de saber resultado

### Red Flags en Equipos
- ❌ Groupthink - consenso rápido sin debate
- ❌ Síndrome del "not invented here"
- ❌ Cultura de "siempre lo hicimos así"
- ❌ Falta de diversidad cognitiva
- ❌ Miedo a experimentar o fallar
- ❌ Decisiones basadas en HiPPO (Highest Paid Person's Opinion)

---

## ✅ Checklist Anti-Sesgos

Antes de decisión importante:

- [ ] **Pre-mortem:** ¿Por qué podría fallar esta decisión?
- [ ] **Devil's advocate:** ¿Qué argumentos hay en contra?
- [ ] **Base rate:** ¿Cuál es probabilidad histórica de éxito en casos similares?
- [ ] **Alternativas:** ¿Consideré mínimo 3 opciones diferentes?
- [ ] **Diverse input:** ¿Consulté perspectivas de diferentes roles/experiencias?
- [ ] **Decision journal:** ¿Documenté razones, expectativas y métricas de éxito?
- [ ] **Reversibilidad:** ¿Es reversible? ¿Puedo testear pequeño primero?
- [ ] **Data vs intuition:** ¿Tengo datos objetivos o solo "gut feeling"?
- [ ] **Incentivos:** ¿Qué comportamientos podría incentivar esta decisión (explícita e implícitamente)?
- [ ] **Future regret:** ¿De qué me podría arrepentirme en 6 meses?
- [ ] **Framing:** ¿Analicé desde perspectivas positiva y negativa?
- [ ] **Sunk cost:** ¿Estoy decidiendo por valor futuro o por inversión pasada?

---

## 🎯 Template para RFCs Anti-Sesgo

```markdown
## [RFC-XXX] Título de la Decisión Técnica

### Contexto
[Descripción del problema y contexto]

### Hipótesis
[Qué creemos que mejorará y por qué]

### Base Rates
[Datos históricos relevantes de decisiones similares]

### Alternativas Consideradas
1. **Opción A:** [Pros/Cons]
2. **Opción B:** [Pros/Cons]
3. **Opción C:** [Pros/Cons]

### Decisión Propuesta
[Opción elegida y justificación]

### Pre-mortem
[¿Por qué podría fallar esta decisión?]
1. Riesgo 1 y mitigación
2. Riesgo 2 y mitigación
3. Riesgo 3 y mitigación

### Métricas de Éxito
[Cómo mediremos si funcionó]
- Métrica 1: [valor actual] → [valor objetivo]
- Métrica 2: [valor actual] → [valor objetivo]

### Criterios de Reversión
[En qué condiciones revertiremos la decisión]

### Reversibilidad
- [ ] Reversible (Type 2 decision)
- [ ] Irreversible (Type 1 decision)

### Timeline
[Cuándo implementar, cuándo evaluar]
```

---

## 🎯 Casos Prácticos en Tecnología

### Caso 1: Migración de Monolito a Microservicios

**Sesgos detectados:**
- Optimismo en estimaciones (Planning Fallacy)
- Anclaje a arquitectura anterior
- Aversión a pérdida de control centralizado
- Social proof ("todos usan microservicios")

**Estrategia anti-sesgo aplicada:**

```python
# Enfoque basado en datos, no opiniones
def migration_strategy():
    # 1. Medir métricas base
    baseline = measure_monolith_metrics()
    
    # 2. Pre-mortem documentado
    risks = document_failure_scenarios()
    
    # 3. Piloto con límites claros
    pilot = run_pilot(
        service="payment_processing",
        max_duration="6 weeks",
        rollback_criteria=[
            "latency_increase > 20%",
            "error_rate > 1%"
        ]
    )
    
    # 4. Decisión basada en datos
    return decide_based_on(pilot.metrics, baseline, risks)
```

### Caso 2: Selección de Framework para IA

**Sesgos evitados:**
- Efecto halo por hype (ej: "todos usan PyTorch")
- Autoridad (opinión de un senior sin pruebas)
- Falso consenso ("todos en el equipo están de acuerdo")

**Proceso seguido:**
1. Definir requisitos técnicos específicos (latencia, escalabilidad, habilidades del equipo)
2. Ejecutar benchmarks objetivos con datos reales
3. Calcular TCO (Total Cost of Ownership) incluyendo mantenimiento
4. Documentar decisión en RFC con pre-mortem incluido

### Caso 3: Priorización de Features con RICE

**Sesgos mitigados:**
- Voz del cliente ruidosa (un cliente enterprise pide feature compleja)
- Sunk cost en features
- Efecto de encuadre

**Framework aplicado:**

```python
def rice_score(feature):
    """
    RICE = (Reach × Impact × Confidence) / Effort
    """
    reach = estimate_users_affected()  # Usuarios impactados
    impact = estimate_impact_per_user()  # 0.25, 0.5, 1, 2, 3
    confidence = estimate_confidence()  # 0-100%
    effort = estimate_person_months()
    
    return (reach * impact * confidence) / effort
```

---

## 📚 Recursos

### Libros Fundamentales
- [Thinking, Fast and Slow - Daniel Kahneman](https://www.amazon.com/Thinking-Fast-Slow-Daniel-Kahneman/dp/0374533555) - Fundamentos de sesgos cognitivos
- [Predictably Irrational - Dan Ariely](https://www.amazon.com/Predictably-Irrational-Revised-Expanded-Decisions/dp/0061353248) - Economía del comportamiento
- [The Art of Thinking Clearly - Rolf Dobelli](https://www.amazon.com/Art-Thinking-Clearly-Rolf-Dobelli/dp/0062219693) - 99 sesgos explicados
- [Thinking in Bets - Annie Duke](https://www.amazon.com/Thinking-Bets-Making-Smarter-Decisions/dp/0735216355) - Tomar decisiones bajo incertidumbre
- [The Psychology of Computer Programming - Gerald Weinberg](https://www.amazon.com/Psychology-Computer-Programming-Silver-Anniversary/dp/0932633420) - Sesgos en desarrollo de software
- [Weapons of Math Destruction - Cathy O'Neil](https://www.amazon.com/Weapons-Math-Destruction-Increases-Inequality/dp/0553418815) - Ética en algoritmos

### Recursos Online
- [Wikipedia: List of Cognitive Biases](https://es.wikipedia.org/wiki/Anexo:Sesgos_cognitivos)
- [Farnam Street - Mental Models](https://fs.blog/mental-models/)
- [ML Checklist by Google](https://ml-ops.org)
- [Awesome Cognitive Bias](https://github.com/bugout-dev/awesome-cognitive-biases)
- [Decision Journal Template](https://github.com/davidklaing/decision-journal)

---

## 💡 Clave para Semi-Seniors

Reconocer sesgos y falacias no es teoría abstracta: **es lo que evita bugs estratégicos en producto, arquitectura y negocio.**

Los mejores tech leads y PMs no son los que no tienen sesgos (todos los tenemos), sino los que:
1. **Reconocen** sus propios sesgos
2. **Implementan procesos** para mitigarlos
3. **Crean cultura** donde cuestionar assumptions es valorado
4. **Deciden con datos** sobre intuición cuando es posible
5. **Documentan decisiones** para aprender de aciertos y errores

---

[⬅️ Anterior: Onboarding](./28-onboarding.md) | [⬆️ Volver arriba](#29-sesgos-cognitivos-falacias-y-leyes-a-evitar) | [➡️ Siguiente: Prompts y Agentes de IA](./30-prompts-agentes.md)