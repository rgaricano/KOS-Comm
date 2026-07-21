# KOS-Comn — Development State

## Estado

**Activo — fase de reconstrucción y definición arquitectónica.**

## Repositorio y rama

- Repositorio operativo: `rgaricano/KOS-Lab`
- Rama aislada: `KOS-Comn`
- Base de creación: `dev`
- Integración con `dev`: no autorizada todavía.

## Propósito

Replantear el subsistema de información y comunicaciones de KOS desde una perspectiva de ingeniería de telecomunicaciones, sistemas, información y codificación.

El foco original KCP/KSCL se amplía a una arquitectura superior denominada **KCA — Knowledge Communication Architecture**.

## Arquitectura de referencia actual

```text
Persistence
   ↓
KRM — Knowledge Representation Model
   ↓
KEncoding — Knowledge Encoding
   ↓
KCP — Knowledge Communication Protocol
   ↓
KSCL — Knowledge Session Continuity Layer
   ↓
CP — Cognitive Projection
   ↓
Consumers
```

## Decisiones consolidadas

1. KCA es el marco arquitectónico superior del trabajo KOS-Comn.
2. KCP no representa por sí solo todo el subsistema de comunicaciones.
3. KSCL se estudia como capa de continuidad y reconstrucción de estado, no únicamente como lenguaje documental.
4. Representación, codificación, comunicación, continuidad y proyección deben mantenerse separadas por contrato.
5. La proyección cognitiva no adquiere autoridad canónica sobre el conocimiento fuente.
6. La arquitectura propuesta debe contrastarse con las fronteras ya acreditadas en KOS antes de cualquier integración.
7. La persistencia documental en Git es obligatoria para permitir reentrada después de pérdida de contexto.

## Estado por componente

| Componente | Estado | Próximo trabajo |
|---|---|---|
| KCA | INITIAL DRAFT | formalizar capas, interfaces, invariantes y plano de control/datos |
| KRM | PROPOSED | reconstruir modelo de información compatible con KOS |
| KEncoding | PROPOSED | definir requisitos de codificación, integridad y evolución |
| KCP | TO BE RECONSTRUCTED | analizar funciones reales de comunicación y transporte |
| KSCL | TO BE RECONSTRUCTED | analizar continuidad, checkpoints y reconstrucción determinista |
| CP | EXISTING KOS CONCEPT / INTEGRATION PENDING | delimitar interfaz KCA–CP sin reabrir autoridad existente |

## Autoridad y restricciones

KOS-Comn es una rama de laboratorio. No sustituye automáticamente:

- Canon;
- ADR aceptados;
- cierres acreditados;
- arquitectura funcional ya verificada;
- reglas de identidad, evidencia, procedencia y persistencia.

Cualquier contradicción detectada debe registrarse y resolverse explícitamente antes de integrar cambios en `dev`.

## Incidencia operativa GitHub

El Issue #5 es referencia obligatoria para respuestas ambiguas del conector.

```text
AMBIGUOUS CONNECTOR RESPONSE != NO REPOSITORY MUTATION
SEARCH INDEX MISS != BRANCH ABSENCE
WRITE RETRY REQUIRES STATE VERIFICATION
```

Tras una respuesta ambigua de escritura se verificará el estado remoto antes de cualquier reintento.

## Trabajo activo

Consolidación inicial de KCA y establecimiento de la infraestructura documental persistente de KOS-Comn.

## Siguiente acción

1. Consolidar KCA como documento arquitectónico de referencia.
2. Registrar ADR-0001-KCA.
3. Iniciar reconstrucción formal de KRM.
4. Identificar interfaces e invariantes entre KRM, KEncoding, KCP, KSCL y CP.
5. Contrastar el modelo propuesto con los artefactos canónicos y de ingeniería de KOS.
