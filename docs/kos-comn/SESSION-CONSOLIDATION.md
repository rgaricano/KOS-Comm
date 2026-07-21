# KOS-Comn — Session Consolidation

## Checkpoint

**Date:** 2026-07-21

## Context reconstructed

The work concerns the information and communications subsystem of KOS, originally centered on KCP and KSCL.

The active laboratory is isolated in:

- repository: `rgaricano/KOS-Lab`
- branch: `KOS-Comn`
- base: `dev`

The branch exists because the GitHub connector available in this session resolves `KOS-Lab` but not the separate `KOS-Lab_KCP` repository.

## Operational incident rule

Issue #5 is mandatory operational guidance for GitHub connector ambiguity.

```text
AMBIGUOUS CONNECTOR RESPONSE != NO REPOSITORY MUTATION
SEARCH INDEX MISS != BRANCH ABSENCE
WRITE RETRY REQUIRES STATE VERIFICATION
```

Direct ref reads and `compare_commits` are used to verify state before retrying ambiguous writes.

## Architectural result of this session

The communication problem has been reframed from two isolated concepts (KCP and KSCL) into **KCA — Knowledge Communication Architecture**.

```text
Persistence / Canonical Knowledge
            ↓
KRM — Knowledge Representation Model
            ↓
KEncoding — Knowledge Encoding
            ↓
KCP — Knowledge Communication Protocol
            ↓
KSCL — Knowledge Session Continuity Layer
            ↓
CP — Cognitive Projection
            ↓
Consumers
```

## Decisions

1. KCA is the architecture of reference for the KOS-Comn laboratory.
2. KCP is one layer of KCA, not the complete communication subsystem.
3. KSCL is treated as a continuity/reconstruction layer; its final representation remains open.
4. KRM must be defined before closing encoding and protocol structures.
5. KRM must map to existing KOS canonical concepts rather than silently creating a second incompatible knowledge model.
6. CP remains a derived projection boundary and does not gain canonical authority.
7. Data-plane and control-plane separation must be developed explicitly.
8. Repository persistence is mandatory after significant architectural work.

## Persisted documents

- `README.md`
- `docs/kos-comn/DEVELOPMENT-STATE.md`
- `docs/kos-comn/architecture/KCA.md`
- `docs/kos-comn/adr/ADR-0001-KCA.md`
- `docs/kos-comn/SESSION-CONSOLIDATION.md`

## Open engineering questions

- What is the minimum KRM semantic unit?
- Which KOS canonical objects can be communicated directly and which require observations/derived representations?
- How are identity, provenance, evidence and authority encoded across boundaries?
- What is the exact definition of a KEU?
- Which reliability semantics belong to KCP and which belong to underlying transports?
- What is a session in KCA terms?
- What state is necessary and sufficient for deterministic continuity?
- Which KSCL concepts remain useful from the existing approach?
- How are capability/version negotiations represented?
- How should control-plane messages be separated from knowledge-bearing data-plane units?

## Next entry point

Begin **KRM — Knowledge Representation Model**.

The first KRM task is not to invent a new taxonomy. It is to inventory and map the existing KOS concepts relevant to communication:

1. canonical knowledge objects;
2. identity;
3. relations;
4. evidence and provenance;
5. persistent cognitive state;
6. observations;
7. projections;
8. contextual derived views;
9. execution operational identities/results.

From that inventory, define which concepts belong in the KRM communication model and which must remain external references or derived views.
