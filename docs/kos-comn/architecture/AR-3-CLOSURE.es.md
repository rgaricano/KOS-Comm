# AR-3 — Modelo de Binding — Cierre

**Estado:** CLOSED / PASS  
**Fase:** Phase I — Boundary & Representation Foundation  
**Predecesores:** AR-1 CLOSED/PASS, AR-2 CLOSED/PASS  
**Siguiente:** Gate A — evaluación de cierre de Phase I

## 1. Decisión

Tras el modelo inicial, 12 casos de validación y 8 enfrentamientos adversariales:

```text
AR-3 — BINDING MODEL
STATUS: CLOSED
RESULT: PASS
CASES ASSESSED: 20
CRITICAL CONTRADICTIONS: 0
CORE REWORK: NONE
```

## 2. Definición estabilizada

Un `Binding` es un adaptador semántico explícito situado en la frontera entre un dominio y las representaciones neutrales KCA.

```text
DOMAIN
  ↕
BINDING
  ↕
KCA REPRESENTATION
```

Es un seam bilateral. Bilateral no implica simetría, reversibilidad ni invertibilidad.

## 3. Responsabilidad

El Binding puede responsabilizarse de reglas de mapeo, resolución de sujeto, correspondencia de capacidades, declaración de pérdidas, correlaciones, precondiciones, diagnósticos, compatibilidad contractual y admisibilidad semántica del mapeo.

No adquiere por implicación autoridad de dominio, importación canónica, persistencia, ejecución, reconstrucción, identidad canónica, promoción, transporte o codificación.

```text
mapping capability != domain authority
```

## 4. Entrada

Un Binding de entrada produce un candidato orientado al dominio:

```text
Representation
  ↓
Binding
  ↓
DomainFacingCandidate
```

Invariantes:

```text
candidate != accepted domain state
receipt != canonical import
```

## 5. Direcciones

```text
OUTBOUND
INBOUND
BIDIRECTIONAL
```

`BIDIRECTIONAL != INVERTIBLE`.

## 6. Resultado de mapeo

```text
BindingResult<T> {
    status
    value?
    property_transitions[]
    diagnostics[]
    correlation?
}
```

Estados estabilizados:

```text
MAPPED
MAPPED_WITH_DEGRADATION
UNMAPPABLE
REJECTED_BY_BINDING_POLICY
UNSUPPORTED_CONTRACT
```

Estado y causa diagnóstica permanecen separados.

## 7. Integración AR-1

Toda pérdida o transformación relevante debe expresarse mediante la semántica AR-1:

```text
PRESERVED
TRANSFORMED_EQUIVALENT
TRANSFORMED_LOSSY
DROPPED
UNKNOWN
```

## 8. Integración AR-2

El Binding produce/consume representaciones AR-2 y respeta su criticidad, cobertura, procedencia y degradación.

Una capacidad requerida para interpretación no soportada impide una interpretación válida.

## 9. Identidad y correlación

```text
identity mapping != identity authority
correlation != canonical identity
```

Para un `BindingContract` interoperable, `binding_identity` es obligatoria y debe ser inequívoca dentro del ámbito de interoperabilidad declarado. No se exige identidad universal global.

Las correlaciones conflictivas no pueden resolverse silenciosamente.

## 10. Degradación y restauración

Regla por defecto:

```text
semantic property strength
is conservatively non-increasing
across transformations
```

Excepción:

```text
property strength may increase
IFF new independent explicit scoped justification/evidence is introduced
```

La nueva base debe atribuirse al punto de restauración y no a la representación previa.

## 11. Política

```text
MAPPING ADMISSIBILITY
    -> Binding

AUTHORITATIVE ACCEPTANCE / PERSISTENCE / EXECUTION
    -> Domain
```

Una política de Binding que asuma automáticamente autoridad de dominio es no conforme.

## 12. Compatibilidad

Se estabilizan dos etapas distintas:

