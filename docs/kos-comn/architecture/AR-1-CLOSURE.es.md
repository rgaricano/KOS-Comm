# AR-1 — Revisión de cierre del modelo de fronteras

**Estado:** CLOSED — PASS  
**Fase:** I — Fundamentos de fronteras y representación  
**Línea:** KOS-Comm experimental (`KOS-Comn`)  
**Fecha:** 2026-07-21  
**Siguiente:** AR-2 — Representation Model / Modelo de representación

## 1. Alcance de la revisión

Esta revisión contrasta:

- `AR-1-BOUNDARY-MODEL.es.md`;
- `AR-1-BOUNDARY-VALIDATION.es.md`;
- `AR-1-BOUNDARY-COMPOSITION.es.md`.

Objetivos:

1. detectar contradicciones;
2. consolidar las decisiones normativas;
3. verificar los criterios de cierre originales;
4. fijar la frontera de responsabilidad AR-1/AR-2;
5. declarar cierre o nuevo refinamiento.

## 2. Resultado ejecutivo

```text
AR-1 — BOUNDARY MODEL
CLOSURE REVIEW: PASS
STATUS: CLOSED
```

No se han identificado contradicciones estructurales que obliguen a un segundo ciclo de refinamiento.

Los documentos de validación y composición refinan el modelo inicial sin alterar su principio fundamental: dominio, información, comunicación y autoridad son dimensiones conceptualmente independientes que pueden coexistir en una transición, pero no inferirse unas de otras.

## 3. Definiciones consolidadas

### 3.1 Frontera de dominio — Domain Boundary

Cambio de contexto de responsabilidad o propiedad arquitectónica.

No se deduce de:

- distancia;
- host;
- proceso;
- red;
- transporte;
- protocolo.

```text
remoto != cambio de dominio
local != mismo dominio
cambio de proceso != cambio de dominio
transporte != cambio de dominio
```

### 3.2 Frontera de información — Information Boundary

Cambio explícito de representación, forma informacional o régimen/contexto de interpretación.

Puede existir localmente y sin comunicación.

### 3.3 Frontera de comunicación — Communication Boundary

Intercambio mediante un mecanismo de comunicación entre participantes, componentes, procesos, nodos o sistemas.

No implica por sí mismo cambio de dominio, cambio de representación ni transferencia de autoridad.

### 3.4 Frontera de autoridad — Authority Boundary

Punto en el que autoridad, legitimidad, capacidad de decisión o incorporación canónica debe evaluarse explícitamente.

La recepción, autenticidad, integridad, confianza, transporte o reconstrucción no sustituyen esa evaluación.

## 4. Modelo compacto consolidado

Se conserva:

```text
B = <D,I,C,A>
```

como resumen compacto de presencia de fronteras:

```text
D = Domain Boundary
I = Information Boundary
C = Communication Boundary
A = Authority Boundary
```

El vector no constituye el modelo completo.

En rutas complejas se utiliza conceptualmente:

```text
BoundaryPath
    =
ordered BoundarySegment[]
```

## 5. Segmento de frontera — BoundarySegment

Unidad mínima arquitectónicamente relevante:

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

Un segmento existe cuando al menos una dimensión D/I/C/A presenta una transición relevante o cuando existe una transición de propiedades que debe conservarse explícitamente.

Un tramo meramente físico sin relevancia arquitectónica no necesita aparecer en el modelo lógico.

## 6. Ruta de fronteras — BoundaryPath

```text
BoundaryPath = ordered BoundarySegment[]
```

Regla de continuidad:

```text
segment[n].destination_context
    ==
segment[n+1].source_context
```

El resumen global puede expresar presencia acumulada:

```text
D(P) = OR D(Si)
I(P) = OR I(Si)
C(P) = OR C(Si)
A(P) = OR A(Si)
```

pero nunca sustituye el análisis de segmentos.

## 7. Regla de no-colapso

Dos segmentos no deben colapsarse si al hacerlo se oculta:

- una frontera de autoridad;
- una transformación semántica;
- una pérdida o degradación;
- un cambio de responsabilidad;
- evidencia relevante de preservación;
- una diferencia entre alcance salto-a-salto y extremo-a-extremo.

## 8. Transición de propiedades — PropertyTransition

