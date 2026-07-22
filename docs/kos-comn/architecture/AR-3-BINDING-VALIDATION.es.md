# AR-3 — Modelo de Binding — Validación, pasada 1

**Estado:** COMPLETE — PASS WITH REFINEMENT  
**Base:** `AR-3-BINDING-MODEL.es.md`  
**Objetivo:** someter el modelo inicial a los doce escenarios previstos y refinar responsabilidades, compatibilidad, política, correlación y composición.

## 1. Resultado global

```text
CASES: 12
PASS: 12
PASS WITHOUT CHANGE: 6
PASS WITH REFINEMENT: 6
CRITICAL CONTRADICTIONS: 0
REWORK OF CORE PREMISE: NO
```

El principio fundamental sobrevive:

```text
Binding = explicit bilateral semantic seam
bilateral != symmetric/reversible
mapping capability != domain authority
```

La validación exige, no obstante, varios refinamientos antes del cierre.

## 2. Caso 1 — KOS → KCA: observación parcial

Un contrato KOS estabilizado expone una observación parcial. El Binding la proyecta a AR-2 declarando cobertura `PARTIAL`, procedencia disponible y transiciones AR-1.

No es necesario importar semántica interna KOS al núcleo KCA.

```text
KOS contract
  ↓ Binding
AR-2 Representation
  coverage = PARTIAL
```

**PASS.**

Refuerzo: el Binding debe distinguir propiedades del dominio que no salen de aquellas que salen degradadas.

## 3. Caso 2 — KCA → KOS: resultado recibido sin importación canónica

Una representación recibida puede mapearse a un candidato orientado al dominio.

```text
Representation
  ↓ Binding
DomainFacingCandidate
```

El Binding no ejecuta importación canónica ni persistencia.

```text
receipt != canonical import
candidate != accepted state
```

**PASS.**

## 4. Caso 3 — No-KOS A → KCA → No-KOS B

Dos dominios independientes pueden utilizar Bindings propios:

```text
Domain A
 ↓ Binding A
KCA Representation
 ↓ exchange
KCA Representation
 ↓ Binding B
Domain B Candidate
```

No se requiere tipo KOS, identidad KOS ni autoridad KOS.

**PASS.**

Este caso confirma neutralidad conceptual de AR-3, pero no sustituye Gate C.5, que deberá aportar evidencia implementada/experimental.

## 5. Caso 4 — Identidad local entre espacios de nombres distintos

```text
A: namespace=A, identifier=17
B: namespace=B, identifier=alpha
```

El Binding puede mantener una correlación contextual explícita.

No puede afirmar identidad universal sólo por existencia de la correlación.

**PASS WITH REFINEMENT.**

Se introduce:

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

La `basis` explica por qué existe la correlación. No implica autoridad canónica.

## 6. Caso 5 — Capacidad crítica no soportada en entrada

Una capacidad AR-2 `REQUIRED_FOR_INTERPRETATION` no soportada por el Binding receptor impide producir interpretación de dominio válida.

Resultado refinado:

```text
status = UNMAPPABLE
reason = UNSUPPORTED_CAPABILITY
```

**PASS WITH REFINEMENT.**

Se concluye que `UNMAPPABLE` debe ser estado y la causa debe ir separada como diagnóstico. Esto evita inflar la enumeración de estados.

## 7. Caso 6 — Salida con pérdida declarada

Un dominio contiene propiedades A+B+C y la representación sólo conserva A+B.

El Binding debe declarar C como `DROPPED` o `TRANSFORMED_LOSSY` según corresponda.

```text
MAPPED_WITH_DEGRADATION
```

**PASS.**

No puede declararse `MAPPED` sin cualificación cuando la pérdida sea semánticamente relevante.

## 8. Caso 7 — Binding sólo OUTBOUND

Un Binding puede ser válido aunque sólo implemente salida.

```text
supported_directions = [OUTBOUND]
```

La ausencia de entrada no es defecto de conformidad si está declarada.

**PASS.**

Esto confirma que `binding_identity` no debe depender de bidireccionalidad.

