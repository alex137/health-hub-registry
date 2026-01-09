# Schema: Provider↔Hub Endpoint Manifest

Participants exchange relationship endpoints via an STP manifest table:

`[SeqNo]\t[TS]\t+\t[endpoint_type]\t[URL]`

Endpoint types:
- `fhir_subscribe`
- `fhir_read`
- `direct_message`
- `manifest_notify`

Change propagation:
- When a participant updates its manifest, it POSTs a notify to the peer’s `manifest_notify` URL with `table=<Manifest_URL>`.
- Peers MAY poll manifests; recipients use GET with `since_id` to recover gaps.

Unknown `endpoint_type` values MUST NOT break clients.
