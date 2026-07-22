# AR-3 — Modelo de Binding — Enfrentamientos adversariales, pasada 2

**Estado:** COMPLETE — PASS WITH FINAL REFINEMENT  
**Base:** AR-3 Initial Model + Validation Pass 1

## 1. Resultado

```text
ADVERSARIAL CASES: 8
PASS: 8
CRITICAL CONTRADICTIONS: 0
CORE REWORK: NO
FINAL REFINEMENTS REQUIRED: YES
CLOSURE CANDIDATE: YES
```

## 2. Enfrentamiento A — Composición con degradación acumulada

Cadena:

```text
Domain A
 ↓ Binding A
R1: P=TRANSFORMED_LOSSY
 ↓ Binding B
R2/DomainCandidate: Q=DROPPED
```

La composición no puede ocultar P ni Q. El resultado compuesto debe conservar la trazabilidad de transiciones relevantes.

Se estabiliza:

```text
CompositionTransitionSet
    = inherited transitions
    + local transitions
    + explicitly justified restorations
```

Una restauración justificada no borra el historial de degradación previo.

**PASS.**

## 3. Enfrentamiento B — Correlaciones conflictivas

Dos fuentes declaran:

```text
A: subject-17 ↔ B: alpha
A: subject-17 ↔ B: beta
```

sin base que permita relación uno-a-varios.

El Binding no puede escoger silenciosamente.

Resultado:

```text
UNMAPPABLE
+ SEMANTIC_CONFLICT
```

salvo que ámbito/basis permitan resolver explícitamente la aparente contradicción.

Se introduce regla:

```text
correlation conflict MUST remain explicit
unless resolved by declared scope/basis/authority external to Binding semantics
```

El Binding puede aplicar una regla de resolución declarada, pero esa regla no crea autoridad canónica por sí misma.

**PASS.**

## 4. Enfrentamiento C — Transición de versión contractual

Binding B declara:

```text
domain_contract_range = [2.x]
```

El dominio evoluciona a 3.0 con cambio semántico incompatible.

El Binding no puede asumir compatibilidad por similitud estructural.

Resultado:

```text
UNSUPPORTED_CONTRACT
+ CONTRACT_RANGE_MISMATCH
```

Si existe adaptador/version bridge explícito, éste debe declarar su propia transformación y pérdidas.

Regla estabilizada:

```text
version compatibility is semantic and declared
not inferred from shape or parse success
```

**PASS.**

## 5. Enfrentamiento D — Política intentando asumir autoridad

Una política de Binding declara:

```text
if provenance=KNOWN -> automatically persist as canonical
```

Esto excede la admisibilidad de mapeo y invade autoridad de dominio.

Resultado:

```text
NON-CONFORMANT BINDING POLICY
```

AR-3 estabiliza:

```text
Binding policy MAY decide whether mapping is admissible
Binding policy MUST NOT decide authoritative domain acceptance/action by implication
```

Una implementación puede invocar posteriormente una API autoritativa del dominio, pero esa invocación es una operación separada y gobernada por el contrato del dominio.

**PASS.**

## 6. Enfrentamiento E — Restauración con evidencia local adicional

Entrada:

```text
Representation: property P = UNKNOWN
```

El Binding dispone de fuente local independiente E que permite verificar P.

Puede producir:

```text
P = VERIFIED
```

sólo si registra explícitamente:

- la nueva evidencia/base;
- el ámbito de la verificación;
- la transición;
- la procedencia pertinente.

La restauración no se atribuye a la representación recibida.

Se estabiliza:

```text
PROPERTY STRENGTH MAY INCREASE
IFF new independent justified basis is introduced and declared
```

**PASS.**

## 7. Enfrentamiento F — Contexto semántico insuficiente

Una representación contiene contenido estructuralmente válido pero carece del contexto requerido por una capacidad necesaria.

Resultado:

```text
UNMAPPABLE
+ INSUFFICIENT_CONTEXT
```

El Binding no debe rellenar contexto mediante suposiciones implícitas.

Puede obtener contexto externo únicamente si la fuente y la regla de incorporación están declaradas.

**PASS.**

## 8. Enfrentamiento G — Colisión de identidad de Binding

Dos Bindings se presentan con la misma identidad dentro del mismo ámbito interoperable pero contratos/reglas incompatibles.

La identidad deja de ser inequívoca.

Resultado:

