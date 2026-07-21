# Colaboración KOS-Comm ↔ KOS-Lab

**Fecha:** 2026-07-21  
**Estado:** GATE 0 — ARCHITECTURAL CONSENSUS — PASS  
**Línea:** KOS-Comm experimental (`KOS-Comn`)  
**Impacto sobre baseline KOS-Lab:** NINGUNO  
**Contraparte autoritativa:** `governance/collaboration/KOS-Lab_KOS-Comm-COLLABORATION-2026-07-21.es.md` en `dev` de KOS-Lab, commit declarado `3b0f1d545ec64cebb8b8f130d49b16c8aa22b95c`.

## 1. Propósito

Este documento preserva en la línea KOS-Comm el cierre de la reconciliación arquitectónica mantenida con la supervisión de KOS-Lab. Debe utilizarse como checkpoint de reentrada ante dudas sobre autoridad, dependencia, KCA, Binding, KSCL, Encoding, KCP, Reconstruction o promoción de resultados experimentales.

No sustituye la autoridad documental de KOS-Lab. Conserva la perspectiva y compromisos de KOS-Comm y referencia el charter autoritativo persistido por KOS-Lab.

## 2. Consenso fundamental

> KOS-Lab define las semánticas autoritativas de sus dominios; KOS-Comm investiga semánticas neutrales de frontera informacional; los Bindings conectan ambos sin transferencia implícita de propiedad ni autoridad.

Objetivo: colaboración experimental controlada, no absorción ni integración indiscriminada.

```text
KOS-Lab
   │ stabilized authoritative contracts
   ▼
Explicit Binding
   ▼
Information Boundary / KCA Contracts
   ▼
KOS-Comm
   ├── KSCL research
   ├── Encoding research
   └── KCP protocol research
   ↓
Experimental Evidence
   ↓
KOS-Lab Governance
   ├── ACCEPT
   ├── REWORK
   └── REJECT
```

## 3. Autonomía bilateral

```text
KOS-Comm MUST NOT require KOS internal semantics
beyond explicit bindings.

KOS-Lab MUST NOT require KOS-Comm implementation details
beyond explicit contracts.
```

KOS-Comm debe adaptarse a fronteras explícitas y contratos estabilizados de KOS-Lab. KOS-Lab no debe deformar sus dominios para acomodar KOS-Comm.

KOS-Comm debe permanecer suficientemente neutral para demostrar operación entre sistemas no-KOS.

## 4. Modelo de fronteras — AR-1

La investigación debe formalizar al menos:

- Domain Boundary — cambio de responsabilidad/propiedad arquitectónica.
- Information Boundary — cambio explícito de representación o contexto de interpretación.
- Communication Boundary — intercambio mediante mecanismo de comunicación.
- Authority Boundary — punto donde autoridad debe evaluarse, transferirse o rechazarse explícitamente.

Invariantes:

```text
Information Boundary != Communication Boundary
Communication Boundary != Authority Transfer
Receipt != Import
Transmission != Authority Transfer
Projection != Canonical Object
Observation != Canonical Serialization
```

AR-1 debe estudiar composición de fronteras y propiedades que deben preservarse al atravesarlas.

## 5. KCA y Representation — AR-2

KCA permanece como identificador experimental; su expansión nominal no queda congelada.

Hipótesis funcional:

> KCA es una arquitectura transversal que gobierna las propiedades semánticas que deben preservarse cuando una representación atraviesa una frontera informacional.

El anterior `KCA Neutral Information Model` debe revisarse como `KCA Information Representation Model` o denominación equivalente.

```text
Representation != Source Object
Representation != Canonical Object
Representation != necessarily Serialization
```

Las clases OBSERVATION, RESULT, OPERATION, REFERENCE, EVIDENCE, RELATION, PROVENANCE, etc. permanecen como clases semánticas experimentales KCA y banco de pruebas de expresividad; no son tipos canónicos KOS por defecto.

## 6. Binding — AR-3 y architectural seam

El punto de acoplamiento preferente es:

