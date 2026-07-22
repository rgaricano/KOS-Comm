# NS-2 — KSCL Semantic Constructs

**Status:** WORKING DRAFT  
**Phase:** Phase III — Normative Specification

## 1. Scope

This specification defines the normative semantic constructs that build upon the KSCL Core. It specifies how semantic constructs are organized into reusable forms without changing the meaning of the core ontology.

This specification does not redefine KSCL Core categories, core invariants, or conformance principles.

## 2. Conformance

An implementation is KSCL Semantic Constructs conformant if and only if it preserves KSCL Core conformance and correctly applies the semantic construct rules defined by this specification.

## 3. Construct Model

Semantic constructs are derived from the KSCL Core categories and are expressed as specializations or compositions of those categories.

Constructs SHALL remain domain-neutral unless explicitly stated otherwise by a domain-specific profile.

## 4. Construct Families

### 4.1 Identity Constructs
Identity constructs express semantic identity, correlation and identity-related assertions without introducing new ontology categories.

### 4.2 Representation Constructs
Representation constructs express representational capability, coverage and provenance of semantic material.

### 4.3 Evidence Constructs
Evidence constructs express support, justification and evidential traceability.

### 4.4 Reconstruction Constructs
Reconstruction constructs express candidate generation, scope-relative reconstruction, fidelity assessment and resolution of ambiguity.

### 4.5 Binding Constructs
Binding constructs express compatibility, mapping admissibility and semantic correspondence between domains and representations.

## 5. Reuse Rules

All construct families SHALL reuse KSCL Core primitives and SHALL NOT redefine the meaning of any core category.

## 6. Notes

NS-2 is intentionally constructive and remains subordinate to NS-1.
