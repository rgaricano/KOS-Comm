# AR-1 — Boundary Model

**Estado:** ACTIVE — INITIAL MODEL  
**Fase:** I — Boundary & Representation Foundation  
**Línea:** KOS-Comm experimental (`KOS-Comn`)  
**Dependencia de autoridad KOS:** ninguna salvo contratos explícitos utilizados en futuros bindings  
**Objetivo:** establecer una semántica neutral y verificable de fronteras antes de definir Representation Model (AR-2) y Binding Model (AR-3).

## 1. Propósito

AR-1 define qué significa que información, responsabilidad, comunicación o autoridad atraviesen una frontera.

El modelo debe impedir que conceptos distintos queden implícitamente colapsados, especialmente:

```text
information transfer
communication
representation change
authority transfer
canonical import
```

La existencia de una transición en una dimensión no implica transición en las demás.

## 2. Principio fundamental

Una frontera no se modela únicamente por el mecanismo que transporta datos, sino por las propiedades semánticas que cambian o deben preservarse al atravesarla.

```text
Boundary Crossing
    =
Source Context
    + Transition
    + Preservation/Loss Rules
    + Destination Context
```

## 3. Tipos fundamentales de frontera

### 3.1 Domain Boundary

Marca cambio de dominio de responsabilidad o propiedad arquitectónica.

No implica necesariamente comunicación remota, cambio de representación ni transferencia de autoridad.

### 3.2 Information Boundary

Marca cambio explícito de representación, contexto de interpretación o forma informacional.

Puede existir localmente y sin transporte.

### 3.3 Communication Boundary

Marca intercambio mediante un mecanismo de comunicación entre participantes, componentes, procesos, nodos o sistemas.

No implica por sí mismo transferencia de autoridad.

### 3.4 Authority Boundary

Marca un punto donde autoridad, legitimidad, capacidad de decisión o incorporación canónica debe evaluarse explícitamente.

Atravesar una Authority Boundary requiere semántica de evaluación/autorización; no puede inferirse de recepción, transporte o reconstrucción.

## 4. Ortogonalidad inicial

```text
Domain Boundary        ⟂ Information Boundary
Information Boundary   ⟂ Communication Boundary
Communication Boundary ⟂ Authority Boundary
Reconstruction         ⟂ Authority
Receipt                ⟂ Canonical Import
```

La notación `⟂` expresa independencia conceptual, no imposibilidad de coexistencia.

Una operación concreta puede atravesar varias fronteras simultáneamente, pero cada dimensión debe declararse y verificarse por separado.

## 5. Invariantes iniciales

```text
Information Boundary != Communication Boundary
Communication Boundary != Authority Transfer
Receipt != Import
Transmission != Authority Transfer
Projection != Canonical Object
Observation != Canonical Serialization
Reconstruction != Authorization
Technical Compatibility != Authority
```

## 6. Boundary Vector

Hipótesis de trabajo para describir un cruce:

```text
B = <D, I, C, A>
```

donde:

```text
D = Domain Boundary crossed?
I = Information Boundary crossed?
C = Communication Boundary crossed?
A = Authority Boundary crossed?
```

Cada componente debe enriquecerse posteriormente con propiedades del cruce, no limitarse a booleanos.

Ejemplos preliminares:

```text
Local projection:
<D=0, I=1, C=0, A=0>

Remote observation transfer:
<D=?, I=1, C=1, A=0>

Canonical transfer candidate reception:
<D=?, I=1, C=1, A=1>
```

`D` depende de la distribución de responsabilidades de los participantes y no debe deducirse automáticamente de `C`.

## 7. Propiedades a preservar

AR-1 investigará qué propiedades pueden requerir preservación a través de una frontera:

- identity;
- semantic meaning;
- references;
- relations;
- provenance;
- evidence;
- ordering;
- context;
- revision/version;
- integrity;
- authority metadata;
- reconstruction guarantees.

La preservación de una propiedad no implica preservación de autoridad.

