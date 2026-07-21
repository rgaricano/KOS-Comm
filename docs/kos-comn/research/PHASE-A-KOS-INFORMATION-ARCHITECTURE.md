# Phase A — KOS Information Architecture Reconstruction

**Repository source of truth:** `rgaricano/KOS-Lab`  
**Source orientation ref:** `dev`  
**Historical evidence refs:** engineering branches and commits  
**Research branch:** `KOS-Comn`  
**Date:** 2026-07-21

## 1. Purpose

Reconstruct the information architecture actually established and evidenced by KOS before specifying the neutral communication model of KCA.

This document is a persistent research log. Findings must distinguish source facts, provisional engineering interpretations and KCA consequences.

## 2. Retrieval method

1. Use `README.md` on `dev` as the current orientation/source-of-truth entry point.
2. Recover historical engineering artifacts from their original branches/commits.
3. Do not interpret search-index misses as branch absence.
4. Use direct ref resolution / compare operations when necessary.
5. Contrast specifications with implementation, tests and evidence before treating provisional historical statements as final architecture.
6. Persist relevant findings in `KOS-Comn`.

Issue #5 connector rule remains mandatory:

```text
AMBIGUOUS CONNECTOR RESPONSE != NO REPOSITORY MUTATION
SEARCH INDEX MISS != BRANCH ABSENCE
WRITE RETRY REQUIRES STATE VERIFICATION
```

## 3. Reconstructed conceptual baseline

### Finding A-001 — Holographic persistent state

Historical ADR-0002 establishes that KOS has no privileged architectural or functional centre. The global concept is Persistent Cognitive State.

Persistent Cognitive State is constituted by canonical objects together with relationships, constraints, evidence and history.

### Finding A-002 — State and context are different categories

State is persistent. Context is a temporary projection of state.

A context or representation therefore cannot be treated as the knowledge source merely because it contains information derived from that state.

### Finding A-003 — Representation is not authority

Any representation, including consolidated Canon rendering, is a projection of state rather than the source of knowledge.

KCA consequence: encoded or transmitted representations cannot automatically acquire canonical authority at the receiver.

## 4. EP-0001 Canonical Object Model findings

Historical source: `engineering/ep/EP-0001-Canonical-Object-Model.md` on `engineering/KM-0001-persistent-knowledge-model`.

### Finding A-004 — Technology-independent canonical contract

`CanonicalObject` is conceptual/contractual and explicitly independent of programming language, JSON, SQL, graph databases, Git and concrete persistence mechanisms.

This is directly compatible with the KCA decoupling objective: KCA must preserve semantic contracts without requiring the KOS implementation technology.

### Finding A-005 — Minimal canonical unit

`CanonicalObject` is defined as the minimum identifiable/manageable unit in KOS.

Conceptual composition:

```text
CanonicalObject
├── Identity
├── State
├── Version
├── Relationship[]
├── Evidence[]
└── Metadata
```

Any element that KOS must persist, relate, version, audit, project or use as evidence must be representable by a CanonicalObject or an explicitly related structure.

### Finding A-006 — Identity invariants

Identity is stable across time, versions, representations and projections. It must not depend on physical/document location or encode mutable structural hierarchy.

Initial conceptual form:

```text
Identity
├── canonical_id
├── type
└── namespace/domain
```

The exact identifier system remained subject to later formalisation in this historical document.

### Finding A-007 — Identity, state, persisted representation and contextual projection are distinct

KOS explicitly separates:

```text
object identity
object state
persisted state representation
contextual state projection
```

A state change does not by itself imply an identity change.

### Finding A-008 — Version is not identity

A canonical object can retain identity through multiple versions. Relevant evolution must be reconstructible without relying exclusively on implicit storage history.

### Finding A-009 — Evidence is not truth

Evidence can refer to documents, observations, tests, commits, execution results, external sources or canonical objects.

Conceptual candidate:

```text
Evidence
├── reference
├── kind
├── provenance
├── observed_at
└── integrity
```

Evidence supports an assertion or decision but does not automatically equal truth; provenance must be preserved.

### Finding A-010 — Persistence is representation, not ontology

The concrete persisted form is a representation of the object and does not define the object's ontology.

KCA consequence: wire encoding and storage encoding must not define the semantic information model.

## 5. Relationship canonicalisation findings

Historical source: `engineering/ep/EP-0001-Relationship-Canonicalization.md`.

### Finding A-011 — Relationships are first-class canonical candidates

The historical increment provisionally models `Relationship` as a first-class CanonicalObject capable of independent identity, state, version, evidence, metadata and evolution.

This specific document was provisional pending implementation/evidence, so later evidence must be checked before marking it final.

### Finding A-012 — Referential graph, not recursive embedding

Objects reference relationships by identity and relationships reference endpoints by identity.

```text
Object A --relationship_ref--> R1
R1 --source_ref--> A
R1 --target_ref--> B
Object B --relationship_ref--> R1
```

