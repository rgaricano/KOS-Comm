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

### KSCL-TERM-0030 — Core Invariant
A normative semantic property that SHALL remain true for every valid KSCL semantic model.

### KSCL-TERM-0031 — Ontological Membership
The unique assignment of a semantic construct to exactly one Core Ontology category.

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

### 6.1 Identity Invariants

#### KSCL-INV-IDN-001
Every Semantic Atom SHALL possess exactly one semantic identity.

Verification rule: `cardinality(semanticIdentity)=1`.

Required evidence: semantic model, identity registry, validation report.

#### KSCL-INV-IDN-002
The semantic identity of a Semantic Atom SHALL remain invariant throughout its lifetime.

Verification rule: `semanticIdentity(t1)=semanticIdentity(t2)` for any two valid observations of the same Semantic Atom.

Required evidence: historical trace, identity comparison.

#### KSCL-INV-IDN-003
Semantic identity SHALL be independent of representation.

Verification rule: semantically equivalent representations SHALL resolve to the same semantic identity.

Required evidence: representation mapping, semantic resolution report.

### 6.2 Structural Invariants

#### KSCL-INV-STR-001
Every semantic dependency SHALL reference an existing semantic construct.

Verification rule: every dependency target SHALL resolve uniquely.

Required evidence: dependency validation report.

#### KSCL-INV-STR-002
Every semantic construct SHALL belong to exactly one Core Ontology category.

Verification rule: `cardinality(category)=1`.

Required evidence: semantic model, category validation report.

#### KSCL-INV-STR-003
Every semantic construct SHALL satisfy all dependency constraints defined by the Core Dependency Matrix.

Verification rule: every dependency edge SHALL be valid.

Required evidence: dependency graph, validation report.

### 6.3 Semantic Invariants

#### KSCL-INV-SEM-001
The semantic meaning of a Semantic Atom SHALL NOT be altered by any Semantic Assertion, Semantic Evaluation, or Semantic Operation.

Verification rule: `semanticMeaning(before)=semanticMeaning(after)`.

Required evidence: semantic identity report, semantic comparison report.

#### KSCL-INV-SEM-002
A Semantic Evaluation SHALL characterize semantic constructs without modifying their semantic meaning.

Verification rule: `meaning(before)=meaning(after)`.

Required evidence: evaluation input, evaluation output, semantic equivalence report.

#### KSCL-INV-SEM-003
A Semantic Operation SHALL preserve every applicable Core Invariant.

Verification rule: validate every applicable Core Invariant before and after execution.

Required evidence: operation trace, invariant validation report.

#### KSCL-INV-SEM-004
Semantic meaning SHALL be independent of representation.

Verification rule: semantically equivalent representations SHALL yield the same semantic interpretation.

Required evidence: representation mapping, semantic interpretation report.

## 7. Semantic Integrity

### KSCL-PRN-002
The semantic integrity of KSCL SHALL be preserved across all conformant semantic models and conformant operations.

### KSCL-INV-INT-001
Semantic integrity SHALL remain preserved across all conformant semantic models.

Verification rule: validate that every applicable Core Invariant remains true for the model under test.

Required evidence: integrity validation report.

### KSCL-INV-INT-002
No conformant operation SHALL introduce a violation of semantic integrity.

Verification rule: execute the operation and verify that no Core Invariant or applicable requirement is violated.

Required evidence: operation trace, integrity validation report.

### KSCL-INV-INT-003
Semantic integrity SHALL be assessed independently from serialization and transport.

Verification rule: alter only serialization or transport characteristics; the integrity result SHALL remain unchanged.

Required evidence: integrity assessment report, variant serialization set.

## 8. Conformance Evidence

A conformant implementation SHALL provide conformance evidence for each applicable requirement and invariant.

A conformance report SHALL reference the exact KSCL-REQ and KSCL-INV identifiers satisfied or failed.

## 9. Extension Rules

Extensions MAY add new semantic structures only as specializations or compositions of the core categories.

Extensions SHALL NOT redefine the meaning of the core categories.

## 10. Notes

The normative master language is English. Localizations SHALL be semantically equivalent documents with identical identifiers.