```text
BINDING IDENTITY COLLISION
-> compatibility/discovery failure
```

No se selecciona uno arbitrariamente.

Se refina:

```text
binding_identity uniqueness requirement
    = unique within declared interoperability scope
```

La detección concreta pertenece a despliegue/registro/gobernanza, pero AR-3 exige que la ambigüedad no sea tratada como conformidad válida.

**PASS.**

## 9. Enfrentamiento H — Cadena no-KOS con capacidades parcialmente solapadas

```text
Domain A Binding
 supports {X,Y,Z}

KCA Representation
 declares X=REQUIRED_FOR_INTERPRETATION
          Y=OPTIONAL
          Z=OPTIONAL

Domain B Binding
 supports {X,Y}
```

Z puede ignorarse si su criticidad y dependencias permiten degradación segura.

Si Z fuera `REQUIRED_FOR_INTERPRETATION`, el resultado sería `UNMAPPABLE`.

No aparece ninguna necesidad de tipos KOS.

**PASS.**

Este enfrentamiento refuerza la neutralidad conceptual y la utilidad de la criticidad AR-2.

## 10. Modelo refinado de composición

Se propone como candidato de cierre:

```text
BindingCompositionAssessment {
    participants[]
    contract_compatibility
    capability_coverage
    identity_scope_consistency
    correlation_consistency
    accumulated_property_transitions[]
    admissibility_constraints[]
    result
    diagnostics[]
}
```

No implica que KCA necesite un motor universal de composición. Define qué debe evaluarse cuando una arquitectura compone Bindings.

## 11. Restauración y monotonicidad

La regla final queda:

```text
DEFAULT:
property strength is conservatively monotonic non-increasing
across transformations

EXCEPTION:
property strength may increase only with
new + independent + explicit + scoped justification/evidence
```

La nueva base debe quedar atribuida al punto que realiza la restauración.

## 12. Correlación

`CorrelationDescriptor` queda como:

```text
CorrelationDescriptor {
    correlation_id?
    relation
    endpoints[]
    scope
    basis?
    validity?
}
```

Reglas:

```text
correlation != identity authority
conflict != implicit resolution
persistence != Binding semantic ownership requirement
```

## 13. Política

Frontera estabilizada:

```text
MAPPING ADMISSIBILITY
        -> Binding

AUTHORITATIVE ACCEPTANCE / PERSIST / EXECUTE
        -> Domain
```

## 14. Compatibilidad

Se estabilizan dos etapas:

```text
DECLARED CONTRACT COMPATIBILITY
        ↓
RUNTIME SEMANTIC MAPPABILITY
```

Ninguna sustituye a la otra.

## 15. Identidad del Binding

Para `BindingContract` interoperable:

```text
binding_identity = REQUIRED
unique within declared interoperability scope
```

No se exige identidad global universal.

## 16. Evaluación frente a invariantes

| Invariante | Resultado |
|---|---|
| bilateral ≠ reversible | PASS |
| mapping ≠ authority | PASS |
| candidate ≠ accepted state | PASS |
| receipt ≠ canonical import | PASS |
| identity mapping ≠ identity authority | PASS |
| degradación no se eleva silenciosamente | PASS |
| restauración exige nueva base | PASS |
| compatibilidad declarada ≠ mapeabilidad | PASS |
| composición no asumida | PASS |
| política Binding ≠ autoridad dominio | PASS |
| neutralidad no-KOS | PASS |
| separación de transporte/codificación | PASS |

## 17. Riesgos residuales

No bloqueantes para el modelo conceptual:

1. estrategia concreta de descubrimiento/registro de Bindings;
2. sintaxis de reglas de mapeo;
3. almacenamiento de correlaciones;
4. negociación de perfiles de capacidades;
5. estrategia concreta de versionado y migración;
6. instrumentación de evidencia para restauraciones;
7. implementación de evaluación de composición.

Estos elementos pertenecen a diseño/implementación posterior o a AR subsiguientes, salvo que nueva evidencia obligue a reabrir AR-3.

## 18. Recomendación de cierre

Los ocho enfrentamientos adversariales preservan el núcleo.

```text
AR-3
  Initial Model        COMPLETE
  Validation Pass 1    PASS WITH REFINEMENT
  Adversarial Pass 2   PASS WITH FINAL REFINEMENT

RECOMMENDATION:
  PRODUCE AR-3 CLOSURE
  THEN EVALUATE GATE A
```
