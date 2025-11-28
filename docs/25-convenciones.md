# 25 - Convenciones y Estándares

> Nomenclatura, flujo Git, gestión de dependencias, configuración y convenciones de equipo.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🔤 Nomenclatura](#nomenclatura)
- [📁 Estructura de Carpetas](#estructura-de-carpetas)
- [🔀 Git Workflow](#git-workflow)
- [📦 Gestión de Dependencias](#gestion-de-dependencias)
- [🌍 i18n y l10n](#i18n-y-l10n)
- [⚙️ Configuración y Entornos](#configuracion-y-entornos)
- [🔒 .gitignore](#gitignore)
- [📋 Code Style](#code-style)
- [📝 Comentarios y Documentación](#comentarios-y-documentacion)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 🔤 Nomenclatura

**What:** Reglas consistentes para nombrar variables, funciones, archivos y componentes.

**Why:** Código se lee 10x más que se escribe. Buenos nombres = documentación viva.

**Who:** Todo el equipo, enforcement vía linters.

**When:** Siempre, desde el primer archivo.

**Where:** Todo el codebase sin excepciones.

**How:** Style guides + linters automáticos + code review.

**How much:** Inversión inicial configurar linters (2-4h), ahorra horas en code review.

### Por Lenguaje

| Lenguaje | Variables/Funciones | Clases/Tipos | Constantes | Archivos |
|:---------|:-------------------|:-------------|:-----------|:---------|
| **Python** | `snake_case` | `PascalCase` | `UPPER_SNAKE` | `snake_case.py` |
| **JavaScript/TS** | `camelCase` | `PascalCase` | `UPPER_SNAKE` | `kebab-case.ts` o `PascalCase.tsx` |
| **Java** | `camelCase` | `PascalCase` | `UPPER_SNAKE` | `PascalCase.java` |
| **SQL** | `snake_case` | N/A | N/A | `snake_case` |
| **CSS** | `kebab-case` | N/A | N/A | `kebab-case.css` |

### Principios Generales

| Principio | Mal ❌ | Bien ✅ |
|:----------|:-------|:--------|
| **Descriptivo** | `d`, `tmp`, `data` | `userCreatedAt`, `tempPassword` |
| **Específico** | `process()`, `handle()` | `validateEmail()`, `handleLoginClick()` |
| **Evitar abreviaturas** | `usr`, `btn`, `msg` | `user`, `button`, `message` |
| **Booleanos con is/has** | `active`, `valid` | `isActive`, `hasPermission` |
| **Arrays plurales** | `user`, `data` | `users`, `transactions` |
| **Funciones verbos** | `email()`, `user()` | `sendEmail()`, `getUser()` |

**Excepciones aceptables:**
- Loops: `i`, `j`, `k` (si contexto claro)
- Callbacks: `e` (event), `err` (error)
- Math: `x`, `y`, `z`

---

## 📁 Estructura de Carpetas

**What:** Organización lógica de archivos y directorios en el proyecto.

**Why:** Estructura clara = onboarding rápido, ubicación predecible de archivos, escalabilidad.

**Who:** Architects definen, equipo mantiene.

**When:** Al inicio del proyecto, evolucionando según necesidad.

**Where:** Todo el repositorio.

**How:** Elegir patrón según tamaño y complejidad del proyecto.

**How much:** Decisión temprana de alto impacto, difícil cambiar después.

### Backend - Por Tipo de Fichero

**What:** Agrupar por categoría técnica (controllers, services, models).

**When:** Proyectos pequeños-medianos (< 20 endpoints), equipo único.

**Pros:** ✅ Simple, ✅ Intuitivo para juniors  
**Cons:** ❌ Escala mal, ❌ Difícil encontrar features

```
src/
├── controllers/     # HTTP handlers
│   ├── userController.js
│   ├── orderController.js
│   └── productController.js
├── services/        # Business logic
│   ├── userService.js
│   ├── orderService.js
│   └── emailService.js
├── repositories/    # Data access
│   ├── userRepository.js
│   └── orderRepository.js
├── models/          # Entities, DTOs
│   ├── User.js
│   ├── Order.js
│   └── Product.js
├── middleware/      # Express/FastAPI middleware
│   ├── auth.js
│   ├── errorHandler.js
│   └── logger.js
├── utils/           # Helpers, utilities
│   ├── validators.js
│   └── formatters.js
├── config/          # Configuration
│   ├── database.js
│   └── env.js
└── tests/           # Tests (mirrors src/)
    ├── unit/
    └── integration/
```

### Backend - Por Funcionalidad/Módulo

**What:** Agrupar por feature/bounded context de negocio.

**When:** Proyectos medianos-grandes, múltiples equipos, microservicios.

**Pros:** ✅ Escalable, ✅ Features autónomas, ✅ Ideal para equipos  
**Cons:** ❌ Duplicación inicial, ❌ Puede confundir a juniors

```
src/
├── auth/                    # Feature: Authentication
│   ├── controllers/
│   │   └── authController.js
│   ├── services/
│   │   └── authService.js
│   ├── models/
│   │   └── User.js
│   ├── middleware/
│   │   └── jwtMiddleware.js
│   └── tests/
├── orders/                  # Feature: Order management
│   ├── controllers/
│   ├── services/
│   ├── models/
│   └── tests/
├── products/                # Feature: Product catalog
│   ├── controllers/
│   ├── services/
│   ├── models/
│   └── tests/
└── shared/                  # Código compartido
    ├── database/
    ├── utils/
    └── config/
```

### Backend - Por Arquitectura Hexagonal

**What:** Separar lógica de negocio (core) de infraestructura (adaptadores).

**When:** Dominios complejos, testability crítica, independencia de frameworks.

**Pros:** ✅ Testeable sin infra, ✅ Cambiar DB/framework sin tocar core  
**Cons:** ❌ Más archivos, ❌ Curva de aprendizaje

```
src/
├── domain/                  # Core: Business logic
│   ├── entities/           # Pure domain objects
│   │   ├── User.ts
│   │   └── Order.ts
│   ├── value-objects/      # Immutable values
│   │   ├── Email.ts
│   │   └── Money.ts
│   ├── repositories/       # Interfaces (ports)
│   │   └── IUserRepository.ts
│   └── services/           # Business rules
│       └── OrderService.ts
├── application/             # Use cases
│   ├── commands/           # Write operations
│   │   ├── CreateUserCommand.ts
│   │   └── PlaceOrderCommand.ts
│   └── queries/            # Read operations
│       └── GetUserQuery.ts
├── infrastructure/          # Adapters (implementaciones)
│   ├── repositories/       # DB implementations
│   │   └── PostgresUserRepository.ts
│   ├── http/              # API adapters
│   │   ├── controllers/
│   │   └── routes/
│   ├── messaging/         # Event bus, queues
│   └── persistence/       # Migrations, seeds
└── tests/
    ├── unit/              # Domain + Application
    └── integration/       # Infrastructure
```

### Backend - Por DDD (Domain-Driven Design)

**What:** Organizar por bounded contexts y agregados del dominio.

**When:** Dominios muy complejos, múltiples subdominios, enterprise.

**Pros:** ✅ Refleja negocio, ✅ Ubiquitous language, ✅ Boundaries claros  
**Cons:** ❌ Requiere expertise DDD, ❌ Over-engineering en dominios simples

```
src/
├── contexts/                    # Bounded Contexts
│   ├── sales/                  # Subdominio: Ventas
│   │   ├── domain/
│   │   │   ├── aggregates/    # Order (root), OrderItem
│   │   │   │   ├── Order.ts
│   │   │   │   └── OrderItem.ts
│   │   │   ├── entities/
│   │   │   ├── value-objects/  # Money, Address
│   │   │   ├── events/        # OrderPlaced, OrderShipped
│   │   │   ├── repositories/  # Interfaces
│   │   │   └── services/      # Domain services
│   │   ├── application/       # Use cases
│   │   │   ├── commands/
│   │   │   └── queries/
│   │   ├── infrastructure/    # Adaptadores
│   │   │   ├── persistence/
│   │   │   └── http/
│   │   └── tests/
│   ├── inventory/             # Subdominio: Inventario
│   │   └── (misma estructura)
│   └── shipping/              # Subdominio: Envíos
│       └── (misma estructura)
├── shared-kernel/             # Código compartido entre contexts
│   ├── domain/
│   └── infrastructure/
└── anti-corruption-layer/     # Traducción entre contexts
```

### Frontend - Por Tipo de Fichero

**What:** Agrupar por categoría técnica (components, pages, hooks).

**When:** Proyectos pequeños (< 30 componentes), prototipado rápido.

**Pros:** ✅ Simple, ✅ Flat structure  
**Cons:** ❌ Difícil escalar, ❌ Componentes relacionados separados

```
src/
├── components/          # Todos los componentes
│   ├── Button.tsx
│   ├── Card.tsx
│   ├── Header.tsx
│   └── UserProfile.tsx
├── pages/              # Páginas/Routes
│   ├── Home.tsx
│   ├── Dashboard.tsx
│   └── Profile.tsx
├── hooks/              # Custom hooks
│   ├── useAuth.ts
│   └── useFetch.ts
├── services/           # API calls
│   ├── api.ts
│   └── authService.ts
├── store/              # State management
│   ├── slices/
│   └── store.ts
├── utils/              # Helpers
│   └── formatters.ts
├── types/              # TypeScript types
│   └── User.ts
└── assets/             # Images, fonts
```

### Frontend - Por Funcionalidad/Módulo

**What:** Agrupar por feature de negocio.

**When:** Apps medianas-grandes (> 30 componentes), múltiples features.

**Pros:** ✅ Escalable, ✅ Features autónomas, ✅ Fácil eliminar features  
**Cons:** ❌ Puede tener duplicación compartida

```
src/
├── features/                # Features de negocio
│   ├── auth/               # Feature: Autenticación
│   │   ├── components/
│   │   │   ├── LoginForm.tsx
│   │   │   └── RegisterForm.tsx
│   │   ├── hooks/
│   │   │   └── useAuth.ts
│   │   ├── services/
│   │   │   └── authApi.ts
│   │   ├── store/
│   │   │   └── authSlice.ts
│   │   ├── types/
│   │   │   └── User.ts
│   │   └── pages/
│   │       ├── LoginPage.tsx
│   │       └── RegisterPage.tsx
│   ├── dashboard/          # Feature: Dashboard
│   │   ├── components/
│   │   ├── hooks/
│   │   └── pages/
│   └── profile/            # Feature: Perfil usuario
│       └── (similar)
├── shared/                  # Componentes reutilizables
│   ├── components/         # Button, Card, Modal
│   │   ├── ui/            # Componentes UI básicos
│   │   └── layout/        # Header, Sidebar, Footer
│   ├── hooks/             # useDebounce, useLocalStorage
│   ├── utils/             # Helpers generales
│   └── types/             # Types compartidos
└── app/                    # App-level config
    ├── routes/
    ├── store/
    └── providers/
```

### Frontend - Por Atomic Design

**What:** Jerarquía de componentes: Atoms → Molecules → Organisms → Templates → Pages.

**When:** Design systems, componentes altamente reutilizables, equipos design+dev.

**Pros:** ✅ Reutilización máxima, ✅ Storybook friendly, ✅ Consistencia visual  
**Cons:** ❌ Over-engineering para apps simples, ❌ Puede ser rígido

```
src/
├── components/
│   ├── atoms/              # Componentes básicos indivisibles
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.test.tsx
│   │   │   ├── Button.stories.tsx
│   │   │   └── Button.module.css
│   │   ├── Input/
│   │   ├── Label/
│   │   ├── Icon/
│   │   └── Avatar/
│   ├── molecules/          # Combinación de atoms
│   │   ├── SearchBar/      # Input + Button + Icon
│   │   ├── FormField/      # Label + Input + Error
│   │   ├── Card/           # Container con atoms
│   │   └── MenuItem/
│   ├── organisms/          # Secciones complejas
│   │   ├── Header/         # Logo + SearchBar + UserMenu
│   │   ├── ProductCard/    # Card + Button + Image + Price
│   │   ├── NavigationBar/
│   │   └── CommentThread/
│   ├── templates/          # Layouts de página
│   │   ├── MainLayout/     # Header + Sidebar + Content + Footer
│   │   ├── DashboardLayout/
│   │   └── AuthLayout/
│   └── pages/              # Instancias de templates con data
│       ├── HomePage/
│       ├── DashboardPage/
│       └── ProfilePage/
├── hooks/
├── services/
└── store/
```

### Frontend - Híbrido (Features + Atomic para Shared)

**What:** Features por módulo + Atomic Design para componentes compartidos.

**When:** Mejor de ambos mundos para apps grandes con design system.

**Pros:** ✅ Escalable, ✅ Reutilización, ✅ Features aisladas  
**Cons:** ❌ Más complejo inicialmente

```
src/
├── features/                # Por módulo de negocio
│   ├── auth/
│   │   ├── components/     # Componentes específicos de auth
│   │   │   └── LoginForm.tsx
│   │   ├── hooks/
│   │   └── pages/
│   ├── dashboard/
│   └── products/
└── shared/                  # Atomic Design para compartidos
    ├── atoms/              # Button, Input, Icon
    ├── molecules/          # SearchBar, FormField
    ├── organisms/          # Header, Sidebar
    ├── templates/          # MainLayout, DashboardLayout
    ├── hooks/
    └── utils/
```

### Monorepo

**What:** Múltiples apps/packages en un repositorio.

**When:** Microservicios, múltiples frontends, librerías compartidas.

**Pros:** ✅ Código compartido fácil, ✅ Atomic commits cross-repo  
**Cons:** ❌ Build más complejo, ❌ Requiere tooling (Nx, Turborepo)

```
monorepo/
├── apps/                    # Aplicaciones
│   ├── web/                # Frontend web (Next.js)
│   ├── mobile/             # Mobile app (React Native)
│   ├── admin/              # Admin panel
│   ├── api/                # Backend API
│   └── workers/            # Background jobs
├── packages/                # Librerías compartidas
│   ├── ui/                 # Design system compartido
│   │   ├── components/
│   │   └── package.json
│   ├── utils/              # Utilidades compartidas
│   ├── types/              # TypeScript types compartidos
│   ├── config/             # Configs (ESLint, TS, etc)
│   └── api-client/         # Cliente API compartido
├── tools/                   # Scripts build, codegen
├── docs/                    # Documentación
├── package.json            # Root package
├── turbo.json              # Turborepo config
└── nx.json                 # Nx config (alternativa)
```

### Comparación y Decisión

| Estructura | Proyecto Ideal | Complejidad | Escalabilidad | Curva Aprendizaje |
|:-----------|:--------------|:------------|:--------------|:------------------|
| **Por Tipo** | Pequeño, 1 equipo | Baja ⭐ | Baja ⭐⭐ | Baja ⭐ |
| **Por Funcionalidad** | Mediano-grande, múltiples features | Media ⭐⭐ | Alta ⭐⭐⭐⭐ | Media ⭐⭐ |
| **Hexagonal** | Testability crítica, cambios frecuentes de infra | Alta ⭐⭐⭐ | Alta ⭐⭐⭐⭐ | Alta ⭐⭐⭐⭐ |
| **DDD** | Dominio muy complejo, enterprise | Muy Alta ⭐⭐⭐⭐ | Muy Alta ⭐⭐⭐⭐⭐ | Muy Alta ⭐⭐⭐⭐⭐ |
| **Atomic Design** | Design system, componentes reutilizables | Media ⭐⭐⭐ | Media ⭐⭐⭐ | Media ⭐⭐⭐ |
| **Monorepo** | Múltiples apps relacionadas | Alta ⭐⭐⭐⭐ | Muy Alta ⭐⭐⭐⭐⭐ | Alta ⭐⭐⭐⭐ |

**Recomendación general:**
- **Startup/MVP:** Por Tipo (simple y rápido)
- **Producto creciendo:** Por Funcionalidad (escala mejor)
- **Enterprise:** DDD o Hexagonal (testability, complejidad)
- **Design System:** Atomic Design
- **Múltiples apps:** Monorepo

---

## 🔀 Git Workflow

**What (Qué es):** Convenciones para branches, commits y merges.

**Why (Por qué):** Historial limpio, deployment predecible, colaboración efectiva.

**Who (Quién):** Todo el equipo, enforcement vía Git hooks.

**When (Cuándo):** Cada commit, cada branch, cada merge.

**Where (Dónde):** Repositorio Git.

**How (Cómo):** Naming conventions + Conventional Commits + Git hooks.

**How much (Cuánto):** Setup inicial 1-2h, ahorra horas en debugging histórico.

### Branch Naming

| Tipo | Formato | Ejemplo |
|:-----|:--------|:--------|
| **Feature** | `feature/descripcion-corta` | `feature/user-authentication` |
| **Bugfix** | `fix/descripcion-bug` | `fix/login-redirect-loop` |
| **Hotfix** | `hotfix/descripcion` | `hotfix/critical-security-patch` |
| **Refactor** | `refactor/descripcion` | `refactor/extract-user-service` |
| **Docs** | `docs/descripcion` | `docs/api-documentation` |
| **Chore** | `chore/descripcion` | `chore/update-dependencies` |

### Conventional Commits

**Formato:** `<type>(<scope>): <description>`

**Tipos:**
- `feat`: Nueva feature
- `fix`: Bug fix
- `docs`: Solo documentación
- `style`: Formato (no cambia lógica)
- `refactor`: Ni fix ni feature
- `test`: Agregar tests
- `chore`: Mantenimiento (deps, config)
- `perf`: Mejora performance

**Ejemplos:**
```bash
feat(auth): add JWT authentication
fix(api): handle null user in /profile endpoint
docs(readme): update installation instructions
refactor(user-service): extract validation logic
test(auth): add unit tests for login flow
chore(deps): upgrade React to 18.2
```

**Herramientas:** [commitlint](https://commitlint.js.org/), [husky](https://typicode.github.io/husky/)

### GitFlow vs Trunk-Based

| Aspecto | GitFlow | Trunk-Based |
|:--------|:--------|:------------|
| **Branches** | `main`, `develop`, `feature/*`, `release/*`, `hotfix/*` | `main`, `feature/*` (short-lived) |
| **Merge a main** | Via `release` branch | Directo (tras CI/CD) |
| **Feature lifetime** | Días/semanas | <24 horas ideal |
| **Cuándo usar** | Releases planificados, equipos grandes | CI/CD continuo, deploy frecuente |

**Trunk-Based (recomendado moderno):**
```
main ─────●─────●─────●────→ (siempre deployable)
           ↖    ↗
         feature (merge rápido)
```

---

## 📦 Gestión de Dependencias

### Package Managers

| Lenguaje | Manager | Lock File | Comando Install |
|:---------|:--------|:----------|:----------------|
| **JavaScript** | npm, pnpm, yarn | `package-lock.json`, `pnpm-lock.yaml` | `npm install` |
| **Python** | pip, poetry, conda | `requirements.txt`, `poetry.lock` | `pip install -r requirements.txt` |
| **Java** | Maven, Gradle | `pom.xml`, `gradle.lock` | `mvn install` |
| **Go** | go modules | `go.sum` | `go mod download` |
| **Rust** | Cargo | `Cargo.lock` | `cargo build` |

### Best Practices

| Práctica | Why | Cómo |
|:---------|:----|:-----|
| **Pin versions** | Reproducibilidad | `react@18.2.0` no `react@^18.0.0` (prod) |
| **Commit lock files** | Builds deterministas | Git add `package-lock.json` |
| **Security scanning** | Detectar CVEs | Dependabot, Snyk, `npm audit` |
| **Update regularmente** | Evitar tech debt | Mensual, usar bots |
| **Minimizar deps** | Menos superficie ataque | Evaluar cada nueva dep |

**Versioning (SemVer):**
```
1.2.3
│ │ └─ PATCH: Bug fixes
│ └─── MINOR: New features (backward compatible)
└───── MAJOR: Breaking changes
```

**Ranges:**
- `1.2.3`: Exacto
- `^1.2.3`: Compatible con 1.x.x (>= 1.2.3 < 2.0.0)
- `~1.2.3`: Patch updates (>= 1.2.3 < 1.3.0)

---

## 🌍 i18n y l10n

**i18n:** Internationalization (preparar app para múltiples idiomas)  
**l10n:** Localization (traducir para región específica)

### Estructura

```javascript
// locales/en.json
{
  "common": {
    "welcome": "Welcome",
    "logout": "Log out"
  },
  "errors": {
    "notFound": "Page not found",
    "serverError": "Something went wrong"
  }
}

// locales/es.json
{
  "common": {
    "welcome": "Bienvenido",
    "logout": "Cerrar sesión"
  }
}
```

### Best Practices

| Práctica | Cómo |
|:---------|:-----|
| **Claves descriptivas** | `user.profile.editButton` no `btn1` |
| **Pluralización** | Usar librería con soporte (ICU) |
| **Variables** | `"Hello {{name}}"` con interpolación |
| **Formatos** | Usar `Intl` para fechas, monedas, números |
| **RTL support** | CSS con `dir="auto"` |

**Herramientas:**
- [i18next](https://www.i18next.com/) (JS)
- [react-intl](https://formatjs.io/docs/react-intl/) (React)
- [django-modeltranslation](https://django-modeltranslation.readthedocs.io/) (Django)

---

## ⚙️ Configuración y Entornos

### Environments

| Ambiente | Propósito | Características |
|:---------|:----------|:----------------|
| **local** | Desarrollo individual | DB local, debug on, hot reload |
| **dev** | Integración equipo | Shared DB dev, CI/CD, feature branches |
| **staging** | Pre-producción | Datos prod-like, testing final |
| **production** | Usuarios reales | Alta disponibilidad, monitoreo, backups |

### 12-Factor App Config

**Principio:** Config en environment variables, no en código.

```python
# ❌ Mal
DATABASE_URL = "postgresql://localhost/mydb"

# ✅ Bien
import os
DATABASE_URL = os.getenv("DATABASE_URL")
```

**`.env` (solo local, no commitear):**
```bash
DATABASE_URL=postgresql://localhost/mydb
SECRET_KEY=dev-secret-key-not-for-prod
DEBUG=true
```

**Producción:** Usar secrets managers (Vault, AWS Secrets Manager).

---

## 🔒 .gitignore

**Esenciales:**

```gitignore
# Dependencies
node_modules/
venv/
.venv/

# Build outputs
dist/
build/
*.pyc
__pycache__/

# Environment
.env
.env.local

# IDEs
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Testing
coverage/
.pytest_cache/
```

---

## 📋 Code Style

### Formatters (automático)

| Lenguaje | Herramienta | Config |
|:---------|:------------|:-------|
| **JavaScript/TS** | Prettier | `.prettierrc` |
| **Python** | Black, Ruff | `pyproject.toml` |
| **Java** | google-java-format | Maven/Gradle plugin |

### Linters (reglas)

| Lenguaje | Herramienta | Config |
|:---------|:------------|:-------|
| **JavaScript/TS** | ESLint | `.eslintrc.json` |
| **Python** | Pylint, Ruff | `.pylintrc` |
| **Java** | Checkstyle | `checkstyle.xml` |

**Setup:**
```json
// package.json
{
  "scripts": {
    "lint": "eslint src/",
    "format": "prettier --write src/",
    "format:check": "prettier --check src/"
  },
  "husky": {
    "hooks": {
      "pre-commit": "npm run format && npm run lint"
    }
  }
}
```

---

## 📝 Comentarios y Documentación

### Cuándo comentar

| ✅ Comentar | ❌ No comentar |
|:-----------|:---------------|
| **Por qué** existe código complejo | Qué hace (obvio del código) |
| Workarounds temporales | Código autoexplicativo |
| Decisiones arquitecturales | Restating código en español |
| Algoritmos no obvios | TODOs sin contexto |

**Ejemplo:**
```typescript
// ❌ Mal: restating
// Incrementa contador
counter++;

// ✅ Bien: explica por qué
// Workaround: API retorna duplicados, deduplicar manualmente
// TODO: Reportar bug al team de backend (ticket: API-123)
const uniqueUsers = [...new Set(users)];
```

### JSDoc / Docstrings

**Python:**
```python
def calculate_discount(price: float, discount_percent: float) -> float:
    """
    Calcula precio con descuento aplicado.

    Args:
        price: Precio original
        discount_percent: Porcentaje de descuento (0-100)

    Returns:
        Precio final con descuento aplicado

    Raises:
        ValueError: Si discount_percent < 0 o > 100
    """
    if not 0 <= discount_percent <= 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```

**TypeScript:**
```typescript
/**
 * Validates email format using RFC 5322 regex
 * @param email - Email address to validate
 * @returns true if valid, false otherwise
 * @example
 * isValidEmail("user@example.com") // true
 * isValidEmail("invalid") // false
 */
function isValidEmail(email: string): boolean {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
}
```

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Inconsistencia** | Parte camelCase, parte snake_case | Style guide + linter |
| **Magic numbers** | `if (status === 3)` | `if (status === OrderStatus.COMPLETED)` |
| **Branches long-lived** | Merge conflicts, context switching | Feature flags, trunk-based |
| **.env en Git** | Secrets públicos | `.gitignore`, educación |
| **Sin lock files** | "Works on my machine" | Commitear lock files |

---

## 📚 Recursos

- [Conventional Commits](https://www.conventionalcommits.org/)
- [SemVer](https://semver.org/)
- [12 Factor App](https://12factor.net/)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google Style Guides](https://google.github.io/styleguide/)

---

[⬅️ Anterior: Documentación y Diagramas](./24-documentacion-diagramas.md) | [⬆️ Volver arriba](#) | [➡️ Siguiente: Onboarding](./26-onboarding.md)