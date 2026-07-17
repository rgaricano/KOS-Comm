# KOS Query Language (KQL)

## Status

Draft canonical specification for KOS-Lab.

## 1. Purpose

KQL is the declarative query language used to request projections of KOS state. It is not an imperative command language. A KQL expression describes the desired view of the system state; the Runtime resolves the query and the Renderer presents the resulting projection.

KQL is designed to be:

- readable by humans,
- trivial to parse,
- stable across interfaces,
- extensible,
- independent of transport.

## 2. Core principle

KOS maintains a single canonical state. Every query asks for a projection of that state.

- State is unique.
- Projections are multiple.
- Renderers do not invent data.
- Renderers only present a selected view of the same underlying state.

## 3. General form

A KQL query is a colon-separated path-like expression.

```text
KOS : Runtime : Execution : Estado : Tareas
```

Each segment refines the query without changing the meaning of previous segments.

## 4. Segment semantics

The canonical semantic model is:

- **KOS**: top-level namespace.
- **Runtime**: runtime domain.
- **Execution**: execution subsystem.
- **Estado**: information type / view family.
- **Tareas**: subject of the view.
- **Vista qualifiers** (optional): refinement of presentation or expansion level.

Examples of view qualifiers:

- `Desglosadas`
- `General`
- `Resumen`
- `Métricas`
- `Dependencias`
- `Histórico`
- `Críticas`

## 5. Default view

If no explicit qualifier is provided, the query resolves to the default view for that subject.

For example:

```text
KOS : Runtime : Execution : Estado : Tareas
```

defaults to the standard task-state projection.

## 6. Common query patterns

### 6.1 Task views

```text
KOS : Runtime : Execution : Estado : Tareas
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
KOS : Runtime : Execution : Estado : Tareas : Resumen
KOS : Runtime : Execution : Estado : Tareas : Métricas
KOS : Runtime : Execution : Estado : Tareas : Dependencias
```

### 6.2 Other execution views

```text
KOS : Runtime : Execution : Estado : Dependencias
KOS : Runtime : Execution : Estado : Métricas
KOS : Runtime : Execution : Estado : Cambios
KOS : Runtime : Execution : Estado : Salud
```

### 6.3 Temporal refinements

Temporal modifiers may be added as additional qualifiers when needed:

```text
KOS : Runtime : Execution : Estado : Tareas : Changed : SinceLastQuery
KOS : Runtime : Execution : Estado : Tareas : Completed : Today
```

## 7. Query model

KQL queries are declarative projections. They do not cause execution by themselves; they request a view from the Runtime State.

The typical pipeline is:

```text
Query
  ↓
Normalize
  ↓
Resolve path
  ↓
Filter state
  ↓
Render view
```

## 8. Resource vs property distinction

KQL distinguishes between:

- **resources**: `Tasks`, `Queue`, `Workers`, `Events`, `Reports`
- **properties/views**: `Estado`, `Health`, `Metrics`, `Validation`, `Dependencies`

A query may combine both, but the final segment should remain a view qualifier or a constrained subject.

## 9. Output contract

A KQL query must return a projection of state, never a fabricated state.

If the underlying runtime is in emulation mode, the projection must be explicitly marked as simulated.
If the runtime is live, the projection must reflect actual runtime state.

## 10. Naming conventions

Recommended conventions:

- Use `:` as the primary separator in human-facing queries.
- Keep segments short and semantically stable.
- Prefer descriptive Spanish labels for operator-facing views.
- Avoid imperative verbs in KQL.

## 11. Examples

### 11.1 Summary view

```text
KOS : Runtime : Execution : Estado : Tareas
```

### 11.2 Detailed task view

```text
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
```

### 11.3 Changed tasks since last query

```text
KOS : Runtime : Execution : Estado : Tareas : Changed : SinceLastQuery
```

### 11.4 All task states

```text
KOS : Runtime : Execution : Estado : Todas las Tareas
```

## 12. Extensibility

New segments may be added as long as they preserve the projection model and do not introduce ambiguity.

Examples of future extensions:

- `Histórico`
- `Críticas`
- `Bloqueadas`
- `Validación`
- `Actividad`

## 13. Status of this specification

This document is the canonical reference for KQL in KOS-Lab. Any implementation or renderer must conform to the semantic model defined here.
