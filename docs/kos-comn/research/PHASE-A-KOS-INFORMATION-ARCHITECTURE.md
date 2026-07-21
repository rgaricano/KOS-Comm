# Phase A — KOS Information Architecture Reconstruction

**Repository source of truth:** `rgaricano/KOS-Lab`  
**Source orientation ref:** `dev`  
**Historical evidence refs:** engineering branches and commits  
**Research branch:** `KOS-Comn`  
**Date:** 2026-07-21

## 1. Purpose

Reconstruct the information architecture actually established and evidenced by KOS before specifying the neutral communication model of KCA.

This document is a persistent research log. Findings distinguish source facts, accredited results, provisional historical design and derived KCA consequences.

## 2. Retrieval method

1. Use `README.md` on `dev` as current orientation/source-of-truth entry point.
2. Recover historical engineering artifacts from original branches/commits.
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

### Finding A-002 — State and context are different categories
State is persistent. Context is a temporary projection of state.

### Finding A-003 — Representation is not authority
A representation/projection is not automatically the source of knowledge or canonical authority.

## 4. EP-0001 Canonical Object Model findings

### Finding A-004 — Technology-independent canonical contract
`CanonicalObject` is conceptual/contractual and independent of programming language, JSON, SQL, graph databases, Git and concrete persistence mechanisms.

### Finding A-005 — Minimal canonical unit

```text
CanonicalObject
├── Identity
├── State
├── Version
├── Relationship[]
├── Evidence[]
└── Metadata
```

### Finding A-006 — Identity invariants
Identity is stable across time, versions, representations and projections and must not depend on physical/document location.

### Finding A-007 — Identity, state, persisted representation and contextual projection are distinct

```text
object identity
object state
persisted state representation
contextual state projection
```

### Finding A-008 — Version is not identity
A canonical object can retain identity through multiple versions.

### Finding A-009 — Evidence is not truth
Evidence supports an assertion/decision but does not automatically equal truth; provenance must be preserved.

### Finding A-010 — Persistence is representation, not ontology
Concrete persisted form does not define object ontology.

## 5. Relationship canonicalisation findings

### Finding A-011 — Relationships are first-class canonical candidates [HISTORICAL DESIGN]
Historical EP design models `Relationship` as a first-class canonical candidate. Later TST-0003 accredits canonical relation composition, but not every historical design claim is automatically promoted.

### Finding A-012 — Referential graph, not recursive embedding

```text
Object A --relationship_ref--> R1
R1 --source_ref--> A
R1 --target_ref--> B
Object B --relationship_ref--> R1
```

### Finding A-013 — Relationship identity is independent [HISTORICAL DESIGN]
Relationship identity is not assumed to be merely `source + predicate + target`.

### Finding A-014 — Topology must be reconstructible
Later accredited tests confirm relation endpoint reconstruction for knowledge composition.

## 6. State evolution and version semantics findings

### Finding A-015 — Technical mechanisms must not define ontology
Snapshots, events and storage mechanisms are implementation mechanisms.

### Finding A-016 — Transition and event are different

```text
Event != Transition != State
```

### Finding A-017 — Snapshot is a materialized projection

```text
State Field
    ↓ observation boundary
Snapshot
    ↓ serialization
Persistent Representation
```

### Finding A-018 — Version space may require relational/non-linear semantics [HISTORICAL DESIGN]
A simple `previous_version` chain was identified as insufficient for divergence/convergence, but complete navigable branching lineage remains outside accredited KM-0001 scope so far.

### Finding A-019 — Conceptual separation required

```text
Identity
State
Manifestation
Version Relation
Transition
Event
Evidence
Snapshot
Serialization
Persistence
```

### Finding A-020 — Evolution graph hypothesis remains partially bounded
Explicit predecessor and lineage distinctions are accredited; complete general branching/convergence lineage remains unaccredited.

## 7. KM-0001 TST-0001 findings

### Finding A-021 — No second ontological root for knowledge [ACCREDITED]

```text
Knowledge Object
    = Canonical Object
    + knowledge semantic specialization / role
    + domain contracts
```

### Finding A-022 — Canonical identity survives representation versioning [ACCREDITED]

### Finding A-023 — Active repository and durable persistence are separate [ACCREDITED]
Observation does not implicitly hydrate from persistence.

### Finding A-024 — Relations and evidence reuse canonical capabilities [ACCREDITED]

### Finding A-025 — Identity, representation version and historical lineage are distinct [ACCREDITED BOUNDARY]

```text
stable canonical identity
        !=
representation version
        !=
persistent reconstructable historical lineage
```

