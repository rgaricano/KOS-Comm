# KOS-Comm — Reentry and Continuity Guide

**Status:** ACTIVE / OPERATIONAL  
**Working track:** `KOS-Comn`  
**Objective:** reconstruct sufficient, verifiable and semantically coherent context before continuing KOS-Comm development.

## 1. Principle

The operational source of truth is the repository and its verifiable Git state.

Conversation supports development but does not replace persistent documentation.

```text
CONVERSATION
    ↓ consolidation
PERSISTED DOCUMENTATION
    ↓ verification
GIT
    ↓ interpretation
RECONSTRUCTED CONTEXT
```

## 2. Reentry sequence

```text
README / entry point
        ↓
DEVELOPMENT-STATE
        ↓
REENTRY-CHECKPOINT
        ↓
latest session consolidation / KSCL continuity
        ↓
Git verification
        ↓
KOS-Lab ↔ KOS-Comm charter when bilateral boundaries are relevant
        ↓
active architecture document
        ↓
applicable evidence / closures
        ↓
explicit state and next-action declaration
        ↓
development
        ↓
result recording and persistence
```

Missing continuity artifacts must be recorded as continuity debt rather than silently assumed.

## 3. Mandatory Git verification

Before modifying:

- confirm repository `rgaricano/KOS-Lab`;
- confirm branch `KOS-Comn`;
- obtain actual HEAD;
- check divergence against the applicable reference point;
- verify cited documents actually exist on the branch;
- never infer existence or state from conversational memory.

```text
DOCUMENTED STATE != VERIFIED GIT STATE
```

For ambiguous remote results:

```text
AMBIGUOUS REMOTE RESULT
        ↓
DO NOT RETRY BLINDLY
        ↓
QUERY REMOTE STATE
        ↓
VERIFY WHETHER CHANGE EXISTS
        ↓
RECOVER SHA / IDENTITY
        ↓
CREATE / UPDATE / ABORT
```

## 4. Authority layers during reentry

```text
Actual Git
    = existence, branch, HEAD, history and materialization

Collaboration charter
    = KOS-Lab ↔ KOS-Comm boundaries

AR closures / stabilized decisions
    = accredited architectural invariants

Active AR document
    = current hypotheses and work

Evidence
    = accredited validation results

Session consolidation / KSCL
    = semantic continuity and intention reconstruction
```

A session consolidation cannot by itself revoke a closed architectural decision.

## 5. Semantic continuity through KSCL

Until AR-5 determines the definitive KSCL decomposition, KOS-Comm uses KSCL as an experimental semantic-continuity mechanism, not as architectural authority.

Its reentry role is to preserve:

- session intent;
- decisions;
- open hypotheses;
- concept relationships;
- modified artifacts;
- obtained evidence;
- pending uncertainty;
- declared next action.

```text
KSCL continuity != architectural authority
KSCL record != Git verification
KSCL reconstruction != proof
```

## 6. Minimum KSCL continuity record

```text
SessionContinuity {
    session_or_checkpoint_id
    repository
    branch
    verified_head
    architectural_phase
    active_work_item
    closed_items[]
    active_hypotheses[]
    decisions[]
    invariants[]
    evidence[]
    modified_artifacts[]
    unresolved_questions[]
    next_action
}
```

This is an operational experimental structure and does not prejudge the definitive KSCL architecture to be investigated in AR-5.

## 7. Current expected state

```text
KOS-Lab ↔ KOS-Comm reconciliation
    CLOSED

Gate 0
    PASS

KOS-Lab
    AUTHORITATIVE / INDEPENDENT

KOS-Comm
    EXPERIMENTAL / AUTONOMOUS

Coupling
    EXPLICIT BINDINGS

AR-1 — Boundary Model
    CLOSED / PASS

AR-2 — Representation Model
    ACTIVE

AR-3 — Binding Model
    PENDING

Gate A
    PENDING
```

## 8. Context-loss-resistant invariants

```text
KOS-Lab authority is preserved
KOS-Comm autonomy is preserved
Binding is the bilateral seam
KCA must remain neutral
KCP must remain small and replaceable
KSCL is not frozen as a single layer
receipt != canonical import
communication != authority
representation != represented object
representation != authority
reconstruction != authorization
promotion to KOS-Lab requires evidence + governance
```

## 9. AR-2 reentry

If AR-2 remains active, read:

1. `docs/kos-comn/architecture/AR-1-CLOSURE.en.md`;
2. `docs/kos-comn/architecture/AR-2-REPRESENTATION-MODEL.en.md`;
3. corresponding Spanish versions when bilingual equivalence must be checked;
4. any later AR-2 validation documents;
5. latest session consolidation.

Current expected next action:

```text
AR-2
    ↓
first validation pass
    ↓
taxonomy and semantic-capability refinement
```

## 10. Mandatory declaration before continuing

A new session must be able to state:

```text
Verified repository:
Verified branch:
Verified HEAD:
Last closed item:
Active item:
Applicable invariants:
Working document:
Open uncertainties:
Next action:
```

Otherwise context reconstruction is incomplete.

## 11. Session close / checkpoint

Before leaving a session that produced relevant changes:

1. persist documents/results;
2. recover and record relevant commit SHAs;
3. perform a subsequent remote read or comparison;
4. update development state/checkpoint when the phase changes;
5. produce semantic session consolidation when contextual loss is a material risk;
6. record the next action.

## 12. Bilingual rule

The reentry guide must exist in semantically equivalent ES/EN versions.

KSCL records may use a primary language, but technical identifiers, states and invariants must remain unambiguous across languages.

## 13. Expected result

```text
REENTRY
  ↓
VERIFY
  ↓
RECONSTRUCT
  ↓
RECONCILE
  ↓
DECLARE STATE
  ↓
CONTINUE
  ↓
PERSIST
```

Reentry does not attempt to recover a lost conversation literally. It reconstructs a sufficient, traceable and verifiable engineering state so work can continue without external memory.