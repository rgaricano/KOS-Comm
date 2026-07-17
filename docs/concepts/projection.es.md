# Proyección

## Estado

Borrador canónico de referencia para KOS-Lab.

## 1. Definición

Una proyección es una vista temporal construida a partir de un estado canónico. La proyección no modifica el estado original; únicamente selecciona, organiza y presenta una parte de él según un objetivo concreto.

## 2. Propósito

Las proyecciones permiten que el mismo estado sea observado desde múltiples perspectivas sin duplicar la verdad subyacente.

## 3. Propiedades

Toda proyección canónica debe cumplir estas propiedades:

- es derivada;
- es temporal;
- es recuperable;
- es estable dentro de su ámbito;
- no sustituye al estado canónico;
- puede renderizarse en múltiples formatos.

## 4. Relación con el estado

El estado es la fuente de verdad.
La proyección es una materialización parcial del estado para un propósito concreto.

Por ejemplo:

- una vista de tareas;
- una vista de dependencias;
- una vista de salud;
- una vista de métricas;
- una vista documental;
- una vista contextual para inferencia.

## 5. Relación con KQL

KQL solicita proyecciones.

Ejemplo:

```text
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
```

Esta consulta no pide un cambio de estado.
Pide una proyección desglosada del estado de tareas.

## 6. Relación con el Runtime

El Runtime consume proyecciones y las presenta al operador.
No debe confundir la proyección con la fuente de verdad.

## 7. Relación con el Motor de Conocimiento

El Motor de Conocimiento construye proyecciones de conocimiento.
El Runtime construye proyecciones de ejecución.
Ambos siguen el mismo principio: una verdad canónica, múltiples vistas.

## 8. Niveles de detalle

Una proyección puede tener diferentes niveles de expansión:

- resumen;
- general;
- desglosada;
- detallada;
- histórica;
- diferencial;
- crítica.

## 9. Requisitos de honestidad

Toda proyección debe indicar si procede de:

- estado real;
- estado emulado;
- estado parcial;
- estado reconstruido.

No debe presentarse una proyección como si fuera un estado completo cuando no lo es.

## 10. Estado de esta especificación

Este documento define el concepto de proyección en KOS-Lab. Cualquier subsistema que represente información derivada debe respetar esta definición.
