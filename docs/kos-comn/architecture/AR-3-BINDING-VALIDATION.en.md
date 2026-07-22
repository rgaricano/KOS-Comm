# AR-3 — Binding Model — Validation Pass 1

**Status:** COMPLETE — PASS WITH REFINEMENT

## Overall result

```text
CASES: 12
PASS: 12
PASS WITHOUT CHANGE: 6
PASS WITH REFINEMENT: 6
CRITICAL CONTRADICTIONS: 0
REWORK OF CORE PREMISE: NO
```

Core premise preserved: Binding is an explicit bilateral semantic seam; bilateral does not mean symmetric/reversible; mapping capability does not imply domain authority.

## Cases

1. **KOS → KCA partial observation — PASS.** A stabilized KOS contract can map to AR-2 with PARTIAL coverage and AR-1 transitions without importing KOS-internal semantics into KCA.
2. **KCA → KOS received result — PASS.** Inbound mapping produces a DomainFacingCandidate, not canonical import or accepted state.
3. **Non-KOS A → KCA → Non-KOS B — PASS.** No KOS type, identity or authority is required. This supports conceptual neutrality but does not replace Gate C.5 evidence.
4. **Local identity across namespaces — PASS WITH REFINEMENT.** Introduce contextual correlation semantics and optional basis/validity.
5. **Unsupported critical inbound capability — PASS WITH REFINEMENT.** Result is `UNMAPPABLE` with diagnostic `UNSUPPORTED_CAPABILITY`; status and cause should remain separate.
6. **Declared lossy outbound mapping — PASS.** Relevant loss yields `MAPPED_WITH_DEGRADATION` and AR-1 loss transitions.
7. **OUTBOUND-only Binding — PASS.** A declared one-direction Binding is conformant.
8. **Bidirectional non-reversible Binding — PASS.** BIDIRECTIONAL does not imply INVERTIBLE.
9. **Incompatible contracts — PASS WITH REFINEMENT.** Separate declared/static compatibility from runtime semantic mappability.
10. **Local policy stricter than KCA — PASS WITH REFINEMENT.** Mapping-admissibility policy belongs at the Binding boundary; authoritative business/domain acceptance remains with the domain.
11. **Correlation without identity authority — PASS WITH REFINEMENT.** Binding owns correlation semantics but need not own correlation persistence.
12. **Two-Binding chain with accumulated degradation — PASS WITH REFINEMENT.** Without new justified evidence, semantic confidence/property strength must not increase across the chain.

## CorrelationDescriptor

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

Correlation is not canonical identity authority.

## Refined BindingResult

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Primary statuses remain:

```text
MAPPED
MAPPED_WITH_DEGRADATION
UNMAPPABLE
REJECTED_BY_BINDING_POLICY
UNSUPPORTED_CONTRACT
```

Candidate diagnostics:

```text
UNSUPPORTED_CAPABILITY
INSUFFICIENT_CONTEXT
IDENTITY_UNRESOLVED
SEMANTIC_CONFLICT
POLICY_CONSTRAINT
CONTRACT_RANGE_MISMATCH
```

Insufficient information is represented as `UNMAPPABLE + INSUFFICIENT_CONTEXT` when it prevents mapping rather than as another primary status.

## Binding identity

For an interoperable `BindingContract`, binding identity is required and must be unambiguous in its interoperability scope. A universal global identifier is not required. Purely embedded local mapping logic need not be elevated to an interoperable BindingContract identity.

## Policy boundary

```text
Binding policy = semantic mapping admissibility
Domain policy = authoritative acceptance/action
```

## Compatibility

```text
CompatibilityDescriptor {
    domain_contract_range
    kca_contract_range
    capability_profile?
    direction_constraints?
}
```

Declared compatibility is evaluated before runtime mappability. Compatibility does not guarantee every concrete payload is mappable.

## Binding composition

Composition is not automatically safe merely because adjacent Bindings are locally compatible. It must account for required capabilities, accumulated losses, correlations, identity scopes, admissibility policies and contract compatibility.

`BindingComposition` should therefore be explicitly validated rather than assumed.

## Rule dependencies

AR-3 does not require a universal rule language. A realization must be able to declare preconditions, inputs/dependencies, produced semantics and losses/transitions; concrete syntax remains outside the conceptual model.

## Lifecycle

The validation does not justify making DECLARED/VALIDATED/ACTIVE/DEPRECATED/RETIRED part of the core Binding semantics. Keep lifecycle as management/governance metadata for now.

## Refined conformance

A conformant Binding must be unambiguously identified within its interoperability scope; declare linked contract ranges and directions; preserve authority separation; produce candidates rather than authoritative acceptance inbound; declare AR-1 losses; respect AR-2 criticality/degradation; separate result status from diagnostic cause; never elevate properties without explicit new basis; distinguish admissibility from domain authority; treat correlation as relation rather than identity authority; avoid assuming composition safety; separate declared compatibility from runtime mappability; remain separate from encoding/transport; and permit non-KOS realizations.

## Next pass

AR-3 Refinement / Adversarial Pass 2 will test Binding composition, conflicting correlations, contract version changes, policy attempting authority, property restoration with local evidence, insufficient semantic context, Binding identity collision, and a non-KOS chain with partially overlapping capabilities.

## Result

```text
AR-3 VALIDATION PASS 1
    PASS WITH REFINEMENT
CORE PREMISE
    PRESERVED
NEXT
    AR-3 REFINEMENT / ADVERSARIAL PASS 2
```
