# Runtime de KOS

## Estado

Borrador canónico de referencia para KOS-Lab.

## 1. Propósito

El Runtime es el subsistema encargado de ejecutar, supervisar y proyectar el estado operativo del sistema KOS. Su función no es almacenar conocimiento canónico, sino operar sobre el estado que le proporcionan otros subsistemas.

## 2. Responsabilidad

El Runtime coordina la ejecución del sistema y mantiene visibilidad sobre el estado operativo de sus componentes.

Responsabilidades principales:

- ejecutar procesos;
- supervisar el estado operativo;
- exponer el árbol de ejecución;
- coordinar el Supervisor;
- integrar el gestor de sincronización con el repositorio;
- alimentar al renderizador con estado actualizado;
- mantener trazabilidad de ejecución.

## 3. Principio fundamental

El Runtime no es la fuente de verdad del conocimiento.
Su función es operar sobre proyecciones de conocimiento y sobre su propio estado operativo.

## 4. Separación de planos

Se distinguen tres planos:

### 4.1 Estado operativo

Define lo que está ocurriendo en el Runtime en este instante:

- componentes activos;
- componentes pausados;
- componentes finalizados;
- componentes pendientes;
- componentes bloqueados.

### 4.2 Ejecución

Define la actividad en curso:

- tareas en ejecución;
- sincronizaciones activas;
- validaciones pendientes;
- recuperación en curso;
- renderizado activo.

### 4.3 Proyección

Define cómo se presenta el estado al operador:

- consola;
- Markdown;
- JSON;
- GitHub Issue;
- futura interfaz web o API.

## 5. Componentes principales

El Runtime puede incluir, como mínimo, los siguientes subsistemas:

- Execution Runtime;
- Runtime Supervisor;
- Repository Sync Manager;
- Runtime Renderer;
- Runtime Bootstrap.

## 6. Árbol de ejecución

El Runtime debe poder representarse como un árbol de ejecución.

La vista de ejecución puede incluir:

- nodo raíz;
- nodos de nivel 1;
- nodos hijos;
- métricas por nodo;
- estado por nodo;
- validación por nodo.

## 7. Supervisor

El Supervisor es el subsistema responsable de la salud y estabilidad del Runtime.

Debe incluir, al menos:

- monitor de salud;
- watchdog;
- motor de recuperación;
- proveedor de reloj;
- registro de salud.

## 8. Sincronización con el repositorio

El Runtime debe integrar la sincronización con GitHub como una capacidad operativa.

La sincronización incluye:

- registro de documentación;
- registro de tareas;
- registro de informes;
- publicación de Issues de estado;
- actualización de registros persistentes;
- trazabilidad mediante commits.

## 9. Renderer

El Runtime no debe generar salidas arbitrarias.
Debe delegar la presentación al Runtime Renderer.

El Renderer transforma un estado en una vista concreta.

## 10. Bootstrap

El Runtime debe poder reconstruir su estado desde artefactos persistentes.

Como mínimo:

- configuración;
- estado;
- sesión;
- registros;
- referencias.

## 11. Modo de emulación

Cuando el Runtime esté en modo emulación, debe indicarse de forma explícita.
No debe confundirse con un estado operativo real.

## 12. Estado de esta especificación

Este documento define el comportamiento canónico del Runtime de KOS-Lab. Cualquier implementación debe respetar la separación entre ejecución, supervisión, sincronización y proyección.