Estados consolidados:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DEGRADED
OMITTED
NOT_APPLICABLE
UNKNOWN
```

Semántica:

- `PRESERVED`: propiedad preservada respecto de la referencia evaluada;
- `TRANSFORMED_EQUIVALENT`: cambia la forma, no la semántica evaluada;
- `TRANSFORMED_LOSSY`: transformación con pérdida conocida;
- `DEGRADED`: propiedad disponible con fidelidad o calidad reducida;
- `OMITTED`: propiedad deliberadamente ausente;
- `NOT_APPLICABLE`: la propiedad no corresponde al caso;
- `UNKNOWN`: evidencia insuficiente; no equivale a pérdida.

## 9. Alcance de preservación

Se consolidan tres alcances:

```text
HOP_BY_HOP
END_TO_END
LOCAL_TRANSFORMATION
```

En documentación española se expresarán preferentemente como:

```text
salto-a-salto
extremo-a-extremo
transformación local
```

Los identificadores ingleses se reservan para nomenclatura de implementación o contratos técnicos cuando proceda.

## 10. Reglas de composición de propiedades

### 10.1 Omisión

Si una propiedad se omite y no existe reintroducción o reconstrucción explícita posterior:

```text
end_to_end(property) = OMITTED
```

### 10.2 Desconocido

```text
UNKNOWN != DEGRADED
```

Un tramo desconocido no puede presentarse como preservado sin evidencia adicional.

### 10.3 Transformación con pérdida

Una pérdida conocida limita la fidelidad respecto del original y no desaparece por transformaciones posteriores salvo restauración desde una fuente independiente adecuada.

### 10.4 Transformación equivalente

La forma puede cambiar conservando la propiedad semántica evaluada.

## 11. Preservación, reintroducción, reconstrucción y derivación

Se consideran conceptos distintos:

```text
PRESERVATION
REINTRODUCTION
RECONSTRUCTION
DERIVATION
```

AR-1 registra la transición; AR-4 definirá la semántica detallada de reconstrucción.

Invariante:

```text
reconstruido != preservado desde el origen
```

## 12. Autoridad

La autoridad no se propaga implícitamente a través de una ruta.

```text
autorizado en S1
    !=
autorizado en Sn
```

Una ruta puede contener múltiples `AuthorityBoundary` con alcance, sujeto, contexto de decisión y resultado distintos.

No existe:

```text
A1 PASS => todas las evaluaciones posteriores PASS
```

## 13. Confianza, autenticidad e integridad

No se incorporan como nuevas dimensiones de frontera.

```text
confianza != autoridad
autenticidad != autoridad
integridad != autoridad
confianza != autenticidad
```

Pueden ser propiedades o evaluaciones relevantes para una decisión, pero no crean autoridad por sí mismas.

## 14. Reglas normativas de no-inferencia

```text
C=1 no implica D=1
C=1 no implica I=1
C=1 no implica A=1

I=1 no implica C=1
I=1 no implica D=1
I=1 no implica A=1

D=1 no implica C=1
D=1 no implica I=1
D=1 no implica A=1

A=1 no implica D=1
A=1 no implica I=1
A=1 no implica C=1
```

Adicionalmente:

```text
recepción != importación
transmisión != transferencia de autoridad
autenticidad != autoridad
confianza != autoridad
integridad != autoridad
reconstrucción != preservación
reconstrucción != autorización
proyección != objeto canónico
observación != serialización canónica
compatibilidad técnica != autoridad
```

## 15. Matriz D/I/C/A

La revisión de las 16 combinaciones booleanas concluye:

- `<0,0,0,0>` normalmente no constituye un segmento arquitectónicamente observable;
- las otras combinaciones pueden ser válidas según contexto;
- AR-1 no establece una lista rígida de combinaciones permitidas/prohibidas;
- la corrección depende de evidencia, contexto, segmentación y cumplimiento de las reglas de no-inferencia.

## 16. Neutralidad

AR-1 supera la primera prueba conceptual de neutralidad.

Puede describir:

```text
Sistema A no-KOS
    ↓
Adaptación / Binding A
    ↓
Representación neutral
    ↓
Intercambio
    ↓
Representación neutral
    ↓
Adaptación / Binding B
    ↓
