# AR-5 — KSCL Decomposition — Closure

**Status:** CLOSED / PASS  
**Phase:** Phase II — Reconstruction Semantics / KSCL foundation  
**Predecessor:** AR-4 CLOSED/PASS  
**Next:** Gate B — cross-architecture review

## Decision

AR-5 closes with the validated meta-model and the formal KSCL Core.

```text
AR-5 — KSCL DECOMPOSITION
STATUS: CLOSED
RESULT: PASS
```

## Consolidated meta-model

Every KSCL module is described by:

```text
Atoms
    ↓
Assertions
    ↓
Evaluations (optional)
    ↓
Operations (optional)
```

Invariants:

```text
Atoms never depend on upper layers
Assertions never create atoms
Evaluations never mutate assertions
Operations never define semantics
Semantic dependencies are acyclic
```

## Semantic stratification

Four conceptual levels are stabilized:

1. Semantic Atoms — indivisible concepts.
2. Semantic Assertions — relations or declarations over atoms.
3. Semantic Evaluations — observational judgments over assertions.
4. Semantic Operations — processes that consume semantics to produce new assertions or external effects.

Evaluations and operations are optional and do not alter atoms or assertions.

## Formal KSCL core

Normative primitives:

```text
Entity
Reference
PropertyDefinition
PropertyValue
PropertyStrength
Representation
Evidence
Origin
Lineage
Resolution
Coverage
Fidelity
Compatibility
```

Normative relations:

```text
Correlation
Support
Transition
```

## Formal specification

KSCL Core is the minimum set of semantic constructions required to express, exchange and reason about representations, reconstructions and bindings in a domain-neutral way.

Conformance:

```text
A module is KSCL Core compliant iff:
1. every semantic element is classifiable as Atom, Assertion, Evaluation or Operation;
2. every dependency satisfies the KSCL invariants;
3. no semantic cycle exists;
4. no domain authority is introduced;
5. no primitive duplicates another primitive's semantics.
```

## Family reconciliation

- `PropertyStrength` expresses the partial order of preservation/loss.
- `Representation` carries capabilities, coverage and provenance.
- `Binding` is expressed as an operation or composed evaluation over compatibility and correspondence.
- `Reconstruction` is expressed as an operation with resolution, coverage and fidelity evaluated per candidate.
- `Origin` is the input source; `Lineage` is the monotonic chain of reconstructions and transformations.

## Semantic closure

```text
Any new KSCL construction must be expressible as a specialization or composition of the core categories.
```

If a proposal requires a fifth ontological category, the burden of proof lies on the proposal.

## Validation outcome

Atomization and adversarial validation did not reveal a counterexample to the core. Semantic families were preserved, but processes were relegated to the operational level and evaluations to the observational level.

## Reopen conditions

AR-5 should reopen only if a future construction cannot be classified without loss as an atom, assertion, evaluation or operation, or if a new case forces a fifth ontological category.

## Result

```text
AR-5 — KSCL DECOMPOSITION
CLOSED / PASS
```
