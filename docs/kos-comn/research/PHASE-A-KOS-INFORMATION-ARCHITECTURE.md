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
A simple `previous_version` chain was identified as insufficient for divergence/convergence, but complete navigable branching lineage remains outside accredited KM-0001 scope.

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
Explicit predecessor and lineage distinctions are accredited; complete general branching/convergence lineage remains outside the closed KM-0001 contract.

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
preserved previous_version != complete historical revision store
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

### Finding A-043 — Persistent Cognitive State observation is emergent, not a second root ontology [ACCREDITED]

```text
persist -> reconstruct -> observe -> select -> project -> provenance
```

### Finding A-044 — Persisted, active/observed, selected and projected state are distinct [ACCREDITED]

```text
persisted state != active/observed state != contextual selection != derived projection
```

### Finding A-045 — Observation is non-mutating [ACCREDITED]

### Finding A-046 — Context selection operates on canonical references/identities [ACCREDITED]

### Finding A-047 — Derived projection is immutable [ACCREDITED]

### Finding A-048 — Projection provenance preserves source identities [ACCREDITED]

### Finding A-049 — Observation preserves relevant evidence and relation context [ACCREDITED]

### Finding A-050 — Contextual projection excludes unrelated objects [ACCREDITED]

```text
projection completeness != global-state completeness
```

### Finding A-051 — Active state may differ from persisted state without semantic conflict [ACCREDITED]

### Finding A-052 — Projection provenance is not source evidence [ACCREDITED]

### Finding A-053 — Projection does not create lineage [ACCREDITED]

### Finding A-054 — Explicit state-evolution lineage can be reconstructed in observation [ACCREDITED WITH SCOPE]

### Finding A-055 — TST-0004 exposed a remaining public-boundary debt [ACCREDITED HISTORICAL BOUNDARY]
TST-0004 proved integration-layer composition but did not yet formally expose a public observation API. Integral inspection correctly identified this as a contractual debt, later resolved by TST-0005.

Evidence: dedicated `10 PASS`; full regression `1140 PASS`; tested commit `89f5f6837c0c67eebf53c3b2bd68da532fc37e5a`.

## 11. KM-0001 TST-0005 Public Observation Boundary findings

Recovered branch: `engineering/KM-0001-TST-0005-observation-boundary`.

Direct ref comparison confirms it exists and is thirteen commits ahead of TST-0004. It contains the production observation adapter, dedicated tests/evidence, final integral inspection, formal KM-0001 closure in ES/EN, and persistence-map updates.

Actual accredited increment: **Frontera pública de observación del Estado Cognitivo Persistente**.

### Finding A-056 — A public non-owning observation boundary is required and now accredited [ACCREDITED]

TST-0005 resolves the distinction between “a consumer can construct an observation” and “the architecture formally exposes an observation boundary”.

Public API:

```text
observe_canonical_object(obj)
    -> StateObservation

observe_persistent_state(source)
    -> tuple[StateObservation, ...]
```

The implementation resides in `context/observation.py`.

### Finding A-057 — Observation boundary belongs to context, not canonical core [ACCREDITED]

Dependency direction:

```text
src.kos.canonical_object
        ^
        | consume
context.observation
        |
        v produce
context.selection.StateObservation
        |
        v
deterministic_select()
```

The canonical core does not depend on `context.selection`.

KCA consequence: the KOS↔KCA adapter/binding should consume canonical/public observation capabilities from outside the canonical core. Communication concerns must not be injected downward into canonical ontology.

### Finding A-058 — Observation preserves canonical identity and observable type [ACCREDITED]

The public adapter maps:

```text
CanonicalObject.identity.canonical_id -> StateObservation.object_id
CanonicalObject.identity.type         -> StateObservation.kind
```

This is a semantic projection of source identity, not creation of a new canonical identity.

### Finding A-059 — Observation output is deterministic [ACCREDITED]

`observe_persistent_state()` orders source objects by stable canonical identity and returns an immutable tuple of observations.

KCA consequence: deterministic observation is available before encoding/transport. KEncoding should preserve deterministic semantics and avoid introducing gratuitous nondeterminism when canonical ordering is relevant.

### Finding A-060 — Observation boundary performs no contextual selection [ACCREDITED]

