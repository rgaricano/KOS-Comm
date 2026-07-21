# AR-2 — Modelo de representación (Representation Model)

**Estado:** ACTIVE — INITIAL MODEL  
**Fase:** I — Fundamentos de fronteras y representación  
**Línea:** KOS-Comm experimental (`KOS-Comn`)  
**Dependencia:** AR-1 CLOSED / PASS  
**Siguiente posterior:** AR-3 — Binding Model

## 1. Propósito

AR-2 define qué es una representación informacional dentro de KCA y qué propiedades mínimas debe poder declarar para atravesar las fronteras definidas por AR-1 sin importar implícitamente la semántica interna del sistema de origen o destino.

AR-2 debe responder:

```text
¿Qué es una representación?
¿Qué representa?
¿Bajo qué contexto se interpreta?
¿Qué identidad/referencias conserva?
¿Qué procedencia declara?
¿Qué propiedades garantiza?
¿Qué información pierde o transforma?
¿Qué autoridad NO debe inferirse de ella?
```

## 2. Principio fundamental

Una representación no es el objeto que representa.

```text
Representation
    !=
Represented Object
```

Y, en particular:

```text
Representation != Canonical Object
Representation != Authority
Representation != Authorization
Representation != Truth
Representation != Complete Knowledge
```

Una representación es una construcción informacional interpretable que expresa, referencia, proyecta, describe o transporta determinados aspectos de un referente bajo una semántica declarada.

## 3. Separación entre referente, representación y forma codificada

AR-2 adopta inicialmente tres niveles:

```text
REFERENT / REFERENTE
        ↓ representation
SEMANTIC REPRESENTATION
        ↓ encoding (AR-6)
ENCODED FORM
```

El referente puede ser un objeto, estado, evento, relación, resultado, observación, propuesta u otra entidad semánticamente identificable.

La representación pertenece a AR-2.

La forma codificada pertenece principalmente a AR-6.

Por tanto:

```text
same representation
    may have
multiple encodings
```

Y:

```text
same encoding technology
    may encode
multiple representation classes
```

## 4. Hipótesis inicial: RepresentationEnvelope

Se propone como estructura conceptual, no todavía como esquema de implementación:

```text
RepresentationEnvelope {
    representation_identity
    representation_class
    subject
    semantic_context
    provenance
    references[]
    properties[]
    content
}
```

El nombre `RepresentationEnvelope` es provisional y no implica que AR-2 deba terminar definiendo un contenedor físico único.

## 5. Identidad de representación

Debe distinguirse:

```text
representation_identity
    !=
subject_identity
```

Ejemplo conceptual:

```text
Objeto X
   ↓ projection
Representación R1 de X
   ↓ later projection
Representación R2 de X
```

R1 y R2 pueden referirse al mismo sujeto y, aun así, poseer identidades de representación distintas.

Esto permite trazabilidad, revisión, comparación y procedencia sin confundir copia/representación con referente.

## 6. Subject / sujeto representado

Toda representación debe poder declarar qué entidad o conjunto de entidades constituye su sujeto cuando sea aplicable.

El sujeto puede expresarse mediante:

- identidad directa;
- referencia;
- conjunto de referencias;
- descriptor de ámbito;
- sujeto anónimo/no identificable cuando el caso lo requiera.

AR-2 no presupone que todos los sujetos sean objetos canónicos.

## 7. Clase de representación

`representation_class` expresa la función semántica de la representación, no su codificación física.

Taxonomía inicial de investigación:

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

Esta lista NO queda estabilizada en la primera pasada.

Su objetivo es probar si KCA necesita clases semánticas explícitas y cuáles pueden mantenerse neutrales respecto de KOS.

## 8. Contexto semántico

Una representación sólo es interpretable correctamente si existe suficiente contexto semántico.

```text
representation
    +
semantic_context
    ↓
interpretation
```

`semantic_context` puede incluir conceptualmente:

