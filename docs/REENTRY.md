# Reentrada y continuidad

Este documento fija el procedimiento de reconstrucción del contexto para el laboratorio KCA/KCP/KSCL.

## Orden de lectura

1. `README.md`
2. `docs/DEVELOPMENT-STATE.md`
3. `docs/SESSION-CONSOLIDATION.md`
4. `docs/architecture/KCA.md`
5. `docs/adr/ADR-0001-KCA.md`

## Objetivo

Permitir que una nueva sesión reconstruya el estado operativo suficiente para continuar sin depender de memoria externa.

## Antes de modificar

Verificar:

- rama actual;
- HEAD;
- árbol limpio o sucio;
- divergencia con la rama base;
- documento aplicable.

## Estado esperado

Al reentrar, debe ser posible responder:

- qué está cerrado;
- qué está activo;
- qué está propuesto;
- qué documento gobierna;
- cuál es la siguiente acción.

## Regla de persistencia

La fuente de verdad es el repositorio. La conversación solo guía el trabajo.
