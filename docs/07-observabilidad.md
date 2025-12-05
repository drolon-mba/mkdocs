# 07 - Observabilidad y Telemetría

> Capacidad de entender el estado interno de un sistema mediante sus outputs: logs, métricas y traces.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Los Tres Pilares](#los-tres-pilares)
- [📝 Logging (Registros)](#logging-registros)
- [📊 Metrics (Métricas)](#metrics-metricas)
- [🔍 Tracing (Trazas Distribuidas)](#tracing-trazas-distribuidas)
- [🏥 Health Checks](#health-checks)
- [🚨 Alerting (Alertas)](#alerting-alertas)
- [📈 APM (Application Performance Monitoring)](#apm-application-performance-monitoring)
- [🎯 SLIs, SLOs, SLAs](#slis-slos-slas)
- [📊 Dashboards](#dashboards)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 Los Tres Pilares

**What:** Logging, Metrics, Tracing - información complementaria para diagnosticar sistemas.

**Why:** En producción, no puedes hacer debugging con breakpoints. La observabilidad es tu única ventana.

**Who:** Developers, SREs, DevOps, Support.

**How much:** 5-10% overhead en performance, invaluable para incident response.

---

## 📝 Logging (Registros)

**What:** Eventos discretos con timestamp, nivel y contexto.

| Aspecto | What | Why | How | Herramientas |
|:--------|:-----|:----|:----|:-------------|
| **Structured Logs** | JSON con campos consistentes | Queryable, parseable | `{"timestamp": "...", "level": "error", "trace_id": "..."}` | [Winston](https://github.com/winstonjs/winston), [Loguru](https://github.com/Delgan/loguru), [Log4j2](https://logging.apache.org/log4j/2.x/) |
| **Niveles** | DEBUG, INFO, WARN, ERROR, FATAL | Filtrar por severidad | INFO en prod, DEBUG en dev | Configuración por entorno |
| **Correlation IDs** | `trace_id` único por request | Rastrear request completo | Generar UUID en gateway, propagar headers | `X-Trace-Id`, OpenTelemetry |
| **Contexto** | `user_id`, `endpoint`, `duration` | Debugging efectivo | Incluir metadatos relevantes | MDC (Mapped Diagnostic Context) |
| **Rotación** | Archivar logs antiguos | No llenar disco | Rotar diario, retener 30 días | [Logrotate](https://linux.die.net/man/8/logrotate), S3 lifecycle |
| **Agregación** | Centralizar logs de múltiples fuentes | Vista unificada | Enviar a Elasticsearch/Loki | [Fluentd](https://www.fluentd.org/), [Filebeat](https://www.elastic.co/beats/filebeat) |

**Stack ELK:**
- [Elasticsearch](https://www.elastic.co/elasticsearch/): Storage + search
- [Logstash](https://www.elastic.co/logstash/): Procesamiento
- [Kibana](https://www.elastic.co/kibana/): Visualización

**Alternativas:**
- [Loki](https://grafana.com/oss/loki/) + Grafana (más liviano)
- [Splunk](https://www.splunk.com/) (enterprise)
- [Datadog Logs](https://www.datadoghq.com/product/log-management/)

---

## 📊 Metrics (Métricas)

**What:** Valores numéricos agregados en el tiempo.

| Framework | What | When | Ejemplo |
|:----------|:-----|:-----|:--------|
| **RED** | Rate, Errors, Duration | User-facing services | requests/sec, error rate %, p95 latency |
| **USE** | Utilization, Saturation, Errors | Resources (CPU, disk) | CPU %, queue depth, disk errors |
| **Golden Signals** | Latency, Traffic, Errors, Saturation | Google SRE approach | p99 latency, QPS, 5xx rate, memory % |

### Tipos de Métricas

| Tipo | What | When | Ejemplo |
|:-----|:-----|:-----|:--------|
| **Counter** | Solo aumenta (nunca decrece) | Total requests, errores | `http_requests_total` |
| **Gauge** | Valor que sube y baja | Memoria, CPU, connections activas | `active_connections` |
| **Histogram** | Distribución de valores | Latencias, tamaños de response | `http_request_duration_seconds` |
| **Summary** | Percentiles precalculados | Latencias (client-side) | p50, p95, p99 |

### Herramientas

| Tool | What | Why | How |
|:-----|:-----|:----|:----|
| [Prometheus](https://prometheus.io/) | Time-series DB con pull model | Estándar de facto, PromQL potente | Exponer `/metrics`, Prometheus scrapes cada 15s |
| [Grafana](https://grafana.com/) | Dashboards para múltiples fuentes | Visualización flexible | Datasource → Query → Panel |
| [StatsD](https://github.com/statsd/statsd) | Aggregation daemon con push model | Fácil instrumentar | Cliente envía UDP, StatsD agrega |
| [Micrometer](https://micrometer.io/) | Facade para métricas (Java) | Vendor-neutral | Exportar a Prometheus, Datadog, etc. |

---

## 🔍 Tracing (Trazas Distribuidas)

**What:** Seguir una request a través de múltiples servicios.

**Why:** En microservicios, una operación toca N servicios. Tracing muestra el path completo.

| Componente | What | How | Herramientas |
|:-----------|:-----|:----|:-------------|
| **Trace** | Request completo (raíz a hojas) | ID único propagado por headers | `X-B3-TraceId` |
| **Span** | Operación individual dentro de trace | Parent-child relationships | `POST /users` (50ms) → `INSERT INTO users` (30ms) |
| **Context Propagation** | Pasar trace_id entre servicios | Headers HTTP, gRPC metadata | [OpenTelemetry](https://opentelemetry.io/) |
| **Sampling** | Solo trazar % de requests | Reducir overhead | 1% en prod (high traffic), 100% en staging |

### Herramientas

| Tool | What | Why | When |
|:-----|:-----|:----|:-----|
| [Jaeger](https://www.jaegertracing.io/) | Tracing distribuido (Uber) | Open source, escalable | Microservicios con alta complejidad |
| [Zipkin](https://zipkin.io/) | Tracing distribuido (Twitter) | Maduro, ampliamente adoptado | Alternativa a Jaeger |
| [OpenTelemetry](https://opentelemetry.io/) | Estándar unificado (logs+metrics+traces) | Vendor-neutral, CNCF | Reemplazo de OpenTracing+OpenCensus |
| [AWS X-Ray](https://aws.amazon.com/xray/) | Tracing para servicios AWS | Integración nativa | Apps en AWS |

---

## 🏥 Health Checks

**What:** Endpoints para validar estado del servicio.

| Tipo | What | When | Endpoint | Valida |
|:-----|:-----|:-----|:---------|:-------|
| **Liveness** | ¿Está vivo el proceso? | K8s reinicia si falla | `/live` o `/healthz` | Proceso responde |
| **Readiness** | ¿Listo para recibir tráfico? | K8s no envía tráfico si falla | `/ready` | DB conectada, dependencias OK |
| **Startup** | ¿Terminó inicialización? | K8s espera antes de liveness | `/startup` | Warmup completado |

**Ejemplo:**
```json
GET /ready
{
  "status": "healthy",
  "checks": {
    "database": "ok",
    "redis": "ok",
    "external_api": "degraded"
  },
  "uptime": "3d 14h 22m"
}
```

---

## 🚨 Alerting (Alertas)

**What:** Notificaciones automáticas ante problemas.

**Why:** Detectar y responder antes que usuarios reporten.

| Concepto | What | How |
|:---------|:-----|:----|
| **Threshold** | Valor que dispara alerta | `error_rate > 5%` |
| **Window** | Periodo de evaluación | Últimos 5 minutos |
| **Severity** | Nivel de urgencia | Critical → page, Warning → ticket |
| **Runbook** | Guía paso a paso para resolver | Link en alerta |
| **On-call Rotation** | Quién responde | PagerDuty, Opsgenie |

### Herramientas

| Tool | What | When |
|:-----|:-----|:-----|
| [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) | Alertas de Prometheus | Stack Prometheus |
| [PagerDuty](https://www.pagerduty.com/) | Incident management | Equipos on-call |
| [Opsgenie](https://www.atlassian.com/software/opsgenie) | Alertas + escalations | Alternativa PagerDuty |

**Ejemplo Prometheus Alert:**
```yaml
- alert: HighErrorRate
  expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.05
  for: 5m
  labels:
    severity: critical
  annotations:
    summary: "High error rate on {{ $labels.instance }}"
    description: "Error rate is {{ $value | humanizePercentage }}"
```

---

## 📈 APM (Application Performance Monitoring)

**What:** Monitoreo end-to-end de aplicaciones con profiling automático.

**Why:** Detecta N+1 queries, memory leaks, slow transactions sin instrumentación manual.

| Tool | What | When |
|:-----|:-----|:-----|
| [New Relic](https://newrelic.com/) | APM full-stack | Enterprise, soporte 24/7 |
| [Datadog APM](https://www.datadoghq.com/product/apm/) | APM + Infra + Logs | Unified platform |
| [Elastic APM](https://www.elastic.co/apm) | APM integrado con ELK | Ya usas Elasticsearch |
| [Dynatrace](https://www.dynatrace.com/) | AI-powered APM | Apps complejas, auto-discovery |

---

## 🎯 SLIs, SLOs, SLAs

| Concepto | What | Ejemplo |
|:---------|:-----|:--------|
| **SLI** (Service Level Indicator) | Métrica que mide servicio | Latencia p95, error rate |
| **SLO** (Service Level Objective) | Target interno | p95 < 300ms en 99.9% requests |
| **SLA** (Service Level Agreement) | Contrato con usuario | 99.9% uptime, créditos si incumple |
| **Error Budget** | Cuánto downtime tolerable | 0.1% = 43 min/mes |

**Fórmula Error Budget:**
```
Error Budget = 100% - SLO
Si SLO = 99.9%, Error Budget = 0.1% = 43.2 min/mes
```

**Uso:** Si error budget consumido → pausar features, priorizar estabilidad.

---

## 📊 Dashboards

**Qué incluir:**

### Dashboard de Servicio
- Request rate (QPS)
- Error rate (%)
- Latencia (p50, p95, p99)
- Availability (uptime %)
- Active users

### Dashboard de Infraestructura
- CPU, Memory, Disk por nodo
- Network traffic
- Pod/container count
- Database connections

### Dashboard de Negocio
- Conversiones
- Revenue
- Active subscriptions

**Herramientas:** [Grafana](https://grafana.com/), [Kibana](https://www.elastic.co/kibana/), [Datadog](https://www.datadoghq.com/)

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Log everything** | Ruido, costo storage | Log lo relevante, sampling en high cardinality |
| **No correlation IDs** | Impossible rastrear request | Siempre trace_id + user_id |
| **Alertas no accionables** | Alert fatigue | Alerta solo si requiere acción humana |
| **Dashboards vanidosos** | Métricas que nadie usa | Medir SLIs reales, no proxies |
| **Sin runbooks** | Alerta sin guía de resolución | Todo alerta → runbook |

---

## 📚 Recursos

- [Google SRE Book - Monitoring](https://sre.google/sre-book/monitoring-distributed-systems/)
- [Prometheus Best Practices](https://prometheus.io/docs/practices/)
- [OpenTelemetry Docs](https://opentelemetry.io/docs/)
- [The Art of Monitoring - James Turnbull](https://artofmonitoring.com/)

---

[⬅️ Anterior: Seguridad](./06-seguridad.md) | [⬆️ Volver arriba](#07-observabilidad-y-telemetria) | [➡️ Siguiente: Optimización de Performance](./08-performance.md)