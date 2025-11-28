# 22 - Optimización de Costos (FinOps)

> Prácticas para maximizar valor de inversión en cloud y recursos tecnológicos.

[🏠 Volver al índice](./00-indice.md)

---

## 💰 FinOps (Financial Operations)

**What:** Disciplina de gestión financiera cloud que une finanzas, tecnología y negocio.

**Why:** Cloud = OpEx variable. Sin control, costos crecen exponencialmente.

**Who:** DevOps, FinOps Engineers, CFO, engineering leads.

**When:** Desde día 1 en cloud, revisar mensualmente.

**How much:** FinOps bien ejecutado ahorra 20-40% costos cloud.

---

## 📊 Fases FinOps

| Fase | What | Actividades |
|:-----|:-----|:------------|
| **Inform** | Visibilidad total | Tagging, dashboards, chargeback |
| **Optimize** | Reducir waste | Right-sizing, RIs, eliminar recursos idle |
| **Operate** | Cultura continua | Alertas, governance, automation |

---

## 🏷️ Tagging Strategy

**What:** Etiquetar recursos cloud con metadata.

**Why:** Trackear costos por proyecto/equipo/ambiente, accountability.

**When:** Aplicar tags en creación de recursos (policy enforcement).

**Tags obligatorios:**

| Tag | Ejemplo | Uso |
|:----|:--------|:----|
| `Environment` | prod, staging, dev | Separar ambientes |
| `Project` | payments, analytics | Chargeback por proyecto |
| `Owner` | team-platform, alice@company.com | Ownership |
| `CostCenter` | engineering, marketing | Contabilidad |
| `Application` | api, frontend | Agrupar componentes |

**Ejemplo AWS:**
```json
{
  "Environment": "production",
  "Project": "payments-api",
  "Owner": "team-platform",
  "CostCenter": "engineering",
  "Application": "api"
}
```

**Enforcement:** Policies que rechazan recursos sin tags obligatorios.

---

## 📏 Right-Sizing

**What:** Ajustar tamaño de recursos al uso real.

**Why:** Ahorro 20-40% eliminando over-provisioning.

**When:** Revisar mensual, automatizar recomendaciones.

**Proceso:**
1. Monitorear uso real (CPU, memoria, disk)
2. Identificar recursos sobre-dimensionados (<40% uso)
3. Cambiar a instancia más pequeña
4. Validar performance

**Ejemplo:**
```
EC2 m5.4xlarge (16 vCPU, 64GB RAM)
  Uso real: 20% CPU, 30% RAM
  → Cambiar a m5.xlarge (4 vCPU, 16GB)
  Ahorro: $450/mes → $112/mes = $338/mes (75%)
```

