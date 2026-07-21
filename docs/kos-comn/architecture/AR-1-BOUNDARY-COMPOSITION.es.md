# AR-1 — Boundary Composition Semantics

**Estado:** ACTIVE — FORMALIZATION PASS 1  
**Relacionado:** `AR-1-BOUNDARY-MODEL.es.md`, `AR-1-BOUNDARY-VALIDATION.es.md`  
**Objetivo:** formalizar `BoundarySegment`, `BoundaryPath`, reglas mínimas de composición y combinaciones D/I/C/A sin invadir AR-2.

## 1. Unidad mínima: BoundarySegment

Un `BoundarySegment` describe una transición arquitectónicamente relevante entre dos contextos consecutivos.

```text
BoundarySegment {
    source_context
    destination_context
    boundary_state <D,I,C,A>
    property_transitions[]
    authority_boundaries[]
    scope
}
```

AR-1 no define todavía la estructura interna de la representación transportada. Eso pertenece a AR-2.

### 1.1 Condición de existencia

Debe existir un segmento sólo si al menos una de las dimensiones D/I/C/A cambia o si existe una transición explícita de propiedades que deba ser registrada.

Un tramo puramente físico sin relevancia arquitectónica puede quedar fuera del modelo lógico.

## 2. Context

`source_context` y `destination_context` identifican contextos arquitectónicos, no necesariamente hosts o procesos.

Un contexto puede caracterizarse provisionalmente por:

```text
responsibility
interpretation regime
communication participant
applicable authority regime
```

La estructura formal del contexto no se congela en AR-1.

## 3. BoundaryPath

```text
BoundaryPath = ordered BoundarySegment[]
```

Un path representa una secuencia ordenada de transiciones desde un contexto origen hasta un contexto destino.

Propiedades mínimas:

```text
segments are ordered
segment[n].destination_context == segment[n+1].source_context
```

Si esa continuidad no existe, no se trata del mismo `BoundaryPath` o falta un segmento explícito.

## 4. Regla de no-colapso

Dos segmentos consecutivos NO deben colapsarse automáticamente si el colapso elimina:

- una Authority Boundary;
- una transformación semántica;
- una pérdida/degradación;
- un cambio de responsabilidad;
- evidencia relevante de preservación;
- una diferencia entre alcance hop-by-hop y end-to-end.

Formalmente:

```text
collapse(S1,S2) allowed
ONLY IF
semantic_observability(S1 + S2) == semantic_observability(collapsed)
```

La igualdad anterior es conceptual; su formalización matemática se pospone.

## 5. Regla de composición de dimensiones

Para un path P compuesto por segmentos S1..Sn, el resumen global puede calcular presencia de cruces:

```text
D(P) = OR D(Si)
I(P) = OR I(Si)
C(P) = OR C(Si)
A(P) = OR A(Si)
```

Pero este resumen NO sustituye los segmentos.

Ejemplo:

```text
S1 = <0,1,1,0>
S2 = <0,0,0,1>

summary(P) = <0,1,1,1>
```

El resumen global podría sugerir erróneamente que comunicación y autoridad ocurrieron juntas. Los segmentos conservan que fueron transiciones diferentes.

## 6. Composición de PropertyTransition

Las propiedades no se componen mediante OR.

Para cada propiedad `p`, debe evaluarse la cadena:

```text
p(source)
  ↓ T1
p(context1)
  ↓ T2
...
  ↓ Tn
p(destination)
```

Reglas iniciales:

### 6.1 OMITTED es absorbente para preservación directa

Si una propiedad es `OMITTED` y no existe una transición posterior explícita de reintroducción/reconstrucción:

```text
end_to_end(p) = OMITTED
```

### 6.2 UNKNOWN no equivale a DEGRADED

```text
UNKNOWN + PRESERVED => UNKNOWN end-to-end
```

salvo evidencia independiente suficiente para resolver el tramo desconocido.

### 6.3 TRANSFORMED_LOSSY limita fidelidad

