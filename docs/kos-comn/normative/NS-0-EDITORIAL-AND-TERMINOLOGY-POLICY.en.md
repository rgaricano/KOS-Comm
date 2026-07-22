# NS-0 — Editorial and Terminology Policy

**Status:** ACTIVE  
**Phase:** Phase III — Normative Specification

## 1. Purpose

This policy defines the editorial and terminology rules that govern all normative KSCL documents.

## 2. Language policy

### NS0-I18N-001
Each normative specification SHALL exist as an artifact independent of language.

### NS0-I18N-002
Each localization SHALL express exactly the same set of normative requirements.

### NS0-I18N-003
No localization SHALL introduce, remove, or modify normative requirements.

### NS0-I18N-004
Identifiers (`KSCL-REQ-*`, `KSCL-INV-*`, `KSCL-TERM-*`) SHALL be language-independent and SHALL constitute the primary normative reference.

## 3. Master language and localizations

English is the normative master language. Localizations are normative-equivalent documents that express the same requirement set in another language.

## 4. Terminology policy

A shared glossary SHALL be used across all normative documents.

### KSCL-TERM-0003
Semantic Assertion

Preferred ES: **Aseveración semántica**

Deprecated ES: Aserto

Forbidden ES: Confirmación

## 5. Editorial rules

- One idea SHALL map to one canonical term.
- Normative identifiers SHALL not be translated.
- Informative and normative content SHALL be separated explicitly.
- Conformance evidence SHALL be traceable to normative identifiers.

## 6. Canonical Semantic Input

### KSCL-TERM-0010
Canonical Semantic Input (CSI)

The canonical semantic representation of all semantic elements required by a Semantic Evaluation after application of every mandatory normalization rule defined by the applicable specification.

### KSCL-TERM-0011
Semantically Equivalent Canonical Semantic Inputs

Two Canonical Semantic Inputs are semantically equivalent if they represent exactly the same semantic information, regardless of representation-level differences and for all semantic elements relevant to the Semantic Evaluation.

### KSCL-TERM-0012
Evaluation Result

The complete normative output produced by a Semantic Evaluation, including every semantic element defined as normative by the applicable specification.

## 7. Semantic conformance principle

### KSCL-PRIN-001
Conformance to KSCL SHALL be determined exclusively from normative semantic content. Representation-level characteristics SHALL NOT affect conformance unless explicitly required by the applicable specification.

## 8. Notes

This policy applies to all NS documents and any subsequent profiles or validation suites.
