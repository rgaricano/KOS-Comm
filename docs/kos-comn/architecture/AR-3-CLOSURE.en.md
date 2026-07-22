# AR-3 — Binding Model — Closure

**Status:** CLOSED / PASS  
**Phase:** Phase I — Boundary & Representation Foundation  
**Predecessors:** AR-1 CLOSED/PASS, AR-2 CLOSED/PASS  
**Next:** Gate A assessment

## Decision

```text
AR-3 — BINDING MODEL
STATUS: CLOSED
RESULT: PASS
CASES ASSESSED: 20
CRITICAL CONTRADICTIONS: 0
CORE REWORK: NONE
```

A Binding is an explicit semantic adapter at the boundary between a domain and neutral KCA Representations. It is a bilateral seam; bilateral does not imply symmetry, reversibility or invertibility.

## Responsibility

Bindings may own mapping rules, subject resolution, capability correspondence, loss declarations, correlations, mapping preconditions, diagnostics, contract compatibility and semantic mapping admissibility. They do not implicitly own domain authority, canonical import, persistence, execution, reconstruction, canonical identity, promotion, transport or encoding.

`mapping capability != domain authority`.

## Inbound semantics

Inbound mapping produces a `DomainFacingCandidate`; `candidate != accepted domain state` and `receipt != canonical import`.

## Directions

`OUTBOUND`, `INBOUND`, `BIDIRECTIONAL`; `BIDIRECTIONAL != INVERTIBLE`.

## BindingResult

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Statuses: `MAPPED`, `MAPPED_WITH_DEGRADATION`, `UNMAPPABLE`, `REJECTED_BY_BINDING_POLICY`, `UNSUPPORTED_CONTRACT`. Status and diagnostic cause remain separate.

## AR-1 / AR-2 integration

Relevant transformations use AR-1 property transitions. Bindings produce/consume AR-2 Representations and preserve AR-2 criticality, coverage, provenance and degradation semantics.

## Identity and correlation

Identity mapping is not identity authority; correlation is not canonical identity. Interoperable BindingContract identity is required and unambiguous within its declared interoperability scope; no universal global identity is required. Correlation conflicts cannot be silently resolved.

## Degradation/restoration

By default semantic property strength is conservatively non-increasing across transformations. It may increase only when new, independent, explicit and scoped justification/evidence is introduced and attributed to the restoration point.

## Policy

Mapping admissibility belongs to Binding. Authoritative acceptance, persistence and execution belong to the domain. A Binding policy that automatically assumes domain authority is non-conformant.

## Compatibility

Declared contract compatibility and runtime semantic mappability are distinct stages. Syntactic success does not imply semantic compatibility.

## Composition

Composition safety is explicitly assessed rather than inferred from local compatibility. Assessment considers capabilities, contracts, identity scopes, correlations, accumulated losses and admissibility constraints. AR-3 does not require a universal composition engine.

## Neutrality

Binding Model is a neutral architectural contract; KOS Binding is a domain-specific realization. `Non-KOS A → Binding A → KCA → Binding B → Non-KOS B` is conceptually feasible without KOS-internal types. Gate C.5 still requires experimental evidence.

## Preserved boundaries

AR-1 owns boundary property-transition semantics; AR-2 representable semantics; AR-3 domain/Representation correspondence; AR-4 reconstruction; AR-6 encoding; AR-7 KCP/protocol transport. AR-3 does not absorb reconstruction, encoding or transport.

## Stabilized conformance

A conformant Binding is unambiguously identified in its interoperability scope; declares contract ranges/directions; preserves mapping/authority separation; produces inbound candidates rather than authoritative acceptance; reports AR-1 losses; respects AR-2 criticality/degradation; separates status from cause; does not elevate properties without new explicit basis; distinguishes admissibility from domain authority; treats correlation as relation rather than identity authority; exposes correlation conflicts; separates declared compatibility from runtime mappability; validates composition; remains separate from reconstruction/encoding/transport; and permits non-KOS realizations.

## Closure evidence

```text
Initial Model: COMPLETE
Validation Pass 1: 12/12 PASS
Adversarial Pass 2: 8/8 PASS
Total: 20/20 PASS
Critical contradictions: 0
Core premise rework: none
```

## Residual non-blocking risks

Concrete Binding discovery/registry, mapping-rule syntax, correlation storage, profile negotiation, migration/version strategy, restoration evidence instrumentation and composition-assessment implementation remain later design/implementation concerns.

## Reopen conditions

Reopen if later evidence shows neutral Binding requires domain authority, candidate/authoritative-state separation cannot be maintained, conservative degradation/restoration cannot be expressed, AR-1/AR-2 are incompatible, safe composition requires core redefinition, non-KOS realization imports KOS-internal semantics, or AR-4/AR-6/AR-7 require responsibility transfer into Binding.

## Result

```text
AR-3 — BINDING MODEL
CLOSED / PASS

PHASE I COMPONENTS:
AR-1 CLOSED / PASS
AR-2 CLOSED / PASS
AR-3 CLOSED / PASS

NEXT:
GATE A ASSESSMENT
```