```text
KOS domain/state/object
        ↓
explicit KOS ↔ KCA Binding
        ↓
KCA Representation
```

Un Binding puede definir proyección/omisión, identidad, referencias, revisión, relaciones, evidencia, procedencia, metadata de autoridad y garantías de reconstrucción.

Regla de diseño:

```text
A KOS domain MUST NOT depend directly on KCP, KSCL or a
KOS-Comm encoding to expose information across an information
boundary. Interaction SHOULD occur through an explicit binding
or boundary contract.
```

Primeros bindings colaborativos:

1. `StateObservation` → `OBSERVATION Representation`.
2. `ExecutionResult` → `RESULT Representation`.
3. `Canonical Object Reference` → `REFERENCE Representation`.

No comenzar por transferencia canónica completa.

## 7. Reconstruction y KCR — AR-4

Reconstruction debe definirse antes de congelar KSCL.

Clases candidatas:

- reference reconstruction;
- observation reconstruction;
- projection reconstruction;
- graph reconstruction;
- canonical candidate reconstruction.

KCR se investigará como `KCA Reconstruction Capability`, no como propiedad exclusiva de KSCL.

La escala experimental KCR-0..KCR-7 no queda congelada. Debe contrastarse con un posible modelo multidimensional de fidelidad:

- identity fidelity;
- semantic fidelity;
- relation fidelity;
- evidence fidelity;
- provenance fidelity;
- ordering fidelity;
- context fidelity.

Posible combinación a investigar:

```text
KCR coarse profile
        +
Reconstruction Fidelity Vector
```

Invariante fundamental:

```text
RECONSTRUCTION CAPABILITY ⟂ AUTHORITY
```

Máxima capacidad reconstructiva puede coexistir con autoridad canónica nula. Una reconstrucción canónica sólo produce candidato hasta evaluación/autorización/importación explícitas.

## 8. KSCL — AR-5

KSCL continúa como experimento. No se congela:

- su condición de layer;
- su expansión nominal;
- su responsabilidad final;
- su dependencia respecto de KCP.

Debe descomponerse funcionalmente según problemas/responsabilidades, incluyendo:

- representation;
- grammar;
- references;
- patterns;
- derivation;
- reconstruction;
- regeneration;
- realization;
- encoding;
- session/continuity.

Hipótesis abierta: KSCL puede contener varios componentes.

```text
KSCL State != Canonical Knowledge
KSCL Regeneration != Canonical Knowledge Derivation
```

## 9. Encoding — AR-6

Separación requerida:

```text
Semantic Model
    ↓
Logical Representation
    ↓
Physical Encoding
```

No optimizar prematuramente con binary/compact encoding, compression, dictionaries o delta mechanisms antes de acreditar:

- semantic correctness;
- interoperability;
- round-trip behavior;
- loss characteristics;
- reconstruction guarantees.

## 10. KCP — AR-7

KCP pertenece al Communication Domain.

KCA define qué debe preservarse informacionalmente; KCP define cómo se intercambian protocolariamente representaciones compatibles.

KCP debe ser acotado, sustituible y no poseer:

- Canonical Knowledge;
- Cognitive Projection;
- Authority;
- canonical inference;
- reconstruction semantics;
- Persistence.

Objetivo de diseño: que KCP resulte deliberadamente simple una vez resueltas correctamente las responsabilidades semánticas previas.

## 11. Roadmap colaborativo

### PHASE I — Boundary & Representation Foundation

```text
AR-1 Boundary Model
  ↓
AR-2 Representation Model
  ↓
AR-3 Binding Model
  ↓
Gate A — Architectural coherence
```

No pasar Gate A si KCA Representation duplica KOS Canonical Model o si KOS requiere dependencias KOS-Comm internas en vez de Bindings.

### PHASE II — Reconstruction Semantics

```text
AR-4 Reconstruction Model
  ↓
AR-5 KSCL Decomposition
  ↓
Gate B — Semantic/reconstruction coherence
```

No pasar mientras Reconstruction implique ambiguamente canonical reconstruction o KSCL oculte responsabilidades no diferenciadas.

