# AR-3 — Modelo de Binding

**Estado:** ACTIVE — INITIAL MODEL  
**Fase:** Phase I — Boundary & Representation Foundation  
**Predecesores:** AR-1 CLOSED/PASS, AR-2 CLOSED/PASS  
**Objetivo:** definir el seam bilateral entre semánticas de dominio y representación neutral KCA sin transferencia implícita de autoridad, propiedad ni dependencia arquitectónica.

## 1. Definición

Un `Binding` es un adaptador semántico explícito y situado en una frontera.

```text
DOMAIN
  ↕
BINDING
  ↕
KCA REPRESENTATION
```

Su responsabilidad es hacer explícita la correspondencia entre semánticas de dominio y semánticas representables por KCA.

No es el dominio, no es KCA y no es un protocolo de transporte.

## 2. Principio bilateral

El Binding se define como seam bilateral, no como conversor unilateral obligatorio.

```text
OUTBOUND
Domain Semantics
      ↓
   Binding
      ↓
Representation

INBOUND
Representation
      ↓
   Binding
      ↓
Domain-facing Interpretation / Candidate
```

Bilateral no implica simetría perfecta.

```text
map_out(x) = R
```

no exige:

```text
map_in(R) = x
```

Puede existir pérdida, transformación, información contextual local o restricciones de autoridad que impidan reversibilidad.

## 3. Qué posee un Binding

Un Binding puede poseer/responsabilizarse de:

- reglas de mapeo entre conceptos de dominio y AR-2;
- resolución de `SubjectDescriptor` respecto del dominio;
- traducción de capacidades semánticas;
- declaración de pérdidas y transformaciones;
- correlación entre identidades cuando sea necesaria;
- validación de precondiciones semánticas del mapeo;
- producción de diagnósticos de mapeo;
- compatibilidad declarada con versiones de contratos de dominio y KCA;
- políticas locales necesarias para decidir si un mapeo es posible.

## 4. Qué nunca posee por implicación

Un Binding no adquiere automáticamente:

- autoridad sobre el dominio;
- autoridad de importación canónica;
- autoridad de persistencia;
- autoridad de ejecución;
- propiedad del objeto representado;
- propiedad de la representación KCA;
- autoridad de reconstrucción;
- autoridad de promoción hacia KOS-Lab;
- responsabilidad de transporte KCP;
- responsabilidad de codificación AR-6.

Regla:

```text
MAPPING CAPABILITY != DOMAIN AUTHORITY
```

## 5. Contrato lógico candidato

```text
BindingContract {
    binding_identity
    domain_contract_ref
    kca_contract_ref
    supported_directions[]
    mapping_capabilities[]
    compatibility
    declared_constraints[]
}
```

Este contrato es conceptual. AR-3 no fija todavía API, lenguaje, esquema de serialización ni formato de despliegue.

## 6. Direcciones soportadas

```text
OUTBOUND
INBOUND
BIDIRECTIONAL
```

`BIDIRECTIONAL` significa que existen ambos conjuntos de reglas, no que sean inversas matemáticas ni que preserven todas las propiedades.

## 7. Resultado de mapeo

Se propone:

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Estados candidatos:

```text
MAPPED
MAPPED_WITH_DEGRADATION
UNMAPPABLE
REJECTED_BY_BINDING_POLICY
UNSUPPORTED_CONTRACT
```

`REJECTED_BY_BINDING_POLICY` describe decisión local del Binding; no implica autoridad global de KCA.

## 8. Relación con AR-1

El Binding debe declarar transformaciones usando la semántica estabilizada por AR-1:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DROPPED
UNKNOWN
```

No puede declarar equivalencia cuando la transición real sea con pérdida conocida.

## 9. Relación con AR-2

El Binding produce o consume representaciones conformes a AR-2.

Debe poder mapear:

- sujeto;
- contexto semántico;
- capacidades;
- contenido;
- identidad de representación cuando corresponda;
- procedencia cuando corresponda;
- clasificación extensible cuando sea útil.

No puede redefinir las reglas AR-2 de criticidad o degradación.

## 10. Mapeo de identidad

El Binding puede mantener una correlación explícita:

```text
DomainIdentity
    ↕
SubjectDescriptor
```

La correlación puede ser:

```text
ONE_TO_ONE
ONE_TO_MANY
MANY_TO_ONE
CONTEXTUAL
UNRESOLVED
```

La existencia de correlación no convierte una identidad en canónica para el otro extremo.

```text
identity mapping != identity authority
```

## 11. Correlación

Cuando sea necesaria continuidad entre intercambios, el Binding puede emitir o mantener `correlation`.

La correlación:

- relaciona eventos/representaciones/mapeos;
- no sustituye identidad del sujeto;
- no sustituye identidad de representación;
- no confiere autoridad.

## 12. Mapeo de capacidades

Para cada capacidad AR-2 relevante, el Binding debe poder declarar:

```text
SUPPORTED_NATIVE
SUPPORTED_MAPPED
SUPPORTED_WITH_DEGRADATION
UNSUPPORTED
NOT_APPLICABLE
```

Si una capacidad `REQUIRED_FOR_INTERPRETATION` resulta `UNSUPPORTED` en entrada, el Binding no puede producir silenciosamente una interpretación de dominio válida.

## 13. Propagación de degradación

```text
Representation DEGRADED
      ↓
Binding
      ↓