Evidence: dedicated `8 PASS`; full regression `1110 PASS`.

## 8. KM-0001 TST-0002 transactional lifecycle findings

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

### Finding A-028 — Canonical identity survives transactional update [ACCREDITED]

### Finding A-029 — Optimistic concurrency protects persisted knowledge [ACCREDITED]

### Finding A-030 — Operation identity provides idempotency, not knowledge identity [ACCREDITED]

### Finding A-031 — Temporal relation does not imply lineage [ACCREDITED NON-REGRESSION]

### Finding A-032 — `previous_version` is explicit predecessor, not complete lineage [ACCREDITED BOUNDARY]

```text
preserved previous_version
        !=
complete historical revision store
```

Evidence: dedicated `10 PASS`; full regression `1120 PASS`; tested commit `9e3d3863010df6ea671bfaaae7cd6df9ae37114b`.

## 9. KM-0001 TST-0003 relations, evidence and provenance findings

### Finding A-033 — Knowledge relation/evidence composition reuses canonical capabilities [ACCREDITED]

```text
Knowledge Object = CanonicalObject with knowledge role
Knowledge Relation = canonical relation with knowledge semantics
Knowledge Evidence = inline Evidence OR CanonicalObject with evidence role/type
Knowledge Provenance = evidence provenance OR derived projection provenance
```

### Finding A-034 — Relation, evidence, provenance and lineage are independent [ACCREDITED]

```text
relation != evidence != provenance != lineage
```

### Finding A-035 — Evidence can be inline or independently canonical [ACCREDITED]

### Finding A-036 — Shared canonical evidence must not be duplicated structurally [ACCREDITED]

### Finding A-037 — Evidence identity, reference and inline content are different [ACCREDITED]

### Finding A-038 — Evidence provenance can be persistent semantic information [ACCREDITED]

### Finding A-039 — Projection provenance remains derived [ACCREDITED BOUNDARY]
It does not implicitly become canonical identity, knowledge object, persistent evidence, semantic relation or lineage edge.

### Finding A-040 — Provenance does not confer canonical authority [DERIVED KCA CONSEQUENCE]

```text
provenance present != source authoritative != receiver canonical != claim true
```

### Finding A-041 — Canonical relations survive persistence and endpoint reconstruction [ACCREDITED]

### Finding A-042 — Temporal relation remains distinct from lineage [ACCREDITED NON-REGRESSION]

Evidence: dedicated `10 PASS`; full regression `1130 PASS`; tested commit `987151ee49a948a1b275a50a04844f5aeb8fcd7b`.

## 10. KM-0001 TST-0004 Persistent Cognitive State observation findings

Recovered branch: `engineering/KM-0001-TST-0004-persistent-cognitive-state-observation`.

The branch is seven commits ahead of TST-0003 and contains design, inspection, integral inspection, formal closure, dedicated tests and reproducible evidence.

Actual accredited increment: **Observación y proyección del Estado Cognitivo Persistente**.

### Finding A-043 — Persistent Cognitive State observation is emergent, not a second root ontology [ACCREDITED]

TST-0004 confirms, for its scope, that no autonomous `PersistentCognitiveState` root class is required.

The accredited chain is:

```text
persist
  ↓
reconstruct
  ↓
observe
  ↓
select
  ↓
project
  ↓
provenance
```

A cognitive view can emerge from composition over the reconstructed canonical graph without creating another persistent state ontology.

KCA consequence: KSCL should model communicated cognitive state as a representation/projection contract, not as a mandatory new ontological root that replaces the source information model.

### Finding A-044 — Persisted, active/observed, selected and projected state are distinct [ACCREDITED]

```text
persisted state
    !=
active / observed state
    !=
contextual selection
    !=
derived projection
```

These layers compose without collapsing responsibilities.

KCA consequence: a communicated state representation needs to declare what layer it represents. A receiver must not infer `persisted`, `complete` or `canonical` merely from receipt.

### Finding A-045 — Observation is non-mutating [ACCREDITED]

Persistent knowledge can be observed without mutating source knowledge or the persistent registry.

```text
OBSERVE(source)
       ↓
derived observation
       X
source mutation
```

This strengthens KCA-INV-12: observation/receipt is not hydration and is also not source mutation.

### Finding A-046 — Context selection operates on canonical references/identities [ACCREDITED]

Contextual selection operates over references/identities rather than by mutating source state.

KCA consequence: selection semantics should be representable as boundary/reference semantics, not by manufacturing altered source objects merely to indicate inclusion.

### Finding A-047 — Derived projection is immutable [ACCREDITED]

