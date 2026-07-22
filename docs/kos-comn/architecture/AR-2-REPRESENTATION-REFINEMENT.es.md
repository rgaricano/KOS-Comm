# AR-2 — Modelo de representación — Refinamiento, pasada 2

**Estado:** ACTIVE — REFINEMENT PASS 2 COMPLETE  
**Predecesor:** `AR-2-REPRESENTATION-VALIDATION.es.md`  
**Objetivo:** estabilizar el candidato de núcleo semántico, capacidades, identidad del sujeto, afirmaciones/evidencia y degradación segura antes de proponer cierre de AR-2.

## 1. Decisión estructural

Se adopta como candidato de cierre:

```text
REPRESENTATION
    =
MINIMAL SEMANTIC CORE
    +
DECLARED SEMANTIC CAPABILITIES
    +
OPTIONAL EXTENSIBLE CLASSIFICATION
```

Una representación no queda definida principalmente por una clase cerrada, sino por un núcleo interpretable y por las capacidades semánticas que declara.

## 2. Núcleo semántico mínimo refinado

```text
RepresentationCore {
    subject
    semantic_context
    capabilities[]
    content

    representation_identity?
    provenance?
    classification?
}
```

### Obligatorio conceptualmente

- `subject`: qué es representado, incluso cuando sólo pueda describirse de manera contextual;
- `semantic_context`: marco mínimo necesario para interpretar el contenido;
- `capabilities[]`: semánticas adicionales de las que depende la interpretación;
- `content`: información representada.

### Condicional

- `representation_identity`: obligatoria cuando la representación necesita ser referenciada, correlacionada, versionada, compuesta, derivada o auditada; puede omitirse en representaciones efímeras autocontenidas;
- `provenance`: la capacidad de procedencia pertenece al modelo fundamental, pero el dato puede ser `UNKNOWN`, `UNDISCLOSED` o `NOT_APPLICABLE` según contexto;
- `classification`: descriptor extensible y no normativo para el núcleo.

## 3. Regla de identidad de representación

```text
IF representation participates in
    reference
    correlation
    derivation
    composition
    versioning
    audit/evidence linkage
THEN representation_identity REQUIRED
ELSE MAY be ephemeral/unidentified
```

Nunca:

```text
representation_identity == subject_identity
```

por implicación automática.

## 4. SubjectDescriptor

Se refina a:

```text
SubjectDescriptor {
    identifier?
    namespace?
    semantic_type?
    scope?
    qualifiers{}
}
```

Reglas:

1. no existe requisito de identificador global universal;
2. `identifier` sólo es interpretable dentro de un `namespace`, contexto acordado o Binding cuando pueda existir ambigüedad;
3. `semantic_type` es extensible y no debe importar tipos internos de KOS al núcleo;
4. `scope` delimita el dominio en el que la identificación pretende ser válida;
5. `qualifiers` aportan desambiguación sin convertirse en identidad canónica implícita.

Un Binding puede resolver:

```text
DomainIdentity
    ↕
SubjectDescriptor
```

sin transferir autoridad de identidad al núcleo KCA.

## 5. Capacidades: semántica y criticidad

Una capacidad se describe conceptualmente mediante:

```text
SemanticCapability {
    capability_id
    criticality
    semantics_reference?
    parameters?
}
```

`semantics_reference` no obliga a una URI ni a un registro central; representa cualquier mecanismo acordado para identificar inequívocamente la semántica.

### Criticidad

```text
REQUIRED_FOR_INTERPRETATION
REQUIRED_FOR_DECLARED_PROPERTY
OPTIONAL
INFORMATIONAL
```

Esto evita el error de considerar que toda capacidad desconocida puede ignorarse.

## 6. Regla de comprensión

Para una representación R y receptor B:

```text
for capability C in R:

    if C is REQUIRED_FOR_INTERPRETATION
       and B does not understand C:
           R MUST NOT be interpreted as semantically valid

    if C is REQUIRED_FOR_DECLARED_PROPERTY
       and B does not understand C:
           affected property MUST be downgraded to UNKNOWN/UNVERIFIED

    if C is OPTIONAL or INFORMATIONAL
       and B does not understand C:
           B MAY continue if core semantics remain intact
```

