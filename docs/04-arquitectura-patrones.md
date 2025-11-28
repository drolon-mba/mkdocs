# 04 - Arquitectura y Patrones

> Estructuras de alto nivel y soluciones probadas para organizar sistemas complejos, escalables y mantenibles.

[🏠 Volver al índice](./00-indice.md)

---

## 🏗️ Arquitecturas de Software

**What:** Decisiones estructurales fundamentales sobre cómo organizar un sistema.

**Why:** Define cómo el sistema crece, se mantiene y responde al cambio. Una mala arquitectura puede matar un proyecto exitoso.

**Who:** Arquitectos de software, tech leads, senior developers.

**How much:** Decisión temprana de alto impacto. Cambiar arquitectura en sistema maduro = 6-18 meses.

| Arquitectura | What | Why | When | Where | How | Trade-offs |
|:-------------|:-----|:----|:-----|:------|:----|:-----------|
| **Monolítica** | Aplicación única con todos los módulos integrados | Simplicidad, deployment único, debugging fácil | MVPs, equipos pequeños, dominios simples | Startups, sistemas internos | Todo en un proceso, shared DB, deployment único | ✅ Simple, rápido desarrollo inicial<br>❌ Escalado vertical, deploy riesgoso |
| **MVC** | Model-View-Controller: separar datos, UI y control | Claridad en responsabilidades | Apps web tradicionales, dashboards | Backend + templates | Modelos (datos), Vistas (UI), Controladores (lógica coordinación) | ✅ Patrón conocido<br>❌ Controllers crecen (fat controllers) |
| **Microservicios** | Sistema distribuido con servicios independientes | Escalado independiente, equipos autónomos | Sistemas complejos, múltiples equipos | Netflix, Uber, Amazon | Servicios pequeños, comunicación API/eventos, DB por servicio | ✅ Escalabilidad, fault isolation<br>❌ Complejidad operacional, latencia |
| **Hexagonal** | Lógica central aislada de interfaces externas (ports & adapters) | Testability, independencia de frameworks | Dominios complejos, larga vida | Backend crítico | Core (lógica) + Puertos (interfaces) + Adaptadores (implementaciones) | ✅ Testeo fácil, cambiar DB/UI sin tocar core<br>❌ Más código inicial |
| **Capas** | Separación horizontal: presentación, negocio, datos | Modularidad, responsabilidades claras | Sistemas empresariales tradicionales | Monolitos estructurados | Capas solo conocen la inferior, DTO entre capas | ✅ Organización clara<br>❌ Puede ser rígido |
| **Event-Driven** | Comunicación basada en eventos asincrónicos | Desacoplamiento, escalabilidad | Sistemas con workflows complejos, integraciones | E-commerce, IoT, streaming | Event Bus/Broker, productores/consumidores | ✅ Desacoplamiento total<br>❌ Debugging complejo, eventual consistency |
| **Serverless** | Funciones sin servidor dedicado, auto-scaling | Costo por uso, cero gestión servidores | Tareas puntuales, APIs sencillas, jobs | AWS Lambda, Cloud Functions | Funciones stateless, triggers (HTTP, eventos), short-lived | ✅ Escalado automático, low cost<br>❌ Cold starts, vendor lock-in |

---

## 🧩 Patrones de Diseño (Gang of Four)

**What:** Soluciones reutilizables a problemas recurrentes de diseño OOP.

**Why:** No reinventar la rueda, vocabulario común entre developers.

