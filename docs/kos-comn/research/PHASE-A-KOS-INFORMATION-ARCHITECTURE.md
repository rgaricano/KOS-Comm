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

### Finding A-021 — No second ontological root for knowledge [ACCREDITED]

```text
Knowledge Object
    = Canonical Object
    + knowledge semantic specialization / role
    + domain contracts
```

### Finding A-022 — Canonical identity survives representation versioning [ACCREDITED]
`canonical_id` remains stable across versioned representations.

### Finding A-023 — Active repository and durable persistence are separate [ACCREDITED]
Observing active state does not implicitly hydrate objects from persistence.

### Finding A-024 — Relations and evidence reuse canonical capabilities [ACCREDITED]
Persistent Knowledge does not define parallel relation/evidence systems.

### Finding A-025 — Identity, representation version and historical lineage are distinct [ACCREDITED BOUNDARY]

```text
stable canonical identity
        !=
representation version
        !=
persistent reconstructable historical lineage
```

TST-0001 dedicated family: `8 PASS / 0 FAIL / 0 ERROR`.
Full regression: `1110 PASS / 0 FAIL / 0 ERR`.

## 8. KM-0001 TST-0002 transactional lifecycle findings

Recovered branch: `engineering/KM-0001-TST-0002-transactional-lifecycle`.

### Finding A-026 — Four identity/revision dimensions are orthogonal [ACCREDITED]

```text
canonical_id
    !=
Version.version_id / previous_version
    !=
persistent transactional revision
    !=
operation_id
```

### Finding A-027 — Transactional publication does not redefine semantic version [ACCREDITED]
Transactional revision protects publication/concurrency. It does not describe semantic evolution.

### Finding A-028 — Canonical identity survives transactional update [ACCREDITED]
Persistence/reconstruction preserve canonical identity, semantic role, `Version`, and `previous_version`.

### Finding A-029 — Optimistic concurrency protects persisted knowledge [ACCREDITED]
Stale `expected_revision` writes are rejected and do not corrupt the last valid state.

### Finding A-030 — Operation identity provides idempotency, not knowledge identity [ACCREDITED]
Repeated `operation_id` does not duplicate the transition.

### Finding A-031 — Temporal relation does not imply lineage [ACCREDITED NON-REGRESSION]
Temporal ordering does not implicitly create a lineage edge.

### Finding A-032 — `previous_version` is an explicit semantic predecessor, but not complete lineage [ACCREDITED BOUNDARY]

```text
preserved previous_version
        !=
complete historical revision store
```

TST-0002 dedicated family: `10 PASS / 0 FAIL / 0 ERROR`.
Full regression: `1120 PASS / 0 FAIL / 0 ERR`.
Tested commit: `9e3d3863010df6ea671bfaaae7cd6df9ae37114b`.

## 9. KM-0001 TST-0003 relations, evidence and provenance findings

Recovered directly: `engineering/KM-0001-TST-0003-knowledge-evidence-provenance`.

The branch is six commits ahead of TST-0002 and contains design, formal closure, dedicated tests and reproducible evidence.

Actual accredited increment name: **Knowledge Relations, Evidence and Provenance Composition**.

### Finding A-033 — Knowledge relation/evidence composition reuses canonical capabilities [ACCREDITED]

The accredited composition is:

```text
Knowledge Object
    = CanonicalObject with a knowledge semantic role

Knowledge Relation
    = canonical relation with knowledge semantics

Knowledge Evidence
    = inline Evidence
      or CanonicalObject with an evidence role/type

Knowledge Provenance
    = explicit provenance associated with evidence
      or provenance of a derived projection
```

No new `KnowledgeRelation` or `KnowledgeEvidence` root classes are required.

KCA consequence: the neutral communication model may need generic relation/evidence constructs, but a KOS binding must map them onto the existing canonical model rather than manufacture protocol-owned knowledge ontologies.

### Finding A-034 — Relation, evidence, provenance and lineage are semantically independent [ACCREDITED]

```text
relation
    !=
evidence
    !=
provenance
    !=
lineage
```

Semantics:

- relation connects objects semantically;
- evidence supports, justifies or observes a representation;
- provenance describes origin, derivation or production context;
- lineage expresses explicit continuity/revision.

KCA consequence: these concepts require distinct semantic roles even if an encoding later permits compact co-location.

### Finding A-035 — Evidence can be inline or independently canonical [ACCREDITED]

A knowledge object may contain inline evidence or reference a canonical evidence object through `evidence_refs`.

Evidence resolution can compose both forms without losing canonical evidence identity.

This implies at least two communication patterns:

```text
Inline evidence
KnowledgeRepresentation
└── evidence[]

Referenced evidence
KnowledgeRepresentation
└── evidence_ref[] ──> EvidenceRepresentation
```

KCA must not assume that all evidence is embedded or that all evidence possesses independent canonical identity.

### Finding A-036 — Shared canonical evidence must not be duplicated structurally [ACCREDITED]

One canonical evidence object can support multiple knowledge objects while retaining a single canonical identity.

```text
Knowledge A ──evidence_ref──┐
                            ├──> Evidence E
Knowledge B ──evidence_ref──┘
```

This strengthens the requirement for reference-oriented graph communication. Serialization convenience must not silently clone an identity-bearing evidence object into multiple semantically independent objects.

### Finding A-037 — Evidence identity, evidence reference and inline content are different [ACCREDITED]

TST-0003 explicitly keeps distinct:

```text
knowledge identity
evidence identity
evidence reference
inline evidence content
```

KCA consequence: a reference to evidence is not the evidence itself, and inline evidence must not be assigned source canonical identity unless such identity is explicitly present.

### Finding A-038 — Evidence provenance can be persistent semantic information [ACCREDITED]

