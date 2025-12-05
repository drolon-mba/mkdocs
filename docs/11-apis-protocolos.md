# 11 - APIs y Protocolos

> Interfaces para comunicación entre sistemas: REST, GraphQL, gRPC, WebSockets y más.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🎯 Elegir Protocolo](#elegir-protocolo)
- [🌐 REST (Representational State Transfer)](#rest-representational-state-transfer)
- [🔍 GraphQL](#graphql)
- [⚡ gRPC](#grpc)
- [🔌 WebSockets](#websockets)
- [📨 Server-Sent Events (SSE)](#server-sent-events-sse)
- [🎯 Event-Driven / Async](#event-driven-async)
- [📄 Documentación](#documentacion)
- [🔐 Autenticación](#autenticacion)
- [🎨 Diseño de APIs](#diseno-de-apis)
- [🔄 Webhooks](#webhooks)
- [📊 Comparación](#comparacion)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🎯 Elegir Protocolo

**What:** Definir cómo sistemas se comunican.

**Why:** Impacta performance, developer experience, escalabilidad.

**Who:** Arquitectos, backend developers.

**How much:** Decisión difícil de cambiar una vez adoptada.

---

## 🌐 REST (Representational State Transfer)

**What:** APIs basadas en HTTP con recursos y verbos.

**Why:** Estándar universal, cacheable, stateless.

| Aspecto | What | How |
|:--------|:-----|:----|
| **Recursos** | Sustantivos (entidades) | `/users`, `/orders`, `/products` |
| **Verbos HTTP** | Acciones sobre recursos | GET (leer), POST (crear), PUT (actualizar), DELETE (borrar) |
| **Códigos Status** | Resultado de operación | 200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Server Error |
| **Idempotencia** | Mismo request → mismo resultado | GET, PUT, DELETE idempotentes. POST no |
| **HATEOAS** | Hypermedia as Engine of State | Responses incluyen links a recursos relacionados |

**Ejemplo:**
```http
GET /api/v1/users/123
Authorization: Bearer <token>

Response 200:
{
  "id": 123,
  "name": "Alice",
  "email": "alice@example.com",
  "_links": {
    "self": "/users/123",
    "orders": "/users/123/orders"
  }
}
```

---

## 🔍 GraphQL

**What:** Query language para APIs con schema tipado.

**Why:** Cliente pide exactamente lo que necesita, no más ni menos.

| Concepto | What | Ejemplo |
|:---------|:-----|:--------|
| **Schema** | Tipos y relaciones | `type User { id: ID! name: String! posts: [Post] }` |
| **Query** | Leer datos | `{ user(id: "123") { name email } }` |
| **Mutation** | Modificar datos | `mutation { createUser(input: {...}) { id } }` |
| **Subscription** | Real-time updates | `subscription { messageAdded { id text } }` |
| **Resolver** | Función que obtiene datos | `User.posts: (parent) => fetchPosts(parent.id)` |

**Ventajas:**
- Sin overfetching/underfetching
- Un endpoint para todo
- Schema autodocumentado

**Desventajas:**
- Complejidad adicional
- Caching difícil
- Queries costosas (N+1)

**Herramientas:** [Apollo](https://www.apollographql.com/), [Hasura](https://hasura.io/), [GraphQL Yoga](https://the-guild.dev/graphql/yoga-server)

---

## ⚡ gRPC

**What:** RPC framework con Protocol Buffers binario.

**Why:** Performance, tipado fuerte, streaming nativo.

| Aspecto | What | Ventaja |
|:--------|:-----|:--------|
| **Protocol Buffers** | Serialización binaria | Más pequeño y rápido que JSON |
| **HTTP/2** | Multiplexing, server push | Menos conexiones |
| **Streaming** | Bidireccional | Server/Client/Bidirectional streams |
| **Code generation** | Clientes/servers automáticos | Type-safe |

**Ejemplo .proto:**
```protobuf
service UserService {
  rpc GetUser (GetUserRequest) returns (User);
  rpc StreamUsers (StreamUsersRequest) returns (stream User);
}

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}
```

**Cuándo usar:** Microservicios internos, alta performance, streaming.

**Herramientas:** [gRPC](https://grpc.io/), [Buf](https://buf.build/), [grpcurl](https://github.com/fullstorydev/grpcurl)

---

## 🔌 WebSockets

**What:** Conexión bidireccional persistente sobre TCP.

**Why:** Real-time, baja latencia, push de servidor.

| Aspecto | What | Cuándo |
|:--------|:-----|:-------|
| **Full-duplex** | Cliente y servidor envían simultáneamente | Chat, gaming |
| **Persistent** | Conexión abierta continuamente | Notificaciones en tiempo real |
| **Binary/Text** | Soporta ambos formatos | Flexible |

**Ejemplo:**
```javascript
const ws = new WebSocket('wss://api.example.com/ws');

ws.onmessage = (event) => {
  console.log('Message:', event.data);
};

ws.send(JSON.stringify({ type: 'subscribe', channel: 'updates' }));
```

**Cuándo usar:** Chat, gaming, dashboards en tiempo real, collaborative editing.

**Alternativa:** Server-Sent Events (SSE) para one-way server→client.

---

## 📨 Server-Sent Events (SSE)

**What:** Streaming unidireccional server→client sobre HTTP.

**Why:** Más simple que WebSockets para notificaciones.

```javascript
const eventSource = new EventSource('/api/events');

eventSource.addEventListener('update', (event) => {
  console.log('Update:', event.data);
});
```

**Cuándo usar:** Notificaciones, cotizaciones, progress updates.

**Ventajas vs WebSockets:**
- Más simple (HTTP estándar)
- Reconnect automático
- Event IDs para reanudar

---

## 🎯 Event-Driven / Async

**What:** Comunicación basada en eventos via message brokers.

| Broker | What | When |
|:-------|:-----|:-----|
| [RabbitMQ](https://www.rabbitmq.com/) | Message queue con routing | Workflows complejos |
| [Apache Kafka](https://kafka.apache.org/) | Event streaming distribuido | Alto throughput, logs |
| [AWS SQS](https://aws.amazon.com/sqs/) | Queue serverless | Desacople simple en AWS |
| [Redis Pub/Sub](https://redis.io/docs/manual/pubsub/) | Publish/Subscribe en memoria | Eventos en tiempo real |

**Patrones:**
- **Pub/Sub:** Broadcast a múltiples consumidores
- **Queues:** Work distribution, un consumidor procesa
- **Event Sourcing:** Eventos como fuente de verdad

---

## 📄 Documentación

| Protocolo | Herramienta | Ejemplo |
|:----------|:------------|:--------|
| **REST** | [OpenAPI](https://www.openapis.org/) / [Swagger](https://swagger.io/) | Spec YAML → Swagger UI |
| **GraphQL** | Schema introspection | [GraphQL Playground](https://github.com/graphql/graphql-playground) |
| **gRPC** | [Protocol Buffers](https://protobuf.dev/) | `.proto` files → docs |
| **WebSockets** | [AsyncAPI](https://www.asyncapi.com/) | Spec para async APIs |

**Ejemplo OpenAPI:**
```yaml
openapi: 3.0.0
paths:
  /users/{id}:
    get:
      summary: Get user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: User found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
```

---

## 🔐 Autenticación

| Método | What | When | Header |
|:-------|:-----|:-----|:-------|
| **API Key** | String estático | Integraciones internas | `X-API-Key: abc123` |
| **Bearer Token** | JWT en header | SPAs, mobile apps | `Authorization: Bearer <jwt>` |
| **OAuth 2.0** | Delegación con tokens | Third-party integrations | `Authorization: Bearer <access_token>` |
| **Basic Auth** | Usuario:contraseña en base64 | Desarrollo, admin tools | `Authorization: Basic <base64>` |
| **mTLS** | Certificados cliente/servidor | Service-to-service | TLS handshake |

---

## 🎨 Diseño de APIs

| Principio | What | Ejemplo |
|:----------|:-----|:--------|
| **Versionado** | Mantener compatibilidad | `/api/v1/`, `/api/v2/` o header |
| **Paginación** | Evitar payloads gigantes | `?limit=20&offset=40` o cursor |
| **Filtrado** | Permitir búsquedas | `?status=active&role=admin` |
| **Ordenamiento** | Control de orden | `?sort=created_at:desc` |
| **Rate Limiting** | Prevenir abuse | `X-RateLimit-Remaining: 45` |
| **CORS** | Controlar origins | `Access-Control-Allow-Origin: *` |
| **Idempotency Keys** | Evitar duplicados | `Idempotency-Key: uuid` header |

---

## 🔄 Webhooks

**What:** HTTP callbacks cuando ocurre evento.

**Why:** Integración event-driven sin polling.

**Ejemplo:**
```json
POST https://yourapp.com/webhook
X-Signature: sha256=...

{
  "event": "payment.succeeded",
  "data": {
    "amount": 1000,
    "currency": "USD"
  }
}
```

**Seguridad:**
- Validar firma HMAC
- HTTPS obligatorio
- Retry exponential backoff
- Idempotencia en receptor

---

## 📊 Comparación

| Característica | REST | GraphQL | gRPC | WebSocket |
|:---------------|:-----|:--------|:-----|:----------|
| **Protocol** | HTTP | HTTP | HTTP/2 | TCP |
| **Payload** | JSON | JSON | Protobuf | Binary/Text |
| **Typing** | No | Sí (schema) | Sí (protobuf) | No |
| **Streaming** | No | Sí (subscriptions) | Sí | Sí |
| **Caching** | Fácil (HTTP) | Difícil | No | No |
| **Browser Support** | ✅ | ✅ | Limitado | ✅ |
| **Learning Curve** | Bajo | Medio | Alto | Medio |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Verbos en URLs** | `/getUser`, `/createOrder` | Usar HTTP verbs: GET, POST |
| **Sin versionado** | Breaking changes rompen clientes | `/v1/`, deprecation notices |
| **Respuestas inconsistentes** | Diferentes estructuras por endpoint | Estandarizar formato |
| **Sin rate limiting** | Abuse, DDoS | Implementar límites |
| **Exponer IDs internos** | Security risk | Usar UUIDs públicos |

---

## 📚 Recursos

- [REST API Tutorial](https://restfulapi.net/)
- [GraphQL Best Practices](https://graphql.org/learn/best-practices/)
- [gRPC Documentation](https://grpc.io/docs/)
- [WebSocket Protocol RFC](https://datatracker.ietf.org/doc/html/rfc6455)

---

[⬅️ Anterior: Bases de Datos](./10-bases-datos.md) | [⬆️ Volver arriba](#11-apis-y-protocolos) | [➡️ Siguiente: Mobile, UI y UX](./12-mobile-ui-ux.md)