Una transformación lossy no puede convertirse posteriormente en `PRESERVED` respecto del original salvo que exista una fuente independiente que restaure la información perdida.

### 6.4 TRANSFORMED_EQUIVALENT puede preservar semántica

Puede existir:

```text
physical/logical form: transformed
semantic meaning: preserved
```

La propiedad evaluada debe declararse explícitamente.

## 7. Reintroducción y reconstrucción

AR-1 admite que una propiedad omitida/degradada pueda aparecer posteriormente, pero debe distinguir:

```text
PRESERVATION
REINTRODUCTION
RECONSTRUCTION
DERIVATION
```

AR-1 sólo registra que la transición ocurrió. AR-4 definirá semántica detallada de Reconstruction.

Nunca se inferirá:

```text
reconstructed => preserved from source
```

## 8. Authority composition

Authority no se propaga por composición implícita.

```text
authorized at S1
    !=
authorized at Sn
```

Cada `AuthorityBoundary` debe declarar al menos conceptualmente:

```text
authority_scope
decision_context
decision
subject
```

Una autorización puede ser local a una acción, dominio, operación o importación.

No existe una regla general:

```text
A1 PASS => all subsequent A PASS
```

## 9. Communication composition

Múltiples Communication Boundaries pueden constituir un intercambio end-to-end.

```text
A → Relay1 → Relay2 → B
```

AR-1 distingue:

- comunicación hop-by-hop;
- continuidad lógica end-to-end.

La existencia de continuidad end-to-end no implica canal físico único ni protocolo único.

## 10. Domain composition

Un path puede entrar y salir de dominios múltiples.

El resumen `D=1` sólo indica que ocurrió al menos un cambio de responsabilidad.

Para análisis preciso debe conservarse la secuencia:

```text
Domain A
  ↓
Domain B
  ↓
Domain C
```

No debe inferirse que A transfirió ownership a C únicamente porque existe un path.

## 11. Information composition

Una ruta puede contener varias transformaciones informacionales:

```text
Domain Object
  ↓ projection
Logical Representation
  ↓ encoding
Encoded Form
  ↓ decoding
Logical Representation
  ↓ binding
Destination Object
```

AR-1 registra los Information Boundaries y las propiedades afectadas.

AR-2 definirá qué constituye una Representation y sus invariantes internos.

AR-6 tratará Physical Encoding.

## 12. Matriz D/I/C/A — 16 combinaciones booleanas

La matriz se utiliza como prueba de consistencia, no como afirmación de que todas las combinaciones sean igualmente frecuentes.

| D | I | C | A | Interpretación preliminar |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | No boundary crossing relevante; normalmente no requiere segmento. |
| 0 | 0 | 0 | 1 | Decisión de autoridad local sin cambio informacional/comunicación. Válida. |
| 0 | 0 | 1 | 0 | Comunicación transparente dentro del mismo dominio/contexto informacional. Válida. |
| 0 | 0 | 1 | 1 | Comunicación con evaluación de autoridad sin transformación informacional. Válida. |
| 0 | 1 | 0 | 0 | Proyección/transformación local. Válida. |
| 0 | 1 | 0 | 1 | Transformación local sometida a autoridad. Válida. |
| 0 | 1 | 1 | 0 | Intercambio con representación transformada, sin autoridad. Muy común. |
| 0 | 1 | 1 | 1 | Intercambio + transformación + autoridad dentro del mismo dominio de responsabilidad. Válida, debe segmentarse si los eventos no son simultáneos. |
| 1 | 0 | 0 | 0 | Cambio de responsabilidad sin transformación/comunicación explícita; posible transición lógica/organizativa. Válida pero exige contexto claro. |
| 1 | 0 | 0 | 1 | Cambio de responsabilidad con autoridad local explícita. Válida. |
| 1 | 0 | 1 | 0 | Comunicación entre dominios conservando forma informacional. Válida. |
| 1 | 0 | 1 | 1 | Comunicación entre dominios con autoridad. Válida. |
| 1 | 1 | 0 | 0 | Cambio de dominio y representación sin comunicación explícita; posible adaptación local entre responsabilidades. Válida. |
| 1 | 1 | 0 | 1 | Cambio de dominio/representación con evaluación de autoridad. Válida. |
| 1 | 1 | 1 | 0 | Transferencia informacional entre dominios sin autoridad. Muy común. |
| 1 | 1 | 1 | 1 | Caso completo. Válido como resumen, pero probablemente requiere varios segmentos. |

