# AR-1 — Boundary Model Closure Review

**Status:** CLOSED — PASS  
**Phase:** I — Boundary & Representation Foundation  
**Track:** KOS-Comm experimental (`KOS-Comn`)  
**Date:** 2026-07-21  
**Next:** AR-2 — Representation Model

## 1. Scope

This closure consolidates the normative outcome of:

- `AR-1-BOUNDARY-MODEL.es.md`;
- `AR-1-BOUNDARY-VALIDATION.es.md`;
- `AR-1-BOUNDARY-COMPOSITION.es.md`;
- `AR-1-CLOSURE.es.md`.

The English document is semantically equivalent to the Spanish closure baseline. It is not intended to introduce new normative content.

## 2. Closure result

```text
AR-1 — BOUNDARY MODEL
CLOSURE REVIEW: PASS
STATUS: CLOSED
CLOSURE CRITERIA: 7/7 PASS
```

No structural contradiction requires a second refinement cycle.

## 3. Consolidated boundary taxonomy

### 3.1 Domain Boundary

A change in architectural responsibility or ownership context.

It is not inferred from distance, host, process, network, transport or protocol.

```text
remote != domain change
local != same domain
process change != domain change
transport != domain change
```

### 3.2 Information Boundary

An explicit change in representation, informational form, or interpretation regime/context.

It may occur locally and without communication.

### 3.3 Communication Boundary

An exchange through a communication mechanism between participants, components, processes, nodes or systems.

It does not by itself imply domain change, representation change or authority transfer.

### 3.4 Authority Boundary

A point at which authority, legitimacy, decision capability or canonical incorporation must be explicitly evaluated.

Receipt, authenticity, integrity, trust, transport or reconstruction cannot replace this evaluation.

## 4. Compact model

```text
B = <D,I,C,A>
```

where D/I/C/A denote presence of Domain, Information, Communication and Authority Boundaries.

The vector is a compact summary, not the complete model.

Complex routes use:

```text
BoundaryPath = ordered BoundarySegment[]
```

## 5. BoundarySegment

```text
BoundarySegment {
    source_context
    destination_context
    boundary_state <D,I,C,A>
    property_transitions[]
    authority_boundaries[]
    scope
}
```

A segment exists when at least one D/I/C/A dimension contains an architecturally relevant transition or when a property transition must be explicitly retained.

Purely physical hops without architectural relevance need not appear in the logical model.

## 6. BoundaryPath

```text
BoundaryPath = ordered BoundarySegment[]
```

Continuity rule:

```text
segment[n].destination_context
    ==
segment[n+1].source_context
```

A global presence summary may be calculated with OR across segments, but it never replaces segment-level analysis.

## 7. Non-collapse rule

Segments must not be collapsed when doing so hides:

- an Authority Boundary;
- a semantic transformation;
- loss or degradation;
- a responsibility change;
- relevant preservation evidence;
- a hop-by-hop/end-to-end scope distinction.

## 8. PropertyTransition

Consolidated states:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DEGRADED
OMITTED
NOT_APPLICABLE
UNKNOWN
```

`UNKNOWN` means insufficient evidence and is neither known loss nor preservation.

A lossy transformation cannot later become preserved relative to the original unless an adequate independent source restores the lost information.

## 9. Scope

```text
HOP_BY_HOP
END_TO_END
LOCAL_TRANSFORMATION
```

A property guarantee must state the scope to which it applies.

## 10. Preservation and reconstruction

The following remain distinct:

```text
PRESERVATION
REINTRODUCTION
RECONSTRUCTION
DERIVATION
```

Invariant:

```text
reconstructed != preserved from source
```

Detailed reconstruction semantics belong to AR-4.

## 11. Authority

Authority does not propagate implicitly through a path.

```text
authorized at S1 != authorized at Sn
```

A path may contain multiple Authority Boundaries with different scope, subject, decision context and result.

## 12. Trust, authenticity and integrity

They are not additional boundary dimensions.

```text
trust != authority
authenticity != authority
integrity != authority
trust != authenticity
```

They may contribute evidence to a decision but do not create authority by themselves.

## 13. Normative non-inference rules

```text
C=1 does not imply D=1
C=1 does not imply I=1
C=1 does not imply A=1

I=1 does not imply C=1
I=1 does not imply D=1
I=1 does not imply A=1

