# 09 - Bases de Datos

> Sistemas de almacenamiento estructurado para datos persistentes, relacionales y no relacionales.

[🏠 Volver al índice](./00-indice.md)

---

## 🎯 Elegir Base de Datos

**What:** Decisión arquitectónica fundamental sobre cómo persistir datos.

**Why:** Cada tipo optimiza diferentes trade-offs (ACID, escalabilidad, flexibilidad).

**Who:** Arquitectos, DBAs, tech leads.

**How much:** Decisión crítica difícil de revertir. Evaluar con PoC.

---

## 🗄️ SQL (Relacionales)

**What:** Bases con esquema fijo, relaciones explícitas, ACID garantizado.

**Why:** Integridad referencial, transacciones complejas, queries potentes.

| DB | What | Why | When | Trade-offs |
|:---|:-----|:----|:-----|:-----------|
| [PostgreSQL](https://www.postgresql.org/) | RDBMS open-source más avanzado | JSONB, full-text search, extensiones | Default para apps modernas | ✅ Feature-rich, performance<br>❌ Scaling vertical |
| [MySQL](https://www.mysql.com/) | RDBMS popular, ecosistema maduro | Simplicidad, InnoDB engine | WordPress, apps web tradicionales | ✅ Simple, ampliamente conocido<br>❌ Menos features que PostgreSQL |
| [SQL Server](https://www.microsoft.com/sql-server) | RDBMS de Microsoft | Integración .NET, herramientas enterprise | Ecosistema Microsoft | ✅ Herramientas gráficas potentes<br>❌ Licencia costosa |
| [Oracle](https://www.oracle.com/database/) | RDBMS enterprise líder | Features avanzadas, soporte 24/7 | Grandes corporaciones, compliance | ✅ Robusto, compliance<br>❌ Muy costoso |
| [MariaDB](https://mariadb.org/) | Fork de MySQL con mejoras | Drop-in replacement MySQL | Migrar desde MySQL | ✅ Open source puro<br>❌ Comunidad más pequeña |

---

## 📄 NoSQL

**What:** Bases schema-less, escalabilidad horizontal, eventual consistency.

**Why:** Flexibilidad de esquema, performance en lecturas masivas.

### Document Stores

| DB | What | When | Use Case |
|:---|:-----|:-----|:---------|
| [MongoDB](https://www.mongodb.com/) | Documentos JSON con índices | Esquema flexible, prototipos rápidos | CMS, catálogos, perfiles usuario |
| [CouchDB](https://couchdb.apache.org/) | Documentos con sync multi-master | Offline-first, replicación | Apps móviles con sync |
| [Firestore](https://firebase.google.com/products/firestore) | Document DB de Google | Apps móviles, real-time | Chat, dashboards colaborativos |

### Key-Value Stores

| DB | What | When | Use Case |
|:---|:-----|:-----|:---------|
| [Redis](https://redis.io/) | In-memory con persistencia opcional | Caching, sesiones, pub/sub | Cache, rate limiting, leaderboards |
| [Memcached](https://memcached.org/) | In-memory puro (no persistencia) | Cache simple, ultra-rápido | Cache de objetos |
| [DynamoDB](https://aws.amazon.com/dynamodb/) | Key-value serverless de AWS | Scaling automático, alta disponibilidad | Apps serverless, IoT |

### Columnar

| DB | What | When | Use Case |
|:---|:-----|:-----|:---------|
| [ClickHouse](https://clickhouse.com/) | Columnar para analítica | Queries agregadas en TB de datos | Analytics, logs, eventos |
| [Apache Druid](https://druid.apache.org/) | Real-time analytics | Queries sub-segundo en streams | Dashboards en tiempo real |
| [Cassandra](https://cassandra.apache.org/) | Wide-column distribuida | Writes masivos, alta disponibilidad | Time-series, IoT, messaging |

### Graph

| DB | What | When | Use Case |
|:---|:-----|:-----|:---------|
| [Neo4j](https://neo4j.com/) | Graph DB líder | Relaciones complejas | Redes sociales, recomendaciones, fraude |
| [ArangoDB](https://www.arangodb.com/) | Multi-model (document + graph) | Flexibilidad model | Apps con datos relacionales y grafo |

---

## ⏱️ Time Series

**What:** Optimizadas para datos con timestamp (métricas, logs, sensores).

| DB | What | When | Features |
|:---|:-----|:-----|:---------|
| [InfluxDB](https://www.influxdata.com/) | Time-series purpose-built | Métricas, IoT | Retention policies, downsampling |
| [TimescaleDB](https://www.timescale.com/) | Extensión PostgreSQL | Ya usas PostgreSQL | SQL + optimizaciones time-series |
| [Prometheus](https://prometheus.io/) | Time-series para métricas | Monitoring | Pull model, PromQL |

---

## 🔍 Search Engines

**What:** Optimizadas para búsqueda full-text y analítica.

| DB | What | When | Features |
|:---|:-----|:-----|:---------|
| [Elasticsearch](https://www.elastic.co/elasticsearch/) | Search + analytics | Búsqueda compleja, logs | Full-text, agregaciones, Kibana |
| [Apache Solr](https://solr.apache.org/) | Search basado en Lucene | Búsqueda empresarial | Faceting, highlighting |
| [Meilisearch](https://www.meilisearch.com/) | Search API-first | Búsqueda simple, UX | Typo-tolerant, rápido setup |

---

## 🗃️ Embedded

**What:** Bases livianas embebidas en la aplicación.

| DB | What | When | Use Case |
|:---|:-----|:-----|:---------|
| [SQLite](https://www.sqlite.org/) | SQL embebido, single-file | Apps móviles, tests, prototipos | Local storage, demos |
| [H2](https://www.h2database.com/) | SQL Java embebido | Tests Java | In-memory testing |
| [LevelDB](https://github.com/google/leveldb) | Key-value embebido | Bases para otras DBs | Chrome, Bitcoin Core |

---

## 🔄 NewSQL

**What:** SQL con escalabilidad horizontal (mejor de ambos mundos).

| DB | What | When | Trade-offs |
|:---|:-----|:-----|:-----------|
| [CockroachDB](https://www.cockroachlabs.com/) | PostgreSQL distribuido | Global apps, alta disponibilidad | ✅ Geo-distributed<br>❌ Latencia mayor |
| [Google Spanner](https://cloud.google.com/spanner/) | SQL global con TrueTime | Transacciones globales | ✅ Consistencia fuerte global<br>❌ Costoso |
| [YugabyteDB](https://www.yugabyte.com/) | PostgreSQL + Cassandra | PostgreSQL con scale-out | ✅ Compatible PostgreSQL<br>❌ Operacionalmente complejo |

---

## 🎯 Decisión según Caso de Uso

| Caso | Recomendación | Por qué |
|:-----|:--------------|:--------|
| **App web CRUD** | PostgreSQL | ACID, relaciones, features |
| **Analytics** | ClickHouse, BigQuery | Queries agregadas en TB |
| **Cache** | Redis | In-memory, TTL, estructuras |
| **Búsqueda** | Elasticsearch | Full-text, faceting |
| **Real-time** | DynamoDB, Firestore | Low latency, serverless |
| **Graph/Social** | Neo4j | Traversals eficientes |
| **Time-series** | InfluxDB, TimescaleDB | Retention, downsampling |
| **Mobile offline** | SQLite, Realm | Embedded, sync |

---

## 📐 Diseño de Esquema

### SQL

| Principio | What | Ejemplo |
|:----------|:-----|:--------|
| **Normalización** | Eliminar redundancia | 3NF: sin dependencias transitivas |
| **Denormalización** | Duplicar para performance | Agregar campos calculados |
| **Foreign Keys** | Integridad referencial | `user_id REFERENCES users(id)` |
| **Indexes** | Optimizar queries | Index en columnas de WHERE, JOIN |

### NoSQL

| Principio | What | Ejemplo |
|:----------|:-----|:--------|
| **Modelar por queries** | Diseñar según lectura | Duplicar datos si optimiza queries |
| **Desnormalizar** | Embeber documentos relacionados | User con embedded addresses |
| **Evitar JOINs** | No hay JOINs eficientes | Duplicar datos necesarios |

---

## 🔧 Optimización

| Técnica | What | When | How |
|:--------|:-----|:-----|:----|
| **Indexing** | Acelerar búsquedas | Columnas en WHERE, JOIN | Evitar sobre-indexar (slow writes) |
| **Partitioning** | Dividir tabla en chunks | Tablas > 10M rows | Por fecha, rango de IDs |
| **Vacuum/Analyze** | Mantener estadísticas | PostgreSQL periódicamente | `VACUUM ANALYZE` automático |
| **Connection Pooling** | Reutilizar conexiones | Siempre | PgBouncer, HikariCP |
| **Query Plan Analysis** | Entender ejecución | Queries lentos | `EXPLAIN ANALYZE` |

---

## 🔒 Transacciones

| Concepto | What | Ejemplo |
|:---------|:-----|:--------|
| **ACID** | Atomicity, Consistency, Isolation, Durability | PostgreSQL, MySQL InnoDB |
| **Isolation Levels** | Read Uncommitted < Read Committed < Repeatable Read < Serializable | Trade-off: consistency vs performance |
| **Deadlocks** | Dos transacciones esperan mutuamente | Timeout + retry con exponential backoff |
| **Optimistic Locking** | Versionar registros | `UPDATE ... WHERE version = X` |
| **Pessimistic Locking** | Lock explícito | `SELECT ... FOR UPDATE` |

---

## 🔄 Migraciones

| Herramienta | What | When |
|:------------|:-----|:-----|
| [Flyway](https://flywaydb.org/) | Versionado SQL scripts | Java ecosystem |
| [Liquibase](https://www.liquibase.org/) | Migraciones XML/YAML | Multi-DB support |
| [Alembic](https://alembic.sqlalchemy.org/) | Migraciones Python | SQLAlchemy projects |
| [TypeORM](https://typeorm.io/) | Migraciones TypeScript | Node.js + TypeScript |

**Best Practices:**
- Migraciones en un solo sentido (forward-only)
- Testear en staging primero
- Migraciones idempotentes
- Backup antes de migrar

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Sin índices** | Full table scans | Indexar WHERE, JOIN columns |
| **Sobre-indexar** | Writes lentos | Solo índices usados frecuentemente |
| **EAV (Entity-Attribute-Value)** | Queries complejas, sin tipado | Usar JSONB o document DB |
| **VARCHAR(255) everywhere** | Desperdicio espacio | Tamaño apropiado por columna |
| **FLOAT para dinero** | Errores de precisión | DECIMAL o NUMERIC |
| **No usar transacciones** | Datos inconsistentes | Wrap operaciones relacionadas |

---

## 📚 Recursos

- [Use The Index, Luke](https://use-the-index-luke.com/)
- [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)
- [MongoDB University](https://university.mongodb.com/)
- [Database Internals - Alex Petrov](https://www.databass.dev/)

---

[⬅️ Anterior: Performance](./08-performance.md) | [⬆️ Volver arriba](#09---bases-de-datos) | [➡️ Siguiente: APIs y Protocolos](./10-apis-protocolos.md)