Sistema B no-KOS
```

sin requerir como fundamento ontológico tipos internos de KOS.

Esto NO equivale a superar Gate C.5, que requerirá evidencia experimental posterior.

## 17. Casos de validación

Resultado:

```text
V1  Proyección local                         PASS
V2  Observación remota                      PASS
V3  Resultado operacional remoto            PASS
V4  Feedback sin incorporación automática   PASS
V5  Referencia canónica                     PASS
V6  Reconstrucción sin autoridad             PASS
V7  No-KOS ↔ No-KOS                         PASS conceptual
V8  Canonical Transfer Candidate             PASS mediante segmentación
V9  Relay / intermediarios                   PASS mediante BoundaryPath
```

En documentación española se preferirán expresiones como `realimentación` o `retroalimentación` cuando se describa el concepto general; `Feedback` se conservará cuando corresponda a una denominación contractual o tipo propio de KOS.

## 18. Frontera de responsabilidad AR-1 / AR-2

### AR-1 posee

- tipos de frontera;
- segmentación;
- rutas de frontera;
- composición;
- transición, preservación y pérdida de propiedades;
- presencia/localización de fronteras de autoridad;
- alcance salto-a-salto y extremo-a-extremo;
- reglas de no-inferencia.

### AR-1 no posee

- esquema interno de una representación;
- taxonomía definitiva de representaciones;
- serialización;
- codificación física;
- gramática;
- códec;
- algoritmos de reconstrucción;
- mapeos concretos de Binding.

### AR-2 deberá responder

```text
¿Qué es una Representation / representación?
¿Qué invariantes semánticos porta?
¿Cómo expresa identidad, referencias y procedencia?
¿Cómo se declara su clase semántica?
¿Cómo se expresan las garantías sobre propiedades?
```

## 19. Verificación de criterios de cierre originales

### C1 — Cuatro categorías sin solapamiento ambiguo

**PASS.**

Dominio, información, comunicación y autoridad poseen definiciones independientes y reglas explícitas de no-inferencia.

### C2 — Modelo de composición

**PASS.**

`BoundarySegment` + `BoundaryPath` permiten segmentación ordenada, continuidad, composición y conservación de puntos de autoridad y transformaciones.

### C3 — Preservación, transformación y pérdida

**PASS.**

`PropertyTransition` diferencia preservación, transformación equivalente, transformación con pérdida, degradación, omisión, no aplicabilidad y estado desconocido.

### C4 — Autoridad independiente de recepción/comunicación/reconstrucción

**PASS.**

La independencia está establecida como invariante normativo.

### C5 — Casos iniciales modelables

**PASS.**

Los ocho casos originales y un noveno caso con intermediarios han sido modelados.

### C6 — Escenario no-KOS sin semántica KOS oculta

**PASS conceptual.**

La taxonomía AR-1 no requiere conceptos internos KOS. La prueba experimental completa queda reservada a Gate C.5.

### C7 — AR-2 puede construirse sin redefinir frontera

**PASS.**

La responsabilidad entre AR-1 y AR-2 está delimitada explícitamente.

## 20. Cuestiones abiertas transferidas

No bloquean AR-1 y se transfieren a fases posteriores:

- estructura interna y clases de Representation → AR-2;
- mapeo concreto entre dominios y representación → AR-3;
- relación detallada entre propiedades perdidas/reconstruidas y fidelidad → AR-4;
- semántica de reconstrucción → AR-4;
- codificación física → AR-6;
- comunicación protocolaria y garantías de transporte → AR-7;
- prueba experimental completa de neutralidad → Gate C.5.

## 21. Criterio lingüístico documental

KOS-Comm adopta para su documentación el principio de coherencia bilingüe heredado de la colaboración con KOS:

1. los documentos de arquitectura deberán disponer progresivamente de versiones ES/EN equivalentes;
2. en documentos españoles se preferirá terminología española cuando exista una traducción técnica clara;
3. se conservarán términos ingleses cuando sean identificadores de implementación, nombres contractuales, tipos, nombres propios arquitectónicos estabilizados o cuando la traducción introduzca ambigüedad;
4. la primera aparición de un concepto central podrá expresar ambas formas, por ejemplo `segmento de frontera (BoundarySegment)`;
5. las versiones ES/EN deben conservar equivalencia semántica, no necesariamente traducción literal;
6. cualquier diferencia normativa entre versiones debe considerarse defecto documental y reconciliarse.

Este criterio se aplicará desde AR-2 y se utilizará también para normalizar progresivamente la documentación AR-1.

## 22. Decisión de cierre

```text
AR-1 — BOUNDARY MODEL

Taxonomía de fronteras:        STABLE
Semántica de dominio:          STABLE
Vector <D,I,C,A>:              STABLE AS COMPACT SUMMARY
BoundarySegment:               STABLE CANDIDATE
BoundaryPath:                  STABLE CANDIDATE
PropertyTransition:            STABLE CANDIDATE
Reglas de composición:         STABLE CANDIDATE
Reglas de no-inferencia:       NORMATIVE
Neutralidad conceptual:        PASS
Criterios de cierre:           7/7 PASS

STATUS: CLOSED
```

`STABLE CANDIDATE` indica que el concepto queda suficientemente definido para ser consumido por AR-2/AR-3, pero puede recibir refinamientos compatibles si la evidencia posterior lo exige. Cualquier modificación que rompa los invariantes de AR-1 requiere reabrir explícitamente AR-1.

## 23. Siguiente acción

```text
PHASE I

AR-1 Boundary Model
    CLOSED / PASS
        ↓
AR-2 Representation Model
    NEXT
        ↓
AR-3 Binding Model
        ↓
GATE A
```

Antes de iniciar el desarrollo sustantivo de AR-2 se crearán las versiones inglesas equivalentes de los documentos AR-1, preservando el principio de bilingüismo documental.
