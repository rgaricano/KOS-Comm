# AR-4 — Reconstruction Model — Closure

**Status:** CLOSED / PASS  
**Phase:** Phase II — Reconstruction Semantics  
**Predecessor:** Gate A PASS  
**Next:** AR-5 — KSCL Decomposition

## Decision

AR-4 closes without critical contradictions.

```text
AR-4 — RECONSTRUCTION MODEL
STATUS: CLOSED
RESULT: PASS
```

## Stabilized axes

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

These are candidate-relative when multiple candidates exist.

## Structural separation

The model distinguishes:

- global reconstruction result;
- reconstruction candidates;
- target and reconstructed scope;
- input provenance;
- reconstruction lineage.

Consolidated rules:

```text
Resolution is global to the reconstruction task
Coverage and Fidelity are candidate-relative
Input provenance != Reconstruction lineage
```

## Consolidated invariants

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

## Reconstruction, Binding and authority

Reconstruction and Binding are distinct responsibilities.

```text
Representation(s) + Context + Evidence + Reconstruction Rules
        ↓
Reconstruction
        ↓
ReconstructedArtifact / Candidates
        ↓ optional Binding
DomainFacingCandidate
        ↓
DOMAIN AUTHORITY
```

Authority remains outside AR-4.

## Non-KOS neutrality

AR-4 requires no internal KOS semantics. It can operate over neutral Representations, neutral evidence and neutral rules. A domain-specific Binding is used only when the reconstruction result must be projected into a particular domain.

## Provenance and lineage

`Origin` is the source/provenance of inputs; `Lineage` is the chain of reconstructions and transformations. Lineage is monotonic; origin is not rewritten by later reconstructions.

## Time

A historical reconstruction does not imply a statement about current state.

```text
reconstructed state @ t1 != current state @ t2
```

## Reopen conditions

AR-4 should reopen only if later evidence shows it requires transferring reconstruction authority to Binding, changing AR-2 core semantics, making AR-1 unable to express required transitions, introducing circular authority, breaking non-KOS neutrality, or making encoding/transport inseparable from reconstruction semantics.

## Result

```text
AR-4 — RECONSTRUCTION MODEL
CLOSED / PASS
```
