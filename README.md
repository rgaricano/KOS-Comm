# KOS-Lab

Repositorio canónico de ingeniería de KOS.

## Punto de entrada operativo

Si retomas KOS después de otra sesión, trabajas desde otro entorno o necesitas determinar con seguridad dónde continuar, comienza aquí:

1. `governance/persistence-map/KOS-PM.es.md` — mapa general de continuidad y orientación.
2. `governance/persistence-map/DEVELOPMENT-STATE.es.md` — estado operativo persistido.
3. `governance/persistence-map/REENTRY-CHECKPOINT.es.md` — estado esperado para comparación.
4. `governance/persistence-map/REENTRY-GUIDE.es.md` — procedimiento de reentrada y verificación.
5. `governance/persistence-map/SITUATION-PLAN.es.md` — plano conceptual derivado.

Antes de confiar en una rama documentada o en referencias `origin/*` locales:

```bash
git fetch --prune
git status --short
git branch --show-current
git log -1 --oneline
git status -sb
```

Regla operativa:

```text
README = ENTRY POINT / ORIENTATION
KOS-PM = CONTINUITY MAP
REENTRY-CHECKPOINT = EXPECTED STATE
Git = ACTUAL REPOSITORY STATE
Canon / ADR / ARCH = ARCHITECTURAL AUTHORITY
Evidence = ACCREDITED OBSERVATION

DOCUMENTED BRANCH != VERIFIED BRANCH
```

Git es la autoridad para confirmar existencia de ramas, HEAD, upstream, divergencia y ancestry. Los mapas documentales son ayudas de orientación, no sustitutos de esa verificación.

## Estado funcional resumido

```text
CP-0001 — Cognitive Projection
  FORMALLY CLOSED / ACCREDITED

KM-0001 — Persistent Knowledge Model
  FORMALLY CLOSED / ACCREDITED

KP-0001 — Knowledge–Projection Integration
  FORMALLY CLOSED / ACCREDITED

Última regresión integral acreditada
  1162/1162 PASS

Programa funcional activo
  ninguno

Siguiente programa funcional
  no determinado / no abierto
```

La baseline funcional consolidada alcanza actualmente:

```text
Persistent Knowledge
        |
        v
Persistent Cognitive State
        |
        v
Observation Boundary
        |
        v
StateObservation[]
        |
        v
Deterministic Selection
        |
        v
Projection Materialization
        |
        v
ConsumerContextView
```

`ConsumerContextView` es una vista derivada y no propietaria. La identidad, autoridad y propiedad permanecen en los objetos canónicos fuente.

## Mapa estructural resumido

Topología orientativa de líneas de ingeniería relevantes:

```text
proposal/engineering
|
+-- engineering/ET-0001-test-automation
+-- engineering/BL-0001-baseline-governance
+-- engineering/CP-0001-cognitive-projection
+-- engineering/KOS-PM-persistence-map
+-- engineering/KM-0001-persistent-knowledge-model
|    +-- engineering/KM-0001-TST-0002-transactional-lifecycle
|    +-- engineering/KM-0001-TST-0003-knowledge-evidence-provenance
|    +-- engineering/KM-0001-TST-0004-persistent-cognitive-state-observation
|    +-- engineering/KM-0001-TST-0005-observation-boundary
|
+-- engineering/KP-0001-knowledge-projection-integration
```

Este mapa debe mantenerse como orientación de alto nivel en transiciones importantes de programa. Su contenido no demuestra por sí mismo que una rama siga existiendo o esté sincronizada.

## Baseline 0.1

Este repositorio es la fuente de verdad del laboratorio KOS. Toda implementación, decisión, evidencia y artefacto deben ser trazables al Canon.

## Principios

- Conformidad obligatoria con el Canon.
- Trazabilidad completa.
- Auditabilidad completa.
- No simulación salvo indicación explícita.
- Un único modelo canónico para ingeniería y conocimiento.
- Separación explícita entre estado persistido, observación, selección y proyección derivada.
- Verificación Git antes de cualquier operación estructural basada en ramas documentadas.

## Estructura principal

- `canon/` — referencia normativa y fundacional.
- `engineering/` — requisitos, ADR, tareas, evidencias, cierres y reportes.
- `governance/persistence-map/` — continuidad, estado, reentrada, checkpoint, plano y reconciliaciones.
- `runtime/` — estado y bootstrap del runtime.
- `knowledge/` — conocimiento persistente y semántica asociada.
- `context/` — observación, selección, proyección y materialización contextual.
- `storage/` — persistencia y artefactos.
- `api/` — interfaz programática.
- `cli/` — interfaz de línea de comandos.
- `tests/` — validación y conformidad.
- `tools/` y `engineering/tools/` — utilidades y automatización del laboratorio.
- `docs/` — documentación operativa adicional.

## Reentrada mínima

```text
README
 -> KOS-PM
 -> DEVELOPMENT-STATE
 -> REENTRY-CHECKPOINT
 -> git fetch --prune
 -> verificar estado Git real
 -> REENTRY-GUIDE
 -> evidencia/cierres aplicables
 -> declarar rama y siguiente acción
 -> modificar
```

No reabrir CP-0001, KM-0001 o KP-0001 durante una reentrada ordinaria salvo contradicción autoritativa posterior o decisión arquitectónica explícita.