The intended recursion is referential, avoiding infinite material nesting.

KCA consequence: communication representation should favour explicit identifiers/references and graph reconstruction over recursive object duplication.

### Finding A-013 — Relationship identity is independent

A relationship identity is not assumed to be merely `source + predicate + target`, because multiple relations can exist between the same endpoints at different times, states or evidence contexts.

### Finding A-014 — Topology must be reconstructible

The relationship model requires graph topology to be reconstructible from persisted objects and references. Historical relationships must not disappear simply because they are no longer active.

## 6. State evolution and version semantics findings

Historical source: `engineering/ep/EP-0001-State-Evolution-and-Version-Semantics.md`.

### Finding A-015 — Technical mechanisms must not define ontology

Snapshots, events and storage mechanisms are implementation mechanisms and must not accidentally define the KOS ontology.

### Finding A-016 — Transition and event are different

A transition expresses the semantic relation between distinguishable states. An event is an occurrence that may cause, observe, justify or correlate with state changes.

```text
Event != Transition != State
```

### Finding A-017 — Snapshot is a materialized projection

A snapshot is a materialised projection of represented state at an observation boundary. It is not necessarily the state itself.

```text
State Field
    ↓ observation boundary
Snapshot
    ↓ serialization
Persistent Representation
```

KCA consequence: a KSCL state package/snapshot must be explicitly identified as a bounded representation, not the ontological state itself.

### Finding A-018 — Version space is relational and may branch

A simple `previous_version` chain is insufficient for divergence, convergence, partial equivalence and semantic distance.

The historical analysis distinguishes provenance/lineage from proximity/equivalence.

### Finding A-019 — Conceptual separation required

The historical engineering analysis proposes keeping distinct:

```text
Identity       — what entity it is
State          — what condition it presents
Manifestation  — distinguishable realization
Version Relation — relation among manifestations
Transition     — relation among states
Event          — occurrence
Evidence       — support for assertion
Snapshot       — materialized state under a boundary
Serialization  — projection to representation
Persistence    — physical storage mechanism
```

KCA must not collapse these concepts for protocol convenience.

### Finding A-020 — Evolution is graph-oriented

The working hypothesis is that evolution can be represented as a referential graph of materialised states associated with stable identities, allowing branching and potential convergence without reducing versioning to a linear counter or event sourcing ontology.

## 7. Initial KCA compatibility invariants

### KCA-INV-01 — No authority promotion
Transmission does not confer canonical authority.

### KCA-INV-02 — Derived remains derived
A projection received over KCA remains a projection unless an explicit receiver-side operation promotes/imports it.

### KCA-INV-03 — Operational identity is not canonical identity
Exchange/session/correlation identity must remain distinguishable from source canonical identity.

### KCA-INV-04 — Result is not knowledge by default
Operational results do not automatically become persistent knowledge.

### KCA-INV-05 — Communication does not own knowledge
KCA carries representations; source/receiver systems retain ownership and authority rules.

### KCA-INV-06 — Representation is not authority
Serialization, KCP packets and KSCL snapshots are representations and cannot become authority merely through transport.

### KCA-INV-07 — Semantic model is transport-independent
KCA's information semantics must not depend on JSON, CBOR, Protobuf, a database, Git or any transport carrier.

### KCA-INV-08 — References preserve graph semantics
When identity exists, KCA should support reference-based graph reconstruction without requiring recursive duplication.

### KCA-INV-09 — Provenance and evidence remain distinguishable
Evidence must retain provenance; neither should be silently reduced to generic metadata.

### KCA-INV-10 — Snapshot is bounded representation
A communicated snapshot must carry enough boundary/context semantics to avoid being confused with complete persistent state.

## 8. Decoupling implication

KOS compatibility should be implemented through a binding/profile rather than by making KOS classes mandatory KCA primitives.

```text
KOS Canonical Model
        ↓
KOS ↔ KCA Binding
        ↓
KCA Neutral Information Model
        ↓
Encoding / KCP / KSCL
```

A non-KOS system must be able to implement the neutral KCA contracts without implementing `CanonicalObject` internally, while a KOS binding must preserve KOS identity, authority, evidence, provenance and derivation semantics.

## 9. Evidence status

The EP-0001 documents inspected here include both baseline statements and historically provisional decisions. The next reconstruction steps must inspect implementation and test evidence before promoting provisional findings to final KOS compatibility requirements.

## 10. Next investigation

1. Inspect EP-0001 implementation/reference model and evidence for canonical identity and relationship canonicalisation.
2. Inspect state-evolution tests and evidence.
3. Recover KM-0001 TST increments for transactional lifecycle, evidence/provenance, Persistent Cognitive State and Observation Boundary.
4. Build the formal KOS Information Object Taxonomy and Authority/Ownership Matrix.
5. Only after those checks begin the neutral KCA information model specification.
