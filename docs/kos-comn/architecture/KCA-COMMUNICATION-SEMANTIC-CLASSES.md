# KCA Communication Semantic Classes

**Status:** Phase A synthesis / pre-schema  
**Date:** 2026-07-21

## 1. Purpose

Define semantic communication classes before defining serialization or transport.

## 2. Classes

### CSC-01 OBSERVATION
Carries non-owning observed state. Must identify observation semantics and must not imply canonical transfer, persistence or contextual selection.

### CSC-02 PROJECTION
Carries a bounded derived cognitive projection. Must preserve derivation/provenance and boundary semantics sufficient to avoid interpreting the projection as global state.

### CSC-03 CANONICAL_REFERENCE
Carries stable source identity/reference semantics and optional type/version qualifiers. It does not by itself carry complete source state.

### CSC-04 CANONICAL_TRANSFER
Carries information explicitly intended to support canonical reconstruction/import. This is distinct from OBSERVATION and requires stronger completeness, authority and receiver-policy semantics.

### CSC-05 RELATION
Carries semantic relation identity/type/endpoints. Must not be overloaded to represent evidence or lineage implicitly.

### CSC-06 EVIDENCE
Carries inline evidence and/or evidence references. Evidence identity and evidence content remain distinguishable.

### CSC-07 PROVENANCE
Carries origin/derivation information. Provenance does not confer authority or truth.

### CSC-08 LINEAGE
Carries explicit predecessor/evolution references. Transport sequence and timestamps cannot create lineage.

### CSC-09 OPERATION
Carries exchange/correlation/idempotency/publication operation semantics. Operational identity remains separate from source canonical identity.

### CSC-10 RESULT
Carries an operational result/status. A result is not persistent knowledge by default.

### CSC-11 AUTHORITY_ASSERTION
Carries an explicit claim about source authority/ownership/status. The claim is itself data to be evaluated by receiver policy; transport does not make it true.

### CSC-12 BOUNDARY_DESCRIPTOR
Carries selection/projection/completeness scope: what was included, excluded, requested or declared complete relative to a boundary.

## 3. Composition rule

A KCA exchange may compose several semantic classes:

```text
PROJECTION
 + CANONICAL_REFERENCE[]
 + RELATION[]
 + EVIDENCE[]
 + PROVENANCE
 + BOUNDARY_DESCRIPTOR
```

or:

```text
CANONICAL_TRANSFER
 + CANONICAL_REFERENCE
 + RELATION[]
 + EVIDENCE[]
 + PROVENANCE
 + LINEAGE[]
 + AUTHORITY_ASSERTION
```

The class determines semantics; serialization container shape does not.

## 4. Forbidden semantic shortcuts

```text
OBSERVATION => CANONICAL_TRANSFER        forbidden
PROJECTION => GLOBAL COMPLETE STATE      forbidden without boundary assertion
PROVENANCE => AUTHORITY                  forbidden
TIMESTAMP/SEQUENCE => LINEAGE            forbidden
RESULT => KNOWLEDGE                      forbidden
RECEIPT => IMPORT                        forbidden
```
