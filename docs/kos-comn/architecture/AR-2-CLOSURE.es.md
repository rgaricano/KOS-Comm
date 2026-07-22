# AR-2 — Modelo de representación — Cierre

**Estado:** CLOSED / PASS  
**Fase:** Phase I — Boundary & Representation Foundation  
**Predecesor:** AR-1 — Modelo de fronteras  
**Siguiente:** AR-3 — Modelo de Binding

## 1. Decisión de cierre

AR-2 se cierra con el siguiente modelo conceptual:

```text
REPRESENTACIÓN
    =
NÚCLEO SEMÁNTICO MÍNIMO
    +
CAPACIDADES SEMÁNTICAS DECLARADAS
    +
CLASIFICACIÓN EXTENSIBLE OPCIONAL
```

No se adopta una taxonomía universal cerrada ni un formato universal de mensaje.

## 2. Núcleo semántico

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

`subject`, `semantic_context`, `capabilities[]` y `content` son conceptualmente necesarios.

`representation_identity` es condicional y se requiere cuando la representación debe ser referenciada, correlacionada, derivada, compuesta, versionada o auditada.

## 3. Invariantes de identidad

```text
representation != represented object
representation_identity != subject_identity
mapping != authority transfer
```

AR-2 no exige identificador global universal del sujeto.

## 4. SubjectDescriptor

Modelo conceptual estabilizado:

```text
SubjectDescriptor {
    identifier?
    namespace?
    semantic_type?
    scope?
    qualifiers{}
}
```

AR-3 podrá mapear identidades de dominio mediante Binding sin convertir KCA en autoridad de identidad.

## 5. Capacidades semánticas

Las capacidades permiten extender la semántica sin convertir una clasificación cerrada en el eje del modelo.

Criticidad estabilizada:

```text
REQUIRED_FOR_INTERPRETATION
REQUIRED_FOR_DECLARED_PROPERTY
OPTIONAL
INFORMATIONAL
```

Regla:

```text
unknown capability != safe-to-ignore capability
```

## 6. Interpretación y degradación

Estados conceptuales:

```text
FULL
DEGRADED
UNINTERPRETABLE
```

La degradación debe ser explícita y conservadora.

```text
known -> unknown
verified -> unverified
complete -> partial/unknown
```

No se permite promoción inversa sin evidencia adicional.

## 7. Procedencia

La capacidad de expresar procedencia forma parte del modelo fundamental, aunque la información disponible pueda ser:

```text
KNOWN
PARTIAL
UNKNOWN
UNDISCLOSED
NOT_APPLICABLE
```

## 8. Cobertura

```text
COMPLETE_FOR_SCOPE
PARTIAL
SUMMARY
REFERENCE_ONLY
UNKNOWN
```

Invariante:

```text
COMPLETE_FOR_SCOPE requires explicit scope
```

## 9. Afirmación, evidencia, verificación y garantía

Se estabiliza su separación conceptual:

```text
Claim != Evidence
Evidence != Verification
Verification != Guarantee
Verification != Authority
Guarantee != Authority
```

Toda verificación o garantía debe ser interpretable respecto de ámbito y fundamento/base declarados.

## 10. Extensibilidad

Las extensiones de dominio pueden añadir capacidades, clasificaciones, tipos semánticos y parámetros.

No pueden redefinir silenciosamente los invariantes del núcleo.

```text
EXTEND != OVERRIDE CORE
```

## 11. Neutralidad

AR-2 no incorpora semánticas internas KOS como requisitos del núcleo.

En particular no posee autoridad de:

- importación canónica;
- persistencia canónica;
- ejecución;
- Knowledge;
- Projection específica de KOS;
- Reconstruction.

Estas relaciones se resolverán mediante Binding o fases posteriores cuando corresponda.

## 12. RepresentationEnvelope

Se conserva únicamente como modelo lógico de referencia.

```text
RepresentationEnvelope
    != mandatory wire format
    != KCP message
    != serialization schema
```

## 13. Fronteras

```text
AR-1 = semántica de frontera y transición de propiedades
AR-2 = semántica representable
AR-3 = Binding dominio ↔ representación
AR-4 = reconstrucción
AR-6 = codificación
AR-7 = KCP
```

## 14. Evidencia de cierre

- 12 casos iniciales: PASS / PASS WITH REFINEMENT;
- refinamiento estructural completado;
- 7 casos adversariales finales: 7/7 PASS;
- contradicciones críticas: ninguna;
- neutralidad conceptual no-KOS: preservada;
- compatibilidad AR-1: preservada.

## 15. Condiciones de reapertura

Reabrir AR-2 sólo ante evidencia que demuestre, entre otros casos, que:

- el núcleo requiere semántica de dominio para operar;
- la degradación permite falsas interpretaciones;
- falla la separación sujeto/representación;
- AR-3 no puede realizar Binding bilateral sin contaminar el núcleo;
- Gate C.5 demuestra falsa neutralidad.

## 16. Resultado

```text
AR-2 — REPRESENTATION MODEL

STATUS: CLOSED
RESULT: PASS

NEXT:
AR-3 — BINDING MODEL
```
