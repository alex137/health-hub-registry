# Health Hub Registry Protocol

**Health Hub Registry** is a patient-controlled interoperability layer that makes hub authorization and continuous record delivery universal — without the registry ever handling PHI.

The registry is a **routing + discovery** layer that crosswalks **ephemeral match tokens → endpoint URLs**, and enables payers to confirm patient authorization in a way providers can safely honor.

This protocol composes with two open primitives designed for reuse beyond healthcare:
- **STP (State Transfer Protocol):** streaming and synchronizing table state over HTTP with ordering + gap recovery  
  Repository: https://github.com/alex137/state-transfer-protocol
- **EMTP (Ephemeral Match Token Protocol):** privacy-preserving identity matching via rotating HMAC token sets  
  Repository: https://github.com/alex137/ephemeral-match-token-protocol

> **Bottom line:** This is a buildable system (not a research project) using small, auditable primitives.

---

## Repo structure

- `docs/` — narrative overview + implementer notes
- `protocol/` — core registry protocol specification
- `schemas/` — STP schema definitions used by the registry (match streams, endpoints, manifests, etc.)
- `examples/` — worked examples and message flows (hub signup, provider bootstrap, revocation)
- `code/` — reference code (hash/token generation, schema validators)

---

## Quick start

1. Read **Overview**: `docs/overview.md`
2. Read the **Core Spec**: `protocol/spec.md`
3. Implement STP tables using the schemas in `schemas/`
4. Use EMTP to generate rotating match tokens posted into the registry input tables
5. Validate end-to-end behavior using `examples/`

---

## License
MIT
