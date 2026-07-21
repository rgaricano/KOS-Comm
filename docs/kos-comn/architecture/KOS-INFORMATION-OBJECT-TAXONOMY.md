# KOS Information Object Taxonomy — KCA Phase A

**Status:** Working architectural synthesis  
**Basis:** Accredited KOS contracts through KM-0001/TST-0005  
**Branch:** `KOS-Comn`  
**Date:** 2026-07-21

## 1. Purpose

Classify information-bearing entities and representations relevant to KCA without creating a second KOS ontology.

## 2. Taxonomy

### T1 — Canonical entities

#### T1.1 Canonical Object
Stable canonical identity plus state/version/relationship/evidence/metadata capabilities. Source authority remains with the owning system.

#### T1.2 Knowledge-role Canonical Object
A Canonical Object carrying a knowledge semantic role/specialization. It is not a second ontological root.

#### T1.3 Canonical Relationship
Identity-bearing semantic relation between canonical references. Relation semantics remain distinct from evidence, provenance and lineage.

#### T1.4 Canonical Evidence Object
Identity-bearing evidence represented as a Canonical Object with an evidence role/type. It may be shared by reference.

### T2 — Embedded semantic components

#### T2.1 Inline Evidence
Evidence embedded in a source representation without requiring independent canonical identity.

#### T2.2 Evidence Provenance
Origin/context associated with evidence. Provenance improves traceability but does not confer truth or authority.

#### T2.3 Semantic Version
Version semantics attached to the canonical representation. Distinct from canonical identity and transactional persistence revision.

#### T2.4 Explicit Predecessor / Lineage Reference
Explicit revision/evolution relation when present. Temporal order alone does not create lineage.

### T3 — Persistence and operational dimensions

#### T3.1 Persisted Representation
Durable representation of canonical state. Persistence is not ontology.

#### T3.2 Transactional Revision
Persistence-layer revision used for concurrency/publication control. It is not semantic version identity.

#### T3.3 Operation Identity
Idempotency/correlation identity of an operation. It is not canonical identity.

#### T3.4 Publication Result
Operational result of persistence/publication. It is not knowledge by default.

### T4 — Observation and cognition representations

#### T4.1 Persistent Cognitive State
Emergent/reconstructible state over the persistent canonical graph. It is not a second root entity.

#### T4.2 StateObservation
Public, non-owning, deterministic observation derived from canonical state. Current KOS contract exposes `object_id`, `kind`, `status` and observable state attributes. It is not complete CanonicalObject serialization.

#### T4.3 Context Selection
A selection over observed/canonical references for a declared context. Selection does not mutate source state.

#### T4.4 Cognitive Projection
Immutable derived representation built from selected/observed state. Projection remains derived and does not acquire canonical authority through derivation or transmission.

#### T4.5 Projection Provenance
Trace of source identities/derivation associated with a projection. It is not source evidence and does not create lineage.

#### T4.6 Consumer Context View
Consumer-facing contextual view derived from projection. It is not canonical knowledge by default.

### T5 — Communication representations

These are KCA semantic classes, not KOS canonical roots.

#### T5.1 Canonical Reference Representation
Communicable reference to source identity/type/version semantics without implying ownership or import.

#### T5.2 Observation Representation
Communicable representation of one or more observations, explicitly marked as observational rather than canonical transfer.

#### T5.3 Projection Representation
Communicable immutable projection plus declared boundary/provenance semantics.

#### T5.4 Evidence Representation
Inline evidence and/or references to canonical evidence, preserving the distinction.

#### T5.5 Relation Representation
Semantic relation representation with source/target references and relation identity when available.

#### T5.6 Provenance Representation
Evidence or projection provenance represented without authority promotion.

#### T5.7 Lineage Representation
Explicit lineage/predecessor information only. Must never be inferred solely from timestamps, packet order or transport sequence.

#### T5.8 Operation Representation
Communication/transaction operation metadata: exchange, correlation, idempotency or publication operation identity.

#### T5.9 Result Representation
Operational outcome representation. Receipt does not convert it into persistent knowledge.

## 3. Orthogonal dimensions

Every KCA information representation may need independent declarations for:

```text
semantic class
source identity
representation identity
semantic version
transactional revision
operation identity
state layer
boundary/completeness
provenance
authority assertion
persistence/import intent
```

These dimensions must not be collapsed into a single generic identifier or metadata map.

## 4. Fundamental exclusions

```text
StateObservation != CanonicalObject serialization
Projection != CanonicalObject
Provenance != Evidence
Evidence != Truth
Relation != Lineage
Temporal order != Lineage
Operation ID != Canonical ID
Transactional revision != Semantic version
Receipt != Import
Transmission != Authority transfer
```