## 13. Hallazgo sobre la matriz

No existen combinaciones booleanas intrínsecamente prohibidas salvo `<0,0,0,0>` como segmento sin transición observable.

La validez real depende de la semántica y del contexto.

Por tanto, AR-1 no impondrá una tabla rígida de combinaciones permitidas/prohibidas. Impondrá reglas de evidencia y no-inferencia.

## 14. Reglas de no-inferencia

Estas reglas pasan a ser normativas dentro de AR-1:

```text
C=1 does NOT imply D=1
C=1 does NOT imply I=1
C=1 does NOT imply A=1

I=1 does NOT imply C=1
I=1 does NOT imply D=1
I=1 does NOT imply A=1

D=1 does NOT imply C=1
D=1 does NOT imply I=1
D=1 does NOT imply A=1

A=1 does NOT imply D=1
A=1 does NOT imply I=1
A=1 does NOT imply C=1
```

Y adicionalmente:

```text
receipt does NOT imply import
authenticity does NOT imply authority
trust does NOT imply authority
integrity does NOT imply authority
reconstruction does NOT imply preservation
reconstruction does NOT imply authorization
```

## 15. Separación AR-1 / AR-2

### AR-1 posee

- tipos de frontera;
- segmentación;
- paths;
- composición;
- transición/preservación/pérdida de propiedades;
- presencia y localización de Authority Boundaries;
- scope hop-by-hop/end-to-end;
- reglas de no-inferencia.

### AR-1 NO posee

- schema interno de una Representation;
- taxonomía definitiva de tipos de representación;
- serialización;
- encoding físico;
- grammar;
- codec;
- reconstruction algorithm;
- binding mapping concreto.

### AR-2 deberá responder

```text
What is a Representation?
What semantic invariants does it carry?
How are identity/reference/provenance expressed?
How is representation class declared?
How are property guarantees represented?
```

Esto evita que Boundary Model se convierta accidentalmente en Information Representation Model.

## 16. Condiciones de composición segura

Una composición puede tratarse como semánticamente segura cuando:

1. todos los segmentos relevantes son conocidos;
2. ninguna Authority Boundary ha sido ocultada;
3. las pérdidas y transformaciones relevantes están declaradas;
4. `UNKNOWN` no se presenta como `PRESERVED`;
5. propiedades end-to-end tienen evidencia suficiente;
6. ningún cambio de dominio se infiere sólo por topología;
7. ninguna autoridad se infiere por transporte, trust, integrity o reconstruction.

## 17. Estado tras Formalization Pass 1

```text
Boundary taxonomy: STABLE CANDIDATE
Domain semantics: STABLE CANDIDATE
Boundary Vector: COMPACT SUMMARY
BoundaryDescriptor: REFINED HYPOTHESIS
BoundarySegment: FORMALIZED CANDIDATE
BoundaryPath: FORMALIZED CANDIDATE
PropertyTransition: FORMALIZED CANDIDATE
Composition rules: INITIALIZED
D/I/C/A matrix: COMPLETE PASS 1
No-inference rules: ESTABLISHED
AR-1 / AR-2 ownership boundary: ESTABLISHED
```

## 18. Próximo paso AR-1

Realizar `Closure Review Pass`:

1. contrastar el modelo inicial, validación y composición;
2. detectar contradicciones terminológicas;
3. consolidar definiciones normativas;
4. revisar los criterios de cierre originales;
5. decidir `AR-1 READY FOR CLOSURE` o abrir un segundo refinement pass.
