# KCA — Knowledge Communication Architecture

## 1. Propósito

KCA define la arquitectura de referencia para el intercambio, continuidad y proyección de información y conocimiento entre componentes cognitivos de KOS.

KCA no es un protocolo, un formato de serialización ni una API. Es el marco arquitectónico que separa responsabilidades y establece las relaciones entre representación, codificación, comunicación, continuidad y proyección.

## 2. Problema de ingeniería

KOS no necesita únicamente transportar mensajes. Necesita preservar significado, identidad, procedencia, evidencia y estado operativo cuando la información atraviesa fronteras entre componentes, procesos, sesiones o consumidores.

Por ello, el problema se formula como transferencia y reconstrucción de **estado cognitivo verificable**, no como simple mensajería textual.

## 3. Principios

1. **Separación de responsabilidades.** Representación, codificación, comunicación, continuidad y proyección son capas distintas.
2. **Semántica antes que codificación.** El modelo de información precede a cualquier representación física.
3. **Estado antes que conversación.** El activo relevante es el estado cognitivo verificable; una conversación es solo una posible fuente o representación.
4. **Agnosticismo de consumidor.** Las capas inferiores no dependen de un LLM, UI, API o proveedor concreto.
5. **Continuidad determinista.** La reconstrucción debe estar gobernada por entradas, reglas y evidencia explícitas.
6. **Procedencia preservada.** Las transformaciones no deben borrar el origen o autoridad de los datos fuente.
7. **Integridad verificable.** La codificación y comunicación deben permitir detectar corrupción, incompatibilidad o pérdida.
8. **Evolución explícita.** Versiones, capacidades y extensiones deben poder negociarse sin ambigüedad.
9. **Observabilidad.** Los intercambios y transformaciones relevantes deben poder auditarse.
10. **No transferencia implícita de autoridad.** Una representación derivada no se convierte automáticamente en conocimiento canónico.

## 4. Arquitectura en capas

```text
Applications / Cognitive Consumers
──────────────────────────────────
CP — Cognitive Projection
──────────────────────────────────
KSCL — Knowledge Session Continuity Layer
──────────────────────────────────
KCP — Knowledge Communication Protocol
──────────────────────────────────
KEncoding — Knowledge Encoding
──────────────────────────────────
KRM — Knowledge Representation Model
──────────────────────────────────
Persistence / Canonical Knowledge Sources
```

## 5. KRM — Knowledge Representation Model

KRM define la semántica y estructura lógica de las unidades de información y conocimiento relevantes para comunicación.

Debe responder, entre otras, a estas preguntas:

- ¿qué constituye una entidad, observación, relación, decisión, evidencia, intención, restricción o artefacto?;
- ¿qué identidad tiene cada objeto?;
- ¿qué metadatos son obligatorios?;
- ¿cómo se representa procedencia y autoridad?;
- ¿qué relaciones existen entre estado persistente, observación y representación derivada?;

KRM debe reutilizar o mapear explícitamente el modelo canónico de KOS; no debe crear silenciosamente un segundo modelo de conocimiento incompatible.

## 6. KEncoding — Knowledge Encoding

KEncoding transforma estructuras KRM en representaciones intercambiables.

Responsabilidades previstas:

- serialización y deserialización;
- identificación de versión;
- representación de tipos;
- integridad;
- canonicalización cuando sea necesaria;
- compatibilidad y extensibilidad;
- soporte para firmas o autenticidad cuando proceda;
- eficiencia de representación.

La codificación no debe introducir semántica que pertenezca a KRM.

## 7. KCP — Knowledge Communication Protocol

KCP define cómo se intercambian unidades codificadas entre nodos o componentes.

Responsabilidades candidatas:

- encapsulado;
- identificación de origen y destino lógico;
- correlación;
- secuenciación;
- fragmentación y reensamblado cuando sean necesarios;
- confirmación y estados de entrega;
- detección de duplicados;
- negociación de capacidades;
- control de errores a nivel de protocolo.

KCP no debe decidir qué conocimiento es canónico ni cómo debe proyectarse a un consumidor.

### Knowledge Exchange Unit

Se propone **KEU — Knowledge Exchange Unit** como nombre provisional de la unidad lógica de intercambio de KCP.

La definición formal de KEU queda pendiente del trabajo KRM/KEncoding y no se considera todavía cerrada.

## 8. KSCL — Knowledge Session Continuity Layer

KSCL define los mecanismos para preservar y reconstruir continuidad operacional/cognitiva entre sesiones o puntos de ejecución.

Debe estudiar, como mínimo:

- checkpoints;
- referencias de estado;
- contexto activo;
- decisiones abiertas;
- restricciones;
- objetivos;
- tareas pendientes;
- evidencia relevante;
- historial mínimo necesario para reconstrucción;
- detección de divergencia o estado incompleto.

KSCL no debe confundirse con el transporte KCP ni con la persistencia canónica.

## 9. CP — Cognitive Projection

CP adapta un estado observable o reconstruido a las necesidades de un consumidor.

Consumidores posibles:

- LLM;
- agente;
- API;
- CLI;
- interfaz humana;
- auditoría;
- otro componente KOS.

KCA adopta como restricción la frontera ya establecida en KOS: una proyección es derivada y no adquiere por defecto identidad o autoridad canónica sobre los objetos fuente.

## 10. Flujo conceptual

```text
Canonical / Persistent Knowledge
            │
            ▼
           KRM
            │
            ▼
       KEncoding
            │
            ▼
           KCP
            │
            ▼
          KSCL
            │
            ▼
            CP
            │
            ▼
        Consumer
```

Este flujo es conceptual. No implica todavía que toda comunicación real deba atravesar físicamente todas las capas en todos los casos.

## 11. Plano de datos y plano de control

KCA deberá distinguir formalmente al menos:

### Data plane

Transporta o transforma unidades de información/conocimiento.

### Control plane

Gestiona capacidades, versiones, negociación, errores, continuidad, correlación y estados del protocolo.

La separación exacta queda pendiente de especificación.

## 12. Invariantes iniciales

```text
REPRESENTATION != ENCODING
ENCODING != COMMUNICATION
COMMUNICATION != CONTINUITY
CONTINUITY != PROJECTION
PROJECTION != CANONICAL AUTHORITY
```

Y adicionalmente:

```text
DERIVED VIEW != SOURCE KNOWLEDGE
MESSAGE HISTORY != COGNITIVE STATE
TRANSPORT SUCCESS != SEMANTIC ACCEPTANCE
```

## 13. Relación con KOS

KCA debe integrarse con la arquitectura KOS existente sin reabrir de forma implícita programas cerrados.

Se deberán analizar especialmente:

- Persistent Knowledge Model;
- Persistent Cognitive State;
- Observation Boundary;
- Cognitive Projection;
- Context–Runtime Integration;
- Execution–Runtime Integration;
- evidencia y procedencia;
- identidad canónica y operacional.

Las contradicciones deben registrarse como decisiones arquitectónicas explícitas.

## 14. Estado

**INITIAL DRAFT.**

KCA queda aceptada como marco de trabajo de la rama `KOS-Comn`, pero sus capas, contratos, unidades de intercambio y mecanismos de interoperabilidad requieren desarrollo y validación.

## 15. Próximo desarrollo

El siguiente trabajo arquitectónico es **KRM — Knowledge Representation Model**, porque la semántica de las unidades intercambiables debe quedar definida antes de cerrar KEncoding, KCP o KSCL.
