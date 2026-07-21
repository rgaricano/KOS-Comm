# AR-2 — Validación del modelo de representación — Pasada 1

**Estado:** ACTIVE — VALIDATION PASS 1 COMPLETE  
**Dependencia:** `AR-2-REPRESENTATION-MODEL.es.md`  
**Objetivo:** someter el modelo inicial a los 12 casos previstos y refinar taxonomía, capacidades semánticas y estructura común.

## 1. Resultado ejecutivo

Los doce casos iniciales son modelables, pero la validación muestra que una taxonomía rígida de clases no debe constituir el núcleo de AR-2.

Hallazgo principal:

```text
REPRESENTATION
    =
COMMON SEMANTIC CORE
    +
DECLARED CAPABILITIES
    +
OPTIONAL DOMAIN CLASSIFICATION
```

Por tanto, `representation_class` pasa de candidato a eje estructural a descriptor opcional/extensible.

`RepresentationEnvelope` se conserva como modelo lógico de referencia, no como formato obligatorio ni mensaje de protocolo.

## 2. Núcleo semántico mínimo candidato

Toda representación interoperable debe poder expresar, directa o indirectamente:

```text
RepresentationCore {
    representation_identity
    subject
    semantic_context
    provenance
    capabilities[]
    content
}
```

No todos los campos tienen que materializarse con la misma forma ni todos deben contener valor conocido. La capacidad de declarar `UNKNOWN`, `NOT_APPLICABLE` o ausencia justificada forma parte del modelo.

`references`, cobertura, temporalidad, derivación y garantías se modelan mejor como capacidades semánticas declaradas que como campos universales rígidos.

## 3. V1 — Referencia sin transferencia

```text
System A
  ↓
Representation R
  subject/reference → X
  content = reference semantics
  ↓
System B
```

Resultado: **PASS**.

Invariantes:

```text
reference(X) != transfer(X)
reference resolution != authority acquisition
```

Hallazgo: `REFERENCE` no necesita ser clase fundamental; puede expresarse mediante capacidad `REFERENCE_SEMANTICS` y contenido apropiado.

## 4. V2 — Observación parcial de estado

Una observación puede representar sólo un subconjunto de propiedades del sujeto.

Resultado: **PASS**.

Requiere:

```text
subject
semantic_context
coverage = PARTIAL
observed properties
provenance
```

Hallazgo: `OBSERVATION` resulta útil como clasificación descriptiva, pero la semántica esencial reside en procedencia + cobertura + contenido + contexto.

## 5. V3 — Resultado operacional

Un resultado puede referirse a una operación sin representar el estado completo del sujeto.

Resultado: **PASS**.

Debe distinguir:

```text
operation reference
result content
execution provenance
coverage/scope
```

`RESULT` puede mantenerse como clasificación extensible, no como requisito del núcleo.

## 6. V4 — Proyección local

```text
Domain Object X
   ↓ projection
Representation R
```

Resultado: **PASS**.

Requiere registrar relación de derivación y transformaciones/pérdidas relevantes.

```text
R != X
projection != canonical serialization
```

`PROJECTION` describe una relación de derivación más que una clase ontológica obligatoria.

## 7. V5 — Evidencia asociada a una afirmación

Se valida la necesidad de separar:

```text
CLAIM
EVIDENCE
VERIFICATION
GUARANTEE
```

Resultado: **PASS con refinamiento**.

Una afirmación es contenido declarativo. Evidencia es información que puede sustentar o refutar una afirmación. Verificación es un resultado de evaluación. Garantía es una propiedad cuyo nivel y alcance deben estar explícitamente declarados.

No deben colapsarse en un único estado `VERIFIED GUARANTEE`.

## 8. V6 — Propuesta sin autoridad de incorporación

Resultado: **PASS**.

```text
proposal representation
    !=
authorized state change
```

Una representación puede declarar intención/propuesta, pero la autoridad de incorporación permanece fuera de AR-2.

`PROPOSAL` puede ser clasificación de dominio/extensión.

## 9. V7 — Representación derivada con pérdida conocida

Resultado: **PASS**.

Requiere:

```text
derivation relation
PropertyTransition = TRANSFORMED_LOSSY
affected property/scope
provenance chain
```

Confirma la integración con AR-1 sin duplicar sus estados de transición.

## 10. V8 — Representación reconstruible

Resultado: **PASS con límite**.

AR-2 puede declarar información/capacidad de reconstrucción y referencias necesarias, pero no define el algoritmo ni garantiza por sí mismo reconstrucción efectiva.

```text
reconstruction metadata != reconstruction proof
reconstructable claim != authority
```

AR-4 mantiene la responsabilidad semántica detallada.

## 11. V9 — Representación compuesta

Resultado: **PASS**.

Una composición debe conservar cuando corresponda:

- identidad de componentes;
- relaciones;
- procedencia individual;
- garantías/limitaciones individuales.

Hallazgo: `COMPOSITE` se modela mejor como capacidad estructural `COMPOSITION` que como clase fundamental.

## 12. V10 — No-KOS ↔ No-KOS

```text
System A
 ↓ Binding A
Representation
 ↓ KCA
Representation
 ↓ Binding B
System B
```

Resultado: **PASS conceptual**.

Ningún elemento del núcleo candidato exige tipos internos KOS.

Esto mantiene la neutralidad conceptual, sin sustituir la prueba experimental de Gate C.5.

## 13. V11 — Una representación, dos codificaciones

```text
Representation R
   ├── Encoding E1
   └── Encoding E2
```

Resultado: **PASS**.

Confirma:

```text
representation identity != encoding identity
semantic representation != encoded form
```

