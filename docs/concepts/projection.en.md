# Projection

## Status

Canonical reference draft for KOS-Lab.

## 1. Definition

A projection is a temporary view built from a canonical state. The projection does not modify the original state; it only selects, organizes, and presents part of it for a specific purpose.

## 2. Purpose

Projections make it possible to observe the same state from multiple perspectives without duplicating the underlying truth.

## 3. Properties

Every canonical projection must satisfy these properties:

- it is derived;
- it is temporary;
- it is recoverable;
- it is stable within its scope;
- it does not replace canonical state;
- it can be rendered in multiple formats.

## 4. Relationship with state

State is the source of truth.
Projection is a partial materialization of state for a specific purpose.

Examples:

- a task view;
- a dependency view;
- a health view;
- a metrics view;
- a documentation view;
- a context view for inference.

## 5. Relationship with KQL

KQL requests projections.

Example:

```text
KOS : Runtime : Execution : Estado : Tareas : Desglosadas
```

This query does not request a state change.
It requests a detailed projection of the task state.

## 6. Relationship with the Runtime

The Runtime consumes projections and presents them to the operator.
It must not confuse projection with source of truth.

## 7. Relationship with the Knowledge Engine

The Knowledge Engine builds knowledge projections.
The Runtime builds execution projections.
Both follow the same principle: one canonical truth, multiple views.

## 8. Detail levels

A projection may have different expansion levels:

- summary;
- general;
- detailed;
- extended;
- historical;
- differential;
- critical.

## 9. Honesty requirements

Every projection must indicate whether it comes from:

- real state;
- emulated state;
- partial state;
- reconstructed state.

A projection must not be presented as a complete state when it is not one.

## 10. Status of this specification

This document defines the concept of projection in KOS-Lab. Any subsystem that represents derived information must respect this definition.