### PHASE III — Encoding & Communication

```text
AR-6 Encoding
  ↓
AR-7 KCP
  ↓
Gate C — Protocol independence
```

No pasar si KCP contiene Knowledge, Projection, Authority o Reconstruction semantics.

### Gate C.5 — Neutrality Experiment

```text
Non-KOS System A
    ↓ Binding A
KCA Representation
    ↓ exchange
KCA Representation
    ↓ Binding B
Non-KOS System B
```

Debe demostrarse sin importar semánticas internas KOS.

### PHASE IV — KOS-Lab Adoption Experiments

Orden:

1. Observation Transfer.
2. ExecutionResult Transfer.
3. Cognitive Projection / KSCL Experiment.
4. Canonical Transfer Candidate — último y bajo autoridad explícita.

### Gate D — Natural KOS compatibility

No promover soluciones que requieran deformar dominios o invariantes de KOS-Lab.

### PHASE V — Selective Promotion

```text
Finding
  ↓
Evidence
  ↓
Reconciliation
  ↓
Proposal
  ↓
ADR / Programme / TST when applicable
  ↓
KOS-Lab Governance
  ↓
ACCEPT / REWORK / REJECT
```

## 12. Modelo operativo colaborativo

```text
READ
  KOS-Comm reads stabilized KOS-Lab contracts as authority.

EXPERIMENT
  KOS-Comm researches autonomously inside its experimental line.

EVIDENCE
  Results produce verifiable evidence, not implicit authority.

PROMOTE
  No result enters KOS-Lab without reconciliation and explicit governance.
```

Desarrollo paralelo:

```text
KOS-Lab stabilizes contracts
        ↓
KOS-Comm consumes contracts through bindings
        ↓
KOS-Comm experiments
        ↓
KOS-Comm produces evidence
        ↓
KOS-Lab selectively evaluates
```

KOS-Lab no espera a KOS-Comm. KOS-Comm no bloquea KOS-Lab.

## 13. Señales de acoplamiento incorrecto

STOP y reconciliar si aparece:

```text
Knowledge depends on KSCL
CognitiveProjection depends on KCP
CanonicalObject implements KCA Representation
KOS-Lab imports KOS-Comm implementation internals
KOS-Comm requires hidden KOS semantics beyond Binding
```

Forma preferente:

```text
KOS Component
    ↓
Explicit Binding
    ↓
KCA Contract
```

## 14. Gate 0

```text
GATE 0 — ARCHITECTURAL CONSENSUS
PASS
```

Significado: existe consenso suficiente para pasar de negociación meta-arquitectónica a investigación experimental reconciliada.

No significa:

- autorización de integración;
- modificación de baseline;
- promoción de KOS-Comm;
- sustitución de ADR/ARCH-DIR/gobernanza KOS-Lab.

## 15. Estado y siguiente acción

```text
KOS-Lab authority: PRESERVED
KOS-Comm autonomy: PRESERVED
Baseline impact: NONE
Integration: NOT AUTHORIZED / NOT REQUIRED YET
Collaboration: EXPLICIT BINDINGS + EVIDENCE + GOVERNED PROMOTION
```

Siguiente trabajo KOS-Comm:

```text
AR-1 — Boundary Model
```

Después AR-2 y AR-3, hasta Gate A.

KOS-Lab continúa su desarrollo independiente y proporciona, cuando proceda, contratos estabilizados que KOS-Comm podrá consumir experimentalmente mediante Bindings.

## 16. Regla de reentrada

Ante pérdida de contexto o duda arquitectónica sobre la relación KOS-Lab ↔ KOS-Comm:

1. consultar este documento;
2. consultar el charter autoritativo homólogo en `dev` de KOS-Lab;
3. verificar contratos KOS-Lab actuales antes de construir un Binding;
4. distinguir siempre evidencia experimental de autoridad;
5. no asumir integración ni promoción por mera compatibilidad técnica.

Este checkpoint cierra la ronda de reconciliación arquitectónica de 2026-07-21 y abre la fase de desarrollo paralelo colaborativo.