The TST-0004 family accredits immutability of the derived projection.

KCA consequence: a transmitted projection should be treated as an immutable observation artifact for that observation event/boundary. A later changed view should be another projection/representation, not silent mutation of the already identified observation artifact.

### Finding A-048 — Projection provenance preserves source identities [ACCREDITED]

Projection provenance retains source object IDs.

This creates a strong KSCL requirement:

```text
Projection
├── projected content / references
└── provenance
      └── source_object_ids[]
```

The exact neutral KCA schema remains undecided, but source traceability must survive projection and communication when available.

### Finding A-049 — Observation preserves relevant evidence and relation context [ACCREDITED]

The observed state retains evidence and relevant relationship context.

KCA consequence: a state projection intended for meaningful reconstruction cannot be reduced blindly to isolated object payloads. Its evidential/relational context may be semantically required.

### Finding A-050 — Contextual projection excludes unrelated objects [ACCREDITED]

A projection can select a coherent subject-related set while excluding unrelated canonical objects.

Therefore:

```text
projection completeness
    !=
global state completeness
```

A projection may be internally coherent for its declared context while intentionally incomplete relative to the global persistent graph.

This is a precursor to the Observation Boundary contract.

### Finding A-051 — Active state may differ from persisted state without semantic conflict [ACCREDITED]

TST-0004 explicitly accredits separation between active/observed and persisted state.

KCA consequence: freshness/state-layer metadata will likely be required in the neutral model. A receiver cannot safely interpret an observed active view as the persisted authoritative snapshot unless that status is explicitly asserted by the source binding.

### Finding A-052 — Projection provenance is not source evidence [ACCREDITED]

```text
projection provenance
        !=
source knowledge evidence
```

This extends TST-0003: source IDs and derivation information explain how a projection was formed but do not automatically justify the truth of the source knowledge.

### Finding A-053 — Projection does not create lineage [ACCREDITED]

```text
observe/select/project
        !=
knowledge lineage creation
```

Neither observation nor projection creates an implicit semantic revision edge.

### Finding A-054 — Explicit state-evolution lineage can be reconstructed in observation [ACCREDITED WITH SCOPE]

The dedicated family accredits reconstruction of explicit state-evolution lineage for the observed subject/manifestations while retaining the non-regression rule that generic temporal relations do not create lineage.

This means KCA may carry explicit lineage context present in a projection, but must not infer missing lineage from observation order or timestamps.

### Finding A-055 — No dedicated observation adapter is yet architecturally required [ACCREDITED BOUNDARY]

No public `CanonicalObject -> StateObservation` API was identified. TST-0004 demonstrates that composition can occur explicitly in the integration layer without identity loss or mutation.

A future adapter is justified only if multiple consumers require a common contract and real semantic duplication appears.

KCA implication: KCA itself may become one such consumer pressure, but the KOS binding should be designed from the neutral contract rather than prematurely changing KOS production APIs.

### Evidence accreditation — TST-0004

Dedicated family:

```text
tests/test_persistent_cognitive_state_observation.py
10 PASS / 0 FAIL / 0 ERROR
```

It accredits:

- non-mutating persistent knowledge observation;
- contextual selection on canonical references;
- immutable derived projection;
- source IDs preserved in projection provenance;
- evidence/relation context preserved during observation;
- explicit state-evolution lineage reconstruction;
- exclusion of unrelated objects;
- active/observed versus persisted state separation;
- no registry mutation after persistence/reconstruction/projection;
- no implicit lineage from observation/projection.

Full regression:

```text
1140 observed
1140 PASS
0 FAIL
0 ERR
Return code: 0
Verification errors: none
```

Tested commit: `89f5f6837c0c67eebf53c3b2bd68da532fc37e5a`.

Production impact:

```text
Changes in src/: 0
New PersistentCognitiveState root class: 0
New cognitive repository: 0
Projection-owned persistence: 0
```

## 11. Initial KCA compatibility invariants

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
KCA semantics must not depend on JSON, CBOR, Protobuf, database, Git or carrier.

### KCA-INV-08 — References preserve graph semantics
When identity exists, KCA should support reference-based graph reconstruction without recursive duplication.

### KCA-INV-09 — Provenance and evidence remain distinguishable

### KCA-INV-10 — Snapshot is bounded representation

### KCA-INV-11 — Knowledge communication must not create a second KOS ontology

### KCA-INV-12 — Observation is not hydration or mutation
Receiving/observing a remote representation must not implicitly hydrate durable knowledge or mutate source/persisted state.

### KCA-INV-13 — Identity, representation revision and lineage are independent dimensions

