# AR-4 — Reconstruction Model

**Status:** ACTIVE — INITIAL MODEL ESTABLISHED  
**Phase:** Phase II — Reconstruction Semantics  
**Predecessor:** Gate A PASS  
**Next:** AR-4 Validation Pass 1

## Purpose and definition

AR-4 defines what semantic reconstruction means from one or more KCA Representations and what claims may be made about its result. It does not define encoding, transport, KCP or a concrete KSCL implementation.

Reconstruction is the explicit process by which represented information, context and available evidence are used to produce a reconstructed artifact or candidate set, accompanied by a verifiable declaration of scope, fidelity, uncertainty, provenance and degradation.

```text
Representation(s) + Context + Evidence + Reconstruction Rules
                         ↓
                Reconstruction Process
                         ↓
                Reconstruction Result
```

Fundamental invariant: `reconstruction != authorization`.

## Not automatic inversion

A Representation is not assumed to be a reversible serialization of an original object. It may be partial, transformed, degraded, aggregated or ambiguous. Reconstruction therefore does not imply equality with an original object.

## ReconstructedArtifact

`ReconstructedArtifact` is the conceptual semantic reconstruction output and is distinct from DomainState, CanonicalObject, AuthorizedImport and ExecutedState.

## Initial reconstruction classes

`EXACT`: equivalence can be claimed relative to an explicit declared scope with no known relevant loss. It does not mean ontological identity.

`EQUIVALENT`: structure may differ while required semantics for the declared scope are preserved.

`PARTIAL`: only part of the target scope can be supported.

`DEGRADED`: usable reconstruction with explicit semantic loss/weakening.

`AMBIGUOUS`: multiple compatible reconstructions exist and evidence cannot justify selecting one.

`IMPOSSIBLE`: available information/context/evidence cannot produce a valid reconstruction for the required scope.

## ReconstructionResult

```text
ReconstructionResult<T> {
    status
    artifact?
    candidates[]?
    target_scope
    reconstructed_scope
    fidelity
    property_transitions[]
    evidence_refs[]
    provenance[]
    diagnostics[]
}
```

Candidate statuses are EXACT, EQUIVALENT, PARTIAL, DEGRADED, AMBIGUOUS and IMPOSSIBLE. Validation must determine whether reconstruction class and result status should remain unified or separate.

## Scope and fidelity

All reconstruction claims are scope-relative. `EXACT relative to scope S` is meaningful; unqualified absolute EXACT is not assumed.

Candidate scope model:

```text
ReconstructionScope {
    required_properties[]
    optional_properties[]
    semantic_context?
    temporal_scope?
    identity_scope?
}
```

Candidate fidelity model:

```text
FidelityAssessment {
    scope
    preserved[]
    equivalent[]
    degraded[]
    missing[]
    unknown[]
    basis[]
}
```

Fidelity cannot exceed available evidence unless new independent evidence is explicitly introduced.

## Evidence and provenance

Evidence may be represented, contextual, local independent or derived. Derived evidence must remain traceable to its bases. Inference must not be presented as direct observation.

Reconstruction provenance is composite across input Representations, incorporated context, independent evidence, applied rules and significant derivations.

## Degradation and restoration

Without new independent justified evidence, semantic property strength must not increase. Reconstruction may propagate existing losses and add new ones. Restoration requires explicit new basis.

## Ambiguity, partiality and impossibility

Multiple compatible candidates without sufficient selection evidence remain AMBIGUOUS. Silent implementation-convenience selection is prohibited.

PARTIAL is not failure; target scope, reconstructed scope and missing/unknown properties must be declared.

IMPOSSIBLE indicates insufficient basis for a conformant artifact/candidate under the required scope. Candidate diagnostics include INSUFFICIENT_INFORMATION, MISSING_REQUIRED_CONTEXT, CONFLICTING_EVIDENCE, UNSUPPORTED_SEMANTICS, IRRECOVERABLE_LOSS and IDENTITY_UNRESOLVED.

## Binding relationship

Binding and Reconstruction are distinct responsibilities. Binding maps domain semantics to/from KCA Representation. Reconstruction derives reconstructed semantic artifacts/candidates from Representation(s), evidence and context. A concrete Binding may invoke or consume reconstruction, but AR-3 is not redefined as a reconstruction engine. Neutral reconstruction may also exist without a Binding.

## Authority relationship

```text
Representation(s)
  ↓ Reconstruction
ReconstructedArtifact / Candidates
  ↓ optional Binding/domain mapping
DomainFacingCandidate
  ↓
DOMAIN AUTHORITY
```

`reconstructed != accepted != canonical != authorized`.

## Identity, time and determinism

Identity evidence, correlation, claim and authority remain distinct. AR-4 may produce an evidence-supported identity claim/candidate but not canonical identity authority.

Historical reconstructed state at t1 does not imply current state at t2.

Reconstruction need not always be deterministic; multiple candidates and external context are allowed if uncertainty and bases are explicit.

## Neutrality

The model requires no KOS-internal semantics. Neutral Representations plus neutral rules/evidence may produce a neutral ReconstructionResult. Domain Bindings are applied only when connection to a specific domain is required.

## KSCL, encoding and KCP separation

AR-4 defines reconstruction semantics before deciding what belongs to KSCL. AR-5 will assess whether KSCL is one layer or a decomposition into functions/profiles/mechanisms/components.

Reconstruction semantics remain separate from encoding, transport and KCP.

## Initial conformance

A conformant reconstruction declares target/reconstructed scope and class/status; preserves relevant provenance; declares evidence/basis; exposes loss and unknowns; does not elevate fidelity without new independent justified basis; preserves unresolved ambiguity; separates reconstruction from authority and Binding; remains independent of encoding/transport; and permits neutral non-KOS realizations.

## Open validation questions

Validation will examine whether EXACT/EQUIVALENT/etc. are statuses or fidelity classes; whether PARTIAL and AMBIGUOUS may coexist; candidate-set representation; DEGRADED vs PARTIAL; minimum ReconstructionScope properties; evidence conflict; explicit ReconstructionClaim; composition of successive reconstructions; temporal/multi-state reconstruction; and what AR-5/KSCL should consume.

## Planned validation cases

1. complete Representation with equivalent reconstruction;
2. partial Representation with partial reconstruction;
3. irreversible loss preventing required reconstruction;
4. two equally compatible candidates;
5. new local evidence restoring a property;
6. conflicting evidence from two sources;
7. correct reconstruction not authorized by domain;
8. neutral reconstruction without Binding;
9. reconstruction followed by Binding toward KOS;
10. historical-state reconstruction versus current state;
11. reconstruction chain with accumulated degradation;
12. target scope smaller than available information.

## State

```text
AR-4 — RECONSTRUCTION MODEL
INITIAL MODEL: ESTABLISHED
STATUS: ACTIVE
NEXT: VALIDATION PASS 1
```
