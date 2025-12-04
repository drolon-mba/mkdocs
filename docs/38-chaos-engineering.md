# 38 - Chaos Engineering y Resiliencia

> Principios y prácticas de Chaos Engineering para construir sistemas resilientes.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [💥 Chaos Engineering Principles](#chaos-engineering-principles)
- [🔧 Failure Injection](#failure-injection)
- [🎮 Game Days](#game-days)
- [🛡️ Resiliencia Patterns](#resiliencia-patterns)
- [📋 Artefactos](#artefactos)

---

## 💥 Chaos Engineering Principles

### Qué es Chaos Engineering

**Definición:** Disciplina de experimentar en sistemas distribuidos para construir confianza en su capacidad de resistir condiciones turbulentas.

**Principios:**
1. **Hipótesis sobre steady state**: Definir qué es "normal"
2. **Variar eventos del mundo real**: Simular fallos realistas
3. **Ejecutar experimentos en producción**: Donde importa
4. **Automatizar experimentos**: Ejecutar continuamente
5. **Minimizar blast radius**: Empezar pequeño, escalar gradualmente

---

### Proceso

```
1. Define Steady State
   ↓
2. Hypothesize
   ↓
3. Run Experiment
   ↓
4. Verify Hypothesis
   ↓
5. Learn & Improve
```

---

## 🔧 Failure Injection

### Tipos de Fallos

| Tipo | Descripción | Herramienta |
|:-----|:------------|:------------|
| **Network latency** | Agregar delay a requests | Toxiproxy, Chaos Mesh |
| **Service failure** | Matar pods/servicios | Chaos Monkey, Chaos Mesh |
| **Resource exhaustion** | CPU/memory/disk al 100% | Gremlin, Chaos Toolkit |
| **DNS failure** | Resolver DNS falla | Chaos Mesh |
| **Clock skew** | Desincronizar relojes | Chaos Mesh |

---

### Ejemplo: Network Latency con Toxiproxy

```bash
# Instalar Toxiproxy
docker run -d -p 8474:8474 -p 8000-8010:8000-8010 shopify/toxiproxy

# Crear proxy para DB
toxiproxy-cli create database -l localhost:8001 -u postgres:5432

# Agregar latency de 1000ms
toxiproxy-cli toxic add database -t latency -a latency=1000

# Remover latency
toxiproxy-cli toxic remove database -n latency_downstream
```

---

### Ejemplo: Chaos Mesh (Kubernetes)

```yaml
# Matar pods aleatoriamente
apiVersion: chaos-mesh.org/v1alpha1
kind: PodChaos
metadata:
  name: pod-kill-example
spec:
  action: pod-kill
  mode: one
  selector:
    namespaces:
      - production
    labelSelectors:
      app: payment-service
  scheduler:
    cron: "@every 10m"
```

```yaml
# Network delay
apiVersion: chaos-mesh.org/v1alpha1
kind: NetworkChaos
metadata:
  name: network-delay
spec:
  action: delay
  mode: all
  selector:
    namespaces:
      - production
    labelSelectors:
      app: api-gateway
  delay:
    latency: "500ms"
    correlation: "50"
    jitter: "100ms"
  duration: "5m"
```

---

## 🎮 Game Days

### Qué es un Game Day

**Definición:** Simulación de incidente para entrenar equipos en respuesta.

**Objetivos:**
- Validar runbooks
- Entrenar on-call
- Identificar gaps en monitoring/alerting
- Mejorar comunicación

---

### Planificación

```markdown
# Game Day Plan: Database Outage

**Date:** YYYY-MM-DD
**Duration:** 2 hours
**Participants:** On-call SRE, Tech Lead, PM

## Scenario
Simular outage de base de datos principal.

## Hypothesis
- Equipo detecta outage en <5 min
- Failover a replica en <15 min
- Sistema recuperado en <30 min

## Execution
1. **T+0**: Inyectar fallo (matar DB pod)
2. **T+0-5**: Equipo detecta via alertas
3. **T+5-15**: Equipo ejecuta runbook de failover
4. **T+15-30**: Verificar que sistema está estable

## Success Criteria
- [ ] Alerta recibida en <5 min
- [ ] Failover ejecutado en <15 min
- [ ] 0 data loss
- [ ] Runbook seguido correctamente

## Rollback Plan
Si experimento causa impacto real:
1. Detener inyección de fallo
2. Restaurar DB desde backup
3. Comunicar a stakeholders
```

---

## 🛡️ Resiliencia Patterns

### Circuit Breaker

**Qué hace:** Detecta cuando servicio está fallando y deja de llamarlo temporalmente.

**Estados:**
- **Closed**: Normal, requests pasan
- **Open**: Servicio fallando, requests fallan inmediatamente
- **Half-Open**: Probar si servicio se recuperó

**Ejemplo (Python):**
```python
from pybreaker import CircuitBreaker

# Configurar circuit breaker
breaker = CircuitBreaker(
    fail_max=5,  # Abrir después de 5 fallos
    timeout_duration=60  # Intentar cerrar después de 60s
)

@breaker
def call_payment_service(amount):
    response = requests.post('https://payment-api.com/charge', json={'amount': amount})
    response.raise_for_status()
    return response.json()

# Usar
try:
    result = call_payment_service(100)
except CircuitBreakerError:
    # Circuit está abierto, servicio está down
    return {"error": "Payment service unavailable"}
```

---

### Retry with Backoff

**Qué hace:** Reintentar requests fallidos con delay exponencial.

**Ejemplo:**
```python
import time
from functools import wraps

def retry_with_backoff(max_retries=3, base_delay=1):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_retries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_retries - 1:
                        raise
                    delay = base_delay * (2 ** attempt)  # Exponential backoff
                    time.sleep(delay)
        return wrapper
    return decorator

@retry_with_backoff(max_retries=3, base_delay=1)
def call_api():
    response = requests.get('https://api.example.com/data')
    response.raise_for_status()
    return response.json()
```

---

### Bulkhead

**Qué hace:** Aislar recursos para que fallo en un área no afecte otras.

**Ejemplo (Thread Pools):**
```python
from concurrent.futures import ThreadPoolExecutor

# Pool separado para cada servicio
payment_pool = ThreadPoolExecutor(max_workers=10)
notification_pool = ThreadPoolExecutor(max_workers=5)

# Si payment service se satura, notification sigue funcionando
payment_pool.submit(process_payment, order_id)
notification_pool.submit(send_email, user_id)
```

---

### Timeout

**Qué hace:** Limitar tiempo de espera para evitar bloqueos indefinidos.

**Ejemplo:**
```python
import requests

# ❌ MAL: Sin timeout (puede bloquearse indefinidamente)
response = requests.get('https://slow-api.com/data')

# ✅ BIEN: Con timeout
try:
    response = requests.get('https://slow-api.com/data', timeout=5)
except requests.Timeout:
    return {"error": "Request timed out"}
```

---

## 📋 Artefactos

### Chaos Experiment Template

```markdown
# Chaos Experiment: [Título]

**Date:** YYYY-MM-DD
**Owner:** [Name]
**Status:** [Planned / Running / Completed]

## Hypothesis
[Qué esperamos que pase]

Ejemplo: "Si matamos un pod de payment-service, Kubernetes lo recreará en <30s y no habrá downtime perceptible"

## Steady State
[Cómo se ve el sistema "normal"]

Metrics:
- Latency p99: <200ms
- Error rate: <0.1%
- Throughput: 100 RPS

## Blast Radius
[Qué tan grande es el impacto]

- **Scope**: Solo payment-service en staging
- **Duration**: 5 minutos
- **Affected users**: 0 (staging)

## Experiment Steps

### 1. Verify Steady State
- [ ] Check metrics (latency, error rate, throughput)
- [ ] Verify all pods are healthy

### 2. Inject Failure
```bash
kubectl delete pod -n staging -l app=payment-service --force
```

### 3. Observe
- [ ] Monitor metrics
- [ ] Check logs
- [ ] Verify alerts fired

### 4. Verify Recovery
- [ ] New pod created
- [ ] Metrics back to steady state
- [ ] No errors in logs

## Results

**Hypothesis:** [Confirmed / Rejected]

**Observations:**
- [Observation 1]
- [Observation 2]

**Metrics:**
| Metric | Before | During | After |
|:-------|:-------|:-------|:------|
| Latency p99 | 150ms | 180ms | 155ms |
| Error rate | 0.05% | 0.08% | 0.05% |

## Action Items
- [ ] [Action 1]
- [ ] [Action 2]
```

---

### Game Day Runbook

```markdown
# Game Day Runbook: [Scenario]

**Scenario:** [Descripción del incidente simulado]
**Duration:** [Tiempo estimado]
**Participants:** [Roles necesarios]

## Pre-Game Day

### 1 Week Before
- [ ] Comunicar a equipo (fecha, hora, escenario)
- [ ] Preparar scripts de inyección de fallo
- [ ] Verificar que rollback funciona

### 1 Day Before
- [ ] Reminder a participantes
- [ ] Verificar que monitoring está funcionando
- [ ] Preparar war room (Zoom/Slack channel)

## During Game Day

### T-15 min: Setup
- [ ] Todos en war room
- [ ] Verificar steady state
- [ ] Explicar escenario

### T+0: Inject Failure
```bash
[Comando para inyectar fallo]
```

### T+0-30: Observe
- [ ] Equipo detecta incidente
- [ ] Incident Commander asignado
- [ ] Runbook ejecutado
- [ ] Sistema recuperado

### T+30: Debrief
- [ ] ¿Qué salió bien?
- [ ] ¿Qué salió mal?
- [ ] Action items

## Post-Game Day

### Same Day
- [ ] Escribir summary
- [ ] Crear tickets para action items
- [ ] Comunicar resultados a stakeholders

### 1 Week After
- [ ] Verificar que action items están en progreso
- [ ] Planear próximo Game Day
```

---

### Resiliencia Checklist

```markdown
# Resiliencia Checklist

## Patterns Implementados

### Circuit Breaker
- [ ] Implementado para llamadas a servicios externos
- [ ] Thresholds configurados (fail_max, timeout)
- [ ] Fallback behavior definido
- [ ] Metrics expuestas (circuit state, failures)

### Retry with Backoff
- [ ] Implementado para requests transitorios
- [ ] Exponential backoff configurado
- [ ] Max retries definido
- [ ] Idempotencia garantizada

### Bulkhead
- [ ] Thread pools separados por servicio
- [ ] Resource limits configurados (CPU, memory)
- [ ] Isolation verificada (fallo en A no afecta B)

### Timeout
- [ ] Timeouts configurados en todas las llamadas externas
- [ ] Valores razonables (no muy cortos ni muy largos)
- [ ] Timeout handling implementado

## Testing

### Chaos Experiments
- [ ] Experimentos definidos
- [ ] Ejecutados en staging
- [ ] Resultados documentados
- [ ] Action items completados

### Game Days
- [ ] Game Days planificados (al menos 1/quarter)
- [ ] Runbooks testeados
- [ ] Equipo entrenado

## Monitoring

### Metrics
- [ ] Latency (p50, p95, p99)
- [ ] Error rate
- [ ] Throughput
- [ ] Circuit breaker state

### Alerts
- [ ] Alertas configuradas para degradación
- [ ] On-call definido
- [ ] Runbooks vinculados a alertas
```

---

## 📚 Recursos

- [Principles of Chaos Engineering](https://principlesofchaos.org/)
- [Chaos Mesh](https://chaos-mesh.org/)
- [Gremlin](https://www.gremlin.com/)
- [Release It! - Michael Nygard](https://pragprog.com/titles/mnee2/release-it-second-edition/)

---

[⬅️ Anterior: Gestión de Secretos](./37-gestion-secretos.md) | [➡️ Siguiente: Data Literacy](./39-data-literacy.md) | [⬆️ Volver arriba](#38-chaos-engineering-y-resiliencia)
