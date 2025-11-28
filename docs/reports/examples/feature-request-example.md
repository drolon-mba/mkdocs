## 💡 Feature Request

### 📌 Resumen
Agregar "Dark Mode" automático basado en preferencias del sistema operativo.

---

### 😫 El Problema
**¿Qué problema estamos tratando de resolver?**
Como usuario que trabaja de noche o en entornos con poca luz, la interfaz actual (solo clara) causa fatiga visual. Muchos usuarios ya tienen su SO configurado en modo oscuro y esperan que la web se adapte automáticamente.

**Impacto actual:**
- [ ] Bloqueante
- [x] Molestia alta (feedback recurrente en encuestas)
- [ ] Mejora de calidad de vida

---

### 🚀 La Solución Propuesta
Implementar un theme switcher que detecte `prefers-color-scheme: dark` y aplique las variables CSS de modo oscuro automáticamente.

**Flujo deseado:**
1. Usuario entra a la app por primera vez.
2. App detecta configuración del SO.
3. Si es Dark, carga theme oscuro. Si es Light, carga claro.
4. Usuario puede forzar el cambio manual desde el perfil.

**Criterios de Aceptación:**
- [ ] Detecta preferencia de SO al inicio.
- [ ] Persiste preferencia manual en LocalStorage.
- [ ] Transición suave entre temas (sin flash of wrong theme).
- [ ] Todos los componentes tienen contraste accesible en ambos modos.

---

### 🔄 Alternativas Consideradas
- **Opción A:** Mantener solo modo claro. (Descartado: competidores tienen dark mode, es estándar de industria).
- **Opción B:** Botón manual sin detección automática. (Menor UX, usuario tiene que configurarlo cada vez si borra cookies).

---

### 📊 Valor / Beneficio
**¿Por qué deberíamos construir esto ahora?**
- [x] Retención de usuarios (Mejora UX)
- [ ] Nuevas ventas
- [ ] Eficiencia operativa
- [ ] Reducción de deuda técnica

---

### 🔗 Referencias
- Ticket de diseño: #DES-123
- Figma Mockups: [Link]