The boundary observes; selection remains a downstream operation.

```text
Persistent canonical state
        ↓ observe
StateObservation[]
        ↓ select
Context selection
        ↓ project
Cognitive projection
```

This corrects any model that places selection inside the observation adapter.

### Finding A-061 — Observation boundary performs no persistence, projection or ownership [ACCREDITED]

It does not introduce:

```text
PersistentCognitiveState root
parallel cognitive repository
new persistence
commit
context selection
projection
own provenance
relations
implicit lineage
```

The boundary observes only.

### Finding A-062 — Observation equivalence survives persistence/reconstruction [ACCREDITED]

Observable semantics are equivalent after persistence and reconstruction.

KCA consequence: a KOS binding may use the public observation boundary against reconstructed state without changing the intended observable information contract.

### Finding A-063 — Observation is independent of ProjectionRequest, strategy and consumer [ACCREDITED]

The observation layer does not depend on a particular projection request or consumer.

This is a strong decoupling property for KCA: neutral communication can consume observation output without forcing the source to know the eventual projection/consumer policy at observation time.

### Finding A-064 — Observable state is deliberately narrower than the complete canonical object [ACCREDITED IMPLEMENTATION FACT]

Current public `StateObservation` construction exposes:

```text
object_id
kind
attributes:
    status
    state.attributes
```

It does not itself serialize the complete canonical object, evidence graph, relationships, version or persistence metadata.

Therefore:

```text
StateObservation != CanonicalObject serialization
```

KCA/KSCL consequence: the public observation boundary is a source for observable state, not automatically a complete state-transfer format. Rich reconstruction packages may need additional explicitly bound information channels/structures.

### Finding A-065 — Observation boundary is a semantic choke point [DERIVED KCA CONSEQUENCE]

For KOS integration, `context/observation.py` is now the accredited architectural boundary between persistent canonical state and contextual cognition.

KCA should preferentially bind at or above this boundary for observational/state-view communication, while canonical object transfer/import remains a distinct use case requiring explicit authority and persistence semantics.

### Evidence accreditation — TST-0005

Dedicated family:

```text
tests/test_persistent_state_observation_boundary.py
10 PASS / 0 FAIL / 0 ERROR
```

Full regression:

```text
1150 observed
1150 PASS
0 FAIL
0 ERR
Return code: 0
Verification errors: none
```

Tested commit: `ac62f5854772ea8a15c7e27d3d5b7ee29b847f9c`.

## 12. KM-0001 formal program closure

KM-0001 is **FORMALLY CLOSED / ACCREDITED**.

No essential architectural obligation remains that justifies opening TST-0006.

Consolidated architecture:

```text
Canonical Model
    |
    +-- semantic knowledge roles
    +-- canonical identity / version / state
    +-- canonical relationships
    +-- evidence / provenance
    +-- persistence / reconstruction
             |
             v
Persistent Cognitive State
(emergent / reconstructible canonical graph state)
             |
             v
Public Observation Boundary
             |
             v
StateObservation[]
             |
             v
Cognitive Projection
             |
             v
Consumer Context View
```

The closed program explicitly preserves:

```text
KNOWLEDGE MODEL != SECOND CANONICAL MODEL
PERSISTENCE != PROJECTION
OBSERVATION != PROPRIETARY COPY OF STATE
TEMPORAL RELATION != REVISION LINEAGE
PROJECTION != KNOWLEDGE MUTATION
CONSUMER VIEW != CANONICAL KNOWLEDGE
INFERENCE != UNIVERSAL ONTOLOGICAL ROOT
```

The next functional front is not further completion of Persistent Knowledge. It is the end-to-end integration between Persistent Knowledge and Cognitive Projection, which requires its own inspection/formulation/opening decision.

## 13. Initial KCA compatibility invariants

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

### KCA-INV-24 — Projection completeness is boundary-relative

### KCA-INV-25 — Projection source traceability must survive when available

### KCA-INV-26 — Projection does not create source semantics

### KCA-INV-27 — Observation artifacts are immutable representations

### KCA-INV-28 — Observation and selection are separate protocol semantics
A source may expose observable state without selecting a consumer context. KCA/KSCL must not make observation inherently consumer-specific.

