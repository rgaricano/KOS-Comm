# AR-4 — Modelo de Reconstrucción

**Estado:** ACTIVE — INITIAL MODEL ESTABLISHED  
**Fase:** Phase II — Reconstruction Semantics  
**Predecesor:** Gate A PASS  
**Siguiente:** AR-4 Validation Pass 1

## 1. Propósito

AR-4 define qué significa reconstruir semánticamente a partir de una o más representaciones KCA y qué afirmaciones pueden realizarse sobre el resultado.

No define todavía codificación, transporte, KCP ni una implementación concreta de KSCL.

## 2. Definición inicial

Reconstrucción es el proceso explícito por el cual información representada, contexto y evidencia disponible se utilizan para producir un artefacto reconstruido o un conjunto de candidatos, acompañado de una declaración verificable de alcance, fidelidad, incertidumbre, procedencia y degradación.

```text
Representation(s)
    + Context
    + Evidence
    + Reconstruction Rules
            ↓
    Reconstruction Process
            ↓
Reconstruction Result
```

Invariante fundamental:

```text
reconstruction != authorization
```

Reconstruir algo no concede autoridad para aceptarlo, persistirlo, ejecutarlo o convertirlo en estado canónico de un dominio.

## 3. Reconstrucción no es inversión automática

AR-4 rechaza la suposición:

```text
Representation = reversible serialization of original object
```

Una representación puede ser parcial, transformada, degradada, agregada o ambigua.

Por tanto:

```text
representation -> reconstruction
```

no implica:

```text
reconstruction == original object
```

## 4. Objeto reconstruido

Se introduce conceptualmente:

```text
ReconstructedArtifact
```

como resultado semántico de reconstrucción.

No debe confundirse con:

```text
DomainState
CanonicalObject
AuthorizedImport
ExecutedState
```

Una realización de dominio puede posteriormente mapear/evaluar el artefacto reconstruido mediante sus propios contratos y autoridad.

## 5. Clases iniciales de reconstrucción

### 5.1 EXACT

La evidencia disponible permite afirmar equivalencia respecto al alcance declarado sin pérdida conocida relevante.

`EXACT` no significa identidad ontológica con el objeto original; significa equivalencia reconstruida dentro de un alcance explícito.

### 5.2 EQUIVALENT

El resultado puede diferir estructuralmente pero conserva las propiedades semánticas requeridas por el alcance declarado.

### 5.3 PARTIAL

Sólo una parte del alcance objetivo puede reconstruirse de forma sustentada.

### 5.4 DEGRADED

La reconstrucción es utilizable pero presenta pérdidas o debilitamiento semántico explícitos.

### 5.5 AMBIGUOUS

La evidencia permite más de una reconstrucción compatible y no existe base suficiente para seleccionar una de forma justificada.

### 5.6 IMPOSSIBLE

La información, contexto o evidencia disponible no permiten producir una reconstrucción válida para el alcance requerido.

## 6. Resultado de reconstrucción

Modelo conceptual inicial:

```text
ReconstructionResult<T> {
    status
    artifact?
    candidates[]?
    target_scope
    reconstructed_scope
    fidelity
    property_transitions[]
    evidence_refs[]
    provenance[]
    diagnostics[]
}
```

Estados candidatos:

```text
EXACT
EQUIVALENT
PARTIAL
DEGRADED
AMBIGUOUS
IMPOSSIBLE
```

La validación deberá determinar si clase y estado deben permanecer unidos o separarse.

## 7. Alcance objetivo

Toda afirmación de reconstrucción debe estar acotada.

```text
EXACT relative to scope S
```

es válido.

```text
EXACT absolutely
```

no se admite como afirmación por defecto.

Se introduce:

```text
ReconstructionScope {
    required_properties[]
    optional_properties[]
    semantic_context?
    temporal_scope?
    identity_scope?
}
```

La sintaxis definitiva queda abierta.