Domain-facing result
```

El Binding no puede elevar por sí solo las propiedades degradadas.

Puede restaurar una propiedad únicamente si dispone de información/evidencia local adicional y declara explícitamente la base de dicha restauración.

```text
DEGRADED + no new evidence
    != FULL
```

## 14. Asimetría legítima

Ejemplo:

```text
Domain A
  rich local state
      ↓ outbound
Representation R
  partial projection
```

La entrada posterior de R no obliga a reconstruir el estado original de A.

Por tanto:

```text
outbound support
    !=
inbound reconstructability
```

Esto preserva la frontera con AR-4.

## 15. Autoridad de entrada

Un Binding de entrada puede producir:

```text
DomainFacingCandidate
```

pero:

```text
candidate != accepted domain state
receipt != canonical import
```

La aceptación, persistencia o ejecución corresponde al dominio receptor y a sus contratos autoritativos.

## 16. Contratos estabilizados

En el caso KOS:

```text
KOS stabilized contract
        ↕
     KOS Binding
        ↕
        KCA
```

El Binding debe apuntar a contratos estabilizados, no a detalles accidentales de implementación.

Esta regla deriva del charter de colaboración KOS-Lab ↔ KOS-Comm.

## 17. Binding específico KOS y neutralidad

KCA no contiene un `KOSBinding` como requisito universal.

Se distingue:

```text
Binding Model
    = neutral architectural contract

KOS Binding
    = domain-specific realization
```

Otros dominios pueden implementar:

```text
Domain-A Binding
Domain-B Binding
```

sin dependencia de KOS.

## 18. Escenario no-KOS

```text
Non-KOS A
    ↓
Binding A
    ↓
KCA Representation
    ↓
KCA exchange
    ↓
KCA Representation
    ↓
Binding B
    ↓
Non-KOS B
```

AR-3 debe permitir este escenario sin importar tipos internos KOS.

Esto prepara, pero no sustituye, Gate C.5.

## 19. Compatibilidad y versión

Un Binding debe declarar compatibilidad con los contratos que enlaza.

Modelo candidato:

```text
CompatibilityDescriptor {
    domain_contract_range
    kca_contract_range
    capability_profile?
}
```

Principio:

```text
Binding compatibility
    must be explicit
    must not be inferred from successful parsing alone
```

La estrategia concreta de versionado queda abierta para validación posterior.

## 20. Ciclo de vida

Estados conceptuales candidatos:

```text
DECLARED
VALIDATED
ACTIVE
DEPRECATED
RETIRED
```

Estos estados describen el ciclo de vida del Binding, no autoridad de dominio.

La necesidad de todos ellos deberá validarse antes del cierre.

## 21. Política local

Un Binding puede aplicar política local de mapeo, por ejemplo:

- exigir procedencia conocida;
- rechazar degradación por debajo de cierto umbral;
- limitar tipos/capacidades soportados;
- exigir contexto adicional.

Pero debe distinguirse:

```text
BINDING POLICY REJECTION
    !=
KCA SEMANTIC INVALIDITY
```

## 22. Errores y diagnósticos

AR-3 distingue conceptualmente:

```text
SEMANTIC_UNMAPPABLE
UNSUPPORTED_CAPABILITY
INSUFFICIENT_CONTEXT
IDENTITY_UNRESOLVED
POLICY_REJECTED
CONTRACT_INCOMPATIBLE
```

Los diagnósticos deben permitir explicar por qué no se realizó un mapeo sin convertir el Binding en protocolo de transporte.

## 23. Conformidad candidata

Un Binding conforme deberá:

1. declarar contratos enlazados;
2. declarar direcciones soportadas;
3. preservar separación de autoridad;
4. declarar pérdidas/transformaciones conforme AR-1;
5. respetar criticidad/degradación AR-2;
6. no asumir identidad global implícita;
7. no convertir recepción en importación;
8. declarar incompatibilidad cuando no pueda mapear con seguridad;
9. no depender de tipos internos KOS para el contrato neutral;
10. mantener separadas semántica de Binding, codificación y transporte.

## 24. Preguntas abiertas

- ¿Debe `binding_identity` ser siempre obligatoria o sólo para Bindings desplegados/versionados?
- ¿La política local pertenece al Binding o a un envoltorio de integración?
- ¿Cómo expresar dependencias entre reglas de mapeo sin crear un lenguaje universal excesivo?
- ¿Qué compatibilidad mínima debe poder comprobarse estáticamente?
- ¿Cómo modelar correlaciones persistentes sin convertir el Binding en almacén autoritativo?
- ¿Es necesario distinguir `UNMAPPABLE` de `INSUFFICIENT_INFORMATION` como estado principal?
- ¿Qué invariantes adicionales requiere composición de múltiples Bindings?

## 25. Plan de validación AR-3

Casos iniciales:

1. KOS → KCA, observación parcial;
2. KCA → KOS, resultado recibido sin importación canónica;
3. no-KOS A → KCA → no-KOS B;
4. identidad local con namespace distinto;
5. capacidad crítica no soportada por Binding de entrada;
6. salida con pérdida declarada;
7. Binding sólo OUTBOUND;
8. Binding bidireccional no reversible;
9. contratos incompatibles;
10. política local más estricta que KCA;
11. correlación sin autoridad de identidad;
12. cadena de dos Bindings con degradación acumulada.

## 26. Estado

```text
AR-3 — BINDING MODEL

Initial model: ACTIVE / ESTABLISHED
Validation: NEXT
Closure: PENDING
Gate A: PENDING
```
