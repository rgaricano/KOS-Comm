# AR-2 — Representation Model — Refinement Pass 2

**Status:** ACTIVE — REFINEMENT PASS 2 COMPLETE

## Structural decision

Closure candidate:

```text
REPRESENTATION
 = MINIMAL SEMANTIC CORE
 + DECLARED SEMANTIC CAPABILITIES
 + OPTIONAL EXTENSIBLE CLASSIFICATION
```

## Refined minimum core

```text
RepresentationCore {
    subject
    semantic_context
    capabilities[]
    content
    representation_identity?
    provenance?
    classification?
}
```

`subject`, `semantic_context`, `capabilities[]` and `content` are conceptually required. Representation identity is conditional: required for reference, correlation, derivation, composition, versioning or audit/evidence linkage; ephemeral self-contained Representations may omit it.

`representation_identity != subject_identity`.

## SubjectDescriptor

```text
SubjectDescriptor {
    identifier?
    namespace?
    semantic_type?
    scope?
    qualifiers{}
}
```

No universal global identifier is required. Bindings may map domain identity to/from this descriptor without transferring identity authority to KCA.

## Semantic capabilities and criticality

```text
SemanticCapability {
    capability_id
    criticality
    semantics_reference?
    parameters?
}
```

Criticality:

```text
REQUIRED_FOR_INTERPRETATION
REQUIRED_FOR_DECLARED_PROPERTY
OPTIONAL
INFORMATIONAL
```

Unknown capability is not equivalent to safe-to-ignore capability.

If a required-for-interpretation capability is unsupported, the Representation must not be treated as semantically valid. If a capability required for a declared property is unsupported, that property must be downgraded to unknown/unverified. Optional or informational capabilities may be ignored only when core semantics remain intact.

## Safe degradation

Candidate interpretation states:

```text
FULL
DEGRADED
UNINTERPRETABLE
```

Degradation must be explicit and conservative:

```text
known -> unknown
verified -> unverified
complete -> partial/unknown
```

Never promote the inverse without additional evidence.

## Claim, Evidence, Verification, Guarantee

```text
Claim {
    claim_id?
    proposition
    scope
    issuer_or_provenance?
}

EvidenceLink {
    claim_ref
    evidence_ref
    relation
}

VerificationStatement {
    claim_ref
    method_or_basis
    result
    scope
    verifier_or_provenance?
}

GuaranteeStatement {
    property
    scope
    basis
    issuer_or_provenance
    conditions?
}
```

Evidence may support/refute a Claim. Verification evaluates a Claim/property. Guarantee declares a bounded commitment/property. None grants authority over the represented subject.

Minimum verification distinctions:

```text
VERIFIED
REFUTED
INCONCLUSIVE
NOT_VERIFIED
UNKNOWN
```

## Provenance

```text
ProvenanceDescriptor {
    source?
    producer?
    derivation_chain?
    observed_or_created_at?
    disclosure_state
}
```

Disclosure states:

```text
KNOWN PARTIAL UNKNOWN UNDISCLOSED NOT_APPLICABLE
```

Unknown or undisclosed provenance does not imply false provenance.

## Coverage

```text
CoverageDescriptor {
    state
    scope
    omitted_or_unknown_aspects?
}
```

```text
COMPLETE_FOR_SCOPE PARTIAL SUMMARY REFERENCE_ONLY UNKNOWN
```

`COMPLETE_FOR_SCOPE` requires explicit scope.

## Domain extensions

Extensions may add capabilities, classifications, semantic types and parameters, but must not silently redefine core identity separation, criticality, degradation, authority or conservative property propagation.

## Neutrality

The core contains no KOS-internal KnowledgeObject, CanonicalState, KOS-specific ExecutionResult/Projection, import authority, canonical persistence or KOS execution semantics. These may be mapped through Bindings/extensions.

## Composition

Composition cannot elevate component properties merely through aggregation. If a critical component is uninterpretable, the composition cannot be FULL unless an explicit rule demonstrates independence from that component.

## Derivation

AR-2 reuses AR-1 property-transition semantics:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DROPPED
UNKNOWN
```

## Minimum semantic interoperability

Two endpoints can interoperate semantically when they can interpret the minimum core, identify declared capabilities, understand every required-for-interpretation capability, conservatively degrade properties dependent on unsupported capabilities, preserve authority separation, and do not require shared internal domain types.

## Boundaries

AR-2 defines what semantics must be representable.

AR-3 owns domain ↔ Representation Binding semantics.

AR-6/AR-7 own serialization, framing, protocol negotiation, binary codes, transport and message behavior.

AR-4 owns detailed reconstruction semantics and does not receive reconstruction authority from AR-2.

## Closure criteria candidate

Final review must confirm:

- subject / Representation / encoding separation;
- sufficient neutral minimum core;
- extensible capabilities with explicit criticality;
- safe conservative degradation;
- no mandatory global identity;
- explicit provenance and coverage states;
- Claim/Evidence/Verification/Guarantee separation;
- RepresentationEnvelope remains a logical model, not protocol format;
- AR-1 compatibility;
- clear AR-3/AR-4/AR-6/AR-7 boundaries;
- non-KOS conceptual neutrality.

## Residual risks

- minimum core may still be too broad;
- semantic_context may become an undefined container;
- capabilities may drift toward a rigid central registry;
- semantic criticality may be confused with protocol negotiation;
- extensions may indirectly redefine the core;
- complex composition may create false guarantees.

## State

```text
Minimal semantic core:          REFINED CANDIDATE
Representation identity:        CONDITIONAL
SubjectDescriptor:              REFINED CANDIDATE
Semantic capabilities:          REFINED CANDIDATE
Capability criticality:         DEFINED
Safe degradation:               DEFINED
Claim/Evidence/Verification/
Guarantee separation:           DEFINED
Provenance semantics:           REFINED
Coverage semantics:             REFINED
Domain extension rule:          DEFINED
Non-KOS neutrality:             PRESERVED
AR boundaries:                  PRESERVED
```

## Next

Perform AR-2 Final Review / Closure Assessment using adversarial cases: unknown critical capability, degraded composition, ephemeral Representation without identity, subject without global identifier, undisclosed provenance, guarantee dependent on unsupported capability, and conflicting domain extension.

If invariants survive, produce `AR-2-CLOSURE.es.md/.en.md` and proceed to AR-3.
