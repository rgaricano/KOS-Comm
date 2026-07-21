# KOS-Comm — Guía de reentrada y continuidad

**Estado:** ACTIVE / OPERATIONAL  
**Línea de trabajo:** `KOS-Comn`  
**Objetivo:** reconstruir contexto suficiente, verificable y semánticamente coherente antes de continuar el desarrollo de KOS-Comm.

## 1. Principio

La fuente de verdad operativa es el repositorio y su estado Git verificable.

La conversación ayuda a desarrollar el trabajo, pero no sustituye la persistencia documental.

```text
CONVERSACIÓN
    ↓ consolidación
DOCUMENTACIÓN PERSISTIDA
    ↓ verificación
GIT
    ↓ interpretación
CONTEXTO RECONSTRUIDO
```

## 2. Secuencia de reentrada

```text
README / punto de entrada
        ↓
DEVELOPMENT-STATE
        ↓
REENTRY-CHECKPOINT
        ↓
última consolidación de sesión / continuidad KSCL
        ↓
verificación Git
        ↓
charter KOS-Lab ↔ KOS-Comm si afecta a fronteras bilaterales
        ↓
documento arquitectónico activo
        ↓
evidencia / cierres aplicables
        ↓
declaración explícita de estado y siguiente acción
        ↓
desarrollo
        ↓
registro y persistencia del resultado
```

Si algún artefacto de la secuencia todavía no existe, la reentrada debe utilizar los disponibles y registrar la carencia como deuda de continuidad.

## 3. Verificación Git obligatoria

Antes de modificar:

- confirmar repositorio `rgaricano/KOS-Lab`;
- confirmar rama `KOS-Comn`;
- obtener HEAD real;
- comprobar divergencia respecto del punto de referencia aplicable;
- verificar que los documentos citados existen realmente en la rama;
- no inferir existencia o estado desde memoria conversacional.

Regla:

```text
DOCUMENTED STATE != VERIFIED GIT STATE
```

Ante resultado remoto ambiguo:

```text
RESULTADO REMOTO AMBIGUO
        ↓
NO REINTENTAR A CIEGAS
        ↓
CONSULTAR ESTADO REMOTO
        ↓
VERIFICAR SI EL CAMBIO EXISTE
        ↓
RECUPERAR SHA / IDENTIDAD
        ↓
CREATE / UPDATE / ABORT
```

## 4. Capas de autoridad durante la reentrada

```text
Git real
    = existencia, rama, HEAD, historial y materialización

Charter de colaboración
    = fronteras KOS-Lab ↔ KOS-Comm

Cierres AR / decisiones estabilizadas
    = invariantes arquitectónicos ya acreditados

Documento AR activo
    = hipótesis y trabajo actual

Evidencia
    = resultados acreditados de validación

Consolidación de sesión / KSCL
    = continuidad semántica y reconstrucción de intención
```

Una consolidación de sesión nunca puede revocar por sí sola una decisión arquitectónica cerrada.

## 5. Continuidad semántica mediante KSCL

Hasta que AR-5 determine la descomposición definitiva de KSCL, KOS-Comm utilizará KSCL como mecanismo experimental de continuidad semántica, no como autoridad arquitectónica.

Su función de reentrada es preservar:

- intención de la sesión;
- decisiones tomadas;
- hipótesis abiertas;
- relaciones entre conceptos;
- artefactos modificados;
- evidencia obtenida;
- incertidumbres pendientes;
- siguiente acción declarada.

No debe confundirse:

```text
KSCL continuity != architectural authority
KSCL record != Git verification
KSCL reconstruction != proof
```

## 6. Registro mínimo de continuidad KSCL

Cada consolidación significativa debería poder expresar:

```text
SessionContinuity {
    session_or_checkpoint_id
    repository
    branch
    verified_head
    architectural_phase
    active_work_item
    closed_items[]
    active_hypotheses[]
    decisions[]
    invariants[]
    evidence[]
    modified_artifacts[]
    unresolved_questions[]
    next_action
}
```

Esta estructura es operativa y experimental. No prejuzga la arquitectura definitiva de KSCL que será investigada en AR-5.

## 7. Estado esperado actualmente

Una reentrada correcta a fecha de este documento debe reconstruir al menos:

```text
KOS-Lab ↔ KOS-Comm reconciliation
    CLOSED

Gate 0
    PASS

KOS-Lab
    AUTHORITATIVE / INDEPENDENT

KOS-Comm
    EXPERIMENTAL / AUTONOMOUS

Coupling
    EXPLICIT BINDINGS

AR-1 — Boundary Model
    CLOSED / PASS

AR-2 — Representation Model
    ACTIVE

AR-3 — Binding Model
    PENDING

Gate A
    PENDING
```

## 8. Invariantes que deben sobrevivir a la pérdida de contexto

```text
KOS-Lab authority is preserved
KOS-Comm autonomy is preserved

Binding is the bilateral seam

KCA must remain neutral

KCP must remain small and replaceable

KSCL is not frozen as a single layer

receipt != canonical import
communication != authority
representation != represented object
representation != authority
reconstruction != authorization

promotion to KOS-Lab requires evidence + governance
```

## 9. Reentrada en AR-2

Si AR-2 sigue activo, leer en este orden:

1. `docs/kos-comn/architecture/AR-1-CLOSURE.es.md`;
2. `docs/kos-comn/architecture/AR-2-REPRESENTATION-MODEL.es.md`;
3. versión inglesa correspondiente cuando se necesite comprobar equivalencia bilingüe;
4. validaciones AR-2 posteriores que existan;
5. última consolidación de sesión.

La siguiente acción actualmente esperada es:

```text
AR-2
    ↓
primera pasada de validación
    ↓
refinamiento de taxonomía y capacidades semánticas
```

## 10. Declaración obligatoria antes de continuar

Una nueva sesión debe poder declarar explícitamente:

```text
Repositorio verificado:
Rama verificada:
HEAD verificado:
Último elemento cerrado:
Elemento activo:
Invariantes aplicables:
Documento de trabajo:
Incertidumbres abiertas:
Siguiente acción:
```

Si no puede hacerlo, la reconstrucción de contexto no está completa.

## 11. Cierre de sesión / checkpoint

Antes de abandonar una sesión que haya producido cambios relevantes:

1. persistir documentos/resultados;
2. recuperar y registrar SHA de los commits relevantes;
3. verificar lectura o comparación remota posterior;
4. actualizar estado de desarrollo/checkpoint cuando cambie la fase;
5. producir consolidación semántica de sesión cuando exista riesgo de pérdida contextual;
6. registrar siguiente acción.

## 12. Regla bilingüe

La guía de reentrada debe existir en ES/EN con equivalencia semántica.

Los registros KSCL pueden tener una lengua principal, pero los identificadores técnicos, estados e invariantes deben permanecer inequívocos entre idiomas.

## 13. Resultado esperado

```text
REENTRY
  ↓
VERIFY
  ↓
RECONSTRUCT
  ↓
RECONCILE
  ↓
DECLARE STATE
  ↓
CONTINUE
  ↓
PERSIST
```

La reentrada no pretende recuperar literalmente una conversación perdida. Pretende reconstruir un estado de ingeniería suficiente, trazable y verificable para continuar sin depender de memoria externa.