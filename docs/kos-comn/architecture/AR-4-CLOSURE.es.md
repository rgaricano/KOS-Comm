# AR-4 — Modelo de Reconstrucción — Cierre

**Estado:** CLOSED / PASS  
**Fase:** Phase II — Reconstruction Semantics  
**Predecesor:** Gate A PASS  
**Siguiente:** AR-5 — KSCL Decomposition

## 1. Decisión

Tras el modelo inicial, la validación y los enfrentamientos adversariales, AR-4 se cierra sin contradicciones críticas.

```text
AR-4 — RECONSTRUCTION MODEL
STATUS: CLOSED
RESULT: PASS
```

## 2. Ejes estabilizados

Se consolidan tres dimensiones principales de la reconstrucción:

```text
Resolution
    SUCCESS
    AMBIGUOUS
    IMPOSSIBLE

Coverage
    COMPLETE
    PARTIAL

Fidelity
    EXACT
    EQUIVALENT
    DEGRADED
```

Estas dimensiones se evalúan por candidato cuando existan varios candidatos.

## 3. Separación estructural

La validación confirmó que el modelo debe distinguir entre:

- **resultado global** de la reconstrucción;
- **candidatos** de reconstrucción;
- **alcance** objetivo y reconstruido;
- **procedencia de entrada**;
- **linaje de reconstrucción**.

Reglas consolidadas:

```text
Resolution is global to the reconstruction task
Coverage and Fidelity are candidate-relative
Input provenance != Reconstruction lineage
```

## 4. Invariantes consolidados

```text
reconstruction != authorization
reconstruction != inversion by default
reconstructed artifact != accepted/canonical domain state
fidelity claims are relative to explicit scope
unresolved ambiguity must remain explicit
partial reconstruction != failure by definition
property strength may increase only with new independent explicit scoped justification/evidence
historical reconstruction != current-state assertion
```

## 5. Reconstrucción, Binding y autoridad

La reconstrucción y el Binding son responsabilidades distintas.

```text
Representation(s)
    + Context
    + Evidence
    + Reconstruction Rules
        ↓
Reconstruction
        ↓
ReconstructedArtifact / Candidates
        ↓ optional Binding
DomainFacingCandidate
        ↓
DOMAIN AUTHORITY
```

La autoridad permanece fuera de AR-4.

## 6. Neutralidad no-KOS

AR-4 no requiere semántica interna KOS.

Puede operar sobre representaciones neutrales, evidencia neutra y reglas neutrales. El Binding específico de dominio sólo se usa cuando el resultado necesita proyectarse hacia un dominio particular.

## 7. Procedencia y linaje

Se consolida la distinción:

```text
Origin
    = fuente o procedencia de entrada
Lineage
    = cadena de reconstrucciones y transformaciones
```

El linaje es monotónico; el origen no se reescribe por reconstrucciones posteriores.

## 8. Temporalidad

Una reconstrucción histórica no implica una afirmación sobre el estado actual.

```text
reconstructed state @ t1 != current state @ t2
```

## 9. Condiciones de reapertura

AR-4 sólo se reabrirá si evidencia posterior demuestra que:

- requiere transferir autoridad de reconstrucción al Binding;
- exige cambiar la semántica fundamental de AR-2;
- AR-1 no puede expresar las transiciones necesarias;
- aparece dependencia circular de autoridad;
- la neutralidad no-KOS resulta falsa;
- codificación o transporte deben formar parte inseparable del núcleo semántico de reconstrucción.

## 10. Resultado

```text
AR-4 — RECONSTRUCTION MODEL
CLOSED / PASS
```