## 9. Caso 8 — Binding bidireccional no reversible

Salida:

```text
rich domain state -> partial Representation
```

Entrada:

```text
partial Representation -> partial domain-facing candidate
```

No existe contradicción mientras las pérdidas estén declaradas.

**PASS.**

Se confirma:

```text
BIDIRECTIONAL != INVERTIBLE
```

## 10. Caso 9 — Contratos incompatibles

Si el Binding declara compatibilidad con dominio v2 y KCA contract range X, una entrada fuera de esos rangos no puede aceptarse por mero éxito sintáctico.

```text
status = UNSUPPORTED_CONTRACT
```

**PASS WITH REFINEMENT.**

Se separan dos niveles:

```text
STATIC/DECLARED COMPATIBILITY
RUNTIME SEMANTIC MAPPABILITY
```

La primera puede descartar incompatibilidad conocida antes de mapear; la segunda depende del contenido/capacidades concretas.

## 11. Caso 10 — Política local más estricta que KCA

KCA permite procedencia `UNDISCLOSED`, pero un Binding local exige `KNOWN`.

La representación sigue siendo conforme a AR-2, pero el Binding puede rechazarla:

```text
status = REJECTED_BY_BINDING_POLICY
reason = provenance_required
```

**PASS WITH REFINEMENT.**

La política pertenece conceptualmente a la frontera de Binding sólo cuando condiciona la posibilidad de mapear. Las decisiones de negocio/autoridad posteriores pertenecen al dominio.

Regla refinada:

```text
mapping admissibility policy -> Binding boundary
business/domain acceptance policy -> Domain authority
```

## 12. Caso 11 — Correlación sin autoridad de identidad

Una correlación persistente puede existir para continuidad de intercambios sin declarar equivalencia canónica.

**PASS WITH REFINEMENT.**

AR-3 no obliga a que el Binding sea el almacén de correlación.

Se distingue:

```text
Binding owns correlation semantics
Binding need not own correlation persistence
```

La persistencia puede delegarse en infraestructura auxiliar no autoritativa o en el dominio, según arquitectura concreta.

## 13. Caso 12 — Cadena de dos Bindings con degradación acumulada

```text
Domain A
 ↓ Binding A
Representation R1: property P degraded
 ↓ Binding B
Domain B Candidate
```

Binding B no puede restaurar P sin nueva base/evidencia.

Si introduce pérdida adicional Q:

```text
result losses = prior loss(P) + new loss(Q)
```

**PASS WITH REFINEMENT.**

Se introduce principio de monotonicidad conservadora de degradación:

```text
without new justified evidence:
semantic confidence/property strength MUST NOT increase across Binding chain
```

## 14. Refinamiento de BindingResult

La validación favorece separar `status` de `diagnostics/reasons`:

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Estados principales:

```text
MAPPED
MAPPED_WITH_DEGRADATION
UNMAPPABLE
REJECTED_BY_BINDING_POLICY
UNSUPPORTED_CONTRACT
```

Diagnósticos candidatos:

```text
UNSUPPORTED_CAPABILITY
INSUFFICIENT_CONTEXT
IDENTITY_UNRESOLVED
SEMANTIC_CONFLICT
POLICY_CONSTRAINT
CONTRACT_RANGE_MISMATCH
```

Por tanto, no se añade `INSUFFICIENT_INFORMATION` como estado principal: se expresa como `UNMAPPABLE + INSUFFICIENT_CONTEXT` cuando impide mapear.

## 15. Identidad del Binding

Resultado de validación:

`binding_identity` es obligatoria para un Binding que participe en despliegue, descubrimiento, compatibilidad, auditoría, correlación operacional o ciclo de vida.

Para una regla de mapeo embebida puramente local puede existir una realización sin identidad arquitectónica global.

Por tanto:

```text
BindingContract.binding_identity = REQUIRED
```

para entidades que se presenten como `BindingContract` interoperable.

No se exige identificador global universal; sí identidad inequívoca en su ámbito de interoperabilidad.

