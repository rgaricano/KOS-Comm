# AR-2 — Modelo de representación — Revisión final adversarial

**Estado:** COMPLETE — PASS  
**Objeto:** evaluar el candidato refinado de AR-2 intentando refutar sus invariantes antes del cierre.

## 1. Resultado

```text
ADVERSARIAL CASES: 7/7 PASS
CRITICAL CONTRADICTIONS: NONE
REWORK REQUIRED: NO
CLOSURE RECOMMENDATION: PASS
```

La revisión no demuestra completitud universal del modelo. Demuestra que los casos adversariales definidos no rompen sus invariantes y que las cuestiones residuales pueden evolucionar sin reabrir el núcleo de AR-2 mientras se respeten sus fronteras.

## 2. Caso A — Capacidad crítica desconocida

Entrada:

```text
Representation R
  capability X
  criticality = REQUIRED_FOR_INTERPRETATION

Receiver B
  X = unsupported
```

Resultado esperado y observado conceptualmente:

```text
interpretation = UNINTERPRETABLE
```

No se produce aceptación silenciosa ni falsa interpretación parcial.

**PASS.**

## 3. Caso B — Composición con componente degradado

```text
Composite R
  component A = FULL
  component B = DEGRADED
```

Sin regla explícita de independencia:

```text
Composite R != FULL by default
```

Las propiedades dependientes de B deben degradarse. Las independientes pueden conservarse si la relación está explícitamente justificada.

No existe elevación automática de garantías por agregación.

**PASS.**

## 4. Caso C — Representación efímera sin identidad

```text
R {
  representation_identity = absent
  subject = locally interpretable
  semantic_context = present
  capabilities = present
  content = present
}
```

Si R no necesita referencia, correlación, derivación, composición, versionado ni auditoría posterior, puede interpretarse como representación efímera autocontenida.

En el momento en que una operación requiera referenciar R, deberá asignarse/obtenerse una identidad adecuada; no se reutiliza automáticamente la identidad del sujeto.

**PASS.**

## 5. Caso D — Sujeto sin identificador global

```text
SubjectDescriptor {
  identifier = local-17
  namespace = system-A
  scope = experiment-4
}
```

El sujeto es identificable en el contexto declarado sin exigir UUID global, URI global ni identificador KOS.

El Binding puede resolver equivalencias externas cuando existan.

```text
local identity != universal identity
mapping != authority transfer
```

**PASS.**

## 6. Caso E — Procedencia no revelada

```text
provenance.disclosure_state = UNDISCLOSED
```

El receptor puede distinguir:

```text
UNDISCLOSED != UNKNOWN
UNDISCLOSED != FALSE
```

Las políticas externas pueden rechazar la representación si requieren procedencia conocida, pero AR-2 no inventa procedencia ni la considera automáticamente falsa.

**PASS.**

## 7. Caso F — Garantía dependiente de capacidad no soportada

```text
Guarantee G
 depends_on Capability C

C criticality = REQUIRED_FOR_DECLARED_PROPERTY
Receiver does not support C
```

Resultado:

```text
G cannot remain VERIFIED/GUARANTEED for receiver
G -> UNKNOWN/UNVERIFIED
```

La representación puede seguir siendo interpretable si C no era necesaria para el contenido base, pero la garantía afectada se degrada conservadoramente.

**PASS.**

## 8. Caso G — Extensión de dominio conflictiva

Extensión D intenta declarar:

```text
representation_identity == canonical subject identity
```

o redefinir `OPTIONAL` como semántica obligatoria.

Esto contradice el núcleo.

Resultado:

```text
extension = NON-CONFORMANT
```

La extensibilidad no incluye autoridad para redefinir invariantes del núcleo.

**PASS.**

## 9. Ataques adicionales de frontera

### 9.1 `semantic_context` como contenedor arbitrario

Riesgo confirmado. Resolución de cierre:

`semantic_context` sólo debe contener o referenciar información necesaria para interpretar el contenido y sus capacidades. No es un contenedor genérico para estado de aplicación, autoridad, transporte o políticas no semánticas.

```text
semantic_context scope = interpretation
```

### 9.2 Registro central de capacidades

AR-2 no exige registro central.

Sólo exige identificación semántica suficientemente inequívoca dentro del acuerdo/interoperabilidad aplicable.

```text
capability identification != mandatory global registry
```

### 9.3 Criticidad vs negociación

Se mantiene:

```text
criticality = semantic property
negotiation = later protocol/binding mechanism
```

AR-2 no prescribe handshake ni mecanismo de negociación.

## 10. Evaluación de criterios de cierre

| Criterio | Resultado |
|---|---|
| sujeto / representación / codificación separados | PASS |
| núcleo mínimo neutral | PASS |
| capacidades extensibles | PASS |
| criticidad explícita | PASS |
| degradación conservadora | PASS |
| identidad global no obligatoria | PASS |
| procedencia explícitamente modelable | PASS |
| cobertura explícitamente modelable | PASS |
| Claim/Evidence/Verification/Guarantee separados | PASS |
| RepresentationEnvelope no protocolizado | PASS |
| compatibilidad AR-1 | PASS |
| frontera AR-3 | PASS |
| frontera AR-4 | PASS |
| frontera AR-6 | PASS |
| frontera AR-7 | PASS |
| neutralidad conceptual no-KOS | PASS |

## 11. Decisión

```text
AR-2 FINAL REVIEW
        PASS
```

No se identifica necesidad de `REWORK` antes del cierre.

## 12. Condiciones que obligarían a reabrir AR-2

AR-2 deberá reconsiderarse si evidencia posterior demuestra que:

1. el núcleo mínimo no permite representar un caso necesario sin importar semántica de dominio;
2. la degradación conservadora es insuficiente para evitar falsas interpretaciones;
3. la separación sujeto/representación no puede mantenerse;
4. una capacidad fundamental requiere redefinir autoridad o transporte;
5. AR-3 demuestra que el modelo no puede ser enlazado de forma bilateral sin contaminar el núcleo;
6. Gate C.5 demuestra que la neutralidad no-KOS era sólo aparente.

## 13. Recomendación

Producir cierre bilingüe de AR-2 y avanzar a:

```text
AR-3 — BINDING MODEL
```
