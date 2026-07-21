# AR-1 — Boundary Model — Validation Matrix

**Estado:** ACTIVE — VALIDATION PASS 1  
**Relacionado:** `AR-1-BOUNDARY-MODEL.es.md`  
**Objetivo:** someter la taxonomía de fronteras a casos heterogéneos antes de estabilizar AR-1.

## 1. Decisión de modelado: Domain Boundary

`Domain Boundary` se conserva como dimensión del Boundary Vector, pero su valor no se deduce de topología, proceso, host, red ni transporte.

```text
D = change of architectural responsibility/ownership context
```

Por tanto:

```text
remote != domain change
local != same domain
process change != domain change
transport != domain change
```

Esta decisión permite que D sea ortogonal a I/C/A sin reducirlo a una propiedad física.

## 2. Boundary Descriptor

El vector booleano inicial se amplía conceptualmente a un descriptor:

```text
BoundaryDescriptor {
    domain:        BoundaryState,
    information:   BoundaryState,
    communication: BoundaryState,
    authority:     BoundaryState,
    preservation:  PropertyTransitionSet,
    scope:         BoundaryScope,
    confidence:    AssessmentConfidence
}
```

`BoundaryState` provisional:

```text
NO_CROSSING
CROSSING
CONDITIONAL
UNKNOWN
```

El vector compacto `<D,I,C,A>` permanece útil como resumen, pero no constituye el modelo completo.

## 3. Boundary Scope

Se introduce la distinción:

```text
HOP_BY_HOP
END_TO_END
LOCAL_TRANSFORMATION
```

Una propiedad puede preservarse hop-by-hop y perderse end-to-end, o viceversa mediante reconstrucción/reintroducción explícita.

La semántica de preservación debe declarar su scope.

## 4. Property Transition

Para cada propiedad relevante:

```text
PropertyTransition {
    property
    state
    source_semantics
    destination_semantics
    scope
    evidence
}
```

Estados:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DEGRADED
OMITTED
NOT_APPLICABLE
UNKNOWN
```

Se sustituye el `TRANSFORMED` genérico por dos estados diferenciados: transformación equivalente y transformación con pérdida.

`UNKNOWN` significa que no existe evidencia suficiente para clasificar la transición; no equivale a pérdida.

## 5. Trust y Authority

Trust no se incorpora como quinta frontera.

Se trata como una evaluación contextual sobre participantes, evidencia, canal o representación.

```text
Trust != Authority
Trust != Authenticity
Authenticity != Authority
Integrity != Authority
```

Una representación puede ser auténtica e íntegra y, aun así, carecer de autoridad para modificar estado canónico.

## 6. Authority Boundary encadenada

Una ruta puede contener múltiples puntos de autoridad:

```text
Source
  ↓
Authority Check A
  ↓
Representation
  ↓
Communication
  ↓
Authority Check B
  ↓
Assessment
  ↓
Authority Check C
  ↓
Canonical Import
```

Por tanto, `A=1` en el vector compacto sólo indica presencia de al menos una Authority Boundary en el segmento descrito.

Para análisis preciso se requiere:

```text
authority_boundaries[]
```

con identidad, función, decisión y alcance de cada evaluación.

## 7. Caso V1 — Proyección local

```text
Canonical/Source State
        ↓ projection
Local Consumer Representation
```

Clasificación:

```text
D = 0
I = 1
C = 0
A = 0
```

Propiedades esperables:

```text
identity        PRESERVED or TRANSFORMED_EQUIVALENT
semantics       PRESERVED / deliberately projected
provenance      PRESERVED
context         potentially DEGRADED
canonicality    NOT TRANSFERRED
```

Resultado: modelable.

## 8. Caso V2 — Observación remota

```text
Observed State
    ↓ representation
Observation
    ↓ communication
Remote Consumer
```

Clasificación típica:

```text
D = CONDITIONAL
I = 1
C = 1
A = 0
```

Invariante:

```text
remote receipt != authority acquisition
```

Resultado: modelable.

## 9. Caso V3 — Resultado operacional remoto

```text
Execution
   ↓
Operational Result
   ↓ communication
Remote Assessor
```

```text
D = CONDITIONAL
I = 1
C = 1
A = 0
```

El resultado puede generar posteriormente feedback o propuesta, pero esa transición constituye otro segmento y puede introducir nuevas fronteras.

```text
Operational Result
    !=
Knowledge Change
```

Resultado: modelable.

## 10. Caso V4 — Feedback sin incorporación

```text
Remote Feedback
    ↓ communication
Receiver
    ↓ assessment
Local Feedback State
```

Segmento de recepción:

```text
I = 1
C = 1
A = 0
```

Si posteriormente se pretende modificar conocimiento/estado autoritativo:

```text
Feedback
   ↓
