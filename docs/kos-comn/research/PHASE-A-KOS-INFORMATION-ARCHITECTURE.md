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

```text
Identity
├── canonical_id
├── type
└── namespace/domain
```

The exact identifier system remained subject to later formalisation in this historical document.

### Finding A-007 — Identity, state, persisted representation and contextual projection are distinct

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

```text
Event != Transition != State
```

A transition expresses the semantic relation between distinguishable states. An event is an occurrence that may cause, observe, justify or correlate with state changes.

### Finding A-017 — Snapshot is a materialized projection

```text
State Field
    ↓ observation boundary
Snapshot
    ↓ serialization
Persistent Representation
```

A snapshot is a materialised projection of represented state at an observation boundary. It is not necessarily the state itself.
KCA consequence: a KSCL state package/snapshot must be explicitly identified as a bounded representation, not the ontological state itself.

### Finding A-018 — Version space is relational and may branch
A simple `previous_version` chain is insufficient for divergence, convergence, partial equivalence and semantic distance.
The historical analysis distinguishes provenance/lineage from proximity/equivalence.

### Finding A-019 — Conceptual separation required

```text
Identity         — what entity it is
State            — what condition it presents
Manifestation    — distinguishable realization
Version Relation — relation among manifestations
Transition       — relation among states
Event            — occurrence
Evidence         — support for assertion
Snapshot         — materialized state under a boundary
Serialization    — projection to representation
Persistence      — physical storage mechanism
```

KCA must not collapse these concepts for protocol convenience.

### Finding A-020 — Evolution is graph-oriented
The working hypothesis is that evolution can be represented as a referential graph of materialised states associated with stable identities, allowing branching and potential convergence without reducing versioning to a linear counter or event sourcing ontology.

## 7. KM-0001 accredited Persistent Knowledge findings

Historical branch head inspected: `engineering/KM-0001-persistent-knowledge-model`, commit `c13e0d56c9be7d5f2e31b3126195961209210ce2`.
Formal closure inspected: `engineering/KM-0001-TST-0001-CLOSURE-2026-07-20.en.md`.

### Finding A-021 — No second ontological root for knowledge [ACCREDITED]
TST-0001 formally accredits the hypothesis that persistent knowledge can use the existing Canonical Object model without introducing a `KnowledgeObject` root class or a parallel canonical model.

```text
Knowledge Object
    = Canonical Object
    + knowledge semantic specialization / role
    + domain contracts
```

This is a major KCA compatibility constraint: a KOS binding must not introduce a parallel identity/ontology merely to communicate knowledge.

### Finding A-022 — Canonical identity survives representation versioning [ACCREDITED]
The accredited increment confirms that `canonical_id` remains stable across versioned representations and that changing `Version` does not alter canonical identity.
KCA consequence: wire/encoding revision and object representation revision must not silently mutate source identity.

### Finding A-023 — Active repository and durable persistence are separate [ACCREDITED]
TST-0001 confirms that active repository state and durable persistence are distinct and that observing active state does not implicitly hydrate objects from persistence.
KCA consequence: remote observation must not imply remote hydration/import. Observation, retrieval and incorporation need separate semantics.

### Finding A-024 — Relations and evidence reuse canonical capabilities [ACCREDITED]
Persistent Knowledge does not define parallel relation/evidence systems. It reuses existing canonical capabilities.
KCA consequence: the KOS binding should map canonical relations/evidence consistently rather than create protocol-only substitutes that lose canonical semantics.

### Finding A-025 — Identity, representation version and historical lineage are distinct [ACCREDITED BOUNDARY]

```text
stable canonical identity
        !=
representation version
        !=
persistent reconstructable historical lineage
```

At TST-0001 closure, identity and versioning were accredited, but complete persistent reconstructable revision history was not yet accredited.

### Evidence accreditation — TST-0001

```text
tests/test_persistent_knowledge_conformance.py
8 PASS / 0 FAIL / 0 ERROR

Full regression:
1110 observed
1110 PASS
0 FAIL
0 ERR
```

Tested commit: `a24e15385fe2227212e9509a24715f1e873fb423`.

## 8. KM-0001 TST-0002 transactional lifecycle findings

Recovered branch by direct ref resolution despite branch-search miss: `engineering/KM-0001-TST-0002-transactional-lifecycle`.

The branch is six commits ahead of the TST-0001 branch head and contains design, closure, dedicated tests and reproducible evidence.

Important naming correction: the actual TST-0002 is **Persistent Knowledge Transactional Lifecycle Conformance**, not a general Revision and Lineage implementation. TST-0001 had identified lineage as the next boundary to inspect, but cumulative inspection resulted in a narrower accredited transactional contract while explicitly retaining complete historical lineage as unsolved.

### Finding A-026 — Four identity/revision dimensions are orthogonal [ACCREDITED]

TST-0002 accredits:

```text
canonical_id
    !=
Version.version_id / previous_version
    !=
persistent transactional revision
    !=
operation_id
```

Semantics:

```text
canonical_id
    = stable object identity

Version.version_id / previous_version
    = semantic version and declared semantic predecessor

persistent registry revision
    = infrastructure transactional revision

operation_id
    = transactional/idempotent operation identity
```

KCA consequence: communication correlation/idempotency identifiers must never be overloaded as canonical identity, semantic version or persistent revision.

### Finding A-027 — Transactional publication does not redefine semantic version [ACCREDITED]

A valid persistent write can increment the registry transactional revision independently from `Version.version_id`.

Transactional revision protects publication/concurrency. It does not describe the semantic evolution of the knowledge object.

