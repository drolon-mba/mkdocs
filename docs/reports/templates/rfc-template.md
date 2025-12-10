# 📝 RFC: Request for Comments

## ℹ️ Meta Información

- **RFC ID:** [RFC-000]
- **Título:** [Título descriptivo]
- **Autor:** [Nombre]
- **Estado:** [Draft / Review / Approved / Rejected]
- **Fecha:** [YYYY-MM-DD]

---

## 📋 Contexto y Alcance

[Describe el contexto. ¿Por qué estamos proponiendo esto? ¿Cuál es el objetivo?]

---

## 🏗️ Diseño Propuesto

[Detalles técnicos de la solución. Diagramas, esquemas de DB, APIs, etc.]

**Arquitectura:**

- Componente A habla con B mediante...

**Modelo de Datos:**

```sql
CREATE TABLE ...
```

**API:**

- `POST /api/v1/resource`

---

## 🔄 Alternativas Consideradas

[Es crítico listar qué otras opciones se evaluaron y por qué se descartaron]

1. **Opción A:** ...
2. **Opción B:** ...

---

## ⚠️ Riesgos y Desafíos

- **Seguridad:** [Riesgos de seguridad]
- **Escalabilidad:** [¿Aguanta 10x tráfico?]
- **Migración:** [¿Cómo movemos los datos viejos?]

---

## ✅ Plan de Implementación

1. Fase 1: MVP
2. Fase 2: Migración
3. Fase 3: Cleanup

---

## ❓ Preguntas Abiertas

- ¿Deberíamos usar Redis o Memcached?
- ¿El nombre de la tabla es adecuado?

---

[➡️ Ver Ejemplo](../examples/rfc-example.md)
