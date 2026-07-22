# AR-3 — Binding Model

**Status:** ACTIVE — INITIAL MODEL  
**Phase:** Phase I — Boundary & Representation Foundation  
**Predecessors:** AR-1 CLOSED/PASS, AR-2 CLOSED/PASS

## Definition

A `Binding` is an explicit semantic adapter located at a boundary:

```text
DOMAIN
  ↕
BINDING
  ↕
KCA REPRESENTATION
```

It makes correspondence between domain semantics and KCA-representable semantics explicit. It is neither the domain, KCA itself, nor a transport protocol.

## Bilateral principle

Bindings may support outbound and/or inbound mappings. Bilateral does not mean perfectly symmetric or reversible.

`map_out(x)=R` does not require `map_in(R)=x`.

## Binding responsibilities

A Binding may own mapping rules, SubjectDescriptor resolution, semantic capability mapping, declared loss/transformation, identity correlation, semantic mapping preconditions, diagnostics, contract compatibility declarations and local mapping policy.

It does not implicitly own domain authority, canonical import, persistence, execution, represented-object ownership, KCA Representation ownership, reconstruction authority, KOS-Lab promotion authority, KCP transport or AR-6 encoding.

`MAPPING CAPABILITY != DOMAIN AUTHORITY`.

## Candidate logical contract

```text
BindingContract {
    binding_identity
    domain_contract_ref
    kca_contract_ref
    supported_directions[]
    mapping_capabilities[]
    compatibility
    declared_constraints[]
}
```

This is conceptual; AR-3 does not fix an API, language, serialization schema or deployment format.

## Directions

```text
OUTBOUND
INBOUND
BIDIRECTIONAL
```

BIDIRECTIONAL means both rule sets exist, not that they are mathematical inverses.

## Mapping result

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Candidate states:

```text
MAPPED
MAPPED_WITH_DEGRADATION
UNMAPPABLE
REJECTED_BY_BINDING_POLICY
UNSUPPORTED_CONTRACT
```

## AR-1 relationship

Bindings declare transformations using AR-1 semantics: `PRESERVED`, `TRANSFORMED_EQUIVALENT`, `TRANSFORMED_LOSSY`, `DROPPED`, `UNKNOWN`.

## AR-2 relationship

Bindings produce/consume AR-2 conformant Representations and may map subject, semantic context, capabilities, content, Representation identity, provenance and extensible classification. They cannot redefine AR-2 criticality/degradation rules.

## Identity and correlation

Domain identity may map to/from SubjectDescriptor with one-to-one, one-to-many, many-to-one, contextual or unresolved correlation. Mapping does not establish canonical identity or authority.

Correlation may relate exchanges/mappings but does not replace subject identity or Representation identity and grants no authority.

## Capability mapping

Candidate support states:

```text
SUPPORTED_NATIVE
SUPPORTED_MAPPED
SUPPORTED_WITH_DEGRADATION
UNSUPPORTED
NOT_APPLICABLE
```

Unsupported `REQUIRED_FOR_INTERPRETATION` capability cannot silently produce a valid domain interpretation.

## Degradation

Bindings cannot elevate degraded properties without additional local information/evidence and an explicit declared basis.

`DEGRADED + no new evidence != FULL`.

## Legitimate asymmetry

Outbound projection of rich domain state into a partial Representation does not imply inbound reconstructability. This preserves the AR-4 boundary.

## Inbound authority

An inbound Binding may produce a `DomainFacingCandidate`, but `candidate != accepted domain state` and `receipt != canonical import`. Acceptance, persistence and execution remain with the receiving authoritative domain.

## Stabilized contracts

For KOS, Bindings must target stabilized KOS contracts rather than accidental implementation details, consistent with the KOS-Lab ↔ KOS-Comm collaboration charter.

## KOS-specific Binding vs neutral model

The Binding Model is a neutral architectural contract. A KOS Binding is a domain-specific realization. Non-KOS domains can implement their own Bindings without KOS dependency.

## Non-KOS scenario

```text
Non-KOS A → Binding A → KCA → Binding B → Non-KOS B
```

AR-3 must permit this without KOS-internal types, preparing but not replacing Gate C.5.

## Compatibility/version

```text
CompatibilityDescriptor {
    domain_contract_range
    kca_contract_range
    capability_profile?
}
```

Compatibility must be explicit and cannot be inferred from successful parsing alone.

Candidate lifecycle: `DECLARED`, `VALIDATED`, `ACTIVE`, `DEPRECATED`, `RETIRED`; this requires validation.

## Local policy

A Binding may impose local mapping policy, but `BINDING POLICY REJECTION != KCA SEMANTIC INVALIDITY`.

## Diagnostics

Candidate diagnostic classes:

```text
SEMANTIC_UNMAPPABLE
UNSUPPORTED_CAPABILITY
INSUFFICIENT_CONTEXT
IDENTITY_UNRESOLVED
POLICY_REJECTED
CONTRACT_INCOMPATIBLE
```

## Candidate conformance

A conformant Binding declares linked contracts/directions, preserves authority separation, reports AR-1 losses, respects AR-2 criticality/degradation, avoids implicit global identity and receipt/import equivalence, declares unsafe incompatibility, remains neutral at the contract level, and separates Binding semantics from encoding/transport.

## Open questions

- mandatory vs conditional Binding identity;
- local policy placement;
- mapping-rule dependencies without an excessive universal language;
- minimum statically checkable compatibility;
- persistent correlation without authoritative storage;
- `UNMAPPABLE` vs `INSUFFICIENT_INFORMATION`;
- composition of multiple Bindings.

## Validation plan

1. KOS → KCA partial observation;
2. KCA → KOS received result without canonical import;
3. non-KOS A → KCA → non-KOS B;
4. local identity across namespaces;
5. unsupported critical inbound capability;
6. declared lossy outbound mapping;
7. OUTBOUND-only Binding;
8. bidirectional non-reversible Binding;
9. incompatible contracts;
10. local policy stricter than KCA;
11. correlation without identity authority;
12. two-Binding chain with accumulated degradation.

## State

```text
AR-3 — BINDING MODEL
Initial model: ACTIVE / ESTABLISHED
Validation: NEXT
Closure: PENDING
Gate A: PENDING
```