## 8. Pérdida y transformación

Todo cruce debe poder declarar, cuando proceda:

```text
PRESERVED
TRANSFORMED
DEGRADED
OMITTED
NOT_APPLICABLE
UNKNOWN
```

Esto permitirá posteriormente relacionar AR-1 con Representation (AR-2) y Reconstruction (AR-4).

## 9. Composition

Las fronteras pueden componerse.

Ejemplo:

```text
Source Domain
    ↓ Information Boundary
Representation
    ↓ Communication Boundary
Remote Representation
    ↓ Information Boundary
Destination Projection
```

La composición no debe ocultar Authority Boundaries.

Si existe una operación de importación canónica:

```text
Received Representation
    ↓ Assessment
Authority Boundary
    ↓ Explicit Authorization
Canonical Import
```

## 10. Neutralidad

AR-1 no puede depender de que los extremos sean KOS.

El modelo debe poder describir:

```text
System A
   ↓
Boundary/Representation
   ↓
Communication
   ↓
Boundary/Representation
   ↓
System B
```

sin introducir conceptos internos KOS como prerrequisitos ocultos.

Los bindings KOS serán una aplicación posterior del modelo, no su fundamento ontológico.

## 11. Relación con KOS-Lab

Cuando KOS-Comm interactúe con KOS-Lab:

```text
KOS stabilized contract
        ↓
Explicit Binding
        ↓
KCA Representation
```

AR-1 sólo define las fronteras y propiedades del cruce. AR-3 definirá el Binding.

No se utilizarán detalles accidentales de implementación KOS como base del Boundary Model.

## 12. Casos iniciales de validación

AR-1 deberá poder modelar al menos:

1. proyección local sin comunicación;
2. observación remota sin transferencia de autoridad;
3. resultado operacional remoto;
4. feedback recibido sin incorporación automática;
5. referencia a objeto canónico sin transferencia del objeto;
6. reconstrucción de una representación sin autoridad canónica;
7. transferencia entre dos sistemas no-KOS;
8. Canonical Transfer Candidate con Authority Boundary explícita.

## 13. Preguntas abiertas

- ¿Debe `Domain Boundary` modelarse como dimensión ortogonal o como contexto estructural del cruce?
- ¿Qué taxonomía mínima describe transformación semántica sin anticipar AR-2?
- ¿Cómo representar múltiples Authority Boundaries en una cadena de intermediarios?
- ¿Qué propiedades son end-to-end y cuáles hop-by-hop?
- ¿Cómo expresar pérdida conocida frente a pérdida no evaluada?
- ¿Cómo representar confianza sin confundirla con autoridad?
- ¿Qué relación formal debe existir entre Boundary Vector y futuros Reconstruction Fidelity Vectors?

## 14. Criterios preliminares de cierre AR-1

AR-1 podrá considerarse candidato a cierre cuando:

- las cuatro categorías de frontera estén definidas sin solapamiento ambiguo;
- exista modelo de composición;
- puedan declararse preservación, transformación y pérdida;
- Authority sea explícitamente independiente de receipt/communication/reconstruction;
- los casos iniciales sean modelables;
- un escenario no-KOS sea describible sin semántica KOS oculta;
- AR-2 pueda construirse encima sin redefinir qué es una frontera.

## 15. Relación con Gate A

AR-1 por sí solo no supera Gate A.

```text
AR-1 Boundary Model
        ↓
AR-2 Representation Model
        ↓
AR-3 Binding Model
        ↓
Gate A — Architectural Coherence
```

## 16. Estado

```text
Reconciliation KOS-Lab ↔ KOS-Comm: CLOSED
AR-1: ACTIVE
Boundary taxonomy: INITIALIZED
Boundary Vector: HYPOTHESIS
Composition model: INITIALIZED
Authority separation: REQUIRED INVARIANT
Non-KOS neutrality: REQUIRED
Next: refine AR-1 through validation cases and formal boundary semantics
```
