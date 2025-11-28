# 27 - Checklist de Producción

> Validación exhaustiva antes de desplegar código a producción para minimizar riesgos y maximizar confiabilidad.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Pre-Deploy Checklist](#pre-deploy-checklist)
- [✅ Código y Testing](#codigo-y-testing)
- [🔒 Seguridad](#seguridad)
- [🗄️ Base de Datos](#base-de-datos)
- [📊 Performance](#performance)
- [🔍 Observabilidad](#observabilidad)
- [🌐 Infraestructura](#infraestructura)
- [📝 Documentación](#documentacion)
- [🔄 Proceso de Deploy](#proceso-de-deploy)
- [✅ Post-Deploy Verification](#post-deploy-verification)
- [🚨 Rollback Criteria](#rollback-criteria)
- [🎯 Checklist por Tipo de Change](#checklist-por-tipo-de-change)
- [📋 Sign-off](#sign-off)
- [🚫 Common Mistakes](#common-mistakes)
- [🎓 Mejora Continua](#mejora-continua)
- [📚 Recursos](#recursos)
- [✅ Final Approval](#final-approval)
- [🎉 ¡Checklist Completo!](#checklist-completo)
---

## 🎯 Pre-Deploy Checklist

**What:** Lista de verificación obligatoria antes de cualquier deploy a producción.

**Why:** Un deploy fallido puede costar $100k+/hora en downtime y reputación.

**Who:** Developer + reviewer + DevOps (según org).

**When:** Antes de CADA deploy a producción, sin excepciones.

**How much:** 10-30 min de verificación previene horas/días de incident response.

---

## ✅ Código y Testing

### Calidad de Código

- [ ] **Tests unitarios pasan al 100%**
  - Ejecutar: `npm test` / `pytest` / `mvn test`
  - Sin tests skippeados temporalmente
  
- [ ] **Tests de integración pasan**
  - Ejecutar suite completa
  - Validar integraciones con servicios externos
  
- [ ] **Code coverage ≥ 80% en lógica crítica**
  - Revisar reporte de coverage
  - Nuevas features tienen tests
  
- [ ] **Linter pasa sin errores**
  - `npm run lint` / `pylint` / `checkstyle`
  - Sin warnings críticos
  
- [ ] **Code review aprobado**
  - Mínimo 1 aprobación (2 para cambios críticos)
  - Comentarios resueltos
  - No hay "LGTM" superficial
  
- [ ] **Sin código comentado**
  - Eliminar código muerto
  - Usar control de versiones, no comentarios
  
- [ ] **Sin console.log / print debug**
  - Reemplazar con logging apropiado
  - Usar niveles correctos (DEBUG, INFO, WARN, ERROR)

---

## 🔒 Seguridad

- [ ] **Sin secrets hardcodeados**
  - Buscar: `git grep -i "password\|api_key\|secret"`
  - Usar variables de entorno / secrets manager
  
- [ ] **Dependencies sin vulnerabilidades críticas**
  - Ejecutar: `npm audit` / `snyk test`
  - Actualizar/patchear CVEs conocidos
  
- [ ] **Input validation implementada**
  - Validar todos los inputs de usuario
  - Sanitizar antes de queries DB
  
- [ ] **Output encoding (prevenir XSS)**
  - Escapar HTML en templates
  - Content-Security-Policy headers
  
- [ ] **Authentication & Authorization correctas**
  - Endpoints protegidos apropiadamente
  - Roles y permisos validados
  
- [ ] **HTTPS obligatorio**
  - Redirect HTTP → HTTPS
  - HSTS header configurado
  
- [ ] **CORS configurado correctamente**
  - No usar `Access-Control-Allow-Origin: *` en prod
  - Whitelist de origins permitidos

---

## 🗄️ Base de Datos

- [ ] **Migrations testeadas en staging**
  - Ejecutar en ambiente staging primero
  - Validar que no rompen datos existentes
  
- [ ] **Rollback plan para migrations**
  - Script de rollback probado
  - Backups recientes disponibles
  
- [ ] **Índices apropiados**
  - Queries optimizadas (EXPLAIN ANALYZE)
  - Sin N+1 queries
  
- [ ] **Backup reciente verificado**
  - Último backup < 24 horas
  - Restore testeado periódicamente
  
- [ ] **Connection pooling configurado**
  - No crear conexiones ilimitadas
  - Timeouts apropiados

---

## 📊 Performance

- [ ] **Load testing ejecutado**
  - Soporta carga esperada + 20%
  - p95 latency < 500ms
  
- [ ] **Sin memory leaks**
  - Profiling ejecutado
  - Memoria se libera correctamente
  
- [ ] **Assets optimizados**
  - Imágenes comprimidas (WebP, AVIF)
  - JS/CSS minificados
  - Gzip/Brotli habilitado
  
- [ ] **Caching implementado**
  - Cache headers HTTP
  - CDN configurado para assets
  - Redis/Memcached para queries frecuentes
  
- [ ] **Database queries optimizadas**
  - Sin full table scans innecesarios
  - Límites en queries (LIMIT)

---

## 🔍 Observabilidad

- [ ] **Logging estructurado**
  - Logs con `trace_id`, `user_id`, nivel
  - JSON format para parsing
  
- [ ] **Métricas expuestas**
  - `/metrics` endpoint (Prometheus format)
  - Request rate, error rate, latency
  
- [ ] **Tracing implementado**
  - OpenTelemetry / Jaeger spans
  - Context propagation entre servicios
  
- [ ] **Health checks funcionales**
  - `/live`: Proceso vivo
  - `/ready`: Dependencias OK (DB, Redis)
  - `/health`: Validaciones adicionales
  
- [ ] **Alertas configuradas**
  - Error rate > 5%
  - p95 latency > 500ms
  - Health checks failing
  
- [ ] **Dashboards actualizados**
  - Grafana con métricas clave
  - SLIs/SLOs definidos

---

## 🌐 Infraestructura

- [ ] **Auto-scaling configurado**
  - Scale up en alta carga
  - Scale down en baja carga
  
- [ ] **Rate limiting implementado**
  - Protección contra abuse/DDoS
  - Límites por IP/usuario
  
- [ ] **Circuit breakers**
  - Para llamadas a servicios externos
  - Fallbacks definidos
  
- [ ] **Timeouts apropiados**
  - HTTP client timeouts < 30s
  - DB query timeouts
  
- [ ] **Multi-AZ / redundancia**
  - Deploy en múltiples availability zones
  - Load balancer configurado
  
- [ ] **Backups automáticos**
  - DB backups diarios
  - Retention policy (30 días)

---

## 📝 Documentación

- [ ] **API docs actualizadas**
  - Swagger/OpenAPI
  - Ejemplos de requests/responses
  
- [ ] **README actualizado**
  - Cambios significativos documentados
  - Setup instructions correctas
  
- [ ] **CHANGELOG actualizado**
  - Versión semántica (SemVer)
  - Listar breaking changes
  
- [ ] **Runbook actualizado**
  - Pasos para rollback
  - Troubleshooting común
  
- [ ] **ADR documentado** (si aplica)
  - Decisiones arquitecturales significativas
  - Contexto y alternativas consideradas

---

## 🔄 Proceso de Deploy

- [ ] **Feature flags consideradas**
  - Para features grandes
  - Kill switch disponible
  
- [ ] **Estrategia de deploy definida**
  - Rolling, blue-green, canary
  - % tráfico inicial si canary
  
- [ ] **Rollback plan claro**
  - Comando de rollback documentado
  - Testeado en staging
  
- [ ] **Ventana de deploy apropiada**
  - Evitar viernes tarde / vísperas festivos
  - Horario de bajo tráfico si posible
  
- [ ] **Stakeholders notificados**
  - Product, Customer Success, Support
  - Changelog comunicado
  
- [ ] **On-call alertado**
  - Team on-call sabe del deploy
  - Runbook accessible

---

## ✅ Post-Deploy Verification

### Inmediato (primeros 5 min)

- [ ] **Smoke tests pasan**
  - Login funciona
  - Endpoint crítico responde
  - No errores en logs
  
- [ ] **Health checks OK**
  - `/live`, `/ready` retornan 200
  - Todas las instancias healthy
  
- [ ] **Métricas estables**
  - Error rate no aumentó
  - Latencia similar a pre-deploy
  - Throughput normal

### Primeros 30 minutos

- [ ] **Monitoring activo**
  - Revisar dashboards
  - Alertas no disparadas
  
- [ ] **User reports**
  - No incremento en tickets support
  - No quejas en social media
  
- [ ] **Logs sin errores nuevos**
  - Grep por exceptions
  - Nivel ERROR no aumentó

### Primera hora

- [ ] **Métricas de negocio**
  - Conversión no cayó
  - Engagement normal
  
- [ ] **Performance baseline**
  - p95 latency comparable
  - Database load normal

---

## 🚨 Rollback Criteria

**Rollback inmediato si:**
- Error rate > 10%
- p95 latency > 2x baseline
- Health checks failing > 5 min
- Critical feature broken
- Data corruption detectada
- Security vulnerability introducida

**Proceso:**
1. Ejecutar rollback command
2. Verificar health checks
3. Notificar stakeholders
4. Post-mortem blameless

---

## 🎯 Checklist por Tipo de Change

### Cambio de DB Schema

- [ ] Migration backward compatible
- [ ] Deploy en 2 fases si breaking
- [ ] Datos migrados sin pérdida
- [ ] Rollback testeado

### Nueva API Endpoint

- [ ] Autenticación requerida
- [ ] Rate limiting
- [ ] Input validation
- [ ] Docs en Swagger
- [ ] Tests E2E

### Cambio de Config

- [ ] Config en version control
- [ ] Testeado en staging
- [ ] Rollback = config anterior
- [ ] No secrets en Git

### Actualización de Dependency

- [ ] CHANGELOG leído
- [ ] Breaking changes identificados
- [ ] Tests pasados
- [ ] Performance no degradó

---

## 📋 Sign-off

**Antes de deploy:**

```
Deploy Request: #1234
Feature: User authentication with 2FA
Deploy date: 2024-02-15 14:00 UTC
Deploy strategy: Canary (10% → 50% → 100%)

Checklist: ✅ Completed
Tests: ✅ All passing (coverage 85%)
Security scan: ✅ No critical issues
Staging: ✅ Validated
Rollback plan: ✅ Documented

Approvals:
- Developer: @alice (signed)
- Reviewer: @bob (signed)
- Tech Lead: @carol (signed)

Proceed? YES / NO
```

---

## 🚫 Common Mistakes

| Mistake | Consecuencia | Prevención |
|:--------|:-------------|:-----------|
| "Skip tests, bajo riesgo" | Bugs en producción | Nunca skip tests |
| "Deploy viernes 17h" | Weekend debugging | Deploy martes-jueves AM |
| "No probé rollback" | Rollback falla cuando se necesita | Test rollback en staging |
| "Notificar después" | Support sin contexto | Notificar ANTES |
| "Sin monitorear post-deploy" | Problemas no detectados | Monitor activo 1 hora |

---

## 🎓 Mejora Continua

Después de cada deploy:

- [ ] **Retro rápida (5 min)**
  - ¿Algo salió mal?
  - ¿Qué mejorar del proceso?
  
- [ ] **Actualizar checklist**
  - Agregar items si faltó algo
  - Remover si ya no aplica
  
- [ ] **Automatizar lo manual**
  - CI/CD checks automáticos
  - Scripts en vez de pasos manuales

---

## 📚 Recursos

- [Google SRE - Release Engineering](https://sre.google/sre-book/release-engineering/)
- [AWS Well-Architected - Operational Excellence](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/)
- [Production Readiness Checklist - Gruntwork](https://gruntwork.io/devops-checklist/)

---

## ✅ Final Approval

**Este checklist fue completado y aprobado por:**

- Developer: _________________ Fecha: _______
- Code Reviewer: _____________ Fecha: _______
- Tech Lead: _________________ Fecha: _______
- DevOps (si aplica): _________ Fecha: _______

**Deploy autorizado: YES / NO**

**Hora estimada deploy: ____________**

**Ventana de deploy: ____________**

---

[⬅️ Anterior: Onboarding](./26-onboarding.md) | [⬆️ Volver arriba](#) | [🏠 Volver al índice](./00-indice.md)

---

## 🎉 ¡Checklist Completo!

Si completaste todos los ítems, tu deploy tiene alta probabilidad de éxito. Recuerda:

> **"Hope is not a strategy. Preparation is."**

¡Buen deploy! 🚀