## 16. Política

Se resuelve parcialmente la cuestión abierta:

```text
Binding policy
    = semantic mapping admissibility

Domain policy
    = authoritative acceptance/action
```

Una política que decide si puede construirse un mapeo pertenece a la frontera. Una política que decide qué hacer con el resultado pertenece al dominio.

## 17. Compatibilidad

Modelo refinado:

```text
CompatibilityDescriptor {
    domain_contract_range
    kca_contract_range
    capability_profile?
    direction_constraints?
}
```

Dos niveles:

```text
DECLARED_COMPATIBILITY
    ↓
RUNTIME_MAPPABILITY
```

Ser compatible no garantiza que todo contenido concreto sea mapeable.

## 18. Composición de Bindings

La validación indica que la composición no debe suponerse cerrada automáticamente.

```text
Binding A compatible with intermediate X
Binding B compatible with intermediate X
```

no basta para afirmar que:

```text
A ∘ B = semantically safe
```

La composición debe considerar:

- capacidades requeridas;
- pérdidas acumuladas;
- correlaciones;
- ámbitos de identidad;
- políticas de admisibilidad;
- compatibilidad de contratos.

Se propone tratar `BindingComposition` como capacidad/objeto de validación, no como propiedad automática.

## 19. Dependencias entre reglas

AR-3 no necesita todavía un lenguaje universal de reglas.

Es suficiente exigir que una realización pueda declarar:

```text
preconditions
inputs/dependencies
produced semantics
losses/transitions
```

La sintaxis concreta queda fuera del modelo conceptual.

## 20. Ciclo de vida

La validación no demuestra que los estados `DECLARED/VALIDATED/ACTIVE/DEPRECATED/RETIRED` deban formar parte del núcleo semántico de Binding.

Decisión provisional:

- mantener ciclo de vida como metadato de gestión/gobernanza;
- no convertirlo todavía en invariante de conformidad AR-3.

## 21. Conformidad refinada

Un Binding conforme debe:

1. identificarse inequívocamente dentro de su ámbito interoperable;
2. declarar contratos/rangos enlazados;
3. declarar direcciones soportadas;
4. separar mapeo de autoridad;
5. producir candidato, no aceptación autoritativa, en entrada;
6. declarar pérdidas mediante AR-1;
7. respetar criticidad y degradación AR-2;
8. separar estado de resultado y causa diagnóstica;
9. no elevar propiedades sin nueva base explícita;
10. distinguir política de admisibilidad de política autoritativa de dominio;
11. tratar correlación como relación, no como autoridad de identidad;
12. no asumir composición segura por compatibilidad local;
13. separar compatibilidad declarada de mapeabilidad en ejecución;
14. permanecer independiente de codificación y transporte;
15. permitir realizaciones no-KOS.

## 22. Estado de cuestiones abiertas

| Cuestión | Resultado |
|---|---|
| identidad Binding | refinada: obligatoria para BindingContract interoperable |
| política local | frontera resuelta por admisibilidad vs autoridad |
| dependencias de reglas | metamodelo mínimo, sintaxis abierta |
| compatibilidad estática | parcialmente definida |
| correlación persistente | semántica sí; almacenamiento no obligatorio |
| UNMAPPABLE vs insuficiencia | insuficiencia pasa a diagnóstico |
| composición | requiere validación explícita |

## 23. Próxima pasada

Antes del cierre, realizar `AR-3 Refinement / Adversarial Pass 2` centrada en:

1. composición de Bindings;
2. conflicto entre correlaciones;
3. cambio de versión de contrato;
4. política que intenta asumir autoridad;
5. restauración de propiedad con evidencia local;
6. Binding con contexto semántico insuficiente;
7. identidad de Binding colisionante;
8. cadena no-KOS con capacidades parcialmente solapadas.

## 24. Resultado

```text
AR-3 VALIDATION PASS 1
    PASS WITH REFINEMENT

CORE PREMISE
    PRESERVED

NEXT
    AR-3 REFINEMENT / ADVERSARIAL PASS 2
```
