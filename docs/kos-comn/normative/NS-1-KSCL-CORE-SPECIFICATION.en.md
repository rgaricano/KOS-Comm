# NS-1 — KSCL Core Specification

**Status:** WORKING DRAFT  
**Phase:** Phase III — Normative Specification

## 1. Scope

This specification defines the KSCL Core semantic model, including its fundamental ontology, semantic categories, normative invariants, and conformance requirements.

This specification does not define domain-specific semantics, serialization formats, transport protocols, persistence mechanisms, security policies, governance rules, or application-specific semantics.

## 2. Conformance

An implementation is KSCL Core conformant if and only if:

1. Every semantic construct is classifiable as Atom, Assertion, Evaluation, or Operation.
2. All mandatory invariants are preserved.
3. No prohibited dependency is introduced.
4. The semantic dependency graph is acyclic unless a profile explicitly permits otherwise.
5. No implementation-specific extension changes the meaning of the core categories.

## 3. Terms and Definitions

### KSCL-TERM-0010 — Canonical Semantic Input (CSI)
The canonical semantic representation of all semantic elements required by a Semantic Evaluation after application of every mandatory normalization rule defined by the applicable specification.

### KSCL-TERM-0011 — Semantically Equivalent Canonical Semantic Inputs
Two Canonical Semantic Inputs are semantically equivalent if they represent exactly the same semantic information, regardless of representation-level differences and for all semantic elements relevant to the Semantic Evaluation.

### KSCL-TERM-0012 — Evaluation Result
The complete normative output produced by a Semantic Evaluation, including every semantic element defined as normative by the applicable specification.

### KSCL-TERM-0020 — Semantic Dependency
A normative relationship in which the semantic interpretation of one semantic construct requires the existence or interpretation of another semantic construct.

### KSCL-TERM-0021 — Dependency Closure
The complete set of semantic constructs reachable through recursive application of the dependency relation.

## 4. Core Ontology

### 4.1 Semantic Atom
A Semantic Atom is the smallest indivisible semantic construct recognized by KSCL Core.

Mandatory properties:
- Atomic
- Identifiable
- Composable
- Domain-neutral
- Immutable semantic identity

Dependencies: none.

Conformance requirements:
- A Semantic Atom SHALL NOT depend on any upper semantic category.
- A Semantic Atom SHALL preserve its semantic identity independently of implementations.

### 4.2 Semantic Assertion
A Semantic Assertion is a semantic construct that establishes one or more semantic relations among Semantic Atoms.

Mandatory properties:
- Relational
- Deterministic
- Composable
- Traceable

Dependencies: Atoms, Assertions.

Conformance requirements:
- A Semantic Assertion SHALL reference at least one Semantic Atom.
- A Semantic Assertion SHALL NOT create Semantic Atoms.
- A Semantic Assertion MAY reference other Semantic Assertions.

### 4.3 Semantic Evaluation
A Semantic Evaluation is a semantic construct that characterizes one or more Semantic Assertions without modifying their semantic meaning.

Mandatory properties:
- Deterministic
- Observable
- Non-mutating
- Traceable

Dependencies: Atoms, Assertions, Evaluations.

Conformance requirements:
- A Semantic Evaluation SHALL reference at least one Semantic Assertion.
- A Semantic Evaluation SHALL NOT modify any Semantic Assertion.
- A Semantic Evaluation MAY reference another Semantic Evaluation.
- A Semantic Evaluation SHALL be reproducible when evaluated over semantically equivalent Canonical Semantic Inputs under identical conformance-relevant configuration.

### 4.4 Semantic Operation
A Semantic Operation is a semantic construct that consumes semantic structures and produces new semantic structures or external effects while preserving the normative semantics defined by KSCL Core.

Mandatory properties:
- Composable
- Traceable
- Deterministic

Dependencies: Atoms, Assertions, Evaluations, Operations.

Conformance requirements:
- A Semantic Operation SHALL preserve every applicable Core Invariant.
- A Semantic Operation SHALL NOT redefine the semantics of any Core category.
- A Semantic Operation MAY produce Assertions, Evaluations, or External Effects.
- A Semantic Operation SHALL declare every semantic dependency required for its execution.

## 5. Semantic Dependency Model

The Core Dependency Matrix is normative:

| Source | Atom | Assertion | Evaluation | Operation |
|---------|:---:|:---------:|:----------:|:---------:|
| Atom | ✓ | ✗ | ✗ | ✗ |
| Assertion | ✓ | ✓ | ✗ | ✗ |
| Evaluation | ✓ | ✓ | ✓ | ✗ |
| Operation | ✓ | ✓ | ✓ | ✓ |

### KSCL-REQ-DEP-001
A semantic dependency SHALL exist only if permitted by the Core Dependency Matrix.

### KSCL-REQ-DEP-002
Every declared semantic dependency SHALL be explicit.

### KSCL-REQ-DEP-003
Every Semantic Evaluation and every Semantic Operation SHALL operate over the complete Dependency Closure required by the applicable specification.

### KSCL-REQ-DEP-004
Profiles or derived specifications MAY restrict semantic dependency graphs to be acyclic.

### KSCL-INV-DEP-001
Every referenced semantic dependency SHALL resolve to exactly one semantic construct.

### KSCL-INV-DEP-002
No semantic dependency SHALL violate the Core Dependency Matrix.

## 6. Core Invariants

### KSCL-INV-001
Atoms SHALL NOT depend on upper semantic layers.

### KSCL-INV-002
Assertions SHALL reference at least one Atom.

### KSCL-INV-003
Evaluations SHALL NOT modify Assertions.

### KSCL-INV-004
Operations SHALL NOT define semantics.

### KSCL-INV-005
Semantic dependency graphs SHALL be acyclic unless a profile explicitly permits otherwise.

## 7. Conformance Evidence

A conformant implementation SHALL provide conformance evidence for each applicable requirement and invariant.

A conformance report SHALL reference the exact KSCL-REQ and KSCL-INV identifiers satisfied or failed.

## 8. Extension Rules

Extensions MAY add new semantic structures only as specializations or compositions of the core categories.

Extensions SHALL NOT redefine the meaning of the core categories.

## 9. Notes

The normative master language is English. Localizations SHALL be semantically equivalent documents with identical identifiers.
