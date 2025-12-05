# 37 - Gestión de Secretos

> Estrategias y herramientas para gestión segura de secretos, credenciales y configuración sensible.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🔐 Secret Management Tools](#secret-management-tools)
- [🔄 Secret Rotation](#secret-rotation)
- [🔒 Least Privilege](#least-privilege)
- [🚀 Secrets en CI/CD](#secrets-en-cicd)
- [🔍 Detección de Secretos](#deteccion-de-secretos)
- [📋 Artefactos](#artefactos)

---

## 🔐 Secret Management Tools

### Comparación

| Tool | Pros | Cons | Cuándo Usar |
|:-----|:-----|:-----|:------------|
| **HashiCorp Vault** | Flexible, audit logs, dynamic secrets | Complejidad operacional | Empresas, multi-cloud |
| **AWS Secrets Manager** | Integración nativa AWS, rotation automática | Lock-in AWS | Workloads en AWS |
| **Azure Key Vault** | Integración nativa Azure, HSM | Lock-in Azure | Workloads en Azure |
| **GCP Secret Manager** | Integración nativa GCP, simple | Lock-in GCP | Workloads en GCP |
| **Doppler** | UI amigable, multi-env | Costo | Startups, equipos pequeños |

---

### HashiCorp Vault - Ejemplo

```bash
# Inicializar Vault
vault operator init

# Unsealar Vault (requiere 3 de 5 keys)
vault operator unseal <key1>
vault operator unseal <key2>
vault operator unseal <key3>

# Login
vault login <root-token>

# Guardar secreto
vault kv put secret/database/config \
  username=dbuser \
  password=supersecret

# Leer secreto
vault kv get secret/database/config

# Crear policy (least privilege)
vault policy write app-policy - <<EOF
path "secret/data/database/config" {
  capabilities = ["read"]
}
EOF

# Crear token con policy
vault token create -policy=app-policy
```

---

## 🔄 Secret Rotation

### Por Qué Rotar Secretos

| Razón | Frecuencia Recomendada |
|:------|:-----------------------|
| **Compliance** (SOC2, PCI-DSS) | 90 días |
| **Secreto comprometido** | Inmediato |
| **Empleado deja la empresa** | Inmediato |
| **Best practice** | 30-90 días |

---

### Automated Rotation

**Ejemplo con AWS Secrets Manager:**

```python
import boto3
import json

def lambda_handler(event, context):
    """
    Lambda function para rotar secreto de DB.
    Triggered por AWS Secrets Manager cada 30 días.
    """
    service_client = boto3.client('secretsmanager')
    arn = event['SecretId']
    token = event['ClientRequestToken']
    step = event['Step']
    
    if step == "createSecret":
        # Generar nueva password
        new_password = generate_random_password()
        
        # Guardar en "pending" version
        service_client.put_secret_value(
            SecretId=arn,
            ClientRequestToken=token,
            SecretString=json.dumps({"password": new_password}),
            VersionStages=['AWSPENDING']
        )
    
    elif step == "setSecret":
        # Actualizar password en DB
        pending_secret = get_secret_version(arn, "AWSPENDING")
        update_database_password(pending_secret['password'])
    
    elif step == "testSecret":
        # Verificar que nueva password funciona
        pending_secret = get_secret_version(arn, "AWSPENDING")
        test_database_connection(pending_secret['password'])
    
    elif step == "finishSecret":
        # Marcar nueva version como "current"
        service_client.update_secret_version_stage(
            SecretId=arn,
            VersionStage='AWSCURRENT',
            MoveToVersionId=token
        )
```

---

### Zero-Downtime Rotation

**Estrategia:**
1. Crear nueva credencial (sin invalidar la vieja)
2. Deployar aplicación con nueva credencial
3. Verificar que funciona
4. Invalidar credencial vieja

---

## 🔒 Least Privilege

### IAM Policies (AWS)

**❌ MAL (demasiado permisivo):**
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "*",
    "Resource": "*"
  }]
}
```

**✅ BIEN (least privilege):**
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": "arn:aws:secretsmanager:us-east-1:123456789:secret:prod/database/*"
  }]
}
```

---

### Service Accounts (Kubernetes)

```yaml
# Service Account con RBAC
apiVersion: v1
kind: ServiceAccount
metadata:
  name: app-service-account
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  resourceNames: ["database-credentials"]
  verbs: ["get"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-secrets
subjects:
- kind: ServiceAccount
  name: app-service-account
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 🚀 Secrets en CI/CD

### GitHub Actions

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      # ❌ MAL: Secreto en código
      # - run: echo "PASSWORD=supersecret" >> .env
      
      # ✅ BIEN: Secreto desde GitHub Secrets
      - name: Deploy
        env:
          DATABASE_PASSWORD: ${{ secrets.DATABASE_PASSWORD }}
          API_KEY: ${{ secrets.API_KEY }}
        run: |
          # Secretos disponibles como env vars
          ./deploy.sh
```

---

### Evitar Secretos en Logs

```yaml
# ❌ MAL: Secreto puede aparecer en logs
- run: echo "Connecting with password ${{ secrets.PASSWORD }}"

# ✅ BIEN: Mask secretos
- run: |
    echo "::add-mask::${{ secrets.PASSWORD }}"
    # Ahora el secreto será reemplazado por *** en logs
```

---

## 🔍 Detección de Secretos

### Pre-Commit Hooks

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.4.0
    hooks:
      - id: detect-secrets
        args: ['--baseline', '.secrets.baseline']
```

---

### TruffleHog

```bash
# Escanear repo completo (incluyendo historia)
trufflehog git file://. --only-verified

# Escanear solo cambios recientes
trufflehog git file://. --since-commit HEAD~10

# Escanear antes de push
git diff --staged | trufflehog --no-update
```

---

### git-secrets

```bash
# Instalar hooks
git secrets --install

# Agregar patterns a detectar
git secrets --add 'password\s*=\s*.+'
git secrets --add 'api[_-]?key\s*=\s*.+'
git secrets --add --allowed 'example.com'  # Whitelist

# Escanear
git secrets --scan
```

---

## 📋 Artefactos

### Secret Management Checklist

```markdown
# Secret Management Checklist

## Storage
- [ ] Secretos NO están en código
- [ ] Secretos NO están en .env commiteado
- [ ] Secretos están en secret manager (Vault, AWS Secrets Manager, etc)
- [ ] Secretos están encriptados at-rest

## Access Control
- [ ] Least privilege (solo quien necesita tiene acceso)
- [ ] Service accounts (no usar credenciales personales)
- [ ] MFA habilitado para acceso a secretos críticos
- [ ] Audit logs habilitados

## Rotation
- [ ] Secretos críticos rotan cada 90 días
- [ ] Rotation es automática (no manual)
- [ ] Zero-downtime rotation implementada
- [ ] Proceso de rotation documentado

## CI/CD
- [ ] Secretos inyectados como env vars (no hardcoded)
- [ ] Secretos masked en logs
- [ ] Secretos no persisten en artifacts

## Detection
- [ ] Pre-commit hooks configurados (detect-secrets, trufflehog)
- [ ] Escaneo periódico de repo (git-secrets)
- [ ] Alertas si secreto se detecta en código

## Incident Response
- [ ] Playbook para secreto comprometido
- [ ] Contactos de emergencia documentados
- [ ] Proceso de rotation de emergencia testeado
```

---

### Vault Setup Guide

```markdown
# HashiCorp Vault Setup Guide

## 1. Instalación

### Docker (desarrollo)
```bash
docker run -d --name=vault \
  -p 8200:8200 \
  --cap-add=IPC_LOCK \
  vault server -dev
```

### Producción (Kubernetes)
```bash
helm repo add hashicorp https://helm.releases.hashicorp.com
helm install vault hashicorp/vault \
  --set server.ha.enabled=true \
  --set server.ha.replicas=3
```

## 2. Inicialización

```bash
# Inicializar (solo primera vez)
vault operator init -key-shares=5 -key-threshold=3

# Guardar unseal keys y root token de forma segura
# NUNCA commitear estos valores

# Unsealar (requiere 3 de 5 keys)
vault operator unseal <key1>
vault operator unseal <key2>
vault operator unseal <key3>
```

## 3. Configuración

```bash
# Login
export VAULT_ADDR='http://localhost:8200'
vault login <root-token>

# Habilitar KV secrets engine
vault secrets enable -path=secret kv-v2

# Crear secreto
vault kv put secret/myapp/config \
  db_password=supersecret \
  api_key=abc123
```

## 4. Policies

```bash
# Crear policy para app
vault policy write myapp-policy - <<EOF
path "secret/data/myapp/*" {
  capabilities = ["read"]
}
EOF

# Crear token con policy
vault token create -policy=myapp-policy
```

## 5. Integración con App

```python
import hvac

# Conectar a Vault
client = hvac.Client(url='http://localhost:8200', token='<app-token>')

# Leer secreto
secret = client.secrets.kv.v2.read_secret_version(path='myapp/config')
db_password = secret['data']['data']['db_password']
```
```

---

### Secret Leak Response Playbook

```markdown
# Secret Leak Response Playbook

## Detection
**Alerta:** Secreto detectado en código / logs / público

## Immediate Actions (0-15 min)

### 1. Assess Severity
- [ ] ¿Qué secreto se expuso? (DB password, API key, etc)
- [ ] ¿Dónde se expuso? (GitHub público, logs, Slack)
- [ ] ¿Cuánto tiempo estuvo expuesto?

### 2. Revoke Secret
- [ ] Invalidar secreto inmediatamente
- [ ] Rotar a nuevo secreto
- [ ] Verificar que nuevo secreto funciona

### 3. Remove from Source
- [ ] Remover de código (git revert + force push)
- [ ] Remover de logs (si es posible)
- [ ] Remover de caches

## Investigation (15-60 min)

### 4. Audit Access
- [ ] Revisar audit logs (¿alguien usó el secreto?)
- [ ] Identificar accesos sospechosos
- [ ] Determinar blast radius

### 5. Assess Damage
- [ ] ¿Hubo acceso no autorizado?
- [ ] ¿Se comprometieron datos?
- [ ] ¿Se requiere notificación a usuarios/reguladores?

## Remediation (1-24 hours)

### 6. Fix Root Cause
- [ ] Implementar pre-commit hooks
- [ ] Educar al equipo
- [ ] Revisar procesos

### 7. Post-Mortem
- [ ] Escribir post-mortem
- [ ] Identificar action items
- [ ] Asignar responsables

## Communication

### Internal
- Slack #security: "Secret leak detected, investigating"
- Update cada 30 min

### External (si aplica)
- Notificar a usuarios afectados
- Notificar a reguladores (GDPR, etc)
```

---

## 📚 Recursos

- [HashiCorp Vault](https://www.vaultproject.io/)
- [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
- [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html)
- [detect-secrets](https://github.com/Yelp/detect-secrets)

---

[⬅️ Anterior: Priorización y Roadmapping](./36-priorizacion-roadmapping.md) | [⬆️ Volver arriba](#37-gestion-de-secretos) | [➡️ Siguiente: Chaos Engineering](./38-chaos-engineering.md)
