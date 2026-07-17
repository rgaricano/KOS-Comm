# ADR-0002 — Holographic State and Context

## Status
Accepted

## Context

Durante la refundación de KOS-Lab se revisó la arquitectura conceptual para eliminar cualquier noción de componente central privilegiado.

## Decision

KOS no posee un centro arquitectónico ni funcional.

El único concepto global es el Estado Cognitivo Persistente.

El estado está constituido por el conjunto de objetos canónicos, sus relaciones, restricciones, evidencia e historia.

Los contextos no son entidades persistentes; son proyecciones temporales del estado cognitivo.

El Canon no constituye una excepción. El Canon Consolidado es una representación (render) de un estado determinado y deberá poder regenerarse desde el mismo mecanismo que cualquier otro contexto.

## Principles

1. El estado es persistente.
2. El contexto es una proyección temporal del estado.
3. Ningún componente tiene un papel central privilegiado.
4. Todo conocimiento se gestiona mediante los mismos mecanismos.
5. El Canon no requiere un procesador exclusivo.
6. Cualquier representación es una proyección del estado, no la fuente del conocimiento.

## Consequences

- Se descarta la noción de un 'Canon Compiler' como componente permanente.
- El importador del Canon será únicamente una herramienta de migración.
- El Runtime no se modelará alrededor de un núcleo central de conocimiento.
- Las capacidades de composición y renderizado serán genéricas y aplicables a cualquier conjunto de objetos.
