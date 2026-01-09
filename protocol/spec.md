# Health Hub Registry Protocol — Specification (Draft v0.1)

This document specifies the **Health Hub Registry** routing + discovery layer.

## Principles

1. **Registry never handles PHI** — only endpoint URLs and ephemeral match tokens.
2. **Deterministic matching** — performed on ephemeral tokens (rotating HMAC sets).
3. **Authorization enforcement** — payer-confirmed approval is the safe-harbor trigger for exchange.
4. **Auditability** — all control-plane state is expressed as ordered STP tables.

## Components

- **Participants:** payers, providers, hubs, publishers
- **Control plane:** STP tables (registry inputs, match streams, beneficiary endpoints, manifests)
- **Data plane:** FHIR subscriptions/reads + Direct messaging

## Core STP tables

1. **Endpoint→Token inputs** (`schemas/endpoint_token_inputs.schema.md`)
2. **Registry match streams** (`schemas/registry_match_streams.schema.md`)
3. **Payer beneficiary endpoints** (`schemas/beneficiary_endpoint.schema.md`)
4. **Provider↔Hub endpoint manifests** (`schemas/endpoint_manifest.schema.md`)

## High-level flow

1. Participants post endpoint→token mappings (EMTP token sets) to the registry.
2. The registry computes match streams and exposes them as STP tables per participant role.
3. Hubs and providers long-poll match streams and begin monitoring newly returned beneficiary endpoints.
4. Payers expose beneficiary endpoints with `Pending|Approved|Denied` status and URLs.
5. Providers deliver FHIR + accept Direct messages for approved hubs; terminate only on explicit revocation.

_Normative semantics are defined in the schema documents and examples._
