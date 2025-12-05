# 05 - DevOps

> Prácticas, herramientas y cultura para automatizar y unificar desarrollo, operaciones y entrega continua de software.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 ¿Qué es DevOps?](#que-es-devops)
- [🔄 CI/CD (Continuous Integration / Continuous Delivery)](#cicd-continuous-integration-continuous-delivery)
- [🏗️ IaC (Infrastructure as Code)](#iac-infrastructure-as-code)
- [📦 Contenedores y Orquestación](#contenedores-y-orquestacion)
- [🚀 Patrones de Despliegue](#patrones-de-despliegue)
- [🔒 GitOps](#gitops)
- [🛡️ Seguridad en CI/CD](#seguridad-en-cicd)
- [📊 Métricas DORA (DevOps Research and Assessment)](#metricas-dora-devops-research-and-assessment)
- [🔧 Herramientas Clave por Fase](#herramientas-clave-por-fase)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 ¿Qué es DevOps?

**What:** Cultura y conjunto de prácticas que combinan desarrollo (Dev) y operaciones (Ops) para entregar software de forma rápida, confiable y segura.

**Why:** Reduce tiempo de entrega, aumenta frecuencia de deploys, mejora calidad, acelera recuperación ante fallos.

**Who:** Developers, DevOps Engineers, SREs, Platform Engineers.

**How much:** Inversión inicial alta (3-6 meses setup), ROI continuo en velocidad y estabilidad.

---

## 🔄 CI/CD (Continuous Integration / Continuous Delivery)

**What:** Automatizar integración, testing y despliegue de código.

**Why:** Detecta problemas temprano, reduce "works on my machine", deploys predecibles.

| Componente | What | Why | When | How | Herramientas |
|:-----------|:-----|:----|:-----|:----|:-------------|
| **CI** | Integrar cambios frecuentemente con tests automáticos | Detectar conflictos/bugs rápido | Cada push, cada PR | Pipeline: checkout → build → test → report | [GitHub Actions](https://github.com/features/actions), [GitLab CI](https://docs.gitlab.com/ee/ci/), [Jenkins](https://www.jenkins.io/) |
| **CD** | Deploy automático a staging/producción | Reducir errores humanos, entregas rápidas | Tras merge a main (staging), manual/automático (prod) | Pipeline: build → test → package → deploy | [Argo CD](https://argo-cd.readthedocs.io/), [Spinnaker](https://spinnaker.io/) |
| **Pipelines** | Secuencia de pasos automatizados | Reproducibilidad, auditoría | Definir en código (YAML) | Stages paralelos, artifacts entre stages | [Tekton](https://tekton.dev/), [CircleCI](https://circleci.com/) |
| **Artifacts** | Empaquetado versionado de código | Desplegar mismo artifact en todos los ambientes | Tras build exitoso | Docker images, JARs, tarballs con SHA | [Artifactory](https://jfrog.com/artifactory/), [Nexus](https://www.sonatype.com/products/nexus-repository) |
| **Gates** | Validaciones obligatorias pre-deploy | Prevenir deploys rotos | Antes de producción | Tests pasan, cobertura >80%, security scan OK | GitHub Branch Protection, GitLab Protected Branches |

---

## 🏗️ IaC (Infrastructure as Code)

**What:** Gestionar infraestructura mediante código versionado.

**Why:** Reproducibilidad, auditoría, disaster recovery rápido.

| Herramienta | What | Why | When | How |
|:------------|:-----|:----|:-----|:----|
| [Terraform](https://www.terraform.io/) | Provisionar infraestructura multi-nube | Agnóstico de proveedor, state management | Infraestructura compleja, multi-cloud | HCL (`.tf`), plan → apply, state en S3/Terraform Cloud |
| [Pulumi](https://www.pulumi.com/) | IaC en lenguajes generales (TS, Python, Go) | Reutilizar lógica de programación | Equipos con fuerte background dev | Código TypeScript/Python, `pulumi up` |
| [Ansible](https://www.ansible.com/) | Configuración de servidores (CM) | Agentless, playbooks legibles | Configurar VMs, on-prem | YAML playbooks, SSH, idempotente |
| [Crossplane](https://www.crossplane.io/) | Provisionar infra desde Kubernetes | Unificar modelo de gestión | K8s-native environments | Custom Resources (CRDs), control loops |

---

## 📦 Contenedores y Orquestación

**What:** Empaquetar apps con sus dependencias, ejecutar en cualquier lado.

**Why:** "Funciona en mi máquina" → "Funciona en producción", escalabilidad.

| Tecnología | What | Why | When | How |
|:-----------|:-----|:----|:-----|:----|
| [Docker](https://www.docker.com/) | Crear y ejecutar contenedores | Portabilidad, aislamiento | Toda app moderna | `Dockerfile` → `docker build` → `docker run` |
| [Kubernetes](https://kubernetes.io/) | Orquestar contenedores a escala | Auto-healing, scaling, rolling updates | Producción con >3 servicios | Deployments, Services, Ingress, HPA |
| [Helm](https://helm.sh/) | Gestión de paquetes para K8s | Reutilizar manifests, versionado | Apps K8s complejas | Charts (templates YAML), `helm install` |
| [Podman](https://podman.io/) | Alternativa a Docker sin daemon | Seguridad (rootless), compatible Docker | Entornos restrictivos | CLI compatible con Docker |

---

## 🚀 Patrones de Despliegue

**What:** Estrategias para liberar código minimizando riesgo.

| Patrón | What | Why | When | How |
|:-------|:-----|:----|:-----|:----|
| **Rolling** | Actualizar pods/instancias progresivamente | Alta disponibilidad, rollback fácil | Siempre | K8s actualiza 1 pod, espera health check, sigue |
| **Blue-Green** | Dos entornos: blue (actual), green (nuevo) | Zero downtime, rollback instantáneo | Apps críticas | Cambiar tráfico de blue a green tras validación |
| **Canary** | Liberar a % pequeño de usuarios | Detectar problemas antes de 100% | Features arriesgadas | 5% tráfico → monitor → 25% → 50% → 100% |
| **Feature Flags** | Activar/desactivar features sin redeploy | Desplegar desacoplado de lanzamiento | Releases coordinados, A/B testing | Flags en DB/config, evaluar en runtime |
| **Shadow** | Ejecutar nueva versión sin exponer | Comparar outputs sin riesgo | Cambios críticos (ML models) | Traffic replicado a ambas versiones, solo actual responde |
| **Recreate** | Detener todo, desplegar nuevo | Simplicidad máxima | Entornos no críticos, mantenimiento | `kubectl delete` → `kubectl apply` |

---

## 🔒 GitOps

**What:** Git como única fuente de verdad para infraestructura y configuración.

**Why:** Auditoría completa, rollback vía git revert, declarativo.

**How:** 
1. Definir estado deseado en Git (YAML)
2. Operator detecta drift (diferencia estado real vs deseado)
3. Operator aplica cambios automáticamente

**Herramientas:** [Argo CD](https://argo-cd.readthedocs.io/), [Flux](https://fluxcd.io/), [Jenkins X](https://jenkins-x.io/)

---

## 🛡️ Seguridad en CI/CD

| Práctica | What | Why | How | Herramientas |
|:---------|:-----|:----|:----|:-------------|
| **SAST** | Static Application Security Testing | Detecta vulnerabilidades en código | Escanear código en CI | [SonarQube](https://www.sonarsource.com/products/sonarqube/), [Checkmarx](https://checkmarx.com/) |
| **DAST** | Dynamic Application Security Testing | Detecta vulnerabilidades en runtime | Probar app desplegada | [OWASP ZAP](https://www.zaproxy.org/), [Burp Suite](https://portswigger.net/burp) |
| **Dependency Scan** | Escanear librerías por CVEs | Actualizar dependencias vulnerables | Analizar `package.json`, `pom.xml` | [Snyk](https://snyk.io/), [Dependabot](https://github.com/dependabot) |
| **Container Scan** | Escanear imágenes Docker | Evitar desplegar vulnerabilidades | Escanear antes de push a registry | [Trivy](https://aquasecurity.github.io/trivy/), [Clair](https://github.com/quay/clair) |
| **Secrets Management** | No hardcodear credenciales | Prevenir leaks en Git | Variables de entorno, secrets managers | [Vault](https://www.vaultproject.io/), [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) |

---

## 📊 Métricas DORA (DevOps Research and Assessment)

| Métrica | What | Elite | High | Medium | Low |
|:--------|:-----|:------|:-----|:-------|:----|
| **Deployment Frequency** | Con qué frecuencia se deploya a prod | On-demand (múltiples por día) | Entre 1 día y 1 semana | Entre 1 semana y 1 mes | < 1 vez al mes |
| **Lead Time for Changes** | Tiempo desde commit hasta producción | < 1 hora | < 1 día | < 1 semana | > 1 semana |
| **MTTR** (Mean Time To Recover) | Tiempo para restaurar servicio tras fallo | < 1 hora | < 1 día | < 1 semana | > 1 semana |
| **Change Failure Rate** | % de deploys que causan fallo | 0-15% | 16-30% | 31-45% | > 45% |

**Objetivo:** Alcanzar niveles High o Elite para ser competitivos.

---

## 🔧 Herramientas Clave por Fase

### Build & Test
- [Maven](https://maven.apache.org/), [Gradle](https://gradle.org/) (Java)
- [npm](https://www.npmjs.com/), [pnpm](https://pnpm.io/) (Node.js)
- [Poetry](https://python-poetry.org/), [pip](https://pip.pypa.io/) (Python)

### CI/CD
- [GitHub Actions](https://github.com/features/actions)
- [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)
- [Jenkins](https://www.jenkins.io/)
- [CircleCI](https://circleci.com/)

### Container Registry
- [Docker Hub](https://hub.docker.com/)
- [AWS ECR](https://aws.amazon.com/ecr/)
- [Google Artifact Registry](https://cloud.google.com/artifact-registry)

### Orchestration
- [Kubernetes](https://kubernetes.io/)
- [Docker Swarm](https://docs.docker.com/engine/swarm/)
- [Nomad](https://www.nomadproject.io/)

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Snowflake Servers** | Servidores únicos configurados manualmente | IaC + contenedores inmutables |
| **Config Drift** | Entornos staging ≠ producción | GitOps, IaC, identical configs |
| **Manual Deploys** | Error humano, no reproducible | CI/CD full automation |
| **Long-lived Branches** | Integration hell | Trunk-based development, feature flags |
| **Shared CI Server** | Builds lentos, colas | Runners paralelos, caching |

---

## 📚 Recursos

- [The DevOps Handbook](https://itrevolution.com/product/the-devops-handbook-second-edition/)
- [Accelerate (State of DevOps)](https://cloud.google.com/devops/state-of-devops)
- [Kubernetes Patterns - O'Reilly](https://www.oreilly.com/library/view/kubernetes-patterns/9781492050278/)
- [GitOps with Argo CD](https://argo-cd.readthedocs.io/)

---

[⬅️ Anterior: Arquitectura y Patrones](./04-arquitectura-patrones.md) | [⬆️ Volver arriba](#05-devops) | [➡️ Siguiente: Seguridad](./06-seguridad.md)