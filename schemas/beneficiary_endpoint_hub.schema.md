# Schema: Payer Beneficiary Endpoint (Hub View)

`[SeqNo] \t [TS] \t [+/-] \t [Pending|Approved|Denied] \t [URL]`

- Pending → Payer_Approval_URL (not revocation)
- Approved → FHIR_Plan_URL (subscribe)
- Denied → Reason_URL (denied or revoked)

Semantics:
- If `FHIR_Plan_URL` changes, hub re-subscribes.
- Delete records + terminate provider subscriptions only when **Denied at all payer endpoints**.
