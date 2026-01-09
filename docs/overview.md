# Overview

Health hubs (Apple Health, Guava, Picnic, OneRecord, etc.) are becoming the primary way patients aggregate records and communicate about care.
But adoption is capped because hubs cannot reliably obtain complete, continuous provider records without manual workflows.

**Health Hub Registry** fixes the missing layer:

- Patients choose a hub
- Payers confirm authorization (revocable)
- Providers continuously deliver records + accept hub-mediated messaging
- The registry only routes **endpoint URLs + ephemeral tokens** (no PHI)

The result is a universal, patient-controlled interoperability layer that enables:
- proxy + emergency access
- faster prior authorization and audits
- targeted safety messages (recalls, safety signals)
- real-world evidence capture and trial recruitment

The implementation is intentionally small: most core behavior is expressed as a handful of **STP tables** and **authorization semantics**.

See `protocol/spec.md` for the normative definition.
