# KCA Neutral Information Model v0

**Status:** Initial architectural model — not wire format  
**Date:** 2026-07-21

## 1. Objective

Define a system-neutral information contract that can represent KOS semantics without requiring a peer to implement KOS classes and without coupling semantics to KEncoding, KCP, JSON, CBOR, Protobuf or any carrier.

## 2. Root concept

```text
KCA Information Unit
├── unit_identity
├── semantic_class
├── source_descriptor
├── subject[]
├── state_layer
├── boundary
├── content
├── references[]
├── relations[]
├── evidence[]
├── provenance[]
├── lineage[]
├── authority_assertions[]
├── operation_context
└── completeness
```

This is a conceptual field model, not a finalized schema.

## 3. Core concepts

### 3.1 Unit Identity
Identity of the communicated representation/exchange unit. Must not be confused with source canonical identity.

### 3.2 Semantic Class
One or more KCA Communication Semantic Classes defining what the unit means: OBSERVATION, PROJECTION, CANONICAL_REFERENCE, CANONICAL_TRANSFER, RELATION, EVIDENCE, PROVENANCE, LINEAGE, OPERATION, RESULT, etc.

### 3.3 Source Descriptor
Identifies the source system/binding/authority domain sufficiently for receiver interpretation. It may include source namespace and binding profile.

### 3.4 Subject
References the information subjects represented by the unit. Subject identity is independent from unit identity.

Conceptually:

```text
SubjectRef
├── namespace
├── object_id
├── kind?
├── semantic_version?
└── qualifiers?
```

### 3.5 State Layer
Declares the represented layer where applicable:

```text
PERSISTED
OBSERVED
SELECTED
PROJECTED
TRANSFER
OPERATIONAL
```

Exact vocabulary remains provisional.

### 3.6 Boundary
Declares the semantic scope/completeness boundary.

```text
Boundary
├── boundary_id?
├── basis / selector?
├── included_refs[]?
├── excluded/omission semantics?
└── completeness_scope
```

The boundary prevents a contextual projection from being mistaken for global state.

### 3.7 Content
Class-specific information payload. KCA semantics do not require one universal content shape.

### 3.8 References
Identity-bearing links to external or co-packaged information entities. References are preferred over recursive duplication where shared identity matters.

### 3.9 Relations
Explicit semantic relations with endpoints and optional relation identity/type.

### 3.10 Evidence
Supports both:

```text
inline evidence
referenced identity-bearing evidence
```

### 3.11 Provenance
Carries evidence provenance and/or projection derivation provenance with explicit role discrimination.

### 3.12 Lineage
Carries only explicit lineage/predecessor semantics. It must not be synthesized from packet order or timestamps.

### 3.13 Authority Assertions
Explicit claims concerning source authority, ownership, publication or transfer status. Assertions are evaluated by receiver policy.

### 3.14 Operation Context
Optional exchange/correlation/idempotency/publication context. Operation identity remains independent from subject identity.

### 3.15 Completeness
Declares the KSCL completeness/reconstruction profile and any profile-specific guarantees.

## 4. Identity planes

KCA must support independent identity planes:

```text
representation/unit identity
source subject identity
semantic version identity
transactional revision identity
operation/correlation identity
relation/evidence identity where applicable
```

No single `id` field may be assumed to represent all planes.

## 5. Minimal observation mapping from KOS

```text
KOS StateObservation
    object_id
    kind
    attributes
        ↓
KCA Information Unit
    semantic_class = OBSERVATION
    subject.object_id = object_id
    subject.kind = kind
    state_layer = OBSERVED
    content = attributes
    completeness = KCR-1 or stronger if composed with additional structures
```

This mapping does not create canonical transfer semantics.

## 6. Projection mapping

```text
KOS Cognitive Projection
        ↓
KCA Information Unit
    semantic_class = PROJECTION
    state_layer = PROJECTED
    subjects = source references
    boundary = contextual/projection boundary
    content = projected content
    provenance = projection provenance
    completeness >= KCR-3 according to actual package
```

## 7. Canonical transfer mapping

Canonical transfer is intentionally stronger:

```text
semantic_class = CANONICAL_TRANSFER
state_layer = TRANSFER
subject = canonical source identity
content = required canonical state/version data
relations/evidence/provenance = according to binding contract
completeness >= KCR-6
transfer intent + authority assertion required for KCR-7
```

Receipt still does not imply import.

## 8. Layering

```text
Domain / Source System
        ↓ binding
KCA Neutral Information Model
        ↓ encoding
KEncoding
        ↓ session/semantic exchange
KSCL
        ↓ transport/control
KCP
        ↓ carrier
Network / IPC / file / message bus / other
```

KCA can therefore operate independently of KOS. KOS is one binding/provider of KCA semantics.

## 9. Non-goals of v0

This document does not yet define:

- byte encoding;
- JSON/CBOR/Protobuf schema;
- field numbering;
- packet framing;
- cryptographic envelope;
- routing;
- retransmission;
- discovery;
- session negotiation;
- compression;
- maximum sizes;
- mandatory transport.

Those belong to later KEncoding/KCP/KSCL protocol design after semantic review.

## 10. v0 design tests

A future concrete schema must demonstrate that it can represent without semantic collapse:

1. a KOS `StateObservation`;
2. a contextual cognitive projection;
3. a projection with source provenance;
4. shared referenced evidence;
5. a semantic relation graph;
6. explicit lineage without inferring it from order;
7. an operational publication result;
8. a canonical-transfer candidate;
9. a receiver import decision separate from receipt;
10. a non-KOS source using equivalent neutral semantics.
