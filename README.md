# KOS-Lab — KOS-Comn

Rama de laboratorio dedicada al replanteamiento del **subsistema de información y comunicaciones de KOS**.

Esta rama parte del repositorio canónico `KOS-Lab`, pero mantiene aislado el trabajo de arquitectura de comunicaciones hasta que exista una decisión explícita de integración.

## Punto de entrada de KOS-Comn

Para retomar este trabajo después de una pérdida de contexto, leer en este orden:

1. `README.md` — orientación y alcance de la rama.
2. `docs/kos-comn/DEVELOPMENT-STATE.md` — estado persistente actual.
3. `docs/kos-comn/SESSION-CONSOLIDATION.md` — último checkpoint de trabajo.
4. `docs/kos-comn/architecture/KCA.md` — arquitectura de referencia.
5. `docs/kos-comn/adr/ADR-0001-KCA.md` — decisión arquitectónica fundacional.
6. Documentación KOS relevante en `governance/persistence-map/`, `canon/`, `engineering/`, `knowledge/`, `context/` y `runtime/` cuando sea necesario contrastar autoridad o integración.

## Objetivo

Diseñar una arquitectura coherente para representar, codificar, comunicar, reconstruir y proyectar información y conocimiento entre componentes cognitivos de KOS.

El planteamiento inicial se organiza bajo **KCA — Knowledge Communication Architecture**.

```text
Persistence
   ↓
KRM — Knowledge Representation Model
   ↓
KEncoding — Knowledge Encoding
   ↓
KCP — Knowledge Communication Protocol
   ↓
KSCL — Knowledge Session Continuity Layer
   ↓
CP — Cognitive Projection
   ↓
Consumers
```

## Principio de diseño

KCP y KSCL dejan de considerarse conceptos aislados o el sistema completo de comunicaciones.

KCA pasa a ser el marco arquitectónico superior y separa responsabilidades:

- **KRM** define la semántica de la información/conocimiento intercambiable.
- **KEncoding** define codificación, serialización, integridad y compatibilidad.
- **KCP** define comunicación e intercambio entre nodos.
- **KSCL** define continuidad y reconstrucción determinista de estado.
- **CP** adapta el estado a consumidores sin transferir autoridad canónica a la proyección.

## Relación con KOS

Esta rama no sustituye la arquitectura canónica de KOS ni modifica automáticamente decisiones existentes.

El trabajo KOS-Comn debe contrastarse con las fronteras ya acreditadas en KOS, especialmente conocimiento persistente, estado cognitivo persistente, observación, proyección, contexto, ejecución, procedencia, evidencia e identidad.

## Disciplina de persistencia

La fuente de continuidad es el repositorio, no la conversación.

Después de cada hito relevante se actualizarán:

- `docs/kos-comn/DEVELOPMENT-STATE.md`;
- `docs/kos-comn/SESSION-CONSOLIDATION.md`;
- los documentos arquitectónicos afectados;
- los ADR cuando exista una decisión estructural.

Ante respuestas ambiguas del conector GitHub se aplica obligatoriamente el procedimiento del Issue #5:

```text
AMBIGUOUS CONNECTOR RESPONSE != NO REPOSITORY MUTATION
SEARCH INDEX MISS != BRANCH ABSENCE
WRITE RETRY REQUIRES STATE VERIFICATION
```

## Estado actual

- Repositorio: `rgaricano/KOS-Lab`
- Rama aislada: `KOS-Comn`
- Base inicial: `dev`
- Trabajo activo: definición y consolidación de KCA.
- Primera decisión propuesta: KCA como arquitectura superior de KRM, KEncoding, KCP, KSCL y CP.

## Siguiente acción

Persistir el estado inicial, la consolidación de sesión, la especificación KCA y ADR-0001; después iniciar el análisis formal de KRM y de las interfaces entre capas.
