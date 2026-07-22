# AR-2 — Representation Model — Final Adversarial Review

**Status:** COMPLETE — PASS

## Result

```text
ADVERSARIAL CASES: 7/7 PASS
CRITICAL CONTRADICTIONS: NONE
REWORK REQUIRED: NO
CLOSURE RECOMMENDATION: PASS
```

This review does not prove universal completeness. It establishes that the defined adversarial cases do not break AR-2 invariants and residual issues can evolve without reopening the core while its boundaries are respected.

## Cases

### A — Unknown critical capability

A `REQUIRED_FOR_INTERPRETATION` capability unsupported by the receiver makes the Representation `UNINTERPRETABLE`. No silent acceptance. **PASS.**

### B — Composition with degraded component

A composite containing a degraded component is not FULL by default. Dependent properties degrade; independent properties may remain only when explicit composition rules justify independence. **PASS.**

### C — Ephemeral Representation without identity

A self-contained ephemeral Representation may omit representation identity when no reference, correlation, derivation, composition, versioning or audit is required. Later reference requires an appropriate Representation identity and must not silently reuse subject identity. **PASS.**

### D — Subject without global identifier

A local identifier plus namespace/scope can identify a subject within declared context. Bindings may resolve external equivalence. Local identity does not imply universal identity and mapping does not transfer authority. **PASS.**

### E — Undisclosed provenance

`UNDISCLOSED` remains distinct from `UNKNOWN` and from false provenance. External policy may reject undisclosed provenance, but AR-2 does not invent or falsify it. **PASS.**

### F — Guarantee dependent on unsupported capability

If an unsupported capability is required for a declared property, the affected guarantee cannot remain verified/guaranteed for that receiver and is conservatively downgraded. Base content may remain interpretable when the capability is not required for interpretation. **PASS.**

### G — Conflicting domain extension

An extension attempting to equate Representation identity with canonical subject identity or redefine core criticality semantics is non-conformant. Extensibility does not permit core invariant redefinition. **PASS.**

## Boundary attacks

`semantic_context` is restricted to information needed to interpret content and declared capabilities; it is not a generic application-state, authority, transport or policy container.

AR-2 requires sufficiently unambiguous capability identification but does not require a global central registry.

Capability criticality is semantic; protocol negotiation remains a later mechanism.

## Closure criteria

All candidate closure criteria PASS: subject/Representation/encoding separation, neutral minimum core, extensibility, criticality, conservative degradation, non-global identity, provenance, coverage, Claim/Evidence/Verification/Guarantee separation, non-protocol RepresentationEnvelope, AR-1 compatibility, AR-3/AR-4/AR-6/AR-7 boundaries, and non-KOS conceptual neutrality.

## Decision

```text
AR-2 FINAL REVIEW
        PASS
```

## Reopen conditions

Reconsider AR-2 if later evidence shows that the minimum core requires domain semantics, conservative degradation cannot prevent false interpretation, subject/Representation separation fails, a fundamental capability requires authority/transport redefinition, AR-3 cannot bind bilaterally without contaminating the core, or Gate C.5 demonstrates only apparent non-KOS neutrality.

## Recommendation

Produce bilingual AR-2 closure and proceed to `AR-3 — BINDING MODEL`.