KCA consequence: transport sequencing, exchange revision or delivery attempt counters cannot substitute for semantic object revision.

### Finding A-028 — Canonical identity survives transactional update [ACCREDITED]

A knowledge representation can be transactionally updated while preserving `canonical_id`, semantic role and semantic version semantics.

Persistence round-trip and independent reconstruction preserve identity, type, namespace/domain, `Version`, and `previous_version`.

### Finding A-029 — Optimistic concurrency protects persisted knowledge [ACCREDITED]

Writes using stale `expected_revision` are rejected, and a rejected conflict preserves the last valid persisted state.

KCA consequence: if KCA later supports remote mutation/publication, preconditions and conflict semantics must be explicit rather than inferred from transport success.

### Finding A-030 — Operation identity provides idempotency, not knowledge identity [ACCREDITED]

Retrying the same transactional operation using the same `operation_id` does not duplicate the transition.

KCA consequence: KCP should be free to define exchange/operation identity for correlation and idempotency, but that identity belongs to the communication/operation plane.

### Finding A-031 — Temporal relation does not imply lineage [ACCREDITED NON-REGRESSION]

The cumulative contract explicitly protects the invariant that a temporal relation does not implicitly create a lineage edge.

This is decisive for KCA: timestamps, ordering, `before/after`, receipt order or causal proximity must not be interpreted automatically as semantic predecessor/successor relationships.

### Finding A-032 — `previous_version` is an explicit semantic predecessor, but not complete lineage [ACCREDITED BOUNDARY]

`previous_version` survives persistence and reconstruction and declares a semantic predecessor. It is neither transactional revision nor operation identity.

However, TST-0002 explicitly does **not** accredit a complete navigable history of all prior semantic representations.

```text
preserved previous_version
        !=
complete historical revision store
```

Atomic registry reconstruction and historical knowledge-lineage reconstruction are related but distinct contracts.

Therefore KCA must be able to preserve an explicit predecessor reference when supplied without assuming that it has received or can navigate the entire lineage graph.

### Evidence accreditation — TST-0002

Dedicated family:

```text
tests/test_persistent_knowledge_transactional_lifecycle.py
10 PASS / 0 FAIL / 0 ERROR
```

Full regression:

```text
1120 observed
1120 PASS
0 FAIL
0 ERR
Return code: 0
Verification errors: none
```

Tested commit: `9e3d3863010df6ea671bfaaae7cd6df9ae37114b`.

Production changes:

```text
Changes in src/: 0
New persistence engines: 0
New knowledge identity: 0
Canonical model duplication: 0
```

The cumulative infrastructure was sufficient.

## 9. Initial KCA compatibility invariants

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

### KCA-INV-11 — Knowledge communication must not create a second KOS ontology
KOS knowledge communicated through KCA remains semantically rooted in the existing canonical model; KCA-specific envelopes or information units are transport/interoperability structures, not replacement canonical roots.

### KCA-INV-12 — Observation is not hydration
Receiving/observing a remote representation must not implicitly insert or hydrate it into the receiver's durable knowledge store.

### KCA-INV-13 — Identity, representation revision and lineage are independent dimensions
KCA must be capable of carrying these dimensions separately when present.

### KCA-INV-14 — Transaction identity is not semantic identity
Operation, exchange, correlation and idempotency identifiers belong to the operational plane and must not substitute for canonical object identity or semantic version identity.

### KCA-INV-15 — Transport/order metadata does not imply lineage
Temporal ordering, receipt order, sequence numbers or transport causality must not create semantic predecessor/successor edges unless lineage is explicitly asserted.

### KCA-INV-16 — Partial lineage remains partial
An explicit predecessor reference may be communicated without implying that the complete revision history is available, transferred or reconstructible.

### KCA-INV-17 — Persistence conflict semantics are independent from transport delivery
Successful packet/message delivery does not imply successful persistent publication. If remote publication is supported, its preconditions, conflicts and resulting persistent revision must be represented separately.

## 10. Decoupling implication

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

A non-KOS system must be able to implement the neutral KCA contracts without implementing `CanonicalObject` internally, while a KOS binding must preserve KOS identity, authority, evidence, provenance, derivation, semantic version and explicit lineage semantics.

The accredited KM-0001 results strengthen this separation: KCA must avoid becoming a second ontological root inside KOS and must keep its operational identity/revision plane separate from source semantic identity/versioning.

## 11. Evidence status

Accredited through TST-0002:

- canonical knowledge specialization without a second ontology;
- stable canonical identity across representations;
- semantic version preservation;
- explicit `previous_version` preservation;
- active repository / durable persistence separation;
- non-hydrating observation;
- transactional persistent revision independent from semantic version;
- optimistic concurrency protection;
- operation idempotency independent from knowledge identity;
- temporal relation does not imply lineage.

Still not accredited as complete:

- complete navigable historical revision store;
- general lineage ontology / branching-convergence implementation;
- final first-class relationship canonicalisation status;
- knowledge evidence/provenance contract;
- Persistent Cognitive State observation contract;
- Observation Boundary contract.

## 12. Next investigation

1. Recover `engineering/KM-0001-TST-0003-knowledge-evidence-provenance`.
2. Determine the final accredited evidence/provenance semantics and authority consequences.
3. Recover `engineering/KM-0001-TST-0004-persistent-cognitive-state-observation`.
4. Recover `engineering/KM-0001-TST-0005-observation-boundary`.
5. Cross-check relationship canonicalisation against implementation/tests.
6. Build the formal KOS Information Object Taxonomy and Authority/Ownership Matrix.
7. Only after those checks begin the neutral KCA information model specification.
