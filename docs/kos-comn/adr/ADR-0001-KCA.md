# ADR-0001 — KCA as the architectural framework for KOS communications

- **Status:** ACCEPTED FOR KOS-Comn LABORATORY
- **Scope:** `KOS-Comn`
- **Decision type:** Architectural framing

## Context

The initial work focused on KCP and KSCL as the principal concepts for information exchange and session continuity in KOS.

A telecommunications and information-systems analysis shows that this framing combines responsibilities that should be separated: semantic representation, encoding, communication, continuity and consumer projection.

Treating KCP as the whole communication subsystem would make transport concerns responsible for semantics and state reconstruction. Treating KSCL only as a language would likewise under-specify the continuity problem.

KOS already contains architectural boundaries for persistent knowledge, persistent cognitive state, observation, projection, context consumption and execution. The communication subsystem must integrate with those boundaries rather than silently replacing them.

## Decision

Adopt **KCA — Knowledge Communication Architecture** as the architectural framework for the `KOS-Comn` laboratory.

KCA initially separates the subsystem into:

```text
KRM        — Knowledge Representation Model
KEncoding  — Knowledge Encoding
KCP        — Knowledge Communication Protocol
KSCL       — Knowledge Session Continuity Layer
CP         — Cognitive Projection
```

with persistence/canonical knowledge below the stack and consumers above it.

## Consequences

### Positive

- KCP is no longer overloaded with representation or continuity responsibilities.
- KSCL can be redesigned around deterministic continuity rather than only textual session records.
- Encoding can evolve independently from semantic representation.
- Cognitive Projection remains a derived consumer-facing boundary.
- Interfaces and invariants between layers can be tested independently.
- The architecture becomes suitable for multiple consumers and transports, not only LLM conversations.

### Costs / risks

- Existing KCP and KSCL concepts may require substantial reconstruction.
- Additional interfaces and versioning rules must be specified.
- KRM must be reconciled with the canonical KOS knowledge model to avoid duplication.
- KCA introduces new terminology that must remain tightly governed.

## Invariants

```text
REPRESENTATION != ENCODING
ENCODING != COMMUNICATION
COMMUNICATION != CONTINUITY
CONTINUITY != PROJECTION
PROJECTION != CANONICAL AUTHORITY
```

## Non-decisions

This ADR does not yet decide:

- the final KRM object taxonomy;
- the physical serialization format;
- the wire transport;
- the final KEU structure;
- reliability semantics;
- cryptographic mechanisms;
- session checkpoint format;
- whether KSCL remains a textual DSL, becomes a structured encoding, or exposes both forms.

These require subsequent engineering decisions.

## Integration constraint

This ADR governs the `KOS-Comn` laboratory only. It does not modify the canonical KOS architecture on `dev` until an explicit integration decision is made and compatibility with existing accredited boundaries is demonstrated.

## Next decision area

Define KRM and its mapping to existing KOS canonical knowledge, observation, evidence, provenance and identity concepts.
