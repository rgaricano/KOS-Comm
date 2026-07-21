# AR-2 — Representation Model

**Status:** ACTIVE — INITIAL MODEL  
**Phase:** I — Boundary & Representation Foundation  
**Track:** KOS-Comm experimental (`KOS-Comn`)  
**Dependency:** AR-1 CLOSED / PASS  
**Next after AR-2:** AR-3 — Binding Model

## 1. Purpose

AR-2 defines what an informational Representation is within KCA and which minimum semantic capabilities it must provide to cross AR-1 boundaries without implicitly importing the internal semantics of source or destination systems.

It must answer:

```text
What is a Representation?
What does it represent?
Under which context is it interpreted?
Which identity/references does it preserve?
Which provenance does it declare?
Which properties does it guarantee?
Which information does it lose or transform?
Which authority must NOT be inferred from it?
```

## 2. Fundamental principle

```text
Representation != Represented Object
Representation != Canonical Object
Representation != Authority
Representation != Authorization
Representation != Truth
Representation != Complete Knowledge
```

A Representation is an interpretable informational construction expressing, referencing, projecting, describing or carrying selected aspects of a referent under declared semantics.

## 3. Referent, Representation and Encoded Form

```text
REFERENT
    ↓ representation
SEMANTIC REPRESENTATION
    ↓ encoding (AR-6)
ENCODED FORM
```

The referent may be an object, state, event, relation, result, observation, proposal or another semantically identifiable entity.

Representation belongs to AR-2. Encoded form primarily belongs to AR-6.

The same Representation may have multiple encodings, and the same encoding technology may encode multiple Representation classes.

## 4. Initial RepresentationEnvelope hypothesis

```text
RepresentationEnvelope {
    representation_identity
    representation_class
    subject
    semantic_context
    provenance
    references[]
    properties[]
    content
}
```

This is conceptual and does not imply a mandatory physical envelope.

## 5. Representation identity

```text
representation_identity != subject_identity
```

Different Representations may describe the same subject while retaining distinct identities for traceability, revision, comparison and provenance.

## 6. Subject

A Representation must be able to declare its subject when applicable through direct identity, reference, reference set, scope descriptor or an anonymous/unidentified subject where required.

AR-2 does not assume subjects are canonical objects.

## 7. Representation class

`representation_class` describes semantic function rather than physical encoding.

Initial research taxonomy:

```text
REFERENCE
OBSERVATION
STATE
EVENT
RESULT
PROJECTION
DESCRIPTION
PROPOSAL
EVIDENCE
TRANSFER_CANDIDATE
COMPOSITE
```

This taxonomy is not yet stabilized and must be tested for neutrality.

## 8. Semantic context

A Representation requires sufficient semantic context for correct interpretation.

Potential context includes vocabulary/ontology, semantic-model version, interpretation domain, units, conventions, temporal scope and constraints.

AR-2 must not make a KOS ontology a mandatory hidden dependency.

## 9. Provenance

Initial hypothesis:

```text
Provenance {
    source
    creation_context
    creation_time_or_order
    derivation[]
    previous_representation?
}
```

```text
known provenance != authority
trusted provenance != authority
```

## 10. References

A Representation may reference other entities or Representations.

```text
reference identity != referenced object transfer
reference resolution != authority acquisition
```

AR-2 will determine minimum neutral reference semantics.

## 11. Declared properties and guarantees

AR-2 consumes AR-1 `PropertyTransition` semantics and must allow Representations to declare carried or guaranteed properties such as identity, semantic meaning, references, relations, provenance, ordering, context, revision/version, integrity information and reconstruction information.

An initial distinction to validate is:

```text
CLAIM
EVIDENCE
VERIFIED GUARANTEE
UNKNOWN
```

## 12. Content

`content` denotes the Representation's own semantic payload.

AR-2 does not define binary format, JSON/CBOR/Protobuf serialization, framing, compression, encryption or transport. Those concerns primarily belong to AR-6/AR-7.

## 13. Completeness