### KCA-INV-29 — Observation is not canonical serialization
`StateObservation` is an observable state projection and must not be interpreted as a lossless serialization of `CanonicalObject`.

### KCA-INV-30 — Binding direction must preserve canonical-core independence
KOS communication integration must depend on canonical/context public contracts; the canonical core must not depend on KCA/KCP/KSCL.

### KCA-INV-31 — Deterministic source observation should remain deterministically representable
Where the source observation contract provides stable ordering and deterministic output, encoding/transport layers should not destroy that property without explicit reason.

## 14. Emerging KCA/KSCL state communication model

The corrected accredited sequence is:

```text
Persistent Canonical Graph
        │
        │ persistence / reconstruction
        ▼
Public Observation Boundary
        │
        │ observe only
        ▼
StateObservation[]
        │
        │ contextual selection
        ▼
Selected Observation Set
        │
        │ cognitive projection
        ▼
Immutable Cognitive Projection
        │
        ├── source references
        ├── relevant relations/evidence where projection contract requires them
        └── projection provenance
        │
        │ KOS ↔ KCA binding
        ▼
KCA Neutral Information Representation
        │
        │ KEncoding
        ▼
KSCL / KCP communication structures
```

Important correction from the TST-0004-only reconstruction:

```text
OBSERVATION BOUNDARY
        precedes
CONTEXTUAL SELECTION
```

The boundary itself does not select or project.

Global semantic distinction:

```text
WHAT EXISTS
      !=
WHAT IS PERSISTED
      !=
WHAT IS OBSERVABLE
      !=
WHAT IS OBSERVED
      !=
WHAT IS SELECTED
      !=
WHAT IS PROJECTED
      !=
WHAT IS ENCODED
      !=
WHAT IS TRANSMITTED
      !=
WHAT THE RECEIVER ACCEPTS / IMPORTS
```

## 15. Decoupling implication

```text
KOS Canonical Model
        ↓
KOS Public Observation Boundary / Canonical APIs
        ↓
KOS ↔ KCA Binding
        ↓
KCA Neutral Information Model
        ↓
KEncoding
        ↓
KCP / KSCL
```

For observational communication, KCA should bind at or above the public observation boundary.

For canonical state transfer/import, a separate explicit binding contract is required because observation output is intentionally not a complete canonical serialization and receipt does not confer persistence or authority.

A non-KOS system remains free to expose equivalent neutral semantics without implementing `CanonicalObject` or `StateObservation` internally.

## 16. Evidence status after KM-0001 closure

Accredited:

- canonical knowledge specialization;
- stable canonical identity;
- semantic version / transactional revision / operation identity separation;
- persistent transactional lifecycle and idempotency;
- persistence/reconstruction;
- canonical relations;
- temporal relation / lineage separation;
- inline and referenced evidence;
- evidence provenance and traceability;
- projection provenance separation;
- Persistent Cognitive State as emergent/reconstructible canonical graph state;
- persisted / observed / selected / projected state separation;
- non-mutating observation;
- immutable derived projection;
- source traceability in projection;
- public non-owning observation boundary;
- deterministic observation output;
- observation/selection separation;
- observation independence from projection request/strategy/consumer;
- observable semantic equivalence after persistence/reconstruction;
- canonical-core independence from context observation layer.

Outside the closed KM-0001 contract / future work:

- complete general historical revision store and full branching/convergence lineage ontology;
- receiver-side import/promotion/authority policy;
- neutral KCA information schema;
- KSCL completeness/reconstruction profiles;
- communication encoding and transport semantics;
- end-to-end Knowledge ↔ Projection integration program beyond the now-accredited boundary.

## 17. Phase A decision point

The KM-0001 historical reconstruction is now sufficiently closed for KCA purposes.

Next work should stop extending the KM-0001 chronology unless a contradiction is discovered and move to synthesis:

1. Build **KOS Information Object Taxonomy** from accredited contracts.
2. Build **Authority / Ownership / Derivation Matrix**.
3. Define **Communication Semantic Classes**: observation, projection, canonical-reference, evidence, relation, provenance, lineage, operation, publication-result.
4. Define **KSCL completeness/reconstruction levels** without conflating observation with canonical serialization.
5. Derive the first **KCA Neutral Information Model**.
6. Only then specify KEncoding and KCP wire/transport behavior.