```text
DECLARED CONTRACT COMPATIBILITY
        ↓
RUNTIME SEMANTIC MAPPABILITY
```

El éxito sintáctico no implica compatibilidad semántica.

## 13. Composición

La seguridad de composición no se asume por compatibilidad local.

Debe evaluarse explícitamente considerando capacidades, contratos, ámbitos de identidad, correlaciones, pérdidas acumuladas y restricciones de admisibilidad.

Modelo de evaluación candidato:

```text
BindingCompositionAssessment {
    participants[]
    contract_compatibility
    capability_coverage
    identity_scope_consistency
    correlation_consistency
    accumulated_property_transitions[]
    admissibility_constraints[]
    result
    diagnostics[]
}
```

AR-3 no exige un motor universal de composición.

## 14. Neutralidad

El contrato arquitectónico de Binding es neutral.

```text
Binding Model = neutral architectural contract
KOS Binding = domain-specific realization
```

Es conceptualmente viable:

```text
Non-KOS A → Binding A → KCA → Binding B → Non-KOS B
```

sin tipos internos KOS.

Esto no sustituye Gate C.5, que requerirá evidencia experimental.

## 15. Fronteras preservadas

```text
AR-1 = transición de propiedades en frontera
AR-2 = semántica representable
AR-3 = correspondencia dominio ↔ representación
AR-4 = reconstrucción
AR-6 = codificación
AR-7 = KCP/transporte protocolario
```

AR-3 no absorbe reconstrucción, codificación ni transporte.

## 16. Conformidad estabilizada

Un Binding conforme debe:

1. identificarse inequívocamente dentro de su ámbito interoperable;
2. declarar contratos/rangos y direcciones soportadas;
3. preservar separación entre mapeo y autoridad;
4. producir candidatos, no aceptación autoritativa, en entrada;
5. declarar pérdidas conforme AR-1;
6. respetar criticidad/degradación AR-2;
7. separar estado de resultado y causa;
8. no elevar propiedades sin nueva base explícita;
9. distinguir admisibilidad de autoridad del dominio;
10. tratar correlación como relación, no autoridad de identidad;
11. hacer explícitos los conflictos de correlación;
12. separar compatibilidad declarada y mapeabilidad en ejecución;
13. validar composición en lugar de asumirla;
14. permanecer separado de reconstrucción, codificación y transporte;
15. permitir realizaciones no-KOS.

## 17. Evidencia de cierre

```text
Initial Model: COMPLETE
Validation Pass 1: 12/12 PASS
Adversarial Pass 2: 8/8 PASS
Total: 20/20 PASS
Critical contradictions: 0
Core premise rework: none
```

## 18. Riesgos residuales no bloqueantes

- descubrimiento/registro concreto de Bindings;
- sintaxis de reglas;
- almacenamiento de correlaciones;
- negociación de perfiles;
- estrategia de migración/versionado;
- instrumentación de evidencia para restauraciones;
- implementación de evaluación de composición.

Estos puntos quedan para diseño/implementación posterior salvo nueva evidencia que contradiga los invariantes.

## 19. Condiciones de reapertura

Reabrir AR-3 si evidencia posterior demuestra que:

- un Binding neutral necesita autoridad de dominio para funcionar;
- la separación candidato/estado autoritativo no puede mantenerse;
- la degradación/restauración no puede expresarse conservadoramente;
- AR-1 o AR-2 resultan incompatibles con el modelo;
- una composición segura exige redefinir el núcleo;
- la realización no-KOS requiere importar semánticas internas KOS;
- AR-4, AR-6 o AR-7 obligan a transferir responsabilidades al Binding.

## 20. Resultado

```text
AR-3 — BINDING MODEL
CLOSED / PASS

PHASE I COMPONENTS:
AR-1 CLOSED / PASS
AR-2 CLOSED / PASS
AR-3 CLOSED / PASS

NEXT:
GATE A ASSESSMENT
```