## 8. Fidelidad

La fidelidad expresa qué relación puede sostenerse entre el resultado reconstruido y el objetivo declarado.

Modelo inicial:

```text
FidelityAssessment {
    scope
    preserved[]
    equivalent[]
    degraded[]
    missing[]
    unknown[]
    basis[]
}
```

La fidelidad no puede exceder la evidencia disponible salvo incorporación explícita de nueva evidencia independiente.

## 9. Evidencia

La reconstrucción puede utilizar:

```text
REPRESENTED_EVIDENCE
CONTEXTUAL_EVIDENCE
LOCAL_INDEPENDENT_EVIDENCE
DERIVED_EVIDENCE
```

`DERIVED_EVIDENCE` debe conservar trazabilidad hacia sus bases.

Una inferencia no debe presentarse como observación directa.

## 10. Procedencia

La reconstrucción debe conservar la procedencia relevante de:

- representaciones de entrada;
- contexto incorporado;
- evidencia independiente;
- reglas o transformaciones aplicadas;
- derivaciones significativas.

La procedencia del resultado es compuesta; no debe atribuirse enteramente a una única entrada cuando intervienen fuentes adicionales.

## 11. Degradación

AR-4 hereda la regla conservadora de Phase I:

```text
without new independent justified evidence:
semantic property strength MUST NOT increase
```

La reconstrucción puede propagar pérdidas existentes y añadir nuevas pérdidas.

Si restaura una propiedad debe declarar la nueva base que permite hacerlo.

## 12. Ambigüedad

Si existen varios candidatos compatibles:

```text
candidate A
candidate B
candidate C
```

sin evidencia suficiente para seleccionar uno, el resultado debe permanecer `AMBIGUOUS`.

Está prohibida la selección silenciosa basada únicamente en conveniencia de implementación.

Una política externa puede seleccionar posteriormente un candidato, pero esa selección debe distinguirse de la reconstrucción sustentada por evidencia.

## 13. Reconstrucción parcial

`PARTIAL` no equivale a fallo.

Debe declarar:

```text
target_scope
reconstructed_scope
missing/unknown properties
```

Un consumidor puede decidir si el alcance parcial es suficiente para su propósito, pero esa decisión pertenece al consumidor/dominio.

## 14. Reconstrucción imposible

`IMPOSSIBLE` significa que no existe base suficiente para producir un artefacto/candidato conforme al alcance requerido.

Debe diagnosticarse la causa, por ejemplo:

```text
INSUFFICIENT_INFORMATION
MISSING_REQUIRED_CONTEXT
CONFLICTING_EVIDENCE
UNSUPPORTED_SEMANTICS
IRRECOVERABLE_LOSS
IDENTITY_UNRESOLVED
```

## 15. Relación con Binding

Binding y Reconstruction son responsabilidades distintas.

```text
Binding:
    Domain semantics ↔ KCA Representation

Reconstruction:
    Representation(s) + evidence/context
        → reconstructed semantic artifact/candidates
```

Un Binding puede invocar o consumir reconstrucción en una implementación concreta, pero AR-3 no se redefine como motor de reconstrucción.

Tampoco toda reconstrucción necesita un Binding: una aplicación neutral puede reconstruir un artefacto KCA sin dominio externo.

## 16. Relación con autoridad

La secuencia correcta es conceptualmente:

```text
Representation(s)
      ↓
Reconstruction
      ↓
ReconstructedArtifact / Candidates
      ↓
(optional Binding / domain mapping)
      ↓
DomainFacingCandidate
      ↓
DOMAIN AUTHORITY
```

Por tanto:

```text
reconstructed != accepted
reconstructed != canonical
reconstructed != authorized
```

## 17. Identidad

La reconstrucción de identidad debe distinguir:

```text
identity evidence
identity correlation
identity claim
identity authority
```

AR-4 puede producir una afirmación/candidato de identidad sustentado por evidencia, pero no adquiere autoridad canónica de identidad.