Provenance associated with serializable/persistent evidence survives persistence and reconstruction.

Therefore evidence provenance may legitimately cross a KCA boundary as part of the evidence semantics.

This does not mean provenance is authority or truth. It describes origin/production context and remains associated with the evidential assertion.

### Finding A-039 — Projection provenance remains derived [ACCREDITED BOUNDARY]

Projection provenance describes how a cognitive projection was obtained.

It does not implicitly become:

```text
canonical identity
knowledge object
persistent evidence
semantic relation
lineage edge
```

KCA consequence: provenance attached to a transmitted projection must preserve its derivation role. Receiving or serializing it must not promote it into canonical source evidence.

### Finding A-040 — Provenance does not confer canonical authority [DERIVED KCA CONSEQUENCE]

Combining A-003, A-009 and TST-0003 yields:

```text
provenance present
        !=
source authoritative
        !=
receiver canonical
        !=
claim true
```

Provenance improves traceability and interpretability; it does not by itself establish truth or receiver-side authority.

This distinction must become explicit in the future KCA Authority/Ownership Matrix.

### Finding A-041 — Canonical relations survive persistence and endpoint reconstruction [ACCREDITED]

Canonical relations can connect knowledge objects without a parallel relation class, and relation endpoints remain resolvable after reconstruction.

This provides accredited support for referential graph reconstruction rather than recursive structural embedding.

### Finding A-042 — Temporal relation remains distinct from lineage [ACCREDITED NON-REGRESSION]

The full TST-0003 regression retains `test_temporal_relation_does_not_create_lineage_edge`.

Evidence/provenance composition therefore does not weaken the explicit-lineage boundary established earlier.

### Evidence accreditation — TST-0003

Dedicated family:

```text
tests/test_persistent_knowledge_evidence_provenance.py
10 PASS / 0 FAIL / 0 ERROR
```

The family accredits:

- referenced canonical evidence resolution;
- inline evidence preservation;
- inline + canonical evidence composition;
- shared canonical evidence reuse without structural duplication;
- persistence/reconstruction of evidence composition;
- canonical knowledge relations;
- relation endpoint reconstruction;
- relation/evidence semantic separation;
- inline evidence provenance persistence;
- projection provenance / canonical identity separation.

Full regression:

```text
1130 observed
1130 PASS
0 FAIL
0 ERR
Return code: 0
Verification errors: none
```

Tested commit: `987151ee49a948a1b275a50a04844f5aeb8fcd7b`.

Production impact:

```text
Changes in src/: 0
New knowledge root classes: 0
New parallel relation ontologies: 0
New persistence engines: 0
```

Cumulative infrastructure was sufficient.

## 10. Initial KCA compatibility invariants

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

### KCA-INV-18 — Relation, evidence, provenance and lineage are independent semantic roles
Communication structures must not collapse semantic connection, evidential support, origin/derivation and revision continuity into one generic link or metadata mechanism.

### KCA-INV-19 — Evidence may be inline or referenced
KCA must permit evidence without independent identity as well as references to independently identifiable evidence when the source model provides it.

### KCA-INV-20 — Shared identity-bearing evidence is referenceable, not duplicative
When the same evidence identity supports multiple communicated objects, the communication model must permit shared reference semantics without requiring identity-destroying structural copies.

### KCA-INV-21 — Provenance does not confer authority
Communicated provenance improves traceability but does not automatically make the representation authoritative, canonical at the receiver, or true.

### KCA-INV-22 — Projection provenance remains projection provenance
Derivation metadata for a projection does not implicitly become source knowledge, persistent evidence, canonical identity, relation or lineage merely because it is transmitted.

## 11. Decoupling implication

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

A non-KOS system must be able to implement neutral KCA contracts without implementing `CanonicalObject` internally.

A KOS binding, however, must preserve where present:

```text
canonical identity
semantic version
explicit predecessor/lineage reference
relations
evidence identity
inline evidence
evidence references
evidence provenance
projection provenance
derivation status
operational identity
transactional revision semantics
```

KCA therefore needs semantic expressiveness without assuming ownership of those semantics.

## 12. Evidence status

Accredited through TST-0003:

- canonical knowledge specialization without a second ontology;
- stable canonical identity across representations;
- semantic version preservation;
- explicit `previous_version` preservation;
- active repository / durable persistence separation;
- non-hydrating observation;
- transactional persistent revision independent from semantic version;
- optimistic concurrency protection;
- operation idempotency independent from knowledge identity;
- temporal relation does not imply lineage;
- canonical knowledge relation composition;
- relation endpoint reconstruction;
- inline evidence;
- referenced canonical evidence;
- shared evidence without structural duplication;
- evidence composition persistence/reconstruction;
- evidence provenance persistence;
- projection provenance separation from canonical knowledge identity.

Still not accredited as complete:

- complete navigable historical revision store;
- general lineage ontology / branching-convergence implementation;
- final status of all historical first-class relationship design claims beyond the composition contract;
- Persistent Cognitive State observation contract;
- Observation Boundary contract;
- receiver-side import/promotion/authority policy for communicated knowledge.

## 13. Next investigation

1. Recover `engineering/KM-0001-TST-0004-persistent-cognitive-state-observation`.
2. Determine exactly what constitutes observable Persistent Cognitive State versus active repository state and derived observation.
3. Recover `engineering/KM-0001-TST-0005-observation-boundary`.
4. Determine observation-boundary identity, completeness, selection and projection semantics.
5. Cross-check remaining relationship canonicalisation claims against implementation/tests where necessary.
6. Build the formal KOS Information Object Taxonomy and Authority/Ownership Matrix.
7. Only after those checks begin the neutral KCA information model specification.
