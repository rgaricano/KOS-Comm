# KOS-Comm — Continuidad KSCL experimental

**Estado:** EXPERIMENTAL / ACTIVE  
**Ámbito:** continuidad semántica y reentrada  
**Autoridad:** NO arquitectónica  
**Revisión futura:** AR-5 — KSCL Decomposition

## Propósito

Este directorio materializa registros `.kscl` experimentales para preservar continuidad semántica entre sesiones y permitir reentrada después de pérdida de contexto.

Hasta AR-5, el formato es operativo y revisable.

```text
Git = autoridad sobre estado material verificable
Documentos AR = autoridad sobre decisiones arquitectónicas cerradas
KSCL = continuidad semántica experimental
```

## Estructura

```text
continuity/
├── CURRENT.kscl
├── README.es.md
├── README.en.md
└── checkpoints/
    └── YYYY-MM-DD-<checkpoint>.kscl
```

`CURRENT.kscl` representa el estado semántico de reentrada vigente.

Los archivos de `checkpoints/` son instantáneas históricas de puntos significativos y no deben reescribirse salvo corrección documental explícita.

## Reglas

1. Verificar Git antes de confiar en SHAs registrados.
2. Un registro KSCL no puede revocar una decisión AR cerrada.
3. `CURRENT.kscl` puede evolucionar con el proyecto.
4. Los checkpoints deben conservar el contexto necesario para reconstruir intención, decisiones, evidencia, incertidumbres y siguiente acción.
5. El formato puede cambiar antes de AR-5; cualquier cambio incompatible debe documentarse.
6. `KSCL reconstruction != proof`.
7. `KSCL continuity != architectural authority`.