Completeness must be explicit and scoped.

Initial states:

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

```text
complete without scope = ambiguous claim
```

## 14. Temporality and revision

A Representation may describe an instant, interval, sequence, event, particular revision or temporally unknown state.

```text
representation revision != subject revision
```

## 15. Derived Representations

```text
R0
 ↓ transform
R1
 ↓ summarize
R2
```

Derivation should preserve enough information to assess provenance, transformations, known losses and relation to the original subject.

Detailed reconstruction belongs to AR-4.

## 16. Composition

A composite Representation may contain or relate multiple Representations. Composition must not erase individual identity, provenance or guarantees when architecturally relevant.

Whether `COMPOSITE` is a class or structural capability remains open.

## 17. Authority

```text
Representation != Authority
```

Even an authentic, integrity-verified, trusted-source, complete-for-scope and exactly reconstructable Representation may lack authority to modify destination state.

Authority-related metadata may be carried but cannot grant authority by mere presence.

## 18. Non-KOS neutrality

```text
System A
  ↓ Binding A
Representation
  ↓ KCA
Representation
  ↓ Binding B
System B
```

AR-2 cannot require internal KOS concepts such as `CanonicalObject`, `CognitiveProjection`, `KnowledgeChangeProposal` or KOS-specific authority types as fundamental fields.

## 19. Binding relationship

AR-2 defines neutral Representation semantics. AR-3 defines explicit mappings between domain semantics and Representation semantics.

## 20. KSCL relationship

AR-2 does not assume KSCL is a single layer.

```text
Representation Model != KSCL Model
```

KSCL decomposition remains an AR-5 concern.

## 21. Encoding and KCP relationship

```text
Representation
    ↓ AR-6 Encoding
Encoded Form
    ↓ AR-7 KCP / communication mechanism
Transported Form
```

KCP must not own Representation semantics.

## 22. Initial validation cases

AR-2 must model at least:

1. reference without object transfer;
2. partial state observation;
3. operational result;
4. local projection;
5. evidence associated with a claim;
6. proposal without incorporation authority;
7. derived Representation with known loss;
8. reconstructable Representation;
9. composite Representation;
10. Non-KOS ↔ Non-KOS exchange;
11. one Representation with two encodings;
12. two Representations of the same subject.

## 23. Open questions

- Mandatory common structure or semantic capability set?
- Which Representation classes are fundamental vs domain specializations?
- How can subject identity remain neutral?
- What normative distinction should exist between claim, evidence and guarantee?
- Is provenance mandatory or class-dependent?
- How should coverage/completeness be expressed neutrally?
- How should Representation relationships be expressed without forcing a universal graph?
- Which minimum metadata is needed outside the source system?
- How do we prevent `RepresentationEnvelope` from prematurely becoming a message format?

## 24. Preliminary closure criteria

AR-2 may become a closure candidate when:

- a neutral Representation definition exists;
- referent, Representation and encoding are separated;
- Representation identity and subject identity are distinct;
- provenance and references have minimum semantics;
- properties/guarantees can be expressed conceptually;
- completeness and context are explicit;
- authority remains external;
- validation cases are modelable;
- Non-KOS use requires no hidden KOS semantics;
- AR-3 can define Bindings without redefining Representation;
- AR-6 can define encoding without redefining Representation semantics.

## 25. Initial state

```text
AR-1 Boundary Model:          CLOSED / PASS
AR-2 Representation Model:    ACTIVE

Representation definition:    INITIALIZED
Referent separation:           ESTABLISHED HYPOTHESIS
Representation identity:       INITIALIZED
Subject identity:              INITIALIZED
Representation classes:        RESEARCH TAXONOMY
Semantic context:              INITIALIZED
Provenance:                    INITIALIZED
References:                    INITIALIZED
Property guarantees:           OPEN
Completeness:                  INITIALIZED
Authority separation:          REQUIRED INVARIANT
Non-KOS neutrality:            REQUIRED

Next:
AR-2 validation and taxonomy refinement
```
