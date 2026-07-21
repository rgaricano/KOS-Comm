# KSCL Completeness and Reconstruction Profiles

**Status:** Phase A synthesis / pre-protocol  
**Date:** 2026-07-21

## 1. Principle

Completeness is relative to a declared semantic boundary. No received structure is globally complete merely because it is syntactically complete.

## 2. Profiles

### KCR-0 — Reference Only
Contains resolvable or opaque source references only.

Guarantee: identity/reference communication.  
Does not guarantee: state, evidence, relations, projection reconstruction or canonical reconstruction.

### KCR-1 — Observation
Contains observed state sufficient to reproduce the declared observation payload.

Typical KOS binding: `StateObservation` semantics.

Guarantee: observation-level interpretation.  
Does not guarantee: complete CanonicalObject reconstruction.

### KCR-2 — Context-Coherent Observation Set
Contains observations plus a declared contextual boundary/selection sufficient to interpret why the set belongs together.

Guarantee: context-relative coherence.  
Does not guarantee: global graph completeness.

### KCR-3 — Projection-Reconstructible
Contains the projection payload plus source references, boundary descriptor and projection provenance sufficient to reconstruct the communicated projection semantics.

Guarantee: reconstruction of the projection as a derived artifact.  
Does not guarantee: source canonical reconstruction.

### KCR-4 — Semantic Graph Package
Contains the declared object/reference set plus required semantic relations and evidence/provenance references for the declared boundary.

Guarantee: reconstruction of the communicated semantic subgraph to the declared scope.  
Does not guarantee: complete source persistence/history.

### KCR-5 — Evidence-Resolved Semantic Package
KCR-4 plus required inline/referenced evidence resolved to the declared evidence completeness policy.

Guarantee: evidence-bearing semantic reconstruction for the declared boundary.  
Does not imply: truth, authority or canonical import.

### KCR-6 — Canonical-Reconstruction Candidate
Contains sufficient source canonical identity/state/version/relation/evidence/provenance information for a compatible binding to reconstruct a candidate canonical representation.

Guarantee: structural/semantic reconstruction candidate.  
Does not imply: receiver acceptance, persistence or authority.

### KCR-7 — Canonical-Transfer Package
KCR-6 plus explicit transfer intent, authority assertion, source/binding contract and receiver-policy prerequisites needed for an explicit import decision.

Guarantee: package is eligible for receiver import evaluation.  
Does not imply: automatic import.

## 3. Monotonicity warning

Profiles describe capabilities, not universal subtype inheritance. A higher profile normally carries stronger reconstruction semantics, but domain/binding rules may make two packages incomparable.

## 4. Required declaration

Every KSCL information unit should declare or make derivable:

```text
semantic_class
completeness_profile
boundary_id / boundary descriptor
source/binding identity where applicable
```

## 5. Receiver rule

```text
received profile
    ↓
validate declared guarantees
    ↓
resolve references as required
    ↓
apply receiver policy
    ↓
observe / project / store / import / reject
```

No profile bypasses receiver policy.
