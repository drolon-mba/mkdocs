# 11 - Mobile, UI y UX

> Desarrollo móvil, diseño de interfaces y experiencia de usuario para apps efectivas y deleitables.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [📱 Mobile Development](#mobile-development)
- [🎨 UI (Interfaz de Usuario)](#ui-interfaz-de-usuario)
- [🧭 UX (Experiencia de Usuario)](#ux-experiencia-de-usuario)
- [🚫 Anti-patrones](#anti-patrones)
- [📚 Recursos](#recursos)
---

## 📱 Mobile Development

**What:** Desarrollo de aplicaciones para dispositivos móviles (iOS, Android).

**Why:** 60%+ del tráfico web es móvil. UX nativa crítica para engagement.

**Who:** Mobile developers, full-stack developers.

---

### Enfoques de Desarrollo

| Enfoque | What | Why | When | Trade-offs |
|:--------|:-----|:----|:-----|:-----------|
| **Nativo** | Lenguaje específico por plataforma | Máxima performance, acceso completo a APIs | Apps complejas, alta calidad | ✅ Performance, UX nativa<br>❌ 2 codebases, costoso |
| **Multiplataforma** | Un código para iOS + Android | Ahorro tiempo/costo, consistencia | Mayoría de apps comerciales | ✅ Velocidad desarrollo<br>❌ Limitaciones platform-specific |
| **Híbrido** | Web app en webview nativo | Reutilizar web skills | MVPs, apps simples | ✅ Rapidez<br>❌ Performance inferior |
| **PWA** | Web app con features nativas | Sin app stores, updates automáticos | Web-first con funcionalidad offline | ✅ Sin aprobación stores<br>❌ Limitaciones iOS |

---

### Tecnologías

| Stack | What | When | Features |
|:------|:-----|:-----|:---------|
| **iOS Nativo** | [SwiftUI](https://developer.apple.com/xcode/swiftui/) + Swift | Apps solo iOS, máxima calidad | Declarative UI, Combine, async/await |
| **Android Nativo** | [Jetpack Compose](https://developer.android.com/jetpack/compose) + Kotlin | Apps solo Android | Declarative UI, Kotlin coroutines |
| **React Native** | [React Native](https://reactnative.dev/) | Reutilizar skills React | Hot reload, large ecosystem |
| **Flutter** | [Flutter](https://flutter.dev/) (Dart) | Performance + custom UI | Propio rendering engine, widgets |
| **Ionic** | [Ionic](https://ionicframework.com/) (Angular/React/Vue) | Reutilizar web frameworks | Capacitor para native APIs |
| **Kotlin Multiplatform** | [KMP](https://kotlinlang.org/docs/multiplatform.html) | Compartir lógica, UI nativa | Shared business logic |

---

### Patrones Mobile

| Patrón | What | Why | How |
|:-------|:-----|:----|:----|
| **Offline-First** | App funciona sin internet | UX resiliente | SQLite, sync cuando online |
| **Deep Linking** | Links abren secciones específicas | Navigation desde web/notifs | URL schemes, Universal Links |
| **Push Notifications** | Notificaciones remotas | Re-engagement | FCM (Firebase), APNs |
| **Background Sync** | Sincronizar en background | Datos actualizados | WorkManager (Android), BackgroundTasks (iOS) |
| **Biometric Auth** | Face ID, Touch ID | Seguridad + UX | Local Authentication framework |

---

## 🎨 UI (Interfaz de Usuario)

**What:** Capa visual con la que usuarios interactúan.

**Why:** Primera impresión, usabilidad, brand.

---

### Principios de Diseño

| Principio | What | How |
|:----------|:-----|:----|
| **Consistencia** | Patrones repetibles | Mismo estilo para acciones similares |
| **Jerarquía Visual** | Guiar la atención | Tamaños, colores, contraste |
| **Feedback** | Confirmar acciones | Loaders, toasts, animaciones |
| **Affordance** | Comunicar qué es clickeable | Botones parecen clickeables |
| **Whitespace** | Espacio respirable | No apretujar elementos |

---

### Design Systems

| Sistema | What | When |
|:--------|:-----|:-----|
| [Material Design](https://m3.material.io/) | Sistema de Google | Apps Android, web moderna |
| [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) | Guidelines de Apple | Apps iOS |
| [Fluent Design](https://www.microsoft.com/design/fluent/) | Sistema de Microsoft | Windows apps |
| [Ant Design](https://ant.design/) | Enterprise UI | Dashboards, admin panels |
| [Chakra UI](https://chakra-ui.com/) | Component library accesible | React apps |

---

### Componentización

| Aspecto | What | Ejemplo |
|:--------|:-----|:--------|
| **Atomic Design** | Átomos → Moléculas → Organismos | Button → SearchBar → Header |
| **Props/State** | Configuración vs estado interno | `<Button variant="primary" />` |
| **Composition** | Componentes dentro de componentes | `<Card><Header/><Body/></Card>` |
| **Theming** | Tokens de diseño reutilizables | `--color-primary`, `--spacing-md` |

---

### Responsividad

| Técnica | What | When |
|:--------|:-----|:-----|
| **Media Queries** | CSS condicional por pantalla | Layouts diferentes mobile/desktop |
| **Fluid Typography** | Tamaños escalables | `clamp(1rem, 2.5vw, 2rem)` |
| **Container Queries** | Condicional por contenedor | Componentes adaptativos |
| **Mobile-First** | Diseñar desde móvil | Mayoría del tráfico |

---

## 🧭 UX (Experiencia de Usuario)

**What:** Cómo se siente usar el producto.

**Why:** UX pobre = abandono. UX excelente = lealtad.

---

### Principios UX

| Principio | What | How |
|:----------|:-----|:----|
| **Don't Make Me Think** | Interfaz intuitiva | Patrones conocidos, etiquetas claras |
| **Prevención de Errores** | Evitar errores del usuario | Validaciones, deshabilitación, confirmaciones |
| **Feedback Inmediato** | Respuesta rápida | Spinners, progress bars, optimistic UI |
| **Simplicidad** | Menos es más | Ocultar complejidad, defaults sensatos |
| **Flujo Natural** | Secuencia lógica | Wizard steps, breadcrumbs |

---

### Research & Testing

| Método | What | When | Output |
|:-------|:-----|:-----|:-------|
| **User Interviews** | Entrevistas 1:1 | Discovery, validación | Insights, pain points |
| **Usability Testing** | Observar usuarios usando prototipo | Pre-lanzamiento | Fricciones, confusiones |
| **A/B Testing** | Comparar variantes | Post-lanzamiento | Conversión, engagement |
| **Heatmaps** | Dónde clickean usuarios | Optimización | Áreas de interés |
| **Analytics** | Métricas comportamiento | Continuo | Funnels, drop-offs |

---

### Accesibilidad (a11y)

**What:** Diseño inclusivo para todos los usuarios, incluyendo discapacidades.

**Why:** Ético, legal (WCAG), amplía audiencia.

| Aspecto | What | How | Herramientas |
|:--------|:-----|:----|:-------------|
| **Contraste** | Texto legible | Min 4.5:1 (AA), 7:1 (AAA) | [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) |
| **Keyboard Nav** | Navegable sin mouse | Tab order, Enter/Space | Test manual |
| **Screen Readers** | Lectura de contenido | Roles ARIA, alt text | [NVDA](https://www.nvaccess.org/), [VoiceOver](https://www.apple.com/accessibility/voiceover/) |
| **Focus Visible** | Indicar elemento activo | Outline claro | CSS `:focus-visible` |
| **Alt Text** | Descripción de imágenes | `<img alt="Description">` | Linters |
| **Semantic HTML** | Tags correctos | `<button>`, `<nav>`, `<main>` | [axe DevTools](https://www.deque.com/axe/devtools/) |

---

### Performance UX

| Métrica | What | Target | Impacto |
|:--------|:-----|:-------|:--------|
| **FCP** | First Contentful Paint | < 1.8s | Primera impresión |
| **LCP** | Largest Contentful Paint | < 2.5s | Contenido principal visible |
| **FID** | First Input Delay | < 100ms | Interactividad |
| **CLS** | Cumulative Layout Shift | < 0.1 | Estabilidad visual |
| **TTI** | Time To Interactive | < 3.8s | Usabilidad completa |

---

### Animaciones

| Uso | What | When | Duración |
|:----|:-----|:-----|:---------|
| **Micro-interactions** | Feedback sutil | Hover, click | 100-200ms |
| **Transiciones** | Cambios suaves | Cambios de estado | 200-400ms |
| **Loading** | Indicar progreso | Operaciones async | Mientras dure |
| **Delight** | Sorprender positivamente | Momentos clave | 500-1000ms |

**Herramientas:** [Framer Motion](https://www.framer.com/motion/), [Lottie](https://airbnb.design/lottie/), [GSAP](https://greensock.com/gsap/)

---

### Patterns UX

| Pattern | What | When |
|:--------|:-----|:-----|
| **Progressive Disclosure** | Mostrar gradualmente | Wizards, formularios largos |
| **Skeleton Screens** | Placeholder mientras carga | Listas, cards |
| **Infinite Scroll** | Cargar más al scrollear | Feeds sociales |
| **Pull to Refresh** | Actualizar con gesto | Apps móviles |
| **Empty States** | UI cuando no hay datos | Primera vez, sin resultados |
| **Confirmation Dialogs** | Validar acciones destructivas | Borrar, cancelar suscripción |

---

## 🚫 Anti-patrones

| Anti-patrón | Problema | Solución |
|:------------|:---------|:---------|
| **Dark Patterns** | Manipular para decisiones no deseadas | Diseño ético, transparente |
| **Carousels** | Baja conversión, accesibilidad | Evitar o hacer pausable |
| **Pop-ups agresivos** | Frustración, abandono | Timing apropiado, fácil cerrar |
| **Formularios largos** | Alta fricción | Multi-step, autocompletado |
| **Inconsistencia** | Confusión | Design system, componentes |

---

## 📚 Recursos

- [Nielsen Norman Group](https://www.nngroup.com/)
- [Laws of UX](https://lawsofux.com/)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Material Design](https://m3.material.io/)
- [Refactoring UI](https://www.refactoringui.com/)

---

[⬅️ Anterior: APIs y Protocolos](./10-apis-protocolos.md) | [⬆️ Volver arriba](#) | [➡️ Siguiente: Infraestructura Cloud](./12-infraestructura-cloud.md)