[Ver todos los patrones explicados en Refactoring Guru](https://refactoring.guru/design-patterns)

### Patrones Creacionales

| Patrón | What | Why | When | How |
|:-------|:-----|:----|:-----|:----|
| **Factory Method** | Crea objetos sin especificar clase exacta | Delegar creación a subclases | Crear objetos de familias similares | Interface `create()`, subclases deciden tipo concreto |
| **Abstract Factory** | Crea familias de objetos relacionados | Consistencia entre productos | UI con temas (Dark/Light) | Factory retorna conjunto de objetos relacionados |
| **Builder** | Construye objetos complejos paso a paso | Muchas opciones de configuración | DTOs complejos, requests HTTP | `builder.setName().setAge().build()` |
| **Prototype** | Clona objetos existentes | Creación costosa, muchas variaciones | Clonar configuraciones, templates | Implementar `clone()`, copiar estado |
| **Singleton** | Garantiza única instancia global | Un punto de acceso (config, logger) | Recursos compartidos únicos | Constructor privado, `getInstance()` estática |

### Patrones Estructurales

| Patrón | What | Why | When | How |
|:-------|:-----|:----|:-----|:----|
| **Adapter** | Convierte interfaz incompatible | Integrar código legacy/third-party | Librerías externas con APIs distintas | Wrapper que traduce llamadas |
| **Bridge** | Separa abstracción de implementación | Variar ambas independientemente | UI multiplataforma (misma lógica, distinto render) | Abstracción tiene referencia a implementación |
| **Composite** | Composición jerárquica (árbol) | Tratar individual y compuesto igual | Menús, file systems, org charts | Interface común, contenedor tiene lista de hijos |
| **Decorator** | Añade funcionalidades dinámicamente | Extender sin modificar clase | Logging, caching, autenticación en requests | Wrapper que implementa misma interface |
| **Facade** | Interfaz simplificada a subsistema complejo | Ocultar complejidad interna | APIs complejas (AWS SDK → helper simple) | Clase que expone métodos high-level |
| **Flyweight** | Minimiza memoria compartiendo datos | Muchos objetos similares | Renderizar 10k íconos (compartir imagen) | Separar estado intrínseco (compartido) de extrínseco |
| **Proxy** | Controla acceso a objeto | Lazy loading, caching, seguridad | Imágenes pesadas, permisos | Proxy implementa misma interface, delega a real |

### Patrones Comportamiento

| Patrón | What | Why | When | How |
|:-------|:-----|:----|:-----|:----|
| **Strategy** | Familia de algoritmos intercambiables | Cambiar comportamiento en runtime | Ordenamiento (bubble, quick, merge) | Interface `execute()`, contexto recibe estrategia |
| **Observer** | Notifica cambios a múltiples objetos | Reacción automática ante eventos | UI reactiva (state → re-render) | Sujeto tiene lista de observadores, `notify()` |
| **Command** | Encapsula solicitud como objeto | Parametrizar, deshacer, encolar | Undo/Redo, job queues | Interface `execute()`, receiver realiza acción |
| **State** | Cambia comportamiento según estado interno | Manejar estados complejos | Workflows (draft→review→published) | Context delega a objeto State actual |
| **Template Method** | Esqueleto de algoritmo, pasos personalizables | Reutilizar estructura | Conectar a DB (común: connect, query, close) | Clase abstracta define pasos, subclases implementan |
| **Chain of Responsibility** | Pasa solicitud por cadena de manejadores | Procesamiento flexible | Middleware (auth → logging → handler) | Cada handler procesa o pasa al siguiente |
| **Visitor** | Añade operaciones sin modificar clases | Operaciones sobre estructura compleja | Export (HTML, PDF, JSON) de mismo árbol | Interface `visit()`, elementos aceptan visitor |
| **Mediator** | Centraliza comunicación entre objetos | Reducir acoplamiento | UI forms (campos se habilitan según otros) | Componentes se comunican vía mediador |
| **Memento** | Guarda y restaura estado | Undo/Redo, snapshots | Editores, juegos | Originator crea memento, caretaker lo guarda |
| **Iterator** | Recorre elementos sin exponer estructura | Acceso secuencial estándar | Colecciones custom | Interface `next()`, `hasNext()` |

---

## 🏗️ Patrones Arquitectónicos Avanzados

| Patrón | What | Why | When | Where | How | Herramientas |
|:-------|:-----|:----|:-----|:------|:----|:-------------|
| **Event Sourcing** | Persistir cambios como secuencia de eventos inmutables | Auditoría completa, time travel, proyecciones | Sistemas financieros, compliance | Event Store | Cada cambio → evento (`OrderPlaced`), reconstruir estado reproduciendo | [EventStore](https://www.eventstore.com/), [Kafka](https://kafka.apache.org/) |
| **CQRS** | Separar modelos de lectura (Query) y escritura (Command) | Optimizar cada uno independientemente | Escrituras complejas + lecturas frecuentes | APIs de alta carga | Commands modifican, Queries leen vistas desnormalizadas | [MediatR](https://github.com/jbogard/MediatR), [Axon](https://axoniq.io/) |
| **Saga Pattern** | Transacciones distribuidas con compensación | Consistencia eventual entre microservicios | Workflows multi-servicio (order→payment→shipping) | Microservicios | Orquestada (coordinador) o Coreografiada (eventos) | [Temporal](https://temporal.io/), [Camunda](https://camunda.com/) |
| **Circuit Breaker** | Prevenir cascadas de fallos | Sistema resiliente ante servicios caídos | Llamadas a APIs externas inestables | Clientes HTTP | Closed→Open (tras N fallos)→Half-Open (test)→Closed | [Resilience4j](https://resilience4j.readme.io/), [Hystrix](https://github.com/Netflix/Hystrix) |
| **Strangler Fig** | Migrar legacy gradualmente | Reemplazo sin big bang | Modernizar monolito → microservicios | Proxy/Gateway | Nuevo código intercepta requests, delega a legacy o nuevo | [nginx](https://nginx.org/), [Envoy](https://www.envoyproxy.io/) |
| **API Gateway** | Punto de entrada único para múltiples servicios | Routing, auth, rate limiting centralizado | Microservicios con necesidades cross-cutting | Edge de la red | Gateway maneja auth, transforma requests, agrega respuestas | [Kong](https://konghq.com/), [AWS API Gateway](https://aws.amazon.com/api-gateway/) |
| **Bulkhead Pattern** | Aislar recursos para prevenir fallo total | Un servicio lento no consume todo | Pools de conexiones, threads | Thread pools, circuit breakers | Separar pools por tipo de operación | [Resilience4j Bulkhead](https://resilience4j.readme.io/docs/bulkhead) |

---

## 🎭 Finite State Machines (FSM)

**What:** Modelar sistemas con estados finitos y transiciones explícitas.

**Why:** Elimina bugs de estados inválidos, documentación visual ejecutable.

**When:** Workflows complejos (pedidos, aprobaciones, onboarding), procesos con múltiples actores.

| Concepto | What | Ejemplo |
|:---------|:-----|:--------|
| **Estados** | Conjunto finito de condiciones | `Pending`, `Paid`, `Shipped`, `Delivered`, `Cancelled` |
| **Transiciones** | Cambios entre estados con condiciones | `Pending → Paid` (al recibir pago) |
| **Eventos** | Triggers que activan transiciones | `PaymentReceived`, `ShipmentDispatched` |
| **Guards** | Condiciones para permitir transición | `Paid → Shipped` solo si `inventory > 0 && address_valid` |
| **Acciones** | Side effects al entrar/salir | Al entrar en `Paid`: enviar email, decrementar stock |

**Herramientas:** [XState](https://xstate.js.org/), [Spring State Machine](https://spring.io/projects/spring-statemachine), [Python transitions](https://github.com/pytransitions/transitions)

**Ejemplo XState:**

```typescript
import { createMachine } from 'xstate';

const orderMachine = createMachine({
  id: 'order',
  initial: 'pending',
  states: {
    pending: {
      on: { PAYMENT_RECEIVED: 'paid' }
    },
    paid: {
      on: { 
        SHIP: { 
          target: 'shipped', 
          cond: 'hasInventory' 
        }
      },
      entry: 'sendConfirmationEmail'
    },
    shipped: {
      on: { DELIVER: 'delivered' }
    },
    delivered: { type: 'final' }
  }
});
```

---

## 📐 Principios de Arquitectura

| Principio | What | Why |
|:----------|:-----|:----|
| **Separation of Concerns** | Separar responsabilidades en módulos/capas | Mantenimiento, testing, escalabilidad |
| **Single Responsibility** | Cada módulo/clase tiene una razón para cambiar | Cohesión alta, bajo acoplamiento |
| **Dependency Inversion** | Depender de abstracciones, no concreciones | Testability, flexibilidad |
| **Open/Closed** | Abierto a extensión, cerrado a modificación | Agregar features sin romper existente |
| **Least Knowledge** | Módulos conocen lo mínimo necesario | Reduce fragilidad |

---

## 🗂️ Distribución de Carpetas

| Enfoque | What | When | Ejemplo |
|:--------|:-----|:-----|:--------|
| **Por tipo** | Separar por categoría técnica | Proyectos pequeños | `/controllers`, `/services`, `/models` |
| **Por feature** | Agrupar por funcionalidad | Proyectos medianos/grandes | `/auth`, `/dashboard`, `/billing` |
| **Por dominio** | Agrupar por contexto de negocio | DDD | `/sales`, `/inventory`, `/shipping` |
| **Monorepo modular** | Múltiples apps/packages en un repo | Microservicios, libs compartidas | `/apps/web`, `/apps/api`, `/packages/ui` |

---

## 🚫 Anti-patrones Arquitectónicos

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Big Ball of Mud** | Sin estructura clara, todo acoplado | Refactorizar incremental, definir módulos |
| **God Object** | Una clase hace todo | Aplicar SRP, extraer responsabilidades |
| **Spaghetti Code** | Flujo imposible de seguir | Linealizar, extraer funciones, FSM |
| **Golden Hammer** | Usar misma solución para todo | Evaluar trade-offs por caso |
| **Premature Generalization** | Abstracciones sin casos de uso reales | Esperar 3 casos antes de generalizar |

---

## 📚 Recursos

- [Refactoring Guru - Patrones](https://refactoring.guru/design-patterns)
- [Software Architecture Patterns - O'Reilly](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/)
- [Building Microservices - Sam Newman](https://samnewman.io/books/building_microservices_2nd_edition/)
- [Clean Architecture - Robert Martin](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)

---

[⬅️ Anterior: Testing](./03-testing.md) | [⬆️ Volver arriba](#04---arquitectura-y-patrones) | [➡️ Siguiente: DevOps](./05-devops.md)