# KOS-Comn Baseline 1.0

**Repository:** `rgaricano/KOS-Lab`  
**Branch:** `KOS-Comn`  
**Status:** FROZEN  
**Purpose:** provide a stable baseline for eventual repository disambiguation and future extraction into a dedicated KOS-Comm repository.

## Scope frozen in this baseline

This baseline freezes the current KOS-Comn laboratory direction as documented in the branch checkpoint artifacts:

- `README.md`
- `docs/kos-comn/DEVELOPMENT-STATE.md`
- `docs/kos-comn/SESSION-CONSOLIDATION.md`
- `docs/kos-comn/architecture/KCA.md`
- `docs/kos-comn/adr/ADR-0001-KCA.md`

## Consolidated architectural position

KOS-Comn is a laboratory branch dedicated to the replanning of the KOS information and communications subsystem under **KCA — Knowledge Communication Architecture**.

The architecture is organized as:

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

## Consolidated decisions

1. KCA is the superior architectural frame of the KOS-Comn work.
2. KCP is one layer of KCA, not the whole subsystem.
3. KSCL is treated as a continuity and reconstruction layer.
4. Representation, encoding, communication, continuity, and projection remain separated by contract.
5. CP does not acquire canonical authority over the source knowledge.
6. KOS-Comn must remain traceable against canonical KOS boundaries and existing engineering artifacts.
7. Persistent repository state is mandatory for reentry and historical traceability.

## Frozen checkpoint state

This baseline freezes the branch as a reference point before any repository disambiguation or extraction work.

Any later move toward a dedicated repository must preserve this baseline as the historical origin of the extraction.

## Next step after baseline

1. Keep KOS-Comn as the historical KCA laboratory branch.
2. Create a dedicated repository for the extracted KOS-Comm work when the branch is ready.
3. Preserve this baseline as the first release reference for the new repository.