D=1 does not imply C=1
D=1 does not imply I=1
D=1 does not imply A=1

A=1 does not imply D=1
A=1 does not imply I=1
A=1 does not imply C=1
```

Additionally:

```text
receipt != import
transmission != authority transfer
authenticity != authority
trust != authority
integrity != authority
reconstruction != preservation
reconstruction != authorization
projection != canonical object
observation != canonical serialization
technical compatibility != authority
```

## 14. D/I/C/A matrix

The sixteen Boolean combinations were reviewed.

`<0,0,0,0>` normally does not constitute an architecturally observable segment. The other combinations may be valid depending on context.

AR-1 therefore imposes evidence, context, segmentation and non-inference rules rather than a rigid allowed/forbidden combination table.

## 15. Neutrality

AR-1 passes the first conceptual neutrality test.

```text
Non-KOS System A
    ↓
Binding / Adapter A
    ↓
Neutral Representation
    ↓
Exchange
    ↓
Neutral Representation
    ↓
Binding / Adapter B
    ↓
Non-KOS System B
```

No internal KOS type is required as an ontological foundation.

This is not Gate C.5. Full neutrality still requires later experimental evidence.

## 16. Validation cases

```text
V1 Local Projection                         PASS
V2 Remote Observation                      PASS
V3 Remote Operational Result               PASS
V4 Feedback without automatic incorporation PASS
V5 Canonical Reference                     PASS
V6 Reconstruction without authority        PASS
V7 Non-KOS ↔ Non-KOS                       PASS conceptual
V8 Canonical Transfer Candidate            PASS through segmentation
V9 Relay/intermediaries                    PASS through BoundaryPath
```

## 17. AR-1 / AR-2 responsibility boundary

AR-1 owns:

- boundary types;
- segmentation;
- boundary paths;
- composition;
- property transition/preservation/loss;
- Authority Boundary presence/location;
- hop-by-hop and end-to-end scope;
- non-inference rules.

AR-1 does not own:

- internal Representation schema;
- definitive Representation taxonomy;
- serialization;
- physical encoding;
- grammar;
- codec;
- reconstruction algorithms;
- concrete Binding mappings.

AR-2 must define what a Representation is, which semantic invariants it carries, how identity/reference/provenance are expressed, how representation class is declared, and how property guarantees are represented.

## 18. Closure criteria

```text
C1 Four unambiguous boundary categories             PASS
C2 Composition model                                PASS
C3 Preservation/transformation/loss                 PASS
C4 Authority independent from receipt/communication/reconstruction PASS
C5 Initial validation cases modelable               PASS
C6 Non-KOS scenario without hidden KOS semantics    PASS conceptual
C7 AR-2 can build without redefining boundary       PASS
```

## 19. Deferred matters

- Representation internal structure/classes → AR-2;
- concrete domain-to-representation mappings → AR-3;
- reconstruction/fidelity semantics → AR-4;
- physical encoding → AR-6;
- protocol communication/transport guarantees → AR-7;
- full experimental neutrality → Gate C.5.

## 20. Bilingual documentation rule

KOS-Comm architecture documentation follows semantic bilingualism:

1. architecture documents shall progressively have equivalent ES/EN versions;
2. each language should use its natural technical terminology;
3. implementation identifiers, contract/type names and stabilized architectural proper names may remain untranslated;
4. first occurrence may show both forms where useful;
5. ES/EN versions require semantic equivalence, not literal translation;
6. normative divergence between versions is a documentation defect and must be reconciled.

## 21. Closure decision

```text
Boundary taxonomy:       STABLE
Domain semantics:        STABLE
<D,I,C,A>:               STABLE AS COMPACT SUMMARY
BoundarySegment:         STABLE CANDIDATE
BoundaryPath:            STABLE CANDIDATE
PropertyTransition:      STABLE CANDIDATE
Composition rules:       STABLE CANDIDATE
Non-inference rules:     NORMATIVE
Conceptual neutrality:   PASS
Closure criteria:        7/7 PASS

STATUS: CLOSED
```

Compatible refinements may be introduced when later evidence requires them. Any change breaking AR-1 invariants requires explicit reopening of AR-1.

## 22. Next

```text
AR-1 Boundary Model
    CLOSED / PASS
        ↓
AR-2 Representation Model
    NEXT
        ↓
AR-3 Binding Model
        ↓
GATE A
```
