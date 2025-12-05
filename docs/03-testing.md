# 03 - Testing

> Estrategias y herramientas para validar que el software funciona correctamente en todos los niveles: unitario, integración, E2E y performance.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 ¿Por qué Testing?](#por-que-testing)
- [🏗️ Pirámide de Testing](#piramide-de-testing)
- [🧪 Testing por Contexto](#testing-por-contexto)
- [🧪 Testing Avanzado](#testing-avanzado)
- [📏 Métricas de Testing](#metricas-de-testing)
- [🎯 Estrategia de Testing por Proyecto](#estrategia-de-testing-por-proyecto)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 ¿Por qué Testing?

**Why:** Tests automatizados son la red de seguridad que permite refactorizar, escalar y desplegar con confianza. Sin tests, cada cambio es un riesgo.

**Who:** Developers (unitarios, integración), QA (E2E, exploratorio), DevOps (smoke tests, performance).

**How much:** Inversión 20-30% del tiempo de desarrollo, reduce bugs en producción 60-90%.

---

## 🏗️ Pirámide de Testing

```
        /\
       /  \  E2E (pocas, lentas, costosas)
      /----\
     / Integ\ Integration (moderadas)
    /--------\
   /  Unit    \ Unit (muchas, rápidas, baratas)
  /____________\
```

**Regla 70-20-10:**
- 70% tests unitarios
- 20% tests de integración
- 10% tests E2E

---

## 🧪 Testing por Contexto

### Backend Testing

**What:** Validar lógica de negocio, persistencia, APIs y servicios.

| Tipo | What | Why | When | Where | How | Herramientas |
|:-----|:-----|:----|:-----|:------|:----|:-------------|
| **Unitarios** | Testear funciones/clases aisladas | Rápidos, debuggables, diseño modular | Toda lógica de negocio | Servicios, utilidades, parsers | Mockear dependencias externas, un assert por concepto | [JUnit 5](https://junit.org/junit5/), [pytest](https://docs.pytest.org/), [Jest](https://jestjs.io/) |
| **Integración** | Validar interacción entre componentes | Detecta problemas en límites (DB, APIs) | Repositorios, clientes HTTP, colas | Capa de persistencia, integraciones | Usar DB de test (Testcontainers), levantar servicios reales | [Testcontainers](https://testcontainers.com/), [pytest-django](https://pytest-django.readthedocs.io/) |
| **Mocks** | Reemplazar dependencias con dobles | Aislar unidad bajo test, tests deterministas | Cuando dependencia es lenta/impredecible | APIs externas, email, jobs async | Verificar llamadas, stubbar respuestas | [Mockito](https://site.mockito.org/), [unittest.mock](https://docs.python.org/3/library/unittest.mock.html) |
| **Cobertura** | Medir % de código ejecutado por tests | Identificar código no testeado | CI/CD pipeline, pre-merge | Todo el codebase | Meta: ≥80% en lógica crítica, 60% general | [JaCoCo](https://www.eclemma.org/jacoco/), [Coverage.py](https://coverage.readthedocs.io/) |
| **API Testing** | Validar contratos REST/GraphQL | Detectar breaking changes | Cada endpoint público | Controllers, resolvers | Testear happy path + edge cases + errores | [Postman](https://www.postman.com/), [Bruno](https://www.usebruno.com/), [REST Assured](https://rest-assured.io/) |

### Frontend Testing

**What:** Validar componentes, interacciones de usuario y flujos completos en browsers.

| Tipo | What | Why | When | Where | How | Herramientas |
|:-----|:-----|:----|:-----|:------|:----|:-------------|
| **Unitarios** | Testear componentes aislados | Rápidos, validan lógica de presentación | Componentes reutilizables, hooks custom | Componentes sin deps externas | Renderizar con props mockeadas, verificar output | [Vitest](https://vitest.dev/), [Jest](https://jestjs.io/), [Testing Library](https://testing-library.com/) |
| **Integración** | Testear composición de componentes | Validan flujo entre componentes | Páginas, features completas | Módulos/páginas | Renderizar árbol de componentes, interactuar con DOM | [Testing Library](https://testing-library.com/), [Enzyme](https://enzymejs.github.io/enzyme/) |
| **E2E** | Testear flujos en browser real | Validan experiencia real de usuario | Flujos críticos (login, checkout, pago) | Toda la app + backend | Automatizar clicks, inputs, navegación | [Playwright](https://playwright.dev/), [Cypress](https://www.cypress.io/) |
| **Visual Regression** | Detectar cambios visuales no deseados | Previene bugs de CSS/layout | Componentes de UI library | Storybook, componentes aislados | Comparar screenshots antes/después | [Chromatic](https://www.chromatic.com/), [Percy](https://percy.io/) |
| **Accesibilidad** | Validar WCAG compliance | Inclusión, cumplimiento legal | Todos los componentes interactivos | Formularios, modales, navegación | Validar roles ARIA, contraste, keyboard nav | [axe-core](https://github.com/dequelabs/axe-core), [jest-axe](https://github.com/nickcolley/jest-axe) |

### Mobile Testing

**What:** Validar apps nativas e híbridas en dispositivos reales y emuladores.

| Tipo | What | Why | When | Where | How | Herramientas |
|:-----|:-----|:----|:-----|:------|:----|:-------------|
| **Unitarios** | Lógica de negocio en app | Rápidos, sin UI | ViewModels, servicios, parsers | Lógica separada de UI | Mockear platform APIs | [XCTest](https://developer.apple.com/documentation/xctest), [JUnit](https://junit.org/) |
| **UI Testing** | Flujos de usuario en emulador | Validan interacción real | Flujos críticos de la app | Pantallas principales | Automatizar taps, swipes, inputs | [Espresso](https://developer.android.com/training/testing/espresso) (Android), [XCUITest](https://developer.apple.com/documentation/xctest) (iOS) |
| **Cross-platform** | Testing multiplataforma | Un código para iOS + Android | Apps híbridas (React Native, Flutter) | Toda la app | Scripts que corren en ambos OS | [Appium](https://appium.io/), [Detox](https://wix.github.io/Detox/) |
| **Device Farm** | Testing en dispositivos reales | Detecta bugs específicos de device | Antes de release | Toda la app | Subir APK/IPA, ejecutar tests remotamente | [AWS Device Farm](https://aws.amazon.com/device-farm/), [BrowserStack](https://www.browserstack.com/) |

### Performance Testing

**What:** Medir latencia, throughput y estabilidad bajo carga.

| Tipo | What | Why | When | Where | How | Herramientas |
|:-----|:-----|:----|:-----|:------|:----|:-------------|
| **Load Testing** | Simular usuarios concurrentes | Validar SLOs (p95 < 500ms) | Antes de lanzar feature, quarterly | Endpoints críticos | Rampa de usuarios, medir latencia/errores | [k6](https://k6.io/), [Gatling](https://gatling.io/), [Locust](https://locust.io/) |
| **Stress Testing** | Llevar sistema al límite | Encontrar punto de quiebre | Capacity planning | Todo el sistema | Aumentar carga hasta fallos | [Artillery](https://www.artillery.io/), [JMeter](https://jmeter.apache.org/) |
| **Spike Testing** | Picos súbitos de tráfico | Validar auto-scaling, circuit breakers | Sistemas con tráfico variable | Load balancers, caches | Enviar 10x tráfico normal repentinamente | [k6](https://k6.io/), [Gatling](https://gatling.io/) |
| **Soak Testing** | Carga sostenida por horas/días | Detectar memory leaks, degradación | Sistemas 24/7 | Backend services | Carga constante 8-48 horas, monitorear memoria | [k6](https://k6.io/), [Locust](https://locust.io/) |

---

## 🧪 Testing Avanzado

| Tipo | What | Why | When | Where | How | Herramientas |
|:-----|:-----|:----|:-----|:------|:----|:-------------|
| **Contract Testing** | Validar contratos entre servicios | Evita breaking changes | Microservicios, APIs públicas | Provider-Consumer | Consumer define expectativas (Pact), Provider valida | [Pact](https://pact.io/), [Spring Cloud Contract](https://spring.io/projects/spring-cloud-contract) |
| **Mutation Testing** | Validar calidad de tests mutando código | Tests débiles no detectan bugs reales | Lógica crítica con alta cobertura | Algoritmos, validadores | Cambiar `>` por `>=`, `&&` por `||`, verificar tests fallen | [Stryker](https://stryker-mutator.io/), [mutmut](https://github.com/boxed/mutmut) |
| **Chaos Engineering** | Inyectar fallos para validar resiliencia | Validar que el sistema tolera fallos reales | Sistemas distribuidos críticos | Ver [Capítulo 38 - Chaos Engineering](./38-chaos-engineering.md) para detalles completos | Ver [Capítulo 38](./38-chaos-engineering.md) |
| **Snapshot Testing** | Guardar output como referencia | Detectar cambios no intencionados | Componentes estables, APIs | UI components, JSON responses | Primera ejecución guarda snapshot, siguientes comparan | [Jest Snapshots](https://jestjs.io/docs/snapshot-testing), [pytest-regressions](https://github.com/ESSS/pytest-regressions) |
| **Smoke Testing** | Validar funcionalidad básica post-deploy | Detectar problemas críticos rápido | Cada deploy | Producción | Health checks, login, operación básica | Scripts custom, [Postman](https://www.postman.com/) |
| **Fuzz Testing** | Inputs aleatorios/malformados | Encuentra crashes, vulnerabilidades | Parsers, APIs públicas | Input validation | Generar inputs inválidos masivamente | [AFL](https://github.com/google/AFL), [libFuzzer](https://llvm.org/docs/LibFuzzer.html) |

---

## 📏 Métricas de Testing

| Métrica | Fórmula | Meta | Herramienta |
|:--------|:--------|:-----|:------------|
| **Code Coverage** | (Líneas ejecutadas / Total líneas) × 100 | ≥80% lógica crítica, ≥60% general | JaCoCo, Coverage.py |
| **Test Success Rate** | (Tests pasados / Total tests) × 100 | 100% en main branch | CI/CD dashboard |
| **Test Execution Time** | Tiempo suite completa | <5 min unitarios, <15 min E2E | CI logs |
| **Defect Escape Rate** | Bugs en prod / Total bugs encontrados | <5% | Jira, GitHub Issues |
| **Mutation Score** | (Mutantes muertos / Total mutantes) × 100 | ≥70% | Stryker, mutmut |

---

## 🎯 Estrategia de Testing por Proyecto

| Tipo Proyecto | Enfoque Testing | Razón |
|:--------------|:----------------|:------|
| **Startup/MVP** | E2E en flujos críticos + unitarios en lógica compleja | Velocidad, máximo valor/esfuerzo |
| **Producto maduro** | Pirámide completa 70-20-10 | Estabilidad, refactoring seguro |
| **Sistema legacy** | Tests de regresión (E2E) + caracterización | Proteger funcionalidad existente |
| **Microservicios** | Contract testing + integración | Evitar breaking changes entre equipos |
| **Biblioteca/SDK** | 100% cobertura unitaria + PBT | Usado por terceros, máxima confianza |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Tests frágiles** | Fallan por cambios no relacionados (IDs, orden) | Usar selectores semánticos, no acoplar a estructura |
| **Timeouts arbitrarios** | `sleep(5)` en E2E | Usar wait explícitos (waitForSelector) |
| **Tests interdependientes** | Test B depende que A corra primero | Tests aislados, setup/teardown por test |
| **Assertions múltiples** | Un test valida 10 cosas | Un concepto por test, nombres claros |
| **Mocks excesivos** | Mockear todo, no testear nada real | Mockear solo lo externo/lento |

---

## 📚 Recursos

- [Testing JavaScript - Kent C. Dodds](https://testingjavascript.com/)
- [Effective Software Testing - Maurício Aniche](https://www.effective-software-testing.com/)
- [Growing Object-Oriented Software, Guided by Tests](http://www.growing-object-oriented-software.com/)
- [Google Testing Blog](https://testing.googleblog.com/)

---

[⬅️ Anterior: Disciplinas de Desarrollo](./02-disciplinas-desarrollo.md) | [⬆️ Volver arriba](#03-testing) | [➡️ Siguiente: Arquitectura y Patrones](./04-arquitectura-patrones.md)