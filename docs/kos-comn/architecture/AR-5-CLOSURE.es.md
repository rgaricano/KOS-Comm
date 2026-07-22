# AR-5 — Descomposición de KSCL — Cierre

**Estado:** CLOSED / PASS  
**Fase:** Phase II — Reconstruction Semantics / KSCL foundation  
**Predecesores:** AR-4 CLOSED/PASS  
**Siguiente:** Gate B — revisión transversal

## 1. Decisión

AR-5 se cierra con el meta-modelo validado y el núcleo KSCL formalizado.

```text
AR-5 — KSCL DECOMPOSITION
STATUS: CLOSED
RESULT: PASS
```

## 2. Meta-modelo consolidado

Todo módulo KSCL se describe mediante:

```text
Atoms
    ↓
Assertions
    ↓
Evaluations (optional)
    ↓
Operations (optional)
```

Invariantes:

```text
Atoms never depend on upper layers
Assertions never create atoms
Evaluations never mutate assertions
Operations never define semantics
Semantic dependencies are acyclic
```

## 3. Estratificación semántica

Se consolidan cuatro niveles conceptuales:

1. **Semantic Atoms** — conceptos indivisibles.
2. **Semantic Assertions** — relaciones o declaraciones sobre átomos.
3. **Semantic Evaluations** — juicios observacionales sobre afirmaciones.
4. **Semantic Operations** — procesos que consumen semántica para producir nuevas afirmaciones o efectos externos.

Las evaluaciones y operaciones son opcionales y no alteran los átomos ni las afirmaciones.

## 4. Núcleo KSCL formal

Primitivas normativas consolidadas:

```text
Entity
Reference
PropertyDefinition
PropertyValue
PropertyStrength
Representation
Evidence
Origin
Lineage
Resolution
Coverage
Fidelity
Compatibility
```

Relaciones normativas:

```text
Correlation
Support
Transition
```

## 5. Especificación formal del núcleo

KSCL Core se entiende como el conjunto mínimo de construcciones semánticas necesarias para expresar, intercambiar y razonar sobre representaciones, reconstrucciones y vinculaciones de forma neutral respecto del dominio.

Conformidad:

```text
A module is KSCL Core compliant iff:
1. every semantic element is classifiable as Atom, Assertion, Evaluation or Operation;
2. every dependency satisfies the KSCL invariants;
3. no semantic cycle exists;
4. no domain authority is introduced;
5. no primitive duplicates another primitive's semantics.
```

## 6. Reconciliación de familias semánticas

Se consolidan los hallazgos de AR-1...AR-4:

- `PropertyStrength` expresa el orden parcial de preservación/pérdida.
- `Representation` porta capacidades, cobertura y procedencia.
- `Binding` se expresa como operación o evaluación compuesta sobre compatibilidad y correspondencia.
- `Reconstruction` se expresa como operación con resolución, cobertura y fidelidad evaluadas por candidato.
- `Origin` es la fuente de entrada; `Lineage` es la cadena monotónica de reconstrucciones y transformaciones.

## 7. Clausura semántica

Se adopta el principio normativo de clausura:

```text
Any new KSCL construction must be expressible as a specialization or composition of the core categories.
```

Si una propuesta exige una quinta categoría ontológica, la carga de la prueba recae sobre la propuesta.

## 8. Resultados de validación

La atomización y la validación por enfrentamientos no encontraron contraejemplos para el núcleo. Las familias semánticas se conservaron, pero los procesos se relegaron al nivel operativo y las evaluaciones al nivel observacional.

## 9. Condiciones de reapertura

AR-5 sólo se reabrirá si aparece una construcción futura que no pueda clasificarse sin pérdida como átomo, afirmación, evaluación u operación, o si un nuevo caso obliga a introducir una quinta categoría ontológica.

## 10. Resultado

```text
AR-5 — KSCL DECOMPOSITION
CLOSED / PASS
```