Principio:

```text
unknown capability
    !=
safe-to-ignore capability
```

## 7. Degradación segura

La degradación sólo es válida cuando el receptor puede identificar explícitamente qué semántica pierde.

```text
FULL INTERPRETATION
       ↓ unsupported non-critical capability
DEGRADED INTERPRETATION
       ↓
DECLARED LOSS
```

Nunca:

```text
UNSUPPORTED REQUIRED SEMANTICS
       ↓
SILENT ACCEPTANCE
```

Estados conceptuales candidatos:

```text
FULL
DEGRADED
UNINTERPRETABLE
```

Estos estados describen interpretación, no entrega de transporte ni autoridad.

## 8. Propagación de propiedades bajo degradación

Si una propiedad depende de una capacidad no comprendida:

```text
Property P
 depends_on Capability C

C unsupported
    ↓
P cannot retain VERIFIED/GUARANTEED status
```

La degradación debe ser conservadora:

```text
known -> unknown
verified -> unverified
complete -> partial/unknown
```

pero nunca promover:

```text
unknown -> known
unverified -> verified
partial -> complete
```

sin evidencia adicional.

## 9. Afirmación, evidencia, verificación y garantía

Modelo refinado:

```text
Claim {
    claim_id?
    proposition
    scope
    issuer_or_provenance?
}

EvidenceLink {
    claim_ref
    evidence_ref
    relation
}

VerificationStatement {
    claim_ref
    method_or_basis
    result
    scope
    verifier_or_provenance?
}

GuaranteeStatement {
    property
    scope
    basis
    issuer_or_provenance
    conditions?
}
```

Relaciones:

```text
Evidence MAY support/refute Claim
Verification evaluates Claim or property
Guarantee declares bounded commitment/property
```

Ninguna de ellas confiere autoridad sobre el sujeto representado.

## 10. Resultados de verificación

AR-2 no impone todavía un vocabulario universal exhaustivo, pero requiere distinguir al menos:

```text
VERIFIED
REFUTED
INCONCLUSIVE
NOT_VERIFIED
UNKNOWN
```

El método/base y el ámbito forman parte de la semántica necesaria para interpretar el resultado.

## 11. Procedencia

Modelo conceptual refinado:

```text
ProvenanceDescriptor {
    source?
    producer?
    derivation_chain?
    observed_or_created_at?
    disclosure_state
}
```

`disclosure_state` permite distinguir:

```text
KNOWN
PARTIAL
UNKNOWN
UNDISCLOSED
NOT_APPLICABLE
```

No se infiere falsedad a partir de `UNKNOWN` o `UNDISCLOSED`.

## 12. Cobertura

```text
CoverageDescriptor {
    state
    scope
    omitted_or_unknown_aspects?
}
```

Estados:

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

Regla:

```text
COMPLETE_FOR_SCOPE requires explicit scope
```

## 13. Extensiones de dominio

Una extensión puede añadir:

- nuevas capacidades;
- nuevas clasificaciones;
- nuevos tipos semánticos;
- parámetros específicos.

No puede redefinir silenciosamente:

- identidad de representación;
- separación sujeto/representación;
- criticidad;
- semántica de degradación;
- autoridad;
- reglas de propagación conservadora.

Regla:

```text
DOMAIN EXTENSION
    may extend
    must not silently override CORE SEMANTICS
```

## 14. Protección de neutralidad

El núcleo no contiene:

- `KnowledgeObject`;
- `CanonicalState`;
- `ExecutionResult` KOS específico;
- `Projection` KOS específica;
- autoridad de importación;
- persistencia canónica;
- semántica de ejecución KOS.

Estos conceptos pueden mapearse mediante Binding o extensiones cuando corresponda.

## 15. Composición

Una representación compuesta no puede elevar las propiedades de sus componentes por mera agregación.

```text
CompositeGuarantee
    <=
what composition rules + component evidence justify
```

