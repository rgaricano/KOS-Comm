# AR-2 — Representation Model Validation — Pass 1

**Status:** ACTIVE — VALIDATION PASS 1 COMPLETE  
**Dependency:** `AR-2-REPRESENTATION-MODEL.en.md`

## Executive result

All twelve initial cases are modelable, but validation shows that a rigid class taxonomy should not form the AR-2 core.

```text
REPRESENTATION
    =
COMMON SEMANTIC CORE
    +
DECLARED CAPABILITIES
    +
OPTIONAL DOMAIN CLASSIFICATION
```

`representation_class` therefore becomes an optional/extensible descriptor rather than the structural axis.

`RepresentationEnvelope` remains a logical reference model, not a mandatory format or protocol message.

## Candidate minimum core

```text
RepresentationCore {
    representation_identity
    subject
    semantic_context
    provenance
    capabilities[]
    content
}
```

References, coverage, temporality, derivation and guarantees are better represented as declared semantic capabilities than as rigid universal fields.

## Validation cases

1. Reference without transfer — **PASS**. `reference != transfer`; reference resolution does not grant authority.
2. Partial state observation — **PASS**. Requires subject, context, partial coverage, observed content and provenance.
3. Operational result — **PASS**. Operation reference and result scope remain distinct from full subject state.
4. Local projection — **PASS**. Derivation and relevant transformations/losses must be expressible; projection is not canonical serialization.
5. Evidence associated with a claim — **PASS WITH REFINEMENT**. Claim, Evidence, Verification and Guarantee must remain distinct.
6. Proposal without incorporation authority — **PASS**. Proposal semantics do not grant state-change authority.
7. Derived Representation with known loss — **PASS**. Uses AR-1 `TRANSFORMED_LOSSY` semantics without duplicating them.
8. Reconstructable Representation — **PASS WITH LIMIT**. AR-2 may carry reconstruction information but AR-4 owns detailed reconstruction semantics.
9. Composite Representation — **PASS**. Composition should preserve relevant component identity, provenance and limitations.
10. Non-KOS ↔ Non-KOS — **PASS conceptual**. No internal KOS type is required by the candidate core.
11. One Representation with two encodings — **PASS**. Representation identity remains separate from encoding identity.
12. Two Representations of the same subject — **PASS**. Representation identity remains separate from subject identity.

## Taxonomy refinement

The initial vocabulary:

```text
REFERENCE OBSERVATION STATE EVENT RESULT PROJECTION DESCRIPTION
PROPOSAL EVIDENCE TRANSFER_CANDIDATE COMPOSITE
```

is retained only as extensible/descriptive classification, not a closed core enumeration.

`TRANSFER_CANDIDATE` is especially unsuitable as a neutral core class because it approaches flow/governance semantics.

## Semantic capability model

Primary candidate:

```text
Capabilities {
    SUBJECT_IDENTIFICATION
    REFERENCE_SEMANTICS
    PROVENANCE
    DERIVATION
    COVERAGE
    TEMPORALITY
    RELATIONSHIPS
    COMPOSITION
    PROPERTY_CLAIMS
    EVIDENCE_LINKAGE
    VERIFICATION_STATEMENTS
    RECONSTRUCTION_INFORMATION
}
```

The list remains open.

## Claim / Evidence / Verification / Guarantee

```text
Claim        = proposition declared by a Representation
Evidence     = related information that may support/refute a Claim
Verification = declared evaluation result
Guarantee    = declared commitment/property with explicit scope and basis
```

```text
claim != evidence
evidence != verification
verification != authority
guarantee != authority
```

## Provenance

Provenance capability is treated as core for robust interoperability, while provenance completeness remains variable and may be unknown or deliberately undisclosed.

## Coverage

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

Candidate normative rule:

```text
COMPLETE requires declared scope
```

## Subject identity

AR-2 does not impose a universal global identifier.

Candidate:

```text
SubjectDescriptor {
    identifier?
    namespace_or_context?
    scope?
    qualifiers?
}
```

AR-3 Bindings will map domain-specific identity semantics.

## RepresentationEnvelope status

```text
RepresentationEnvelope
    = LOGICAL REFERENCE MODEL
    != MANDATORY WIRE FORMAT
    != KCP MESSAGE
    != SERIALIZATION SCHEMA
```

## Provisional architectural decision

Validation favors:

```text
MINIMAL COMMON CORE
        +
SEMANTIC CAPABILITIES
        +
EXTENSIBLE CLASSIFICATION
```

over one rigid universal envelope.

## Remaining questions

- exact minimum-core membership;
- whether representation identity is mandatory for ephemeral Representations;
- safe capability extensibility/ignorability without invading AR-7;
- minimum SubjectDescriptor semantics;
- formal Claim/Evidence/Verification/Guarantee relationships;
- protection of the neutral core from domain extensions;
- validation under more complex degradation/composition scenarios.

## State

```text
12 validation cases:             PASS / PASS WITH REFINEMENT
Rigid class taxonomy:            REJECTED AS CORE
Extensible classification:       RETAINED
Minimal common core:              CANDIDATE
Semantic capabilities:            PRIMARY CANDIDATE
RepresentationEnvelope:           LOGICAL REFERENCE MODEL
Authority separation:             PRESERVED
AR-1 compatibility:               PRESERVED
Non-KOS conceptual neutrality:    PRESERVED
AR-6 separation:                  PRESERVED
```

## Next

AR-2 Refinement Pass 2:

1. minimum semantic core;
2. capability/extensibility rules;
3. SubjectDescriptor;
4. Claim/Evidence/Verification/Guarantee;
5. interoperability and safe degradation rules;
6. AR-2 closure criteria.