## 18. Temporalidad

Una reconstrucción debe poder declarar el ámbito temporal al que se refiere cuando sea semánticamente relevante.

Reconstruir un estado observado en `t1` no implica afirmar el estado actual en `t2`.

```text
reconstructed state @ t1
    !=
current state @ t2
```

## 19. Determinismo

AR-4 no exige que toda reconstrucción sea determinista.

Una reconstrucción puede producir múltiples candidatos o depender de contexto externo. Lo obligatorio es que la incertidumbre y las bases queden explícitas.

## 20. Neutralidad no-KOS

El modelo no requiere semánticas internas KOS.

```text
Neutral Representation(s)
        + neutral rules/evidence
        ↓
Neutral Reconstruction Result
```

Los Bindings de dominio se aplican cuando sea necesario conectar ese resultado con un dominio específico.

## 21. Separación respecto a KSCL

AR-4 define semántica de reconstrucción antes de decidir qué parte corresponde a KSCL.

Por tanto:

```text
AR-4 Reconstruction Model
        !=
KSCL implementation definition
```

AR-5 evaluará posteriormente si KSCL es una capa única, un conjunto de funciones, perfiles, mecanismos o componentes diferenciados.

## 22. Separación respecto a codificación y KCP

AR-4 opera sobre semántica ya disponible.

No define cómo se codifica ni transporta una representación.

```text
reconstruction semantics
    != encoding
    != transport
    != KCP
```

## 23. Condiciones iniciales de conformidad

Una reconstrucción conforme deberá:

1. declarar alcance objetivo;
2. distinguir alcance reconstruido del objetivo;
3. declarar estado/clase de reconstrucción;
4. preservar procedencia relevante;
5. declarar evidencia/base;
6. hacer explícitas pérdidas y desconocidos;
7. no elevar fidelidad sin nueva base independiente y justificada;
8. conservar ambigüedad cuando no exista base para resolverla;
9. separar reconstrucción de autoridad;
10. separar reconstrucción de Binding;
11. permanecer independiente de codificación/transporte;
12. admitir realizaciones neutrales no-KOS.

## 24. Cuestiones abiertas para validación

1. ¿`EXACT/EQUIVALENT/...` son estados o clases de fidelidad?
2. ¿Puede un resultado ser simultáneamente `PARTIAL` y `AMBIGUOUS`?
3. ¿Cómo representar candidatos múltiples sin inflar el núcleo?
4. ¿Qué diferencia formal existe entre `DEGRADED` y `PARTIAL`?
5. ¿Qué propiedades mínimas debe tener `ReconstructionScope`?
6. ¿Cómo modelar conflictos entre evidencias de distinta procedencia?
7. ¿Debe existir una noción explícita de `ReconstructionClaim`?
8. ¿Cómo componer reconstrucciones sucesivas sin perder trazabilidad?
9. ¿Cómo expresar reconstrucción temporal/multiestado?
10. ¿Qué parte de este modelo deberá ser consumida por AR-5/KSCL?

## 25. Casos de validación previstos

1. representación completa con reconstrucción equivalente;
2. representación parcial con reconstrucción parcial;
3. pérdida irreversible que impide reconstrucción requerida;
4. dos candidatos igualmente compatibles;
5. nueva evidencia local que restaura una propiedad;
6. evidencia conflictiva entre dos fuentes;
7. reconstrucción correcta pero no autorizada por dominio;
8. reconstrucción neutral sin Binding;
9. reconstrucción seguida de Binding hacia KOS;
10. reconstrucción de estado histórico frente a estado actual;
11. cadena de reconstrucciones con degradación acumulada;
12. alcance objetivo menor que la información disponible.

## 26. Estado

```text
AR-4 — RECONSTRUCTION MODEL
INITIAL MODEL: ESTABLISHED
STATUS: ACTIVE
NEXT: VALIDATION PASS 1
```