Si un componente crítico es `UNINTERPRETABLE`, la composición no puede declararse `FULL` salvo que exista una regla explícita que demuestre independencia respecto de ese componente.

## 16. Derivación y pérdida

AR-2 reutiliza AR-1:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DROPPED
UNKNOWN
```

La representación derivada debe poder asociar pérdida/transformación con el ámbito o propiedad afectada.

AR-2 no redefine estas categorías.

## 17. Interoperabilidad mínima

Dos extremos pueden interoperar semánticamente si:

1. pueden interpretar el núcleo mínimo;
2. pueden identificar las capacidades declaradas;
3. comprenden todas las capacidades `REQUIRED_FOR_INTERPRETATION`;
4. degradan conservadoramente propiedades dependientes de capacidades no comprendidas;
5. no confunden recepción con autoridad;
6. no necesitan compartir tipos internos de dominio.

Esto no exige que ambos extremos implementen todas las capacidades existentes.

## 18. Frontera con AR-3

AR-2 define **qué semántica debe poder representarse**.

AR-3 definirá cómo un sistema concreto mapea:

```text
DOMAIN SEMANTICS
       ↕
REPRESENTATION SEMANTICS
```

AR-2 no debe incorporar reglas particulares de Binding.

## 19. Frontera con AR-6 y AR-7

AR-2 no define:

- serialización;
- framing;
- negociación de protocolo;
- códigos binarios;
- transporte;
- retransmisión;
- orden de mensajes.

La criticidad de capacidades es semántica. El mecanismo mediante el que se codifica o negocia pertenece a fases posteriores.

## 20. Frontera con AR-4

`RECONSTRUCTION_INFORMATION` permite expresar información relevante para reconstrucción.

AR-2 no define:

- algoritmo de reconstrucción;
- suficiencia efectiva;
- prueba de reconstruibilidad;
- autorización de incorporación del resultado reconstruido.

## 21. Criterios candidatos de cierre AR-2

AR-2 podrá cerrarse si una revisión final confirma:

- separación sujeto / representación / codificación;
- núcleo mínimo suficiente sin semántica KOS interna;
- capacidades extensibles con criticidad explícita;
- degradación segura y conservadora;
- identidad no global obligatoria;
- procedencia y cobertura con estados explícitos;
- Claim/Evidence/Verification/Guarantee separados;
- `RepresentationEnvelope` no convertido en formato de protocolo;
- compatibilidad con AR-1;
- fronteras claras con AR-3, AR-4, AR-6 y AR-7;
- neutralidad conceptual no-KOS preservada.

## 22. Riesgos residuales para revisión final

1. que el núcleo mínimo sea todavía demasiado amplio;
2. que `semantic_context` se convierta en contenedor indefinido;
3. que `capabilities[]` evolucione hacia un registro central rígido;
4. que criticidad semántica y negociación de protocolo se mezclen;
5. que extensiones redefinan el núcleo indirectamente;
6. que una degradación compleja produzca falsas garantías por composición.

## 23. Estado

```text
Minimal semantic core:          REFINED CANDIDATE
Representation identity:        CONDITIONAL
SubjectDescriptor:              REFINED CANDIDATE
Semantic capabilities:          REFINED CANDIDATE
Capability criticality:         DEFINED
Safe degradation:               DEFINED
Claim/Evidence/Verification/
Guarantee separation:           DEFINED
Provenance semantics:           REFINED
Coverage semantics:             REFINED
Domain extension rule:          DEFINED
Non-KOS neutrality:             PRESERVED
AR boundaries:                  PRESERVED
```

## 24. Siguiente acción

Realizar **AR-2 Final Review / Closure Assessment**.

La revisión deberá intentar refutar el modelo, especialmente mediante:

- capacidad crítica desconocida;
- composición con componente degradado;
- representación efímera sin identidad;
- sujeto sin identificador global;
- procedencia no revelada;
- garantía dependiente de capacidad no soportada;
- extensión de dominio conflictiva.

Si los invariantes sobreviven, producir `AR-2-CLOSURE.es.md/.en.md` y avanzar a AR-3.
