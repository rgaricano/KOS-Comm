# Runtime Console Specification

# Especificación de la consola del Runtime

## Status / Estado

Draft canonical specification for KOS-Lab.
Borrador canónico de referencia para KOS-Lab.

## 1. Purpose / Propósito

The Runtime Console is the human-facing projection of KOS execution state.
La consola del Runtime es la proyección visible para humanos del estado de ejecución de KOS.

It must present the state clearly, compactly, and consistently.
Debe presentar el estado de forma clara, compacta y consistente.

## 2. Design principles / Principios de diseño

- State-first: the console renders state, it does not invent it.
- Estado primero: la consola representa estado, no lo inventa.
- Projections over commands: the console answers queries, it does not behave as an imperative control surface.
- Proyecciones antes que comandos: la consola responde consultas; no actúa como una superficie imperativa de control.
- Accessibility first: ASCII and symbols are primary; color is only supplemental.
- Accesibilidad primero: ASCII y símbolos son primarios; el color solo es complementario.
- Low-cost rendering: prefer text-based output over heavy graphical output when possible.
- Renderizado de bajo coste: preferir salida textual frente a salida gráfica pesada cuando sea posible.

## 3. Core layout / Estructura base

The canonical console view uses the following column order:
La vista canónica de consola usa el siguiente orden de columnas:

1. Health / Salud
2. Execution state / Estado
3. Progress / Progreso
4. Trend / Tendencia
5. Validation / Validación

Example:
Ejemplo:

```text
Salud   Estado   Progreso         Tendencia   Validación
🟢      ▶        █████████░ 94%   ↗           ✔
```

## 4. Semantics / Semántica

### 4.1 Health / Salud

Health indicates operational condition.
La salud indica la condición operativa.

Recommended symbols:
Símbolos recomendados:

- 🟢 Healthy / Sano
- 🟡 Degraded / Degradado
- 🔴 Unhealthy / No sano
- ⚪ Unknown / Desconocido

### 4.2 Execution state / Estado de ejecución

Execution state indicates lifecycle state.
El estado indica el ciclo de vida.

Recommended symbols:
Símbolos recomendados:

- ◎ Pending / Pendiente
- ▶ Running / En ejecución
- ⏸ Paused / Pausado
- ⟳ Restarting or retrying / Reiniciando o reintentando
- ⏹ Finished / Finalizado
- ⚑ Waiting operator / Esperando operador

### 4.3 Progress / Progreso

Progress is an approximate or exact representation of completion.
El progreso es una representación aproximada o exacta del avance.

Rules:
Reglas:

- ASCII bars are mandatory for the default view.
- Las barras ASCII son obligatorias en la vista por defecto.
- Percentages should be shown when available.
- Los porcentajes deben mostrarse cuando estén disponibles.
- Bars represent coarse buckets, typically 10% increments.
- Las barras representan bloques gruesos, típicamente de 10%.
- Percentages provide precision beyond the bar granularity.
- Los porcentajes aportan precisión más allá de la granularidad de la barra.

### 4.4 Trend / Tendencia

Trend indicates whether the node is improving, stable, or degrading.
La tendencia indica si el nodo mejora, permanece estable o se degrada.

Recommended symbols:
Símbolos recomendados:

- ⇈ accelerating improvement / mejora acelerada
- ↗ improving / mejorando
- → stable / estable
- ↘ degrading / degradándose
- ⇊ rapid degradation / degradación rápida

### 4.5 Validation / Validación

Validation indicates whether the result has been reviewed or accepted.
La validación indica si el resultado ha sido revisado o aceptado.

Recommended symbols:
Símbolos recomendados:

- ◊ not reviewed / no revisado
- ◐ in review / en revisión
- ✔ validated / validado
- ✖ rejected / rechazado

## 5. Output levels / Niveles de salida

The console must support multiple projections.
La consola debe soportar múltiples proyecciones.

Canonical examples:
Ejemplos canónicos:

- `KOS : Runtime : Execution : Estado : Tareas`
- `KOS : Runtime : Execution : Estado : Tareas : Desglosadas`
- `KOS : Runtime : Execution : Estado : Tareas : Resumen`
- `KOS : Runtime : Execution : Estado : Tareas : Métricas`
- `KOS : Runtime : Execution : Estado : Tareas : Dependencias`

## 6. Task tree / Árbol de tareas

The default task view is a tree of execution nodes.
La vista de tareas por defecto es un árbol de nodos de ejecución.

Each node may include:
Cada nodo puede incluir:

- name / nombre
- health / salud
- state / estado
- progress / progreso
- trend / tendencia
- validation / validación
- children / hijos

The tree view must support at least two levels:
La vista en árbol debe soportar al menos dos niveles:

- summary / resumen
- detailed / desglosada

## 7. Representation rules / Reglas de representación

- Do not present simulated state as if it were real.
- No presentar estado simulado como si fuera real.
- If the runtime is emulated, label it explicitly.
- Si el runtime es emulado, debe indicarse explícitamente.
- Keep labels stable across renderers.
- Mantener etiquetas estables entre renderizadores.
- Prefer fixed-width alignment in console outputs.
- Preferir alineación monoespaciada en salidas de consola.

## 8. Console grammar / Gramática de consola

The console view is a projection, not a source of truth.
La consola es una proyección, no la fuente de verdad.

Recommended pipeline:
Pipeline recomendado:

```text
State
  ↓
Filter
  ↓
Expand or collapse
  ↓
Render
```

## 9. Examples / Ejemplos

### 9.1 Summary view / Vista resumen

```text
[KOS Runtime Emulator]

Execution Runtime

Estado de Ejecución : Tareas

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Salud   Estado   Progreso         Tendencia   Validación

Execution Runtime                               🟢  ▶  █████████░  94%  ↗  ✔
```

### 9.2 Detailed view / Vista desglosada

```text
[KOS Runtime Emulator]

Execution Runtime

Estado de Ejecución : Tareas Desglosadas
```

followed by the expanded tree.
seguido por el árbol expandido.

## 10. Accessibility / Accesibilidad

ASCII and symbols must remain understandable in monochrome terminals.
ASCII y símbolos deben seguir siendo comprensibles en terminales monocromos.

Color may be used only as redundant reinforcement.
El color puede usarse únicamente como refuerzo redundante.

## 11. Status of this specification / Estado de esta especificación

This document is a canonical specification for the KOS-Lab runtime console.
Este documento es una especificación canónica de la consola del runtime de KOS-Lab.

Any future renderer must preserve the semantics defined here.
Cualquier renderizador futuro deberá preservar la semántica definida aquí.
