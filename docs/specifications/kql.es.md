# Especificación de KQL

## Estado

Borrador canónico de referencia para KOS-Lab.

## 1. Propósito

KQL es el lenguaje de consulta declarativo usado para solicitar proyecciones del estado de KOS. No es un lenguaje de comandos imperativo. Una expresión KQL describe la vista deseada del sistema; el Runtime resuelve la consulta y el Renderer presenta la proyección resultante.

KQL está diseñado para ser:

- legible por humanos,
- trivial de analizar,
- estable entre interfaces,
- extensible,
- independiente del transporte.

## 2. Principio central

KOS mantiene un único estado canónico. Cada consulta pide una proyección de ese estado.

- El estado es único.
- Las proyecciones son múltiples.
- Los renderizadores no inventan datos.
- Los renderizadores solo presentan una vista seleccionada del mismo estado subyacente.

## 3. Forma general

Una consulta KQL es una expresión tipo ruta separada por dos puntos.

```text
KOS : Runtime : Execution : Estado : Tareas
```

Cada segmento refina la consulta sin cambiar el significado de los anteriores.

## 4. Semántica de los segmentos

El modelo semántico canónico es:

- **KOS**: espacio de nombres superior.
- **Runtime**: dominio del runtime.
- **Execution**: subsistema de ejecución.
- **Estado**: tipo de información / familia de vista.
- **Tareas**: sujeto de la vista.
- **Calificadores de vista** (opcionales): refinamiento de la presentación o del nivel de expansión.

Ejemplos de calificadores de vista:

- `Desglosadas`
- `General`
- `Resumen`
- `Métricas`
- `Dependencias`
- `Histórico`
- `Críticas`

## 5. Vista por defecto

Si no se proporciona un calificador explícito, la consulta resuelve la vista por defecto para ese sujeto.

Por ejemplo:

```text
KOS : Runtime : Execution : Estado : Tareas
```

define la proyección estándar del estado de tareas.

## 6. Patrones de consulta habituales

### 6.1 Vistas de tareas

```text
KOS : Runtime : Execution : Estado : Tareas
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
KOS : Runtime : Execution : Estado : Tareas : Resumen
KOS : Runtime : Execution : Estado : Tareas : Métricas
KOS : Runtime : Execution : Estado : Tareas : Dependencias
```

### 6.2 Otras vistas de ejecución

```text
KOS : Runtime : Execution : Estado : Dependencias
KOS : Runtime : Execution : Estado : Métricas
KOS : Runtime : Execution : Estado : Cambios
KOS : Runtime : Execution : Estado : Salud
```

### 6.3 Refinamientos temporales

Pueden añadirse modificadores temporales como calificadores adicionales cuando sea necesario:

```text
KOS : Runtime : Execution : Estado : Tareas : Changed : SinceLastQuery
KOS : Runtime : Execution : Estado : Tareas : Completed : Today
```

## 7. Modelo de consulta

Las consultas KQL son proyecciones declarativas. No ejecutan por sí mismas; solicitan una vista al estado del Runtime.

El pipeline típico es:

```text
Consulta
  ↓
Normalizar
  ↓
Resolver ruta
  ↓
Filtrar estado
  ↓
Renderizar vista
```

## 8. Distinción entre recurso y propiedad

KQL distingue entre:

- **recursos**: `Tareas`, `Cola`, `Workers`, `Eventos`, `Informes`
- **propiedades/vistas**: `Estado`, `Salud`, `Métricas`, `Validación`, `Dependencias`

Una consulta puede combinar ambos, pero el segmento final debe seguir siendo un calificador de vista o un sujeto acotado.

## 9. Contrato de salida

Una consulta KQL debe devolver una proyección de estado, nunca un estado fabricado.

Si el runtime subyacente está en modo emulación, la proyección debe estar marcada explícitamente como simulada.
Si el runtime es real, la proyección debe reflejar el estado real del runtime.

## 10. Convenciones de nomenclatura

Convenciones recomendadas:

- Usar `:` como separador principal en consultas dirigidas a humanos.
- Mantener los segmentos cortos y semánticamente estables.
- Preferir etiquetas descriptivas en español para las vistas dirigidas al operador.
- Evitar verbos imperativos en KQL.

## 11. Ejemplos

### 11.1 Vista resumen

```text
KOS : Runtime : Execution : Estado : Tareas
```

### 11.2 Vista detallada de tareas

```text
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
```

### 11.3 Tareas cambiadas desde la última consulta

```text
KOS : Runtime : Execution : Estado : Tareas : Changed : SinceLastQuery
```

### 11.4 Todas las tareas

```text
KOS : Runtime : Execution : Estado : Todas las Tareas
```

## 12. Extensibilidad

Pueden añadirse nuevos segmentos siempre que preserven el modelo de proyección y no introduzcan ambigüedad.

Ejemplos de extensiones futuras:

- `Histórico`
- `Críticas`
- `Bloqueadas`
- `Validación`
- `Actividad`

## 13. Estado de esta especificación

Este documento es la referencia canónica de KQL en KOS-Lab. Cualquier implementación o renderizador debe ajustarse al modelo semántico definido aquí.