**Herramientas:** [AWS Compute Optimizer](https://aws.amazon.com/compute-optimizer/), [Google Recommender](https://cloud.google.com/recommender), [CloudHealth](https://www.cloudhealthtech.com/)

---

## 💳 Reserved Instances & Savings Plans

**What:** Compromiso de uso 1-3 años a cambio de descuento.

| Tipo | Compromiso | Descuento | Flexibilidad | Cuándo |
|:-----|:-----------|:----------|:-------------|:-------|
| **On-Demand** | Ninguno | 0% | Total | Carga variable |
| **Savings Plans** | $/hora, 1-3 años | 30-50% | Alta (tipo instancia) | Carga estable |
| **Reserved Instances** | Instancia específica, 1-3 años | 40-70% | Baja | Carga muy predecible |
| **Spot Instances** | Puede terminar | 70-90% | Ninguna | Workloads tolerantes |

**Estrategia recomendada:**
- 60% Savings Plans (baseline predecible)
- 20% On-Demand (flexibilidad)
- 20% Spot (batch jobs, dev)

**ROI Ejemplo:**
```
Workload: 10 instancias m5.large 24/7
On-Demand: $700/mes × 10 = $7,000/mes

Con Savings Plan 1 año:
$7,000 × 0.6 (40% descuento) = $4,200/mes
Ahorro: $2,800/mes = $33,600/año
```

---

## ⚡ Spot Instances

**What:** Capacidad no utilizada con descuento masivo pero puede interrumpirse.

**Why:** 70-90% descuento para workloads fault-tolerant.

**When:** Batch processing, CI/CD, big data, testing.

**Patrones:**

| Pattern | What | Ejemplo |
|:--------|:-----|:--------|
| **Stateless apps** | Sin estado local | Workers procesando cola |
| **Checkpointing** | Guardar estado periódicamente | ML training con S3 checkpoints |
| **Spot Fleet** | Mezcla tipos instancias | Diversificar para disponibilidad |
| **Fallback a On-Demand** | Si no hay Spot disponible | ECS con Spot + On-Demand |

**Interrupción:**
- AWS da 2 min warning
- Handler: checkpoint, guardar estado, shutdown graceful

---

## 📉 Eliminar Waste

| Waste | What | Cómo detectar | Solución |
|:------|:-----|:--------------|:---------|
| **Recursos idle** | Recursos sin uso | CPU <5%, network mínimo | Apagar fuera horario, auto-stop |
| **Snapshots antiguos** | Backups obsoletos | >90 días | Lifecycle policy automático |
| **EBS unattached** | Discos sin instancia | Filter: available | Eliminar tras verificar |
| **Load Balancers vacíos** | LBs sin targets | 0 registered targets | Eliminar |
| **IPs elásticas sin usar** | IPs no asociadas | Charges por IP sin asociar | Release IPs |

**Ejemplo savings:**
```
10 snapshots viejos × $0.05/GB × 100GB = $50/mes
5 EBS unattached × 100GB × $0.10/GB = $50/mes
3 IPs elásticas × $3.6/mes = $10.8/mes
Total: $110.8/mes eliminado ✅
```

---

## ⏰ Scheduling (Apagar recursos)

**What:** Apagar recursos en horarios sin uso.

**Why:** Ahorro 50-70% en ambientes no-prod.

**When:** Dev, staging, QA (no 24/7 necesarios).

**Ejemplo:**
```
Ambiente Dev:
  - 20 instancias
  - Uso: Lunes-Viernes 8am-8pm (12h/día = 60h/semana)
  - Apagar: Noches + weekends (108h/semana)

Ahorro: 108/168 = 64% del costo
$5,000/mes → $1,800/mes = $3,200/mes ahorro
```

**Automatización:**
- AWS Instance Scheduler
- Lambda con CloudWatch Events
- Tags: `AutoStop: true`, `Schedule: business-hours`

---

## 📦 Storage Optimization

### S3 Storage Classes

| Class | Latency | Costo | Uso |
|:------|:--------|:------|:----|
| **Standard** | ms | $0.023/GB | Acceso frecuente |
| **Intelligent-Tiering** | ms | Auto-optimiza | Patrón desconocido |
| **Infrequent Access** | ms | $0.0125/GB | Acceso mensual |
| **Glacier** | minutos-horas | $0.004/GB | Archivos long-term |
| **Deep Archive** | horas | $0.00099/GB | Compliance 7+ años |

**Lifecycle Policy:**
```json
{
  "Rules": [{
    "Status": "Enabled",
    "Transitions": [
      {"Days": 30, "StorageClass": "STANDARD_IA"},
      {"Days": 90, "StorageClass": "GLACIER"},
      {"Days": 365, "StorageClass": "DEEP_ARCHIVE"}
    ],
    "Expiration": {"Days": 2555}
  }]
}
```

### EBS Optimization

- Cambiar GP2 → GP3 (20% cheaper, mismo performance)
- Eliminar snapshots >90 días
- Resize volumes over-provisioned

---

## 🌐 Network Costs

**What:** Data transfer OUT es costoso (típicamente $0.09/GB).

**Why:** Puede ser 10-30% de bill total.

**Optimización:**

| Técnica | Ahorro |
|:--------|:-------|
| **CloudFront CDN** | Cache assets, reduce origin requests | 60-80% |
| **S3 Transfer Acceleration** | Optimiza uploads globales | Variable |
| **VPC Endpoints** | Tráfico privado AWS (sin internet) | Evita $0.09/GB |
| **Compress responses** | Gzip/Brotli | 70-80% menos datos |
| **Same region** | Mantener recursos en misma región | Free intra-region |

---

## 📊 Cost Monitoring & Alerting

### Dashboards

**Secciones clave:**
1. **Spend by Service:** EC2, RDS, S3, etc.
2. **Spend by Environment:** prod, staging, dev
3. **Spend by Team:** Chargeback
4. **Trend:** MoM growth, forecasts
5. **Anomalies:** Spikes inesperados

### Alertas

```
Alert: Daily spend > $1,000
Alert: MoM growth > 20%
Alert: New service > $100/día
Alert: Recursos sin tags
```

**Herramientas:** [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/), [CloudWatch Billing Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html), [Datadog Cloud Cost](https://www.datadoghq.com/product/cloud-cost-management/)

---

## 🎯 FinOps KPIs

| Métrica | Target | Fórmula |
|:--------|:-------|:--------|
| **Savings Rate** | >20% | (Savings / Total Spend) × 100 |
| **RI/SP Coverage** | >70% | Horas covered / Total horas |
| **Untagged Resources** | 0% | Resources sin tags / Total |
| **Idle Resource %** | <5% | Costo recursos idle / Total |
| **Cost per Customer** | ↓ Over time | Total Spend / Active Customers |

---

## 🔄 FinOps Culture

### Shared Responsibility

| Stakeholder | Responsabilidad |
|:------------|:----------------|
| **Engineers** | Write efficient code, right-size, apagar recursos |
| **Architects** | Diseñar cost-effective, usar managed services |
| **Finance** | Budgets, forecasting, chargeback |
| **Leadership** | Priorizar cost optimization, KPIs |

### Best Practices

- **Showback/Chargeback:** Equipos ven su gasto
- **Cost in PRs:** Estimar costo de cambios
- **Budget alerts:** Notificar cuando se acerca límite
- **Regular reviews:** Mensual por equipo
- **Gamification:** Reconocer equipos que más ahorran

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Lift & shift sin optimizar** | Migrar infra sin cambios | Modernizar para cloud-native |
| **No monitorear costos** | Sorpresas en bill | Alertas, dashboards diarios |
| **Over-provisioning "por las dudas"** | Pagar capacidad no usada | Auto-scaling, right-sizing |
| **No usar managed services** | Mantener DBs propias | RDS, Aurora vs self-managed |
| **Ignorar dev/staging costs** | 40% del spend en no-prod | Scheduling, Spot instances |

---

## 📚 Recursos

- [FinOps Foundation](https://www.finops.org/)
- [AWS Cost Optimization](https://aws.amazon.com/aws-cost-management/)
- [Google Cloud Cost Optimization](https://cloud.google.com/cost-management)
- [Azure Cost Management](https://azure.microsoft.com/en-us/products/cost-management)

---

[⬅️ Anterior: Colaboración y Cultura](./21-colaboracion-cultura.md) | [⬆️ Volver arriba](#22---optimización-de-costos-finops) | [➡️ Siguiente: Data Governance](./23-data-governance.md)