Authority Boundary
   ↓ explicit authorization
Canonical Change
```

Resultado: modelable y demuestra necesidad de segmentación.

## 11. Caso V5 — Referencia canónica

```text
Canonical Object
    ↓ reference projection
REFERENCE Representation
    ↓ optional communication
Consumer
```

La referencia preserva identidad referencial sin transferir el objeto.

```text
reference identity != object transfer
object addressability != object authority
```

Resultado: modelable.

## 12. Caso V6 — Reconstruction sin autoridad

```text
Representation
    ↓ decode/reconstruct
Reconstructed Semantic Object
```

```text
I = 1
C = 0 or previous segment
A = 0
```

Incluso reconstrucción exacta:

```text
exact reconstruction != canonical authority
```

Resultado: modelable.

## 13. Caso V7 — Non-KOS A ↔ Non-KOS B

```text
System A Domain Model
    ↓ Binding A
Neutral Representation
    ↓ Exchange
Neutral Representation
    ↓ Binding B
System B Domain Model
```

No requiere conceptos `CanonicalObject`, `CognitiveProjection`, `KnowledgeChangeProposal` ni otros tipos internos KOS.

Clasificación típica del segmento de intercambio:

```text
D = 1
I = 1
C = 1
A = 0 or CONDITIONAL
```

`A` depende del uso de destino, no del intercambio por sí mismo.

Resultado: modelable y compatible con requisito de neutralidad.

## 14. Caso V8 — Canonical Transfer Candidate

```text
Authoritative Source
    ↓ candidate representation
Transfer Candidate
    ↓ communication
Receiver
    ↓ assessment
Authority Boundary
    ↓ authorization
Canonical Import
```

Debe segmentarse:

### Segment A — representación/transporte

```text
I = 1
C = 1
A = 0
```

### Segment B — evaluación/importación

```text
I = potentially 1
C = 0 or independent
A = 1
```

Invariantes:

```text
Receipt != Canonical Import
Candidate != Canonical Object
Reconstruction != Authorization
```

Resultado: modelable. La segmentación evita atribuir autoridad al transporte.

## 15. Caso V9 — Relay/intermediario

```text
Source
  ↓
Relay A
  ↓
Relay B
  ↓
Destination
```

La ruta debe poder expresar propiedades:

- hop-by-hop integrity;
- end-to-end identity;
- end-to-end provenance;
- transformations introducidas por relay;
- authority checks intermedios;
- transport changes.

Conclusión: un único vector global es insuficiente para rutas complejas.

Se introduce:

```text
BoundaryPath = ordered BoundarySegment[]
```

## 16. Boundary Segment

Modelo provisional:

```text
BoundarySegment {
    source_context
    destination_context
    descriptor
    property_transitions[]
    authority_boundaries[]
}
```

Y:

```text
BoundaryPath {
    segments[]
    end_to_end_properties[]
}
```

Esto permite composición sin perder información de cada salto o transformación.

## 17. Hallazgos de Validation Pass 1

1. El vector `<D,I,C,A>` es útil como resumen, pero insuficiente como representación completa.
2. Domain Boundary debe depender de responsabilidad arquitectónica, no de localización física.
3. Los casos complejos requieren segmentación ordenada.
4. Authority Boundary puede aparecer múltiples veces en una ruta.
5. Trust debe mantenerse separado de Authority.
6. `UNKNOWN` debe diferenciarse de pérdida conocida.
7. Transformación equivalente debe distinguirse de transformación lossy.
8. Preservation necesita scope hop-by-hop/end-to-end/local.
9. Canonical Transfer Candidate confirma que transporte y autoridad deben modelarse en segmentos distintos.
10. El caso no-KOS no requiere semántica interna KOS, por lo que la taxonomía inicial supera una primera prueba de neutralidad conceptual.

## 18. Riesgos abiertos

- Sobremodelar AR-1 e invadir AR-2 Representation Model.
- Introducir prematuramente tipos de payload dentro de BoundaryDescriptor.
- Confundir evidence de preservación con Evidence como futura clase semántica de representación.
- Convertir Trust en autoridad indirecta.
- Modelar Domain Boundary según despliegue físico en lugar de ownership/responsibility.

## 19. Próximo refinamiento

Antes de cerrar AR-1:

1. formalizar semántica de `BoundarySegment` y `BoundaryPath`;
2. fijar reglas mínimas de composición;
3. definir qué información pertenece a AR-1 y qué debe delegarse a AR-2;
4. elaborar tabla de combinaciones D/I/C/A válidas y ejemplos;
5. revisar criterios de cierre AR-1 contra los nueve casos de validación.