AR-6 puede operar sin redefinir AR-2.

## 14. V12 — Dos representaciones del mismo sujeto

```text
Subject X
  ├── R1
  └── R2
```

Resultado: **PASS**.

Confirma:

```text
representation_identity != subject_identity
```

R1 y R2 pueden diferir en cobertura, contexto, procedencia, temporalidad, fidelidad y finalidad.

## 15. Refinamiento de taxonomía

La taxonomía inicial:

```text
REFERENCE
OBSERVATION
STATE
EVENT
RESULT
PROJECTION
DESCRIPTION
PROPOSAL
EVIDENCE
TRANSFER_CANDIDATE
COMPOSITE
```

no se estabiliza como enumeración cerrada.

Se reclasifica como **vocabulario descriptivo/extensible**.

Razones:

1. varias categorías describen finalidad (`PROPOSAL`);
2. otras describen relación de derivación (`PROJECTION`);
3. otras describen estructura (`COMPOSITE`);
4. otras describen contenido (`STATE`, `EVENT`, `RESULT`);
5. `TRANSFER_CANDIDATE` está demasiado próximo a una semántica de flujo/gobernanza y no debe formar parte del núcleo neutral.

## 16. Modelo de capacidades semánticas

Se propone investigar como eje principal:

```text
Capabilities {
    SUBJECT_IDENTIFICATION
    REFERENCE_SEMANTICS
    PROVENANCE
    DERIVATION
    COVERAGE
    TEMPORALITY
    RELATIONSHIPS
    COMPOSITION
    PROPERTY_CLAIMS
    EVIDENCE_LINKAGE
    VERIFICATION_STATEMENTS
    RECONSTRUCTION_INFORMATION
}
```

La lista sigue abierta.

Una representación declara las capacidades que utiliza; el receptor puede determinar cuáles entiende, requiere o ignora de forma segura.

## 17. Afirmación, evidencia, verificación y garantía

Refinamiento candidato:

```text
Claim
    = proposición declarada por una representación

Evidence
    = información relacionada que puede sustentar/refutar una Claim

Verification
    = resultado de un procedimiento de evaluación declarado

Guarantee
    = compromiso/propiedad declarada con alcance y base explícitos
```

Reglas:

```text
claim != evidence
evidence != verification
verification != authority
guarantee != authority
```

Una garantía sin alcance o base declarada es semánticamente insuficiente.

## 18. Procedencia

Resultado de validación:

La procedencia es una capacidad fundamental para interoperabilidad robusta, pero puede contener valores desconocidos o deliberadamente no revelados.

Por tanto:

```text
provenance capability: CORE
provenance completeness: VARIABLE
```

No debe confundirse ausencia de procedencia conocida con procedencia falsa.

## 19. Cobertura / completitud

Se conserva:

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

pero como semántica de capacidad `COVERAGE`.

Regla normativa candidata:

```text
COMPLETE requires declared scope
```

## 20. Identidad del sujeto

AR-2 no impondrá inicialmente un identificador global universal.

El sujeto podrá identificarse mediante un descriptor que incluya un espacio de nombres/contexto suficiente.

Hipótesis:

```text
SubjectDescriptor {
    identifier?
    namespace_or_context?
    scope?
    qualifiers?
}
```

El Binding de AR-3 resolverá mapeos con identidades específicas de dominio.

## 21. Estado de RepresentationEnvelope

Después de los doce casos:

```text
RepresentationEnvelope
    = LOGICAL REFERENCE MODEL
    != MANDATORY WIRE FORMAT
    != KCP MESSAGE
    != SERIALIZATION SCHEMA
```

Puede utilizarse para razonar y construir pruebas, pero AR-6/AR-7 no quedan obligados a serializar literalmente esta estructura.

## 22. Decisión provisional: estructura común vs capacidades

La validación favorece un modelo híbrido:

```text
MINIMAL COMMON CORE
        +
SEMANTIC CAPABILITIES
        +
EXTENSIBLE CLASSIFICATION
```

frente a:

```text
ONE RIGID UNIVERSAL ENVELOPE
```

Esto reduce acoplamiento, mejora neutralidad y permite que sistemas con diferentes necesidades intercambien sólo la semántica necesaria.

## 23. Cuestiones pendientes tras Pass 1

- definir con precisión qué elementos pertenecen al núcleo mínimo;
- decidir obligatoriedad de `representation_identity` en representaciones efímeras;
- formalizar negociación/ignorabilidad segura de capacidades sin invadir AR-7;
- determinar semántica mínima de `SubjectDescriptor`;
- formalizar relaciones entre Claim/Evidence/Verification/Guarantee;
- comprobar que extensiones de dominio no contaminan el núcleo;
- validar el modelo híbrido con escenarios de degradación y composición más complejos.

## 24. Estado

```text
12 validation cases:             PASS / PASS WITH REFINEMENT
Rigid class taxonomy:            REJECTED AS CORE
Extensible classification:       RETAINED
Minimal common core:              CANDIDATE
Semantic capabilities:            PRIMARY CANDIDATE
RepresentationEnvelope:           LOGICAL REFERENCE MODEL
Authority separation:             PRESERVED
AR-1 compatibility:               PRESERVED
Non-KOS conceptual neutrality:    PRESERVED
AR-6 separation:                  PRESERVED
```

## 25. Siguiente acción

Realizar `AR-2 Refinement Pass 2` centrado en:

1. núcleo semántico mínimo;
2. capacidades y reglas de extensibilidad;
3. SubjectDescriptor;
4. Claim/Evidence/Verification/Guarantee;
5. reglas de interoperabilidad y degradación segura;
6. criterios de cierre AR-2.