- vocabulario/ontología aplicable;
- versión del modelo semántico;
- dominio de interpretación;
- unidades;
- convenciones;
- ámbito temporal;
- restricciones relevantes.

AR-2 deberá evitar que este contexto se convierta en dependencia obligatoria de una ontología KOS.

## 9. Procedencia — Provenance

La representación debe poder declarar procedencia suficiente para evaluar su origen y transformaciones relevantes.

Hipótesis mínima:

```text
Provenance {
    source
    creation_context
    creation_time_or_order
    derivation[]
    previous_representation?
}
```

Procedencia no equivale a autoridad:

```text
known provenance != authority
trusted provenance != authority
```

## 10. Referencias

Una representación puede contener referencias a otras entidades o representaciones.

Debe distinguirse:

```text
reference identity
    !=
referenced object transfer
```

Y:

```text
reference resolution
    !=
authority acquisition
```

AR-2 investigará qué propiedades mínimas necesita una referencia neutral.

## 11. Propiedades y garantías declaradas

AR-2 consume `PropertyTransition` de AR-1 y debe permitir declarar qué propiedades pretende portar o garantizar una representación.

Ejemplos:

```text
identity
semantic meaning
references
relations
provenance
ordering
context
revision/version
integrity information
reconstruction information
```

Una declaración de propiedad debe diferenciar:

```text
CLAIM
EVIDENCE
VERIFIED GUARANTEE
UNKNOWN
```

Esta distinción es provisional y será objeto de validación.

## 12. Contenido

`content` representa la carga semántica propia de la representación.

AR-2 NO define todavía:

- formato binario;
- JSON/CBOR/Protobuf u otra serialización;
- framing;
- compresión;
- cifrado;
- transporte.

Esos aspectos pertenecen principalmente a AR-6/AR-7.

## 13. Completitud

Una representación no debe asumirse completa.

Se investigará una declaración explícita de cobertura:

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

La completitud siempre debe entenderse respecto de un ámbito declarado.

```text
complete
without scope
    =
ambiguous claim
```

## 14. Temporalidad y revisión

Una representación puede describir:

- estado instantáneo;
- intervalo;
- secuencia;
- evento;
- revisión concreta;
- estado sin referencia temporal conocida.

AR-2 debe permitir expresar temporalidad sin imponer un único modelo temporal.

Asimismo:

```text
representation revision
    !=
subject revision
```

## 15. Representaciones derivadas

Una representación puede derivarse de otra:

```text
R0
 ↓ transform
R1
 ↓ summarize
R2
```

La cadena debe poder conservar información suficiente para evaluar:

- procedencia;
- transformaciones;
- pérdidas conocidas;
- relación con el sujeto original.

Esto conecta con AR-1, pero la reconstrucción detallada pertenece a AR-4.

## 16. Composición

Una representación compuesta puede contener o relacionar varias representaciones.

```text
CompositeRepresentation
    ├── R1
    ├── R2
    └── R3
```

La composición no debe borrar la identidad, procedencia o garantías individuales cuando sean arquitectónicamente relevantes.

Se investigará si `COMPOSITE` debe ser una clase explícita o una propiedad estructural.

## 17. Autoridad y representación

Invariante heredado de AR-1:

```text
Representation != Authority
```

Incluso una representación:

```text
authentic
integrity verified
trusted source
complete for scope
exactly reconstructable
```

puede carecer de autoridad para modificar estado de destino.

AR-2 podrá portar metadatos relacionados con autoridad, pero no conceder autoridad por mera presencia de esos metadatos.

## 18. Neutralidad no-KOS

La representación debe poder funcionar entre sistemas no-KOS:

```text
System A
  ↓ Binding A
Representation
  ↓
KCA
  ↓
Representation
  ↓ Binding B
System B
```

Por ello AR-2 no puede exigir como campos fundamentales conceptos tales como:

- CanonicalObject;
- CognitiveProjection;
- KnowledgeChangeProposal;
- KOS authority types.

Esos conceptos podrán mapearse mediante AR-3 cuando KOS sea uno de los extremos.

## 19. Relación con Binding

AR-2 define la representación neutral.

AR-3 definirá:

```text
Domain Semantics
      ↕
Explicit Binding
      ↕
Representation Semantics
```

El Binding debe asumir la responsabilidad de mapear semánticas específicas de dominio sin introducirlas en el núcleo neutral de AR-2.

## 20. Relación con KSCL

AR-2 no presupone todavía que KSCL sea una única capa.

KSCL podrá utilizar o especializar representaciones, pero su descomposición se investigará en AR-5.

Por tanto:

```text
Representation Model
    !=
KSCL Model
```

## 21. Relación con codificación y KCP

```text
Representation
    ↓ AR-6 Encoding
Encoded Form
    ↓ AR-7 KCP / communication mechanism
Transported Form
```

KCP no debe poseer la semántica de la representación.

El protocolo podrá transportar, identificar o negociar representaciones, pero no convertirse en propietario de su significado.

## 22. Casos iniciales de validación AR-2

AR-2 deberá modelar al menos:

1. referencia a una entidad sin transferirla;
2. observación parcial de estado;
3. resultado operacional;
4. proyección local;
5. evidencia asociada a una afirmación;
6. propuesta sin autoridad de incorporación;
7. representación derivada con pérdida conocida;
8. representación reconstruible;
9. representación compuesta;
10. intercambio no-KOS ↔ no-KOS;
11. misma representación con dos codificaciones diferentes;
12. dos representaciones diferentes del mismo sujeto.

## 23. Preguntas abiertas

- ¿Debe existir una estructura común obligatoria o sólo un conjunto de capacidades semánticas?
- ¿Qué clases de representación son fundamentales y cuáles son especializaciones de dominio?
- ¿Cómo expresar identidad de sujeto sin imponer un esquema global único?
- ¿Qué diferencia normativa debe existir entre `claim`, `evidence` y `guarantee`?
- ¿Debe la procedencia ser obligatoria para toda representación o graduable por clase?
- ¿Cómo expresar cobertura/completitud de forma neutral?
- ¿Cómo representar relaciones entre representaciones sin crear un grafo universal obligatorio?
- ¿Qué metadatos mínimos necesita una representación para ser interpretable fuera de su sistema de origen?
- ¿Cómo evitar que `RepresentationEnvelope` se convierta prematuramente en un formato de mensaje?

## 24. Criterios preliminares de cierre AR-2

AR-2 podrá considerarse candidato a cierre cuando:

- exista definición neutral de representación;
- referente, representación y codificación estén separados;
- identidad de representación y sujeto estén diferenciadas;
- procedencia y referencias tengan semántica mínima;
- exista mecanismo conceptual para propiedades/garantías;
- completitud y contexto puedan declararse explícitamente;
- autoridad permanezca externa a la representación;
- los casos de validación sean modelables;
- el escenario no-KOS no requiera semántica interna KOS;
- AR-3 pueda definir Bindings sin redefinir qué es una representación;
- AR-6 pueda definir codificación sin redefinir la semántica representacional.

## 25. Estado inicial

```text
AR-1 Boundary Model:          CLOSED / PASS
AR-2 Representation Model:    ACTIVE

Representation definition:    INITIALIZED
Referent separation:           ESTABLISHED HYPOTHESIS
Representation identity:       INITIALIZED
Subject identity:              INITIALIZED
Representation classes:        RESEARCH TAXONOMY
Semantic context:              INITIALIZED
Provenance:                    INITIALIZED
References:                    INITIALIZED
Property guarantees:           OPEN
Completeness:                  INITIALIZED
Authority separation:          REQUIRED INVARIANT
Non-KOS neutrality:            REQUIRED

Next:
AR-2 validation and taxonomy refinement
```
