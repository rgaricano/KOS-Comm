# AR-2 — Representation Model — Closure

**Status:** CLOSED / PASS  
**Phase:** Phase I — Boundary & Representation Foundation  
**Predecessor:** AR-1 — Boundary Model  
**Next:** AR-3 — Binding Model

## Closure decision

AR-2 closes with:

```text
REPRESENTATION
 = MINIMAL SEMANTIC CORE
 + DECLARED SEMANTIC CAPABILITIES
 + OPTIONAL EXTENSIBLE CLASSIFICATION
```

No closed universal taxonomy or universal message format is adopted.

## Semantic core

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

Representation identity is conditional and required when reference, correlation, derivation, composition, versioning or audit is needed.

## Identity invariants

```text
representation != represented object
representation_identity != subject_identity
mapping != authority transfer
```

No universal global subject identifier is required.

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

AR-3 may map domain identities through Bindings without making KCA an identity authority.

## Semantic capabilities

Criticality:

```text
REQUIRED_FOR_INTERPRETATION
REQUIRED_FOR_DECLARED_PROPERTY
OPTIONAL
INFORMATIONAL
```

`unknown capability != safe-to-ignore capability`.

## Interpretation and degradation

```text
FULL
DEGRADED
UNINTERPRETABLE
```

Degradation is explicit and conservative: known may become unknown, verified unverified, complete partial/unknown; the inverse requires additional evidence.

## Provenance

Provenance can explicitly express `KNOWN`, `PARTIAL`, `UNKNOWN`, `UNDISCLOSED`, or `NOT_APPLICABLE`.

## Coverage

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

`COMPLETE_FOR_SCOPE requires explicit scope`.

## Claim / Evidence / Verification / Guarantee

```text
Claim != Evidence
Evidence != Verification
Verification != Guarantee
Verification != Authority
Guarantee != Authority
```

Verification and guarantees require interpretable scope and declared basis.

## Extensibility

Domain extensions may add capabilities, classifications, semantic types and parameters but may not silently redefine core invariants.

`EXTEND != OVERRIDE CORE`.

## Neutrality

AR-2 does not require KOS-internal semantics and owns no canonical import, canonical persistence, execution, Knowledge, KOS-specific Projection or Reconstruction authority.

## RepresentationEnvelope

It remains only a logical reference model:

```text
RepresentationEnvelope
 != mandatory wire format
 != KCP message
 != serialization schema
```

## Boundaries

```text
AR-1 = boundary/property-transition semantics
AR-2 = representable semantics
AR-3 = domain ↔ Representation Binding
AR-4 = reconstruction
AR-6 = encoding
AR-7 = KCP
```

## Closure evidence

- 12 initial cases: PASS / PASS WITH REFINEMENT;
- structural refinement complete;
- 7 final adversarial cases: 7/7 PASS;
- critical contradictions: none;
- non-KOS conceptual neutrality preserved;
- AR-1 compatibility preserved.

## Reopen conditions

Reopen only if later evidence shows domain semantics are required by the core, degradation permits false interpretation, subject/Representation separation fails, AR-3 cannot bind bilaterally without core contamination, or Gate C.5 disproves neutrality.

## Result

```text
AR-2 — REPRESENTATION MODEL
STATUS: CLOSED
RESULT: PASS
NEXT: AR-3 — BINDING MODEL
```