### KCA-INV-14 — Transaction identity is not semantic identity

### KCA-INV-15 — Transport/order metadata does not imply lineage

### KCA-INV-16 — Partial lineage remains partial

### KCA-INV-17 — Persistence conflict semantics are independent from transport delivery

### KCA-INV-18 — Relation, evidence, provenance and lineage are independent semantic roles

### KCA-INV-19 — Evidence may be inline or referenced

### KCA-INV-20 — Shared identity-bearing evidence is referenceable, not duplicative

### KCA-INV-21 — Provenance does not confer authority

### KCA-INV-22 — Projection provenance remains projection provenance

### KCA-INV-23 — State layer must remain explicit
Persisted state, active/observed state, contextual selection and derived projection must not be collapsed into one undifferentiated communicated state.

### KCA-INV-24 — Projection completeness is boundary-relative
A projection may be complete/coherent for its declared context while incomplete relative to the global persistent state.

### KCA-INV-25 — Projection source traceability must survive when available
A derived projection should preserve references/identities of source objects needed to explain its derivation.

### KCA-INV-26 — Projection does not create source semantics
Selecting or projecting source objects does not create source evidence, canonical authority, persistence or lineage.

### KCA-INV-27 — Observation artifacts are immutable representations
An identified observation/projection represents a bounded result. Later state changes should produce another representation rather than retroactively alter the semantics of the earlier observation.

## 12. Emerging KCA/KSCL state communication model

TST-0004 makes the future separation increasingly clear:

```text
Persistent Canonical Graph
        │
        │ reconstruct
        ▼
Observable State
        │
        │ select(context / refs)
        ▼
Observation Boundary
        │
        │ project
        ▼
Immutable Cognitive Projection
        │
        ├── source references
        ├── relevant relations
        ├── relevant evidence
        └── projection provenance
        │
        │ encode / communicate
        ▼
KSCL Representation
```

This is not yet a final protocol/schema. It is the accredited semantic decomposition that the neutral KCA model must be able to preserve.

The key distinction is now:

```text
WHAT EXISTS
      !=
WHAT IS PERSISTED
      !=
WHAT IS ACTIVE / OBSERVED
      !=
WHAT IS SELECTED
      !=
WHAT IS PROJECTED
      !=
WHAT IS ENCODED
      !=
WHAT IS TRANSMITTED
      !=
WHAT THE RECEIVER IMPORTS
```

## 13. Decoupling implication

```text
KOS Canonical Model
        ↓
KOS Observation / Binding Composition
        ↓
KOS ↔ KCA Binding
        ↓
KCA Neutral Information Model
        ↓
KEncoding / KCP / KSCL
```

A non-KOS system may expose equivalent state/identity/evidence/provenance/boundary semantics without implementing `CanonicalObject`.

A KOS binding must preserve the accredited distinctions rather than leak implementation classes into the neutral protocol.

## 14. Evidence status

Accredited through TST-0004 now includes:

- canonical knowledge specialization;
- stable canonical identity;
- semantic version / transactional revision / operation identity separation;
- explicit predecessor preservation;
- repository/persistence separation;
- non-hydrating and non-mutating observation;
- canonical relations;
- inline and referenced evidence;
- shared canonical evidence;
- evidence provenance;
- projection provenance separation;
- Persistent Cognitive State observation as emergent composition;
- persisted / active-observed / contextual selection / projection separation;
- immutable derived projection;
- projection source-ID traceability;
- preservation of relevant evidence/relation context;
- contextual exclusion of unrelated objects;
- explicit observed state-evolution lineage reconstruction;
- no implicit lineage from temporal relation or projection.

Still unresolved or requiring further accreditation/analysis:

- complete navigable historical revision store;
- general branching/convergence lineage ontology;
- full final status of historical first-class relationship design claims;
- formal Observation Boundary contract as a separately identified increment/artifact;
- receiver-side import/promotion/authority policy;
- neutral KCA information schema;
- KSCL reconstruction/completeness levels.

## 15. Next investigation

1. Resolve whether `engineering/KM-0001-TST-0005-observation-boundary` exists as a historical branch/artifact or whether the program moved directly to integral inspection/closure after TST-0004.
2. If TST-0005 exists, recover and accredit its Observation Boundary semantics.
3. If it does not, inspect `engineering/KM-0001-INTEGRAL-INSPECTION-2026-07-20.es.md` and later KM-0001 program closure to determine the actual terminal boundary.
4. Build the formal KOS Information Object Taxonomy.
5. Build the Authority / Ownership / Derivation Matrix.
6. Derive the first neutral KCA information model only after the program boundary is verified.
