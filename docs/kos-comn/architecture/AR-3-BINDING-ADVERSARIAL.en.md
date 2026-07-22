# AR-3 — Binding Model — Adversarial Pass 2

**Status:** COMPLETE — PASS WITH FINAL REFINEMENT

## Result

```text
ADVERSARIAL CASES: 8
PASS: 8
CRITICAL CONTRADICTIONS: 0
CORE REWORK: NO
FINAL REFINEMENTS REQUIRED: YES
CLOSURE CANDIDATE: YES
```

## A — Composition with accumulated degradation

Composed results must preserve inherited and local relevant transitions. A justified restoration does not erase prior degradation history.

```text
CompositionTransitionSet
 = inherited transitions
 + local transitions
 + explicitly justified restorations
```

**PASS.**

## B — Conflicting correlations

Conflicting correlations cannot be silently selected. Unless declared scope/basis resolves the apparent conflict, the result is `UNMAPPABLE + SEMANTIC_CONFLICT`. Resolution rules do not create canonical authority by themselves. **PASS.**

## C — Domain contract version transition

A Binding declared for domain contract 2.x cannot assume compatibility with semantically incompatible 3.0 based on structural similarity or parse success. Use `UNSUPPORTED_CONTRACT + CONTRACT_RANGE_MISMATCH` unless an explicit version bridge exists and declares its transformations/losses. **PASS.**

## D — Binding policy attempting domain authority

A policy that automatically performs canonical persistence based on mapping conditions exceeds Binding admissibility semantics and is non-conformant. Binding policy may decide whether mapping is admissible; authoritative domain acceptance/action remains separate. **PASS.**

## E — Property restoration using additional local evidence

Property strength may increase only when new independent justified evidence/basis is introduced and declared with scope, provenance and transition. The restoration must not be attributed to the received Representation itself. **PASS.**

## F — Insufficient semantic context

Structurally valid content lacking required semantic context produces `UNMAPPABLE + INSUFFICIENT_CONTEXT`. A Binding must not fill context through implicit assumptions; external context can be incorporated only through declared source/rules. **PASS.**

## G — Binding identity collision

Two incompatible Bindings with the same identity in the same interoperability scope create an ambiguity and must cause discovery/compatibility failure rather than arbitrary selection. Binding identity must be unique within its declared interoperability scope. **PASS.**

## H — Non-KOS chain with partially overlapping capabilities

A receiver supporting required capability X and optional Y but not optional Z can safely degrade/ignore Z when dependencies permit. If Z is REQUIRED_FOR_INTERPRETATION, mapping becomes UNMAPPABLE. No KOS-internal types are required. **PASS.**

## Candidate composition assessment

```text
BindingCompositionAssessment {
    participants[]
    contract_compatibility
    capability_coverage
    identity_scope_consistency
    correlation_consistency
    accumulated_property_transitions[]
    admissibility_constraints[]
    result
    diagnostics[]
}
```

This does not require a universal KCA composition engine; it identifies what must be assessed when Bindings are composed.

## Restoration rule

Default: property strength is conservatively monotonic non-increasing across transformations.

Exception: strength may increase only with new, independent, explicit and scoped justification/evidence, attributed to the restoration point.

## Correlation

```text
CorrelationDescriptor {
    correlation_id?
    relation
    endpoints[]
    scope
    basis?
    validity?
}
```

Correlation is not identity authority; conflict is not implicit resolution; persistence is not required to be owned by Binding semantics.

## Policy boundary

Mapping admissibility belongs to Binding. Authoritative acceptance, persistence and execution belong to the domain.

## Compatibility

Declared contract compatibility and runtime semantic mappability are separate stages; neither substitutes for the other.

## Binding identity

For interoperable BindingContract, binding identity is required and unique within the declared interoperability scope. No universal global identity is required.

## Invariant assessment

All tested invariants PASS: bilateral/non-reversible separation, mapping/authority separation, candidate/accepted-state separation, receipt/import separation, identity-mapping/identity-authority separation, conservative degradation, evidence-based restoration, declared-compatibility/runtime-mappability separation, explicit composition validation, policy/domain-authority separation, non-KOS neutrality, and transport/encoding separation.

## Residual risks

Non-blocking conceptual risks remain around discovery/registry strategy, mapping-rule syntax, correlation storage, capability-profile negotiation, version migration, restoration evidence instrumentation and composition-assessment implementation.

## Recommendation

```text
AR-3
  Initial Model        COMPLETE
  Validation Pass 1    PASS WITH REFINEMENT
  Adversarial Pass 2   PASS WITH FINAL REFINEMENT

RECOMMENDATION:
  PRODUCE AR-3 CLOSURE
  THEN EVALUATE GATE A
```
