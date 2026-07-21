# KOS-Comm — Experimental KSCL Continuity

**Status:** EXPERIMENTAL / ACTIVE  
**Scope:** semantic continuity and reentry  
**Authority:** NOT architectural  
**Future review:** AR-5 — KSCL Decomposition

## Purpose

This directory materializes experimental `.kscl` records to preserve semantic continuity across sessions and support reentry after context loss.

Until AR-5, the format is operational and revisable.

```text
Git = authority for verifiable material state
AR documents = authority for closed architectural decisions
KSCL = experimental semantic continuity
```

## Structure

```text
continuity/
├── CURRENT.kscl
├── README.es.md
├── README.en.md
└── checkpoints/
    └── YYYY-MM-DD-<checkpoint>.kscl
```

`CURRENT.kscl` represents the current semantic reentry state.

Files under `checkpoints/` are historical snapshots of significant points and should not be rewritten except through explicit documentary correction.

## Rules

1. Verify Git before trusting recorded SHAs.
2. A KSCL record cannot revoke a closed AR decision.
3. `CURRENT.kscl` may evolve with the project.
4. Checkpoints must preserve enough context to reconstruct intent, decisions, evidence, uncertainties and next action.
5. The format may change before AR-5; incompatible changes must be documented.
6. `KSCL reconstruction != proof`.
7. `KSCL continuity != architectural authority`.
