# KOS-Comm — Punto de control de reentrada

**Fecha:** 2026-07-21  
**Rama esperada:** `KOS-Comn`  
**Estado:** CURRENT CHECKPOINT

## Estado arquitectónico

```text
Gate 0                              PASS
Reconciliación KOS-Lab ↔ KOS-Comm  CLOSED
AR-1 — Modelo de fronteras          CLOSED / PASS
AR-2 — Modelo de representación     ACTIVE
AR-3 — Modelo de Binding            PENDING
Gate A                              PENDING
```

## Últimos hitos persistidos

```text
AR-1 closure ES
c5cb853e1cb7152f230a9b306f2489c70567d73f

AR-1 closure EN
301f4106b1ff10c88a6eba0f36c2bbc1a61c7251

AR-2 initial model ES
8561fef92fa8a8ed52edb687dfc223469ba493af

AR-2 initial model EN
2e94f070f11c98e607495961e4438613d39d5c5a

Reentry Guide ES
ba004da7606798d16aea5881699279114a468306
```

La guía inglesa de reentrada se materializa inmediatamente después de la española y debe verificarse mediante el HEAD real de la rama.

## Invariantes activos

```text
KOS-Lab authority preserved
KOS-Comm autonomy preserved
Binding = bilateral seam
KCA = neutral target
KCP = small / replaceable
KSCL = open decomposition
representation != represented object
representation != authority
receipt != canonical import
promotion = evidence + governance
```

## Trabajo activo

```text
AR-2 — Modelo de representación
```

Hipótesis iniciales principales:

- separación referente / representación / forma codificada;
- identidad de representación distinta de identidad del sujeto;
- contexto semántico explícito;
- procedencia y referencias neutrales;
- propiedades/garantías declarables;
- completitud siempre respecto de ámbito;
- autoridad externa a la representación;
- neutralidad no-KOS obligatoria.

## Siguiente acción

```text
AR-2
  ↓
primera pasada de validación
  ↓
12 casos iniciales
  ↓
refinamiento de taxonomía
  ↓
decidir estructura común vs capacidades semánticas
```

## Regla

Este documento expresa el estado esperado. La reentrada debe contrastarlo con Git antes de continuar.

```text
CHECKPOINT != ACTUAL GIT STATE
```