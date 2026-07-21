# Authority / Ownership / Derivation Matrix — KCA Phase A

**Status:** Working architectural synthesis  
**Date:** 2026-07-21

## 1. Rule

KCA transports representations. It does not implicitly transfer source ownership, canonical authority, truth status or persistence status.

## 2. Matrix

| Class | Typical owner/authority | Canonical? | Persistent by definition? | Derived? | Transmittable? | Receipt implies import? | Source identity retained? |
|---|---|---:|---:|---:|---:|---:|---:|
| Canonical Object | source canonical authority | yes | no; persistence is separate | no | yes, by explicit transfer representation | no | yes |
| Knowledge-role Object | source canonical authority | yes | no | no | yes | no | yes |
| Canonical Relationship | source canonical authority | yes/canonical capability | no | no | yes | no | yes when identity exists |
| Inline Evidence | containing/source authority | no independent identity required | with containing representation | no | yes | no | contextual |
| Canonical Evidence Object | source canonical authority | yes | no | no | yes/referenceable | no | yes |
| Evidence Provenance | source/evidence producer | semantic attribute | with represented evidence when persisted | descriptive | yes | no | normally |
| Semantic Version | source semantic authority | dimension of canonical representation | with representation | no | yes | no | yes |
| Transactional Revision | persistence authority | no | persistence-specific | operational | conditionally | no | references source object |
| Operation Identity | operation initiator/coordinator | no | no | operational | yes | no | optional correlation |
| Publication Result | persistence/operation subsystem | no | no | yes/operational | yes | no | may reference source |
| Persistent Cognitive State | source system composition | emergent over canonical graph | reconstructible from persistence | emergent | not directly as a root | no | composed |
| StateObservation | observer/source boundary | no | no | yes | yes | no | yes (`object_id`) |
| Context Selection | selector/context owner | no | no | yes | yes as boundary semantics | no | references selected sources |
| Cognitive Projection | projection producer | no | no | yes | yes | no | yes through provenance |
| Projection Provenance | projection producer | no | no | yes | yes | no | yes |
| Consumer Context View | receiving/consumer context | no | no | yes | yes | no | possibly |

## 3. Authority transitions

Allowed authority changes require an explicit receiver-side act, for example:

```text
RECEIVE
  ↓
VALIDATE / RESOLVE
  ↓
APPLY RECEIVER POLICY
  ↓
IMPORT / ACCEPT / PUBLISH
  ↓
NEW RECEIVER-SIDE AUTHORITY STATUS
```

There is no valid implicit transition:

```text
RECEIVE -> CANONICAL
```

or:

```text
PROVENANCE PRESENT -> AUTHORITATIVE
```

## 4. Ownership rule

Communication ownership and semantic ownership are separate:

```text
packet/message ownership
    !=
representation authorship
    !=
source object ownership
    !=
canonical authority
```

## 5. Derivation rule

Derived information must preserve derivation status across KCA unless an explicit receiver operation creates a new receiver-owned canonical object.

```text
source object
   ↓ observe/select/project
projection
   ↓ transmit
received projection
   ↓ explicit receiver import/transform decision
possible new receiver canonical object
```

The final object, if created, has receiver-side authority semantics and must not masquerade as the unchanged source canonical object unless identity/authority federation explicitly permits that interpretation.
