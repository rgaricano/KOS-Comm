# Motor de Conocimiento

## Estado

Borrador canónico de referencia para KOS-Lab.

## 1. Propósito

El Motor de Conocimiento es el subsistema responsable de operar sobre conocimiento persistente. No posee el conocimiento como tal; lo consume, lo relaciona, lo refina, lo versiona y lo proyecta.

## 2. Responsabilidad

El motor se ocupa de transformar conocimiento en formas útiles para otros subsistemas.

Responsabilidades principales:

- capturar conocimiento;
- resolver referencias;
- refinar conocimiento;
- consolidar duplicados;
- validar consistencia;
- versionar revisiones;
- proyectar vistas;
- recuperar conocimiento;
- materializar representaciones.

## 3. Principio fundamental

El Motor de Conocimiento no es la fuente de verdad.
La fuente de verdad es el repositorio de conocimiento y sus objetos canónicos.

El motor opera sobre esos objetos.

## 4. Separación entre activos y estado

Se distinguen dos niveles:

### 4.1 Activos de conocimiento

Son objetos persistentes de referencia:

- ontología;
- terminología;
- referencias;
- taxonomías;
- reglas;
- conceptos;
- evidencias;
- decisiones.

### 4.2 Estado de conocimiento

Es la situación concreta del conocimiento en un instante dado:

- entidades activas;
- relaciones;
- versiones vigentes;
- dependencias;
- historial;
- evidencia asociada.

## 5. Capacidades del motor

El motor debe exponer capacidades operativas, no solo estructuras de datos.

Capacidades canónicas:

- `Capture()`
- `Normalize()`
- `Refine()`
- `Consolidate()`
- `Relate()`
- `Version()`
- `Validate()`
- `Retrieve()`
- `Project()`
- `Materialize()`

## 6. Proyección del conocimiento

Una proyección es una vista temporal construida a partir del estado de conocimiento.

No altera el estado persistente.

Ejemplos de proyección:

- una vista contextual para una inferencia;
- una vista documental;
- una vista ontológica;
- una vista de referencias;
- una vista de dependencias.

## 7. Holographic Context Field

El Motor de Conocimiento es el subsistema que mantiene y opera sobre el campo de conocimiento del sistema.

Cada elemento del campo contiene una proyección del conjunto desde su posición.
Los elementos cercanos muestran perspectivas casi equivalentes.
Los elementos alejados muestran perspectivas claramente diferenciadas.

## 8. Relación con el Runtime

El Runtime no mantiene el conocimiento canónico.
El Runtime consume proyecciones del Motor de Conocimiento.

Por tanto:

- el conocimiento vive en el motor;
- la ejecución consume proyecciones;
- el renderizado presenta el resultado.

## 9. Relación con la documentación

La documentación canónica es una proyección estabilizada del conocimiento.
No sustituye al motor; se alimenta de él.

## 10. Estado de esta especificación

Este documento define el papel del Motor de Conocimiento dentro de KOS-Lab. Cualquier implementación debe respetar la separación entre activos de conocimiento, estado de conocimiento y proyecciones.
