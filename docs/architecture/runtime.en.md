# KOS Runtime

## Status

Canonical reference draft for KOS-Lab.

## 1. Purpose

The Runtime is the subsystem responsible for executing, supervising, and projecting the operational state of the KOS system. Its role is not to store canonical knowledge, but to operate on the state provided by other subsystems.

## 2. Responsibility

The Runtime coordinates system execution and keeps visibility over the operational state of its components.

Main responsibilities:

- execute processes;
- supervise operational state;
- expose the execution tree;
- coordinate the Supervisor;
- integrate repository synchronization;
- feed the Renderer with up-to-date state;
- maintain execution traceability.

## 3. Core principle

The Runtime is not the source of truth for knowledge.
Its role is to operate on knowledge projections and on its own operational state.

## 4. Separation of planes

Three planes are distinguished:

### 4.1 Operational state

Defines what is happening in the Runtime at this instant:

- active components;
- paused components;
- finished components;
- pending components;
- blocked components.

### 4.2 Execution

Defines the activity in progress:

- running tasks;
- active synchronizations;
- pending validations;
- recovery in progress;
- active rendering.

### 4.3 Projection

Defines how the state is presented to the operator:

- console;
- Markdown;
- JSON;
- GitHub Issue;
- future web or API interface.

## 5. Main components

The Runtime may include, at minimum, the following subsystems:

- Execution Runtime;
- Runtime Supervisor;
- Repository Sync Manager;
- Runtime Renderer;
- Runtime Bootstrap.

## 6. Execution tree

The Runtime must be representable as an execution tree.

The execution view may include:

- root node;
- level-1 nodes;
- child nodes;
- metrics per node;
- state per node;
- validation per node.

## 7. Supervisor

The Supervisor is the subsystem responsible for the health and stability of the Runtime.

It must include, at minimum:

- health monitor;
- watchdog;
- recovery engine;
- clock provider;
- health record.

## 8. Repository synchronization

The Runtime must integrate GitHub synchronization as an operational capability.

Synchronization includes:

- documentation registration;
- task registration;
- report registration;
- publication of status issues;
- updating persistent registries;
- traceability through commits.

## 9. Renderer

The Runtime must not generate arbitrary outputs.
It must delegate presentation to the Runtime Renderer.

The Renderer transforms a state into a concrete view.

## 10. Bootstrap

The Runtime must be able to reconstruct its state from persistent artifacts.

At minimum:

- configuration;
- state;
- session;
- registries;
- references.

## 11. Emulation mode

When the Runtime is in emulation mode, it must be explicitly indicated.
It must not be confused with a real operational state.

## 12. Status of this specification

This document defines the canonical behavior of the KOS-Lab Runtime. Any implementation must respect the separation between execution, supervision, synchronization, and projection.
