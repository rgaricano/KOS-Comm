# KOS-ADR-000001 — Confidence Levels

## Estado
Accepted

## Contexto
Durante el trabajo de laboratorio se detectó la necesidad de distinguir entre datos verificados, estimados, no disponibles e inválidos.

## Decisión
Se adopta un sistema de niveles de confianza común para todos los informes y artefactos del laboratorio.

## Convención
- `✓` Verified
- `◊` Estimated
- `¿?` Unavailable
- `✗` Invalid

## Consecuencias
- Los informes ganan trazabilidad.
- Se reduce la ambigüedad al mostrar datos procedentes de fuentes externas o reconstruidas.
- El formato será reutilizable por el Runtime real.
