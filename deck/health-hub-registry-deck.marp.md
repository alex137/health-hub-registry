---
marp: true
theme: default
paginate: true
style: |
  section {
    font-family: Arial, sans-serif;
    padding: 40px;
  }
  h1 {
    color: #1a5276;
    font-family: Georgia, serif;
    font-size: 1.6em;
  }
  h2 {
    color: #1a5276;
    font-family: Georgia, serif;
  }
  h3 {
    color: #1a5276;
  }
  strong {
    color: #1a5276;
  }
 a {
  color: #1a5276;
  text-decoration: none;
  }
  a:hover {
  text-decoration: underline;
  }
  section.title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  section.title h1 {
    font-size: 2.5em;
    margin-bottom: 0.2em;
  }
  blockquote {
    background: #1a5276;
    color: white;
    padding: 20px 30px;
    border-radius: 8px;
    border-left: none;
    font-size: 1.1em;
  }
  blockquote strong {
    color: white;
  }
  .card {
    background: #f0f4f7;
    padding: 16px 20px;
    border-radius: 6px;
    margin: 12px 0;
  }
  .bottomline {
    background: #e8f1f5;
    border-left: 4px solid #1a5276;
    padding: 16px 20px;
    border-radius: 0 6px 6px 0;
    margin-top: 20px;
  }
---

<!-- _class: title -->

# Patient-Chosen Health Hubs

**A Patient-Controlled Interoperability Layer**

January 2026

---

# Health Hubs

Millions use Apple Health, Guava, Picnic, OneRecord, and others to:

- **Aggregate + organize** medical records across providers
- **Help patients interpret** results and manage conditions (AI-assisted)
- **Enable access** to async care, virtual visits, and home diagnostics
- **Keep clinicians informed** (especially in transitions & emergencies)
- **Support proxies** for seniors and complex chronic care

---

# Promise of Hub Value for Payers

**Better outcomes, lower medical + admin cost.**

- **Lower total cost of care:** better self-management + navigation → fewer avoidable ED visits + better chronic control
- **Administrative deflection:** shift portal + call-center volume to record-aware self-service workflows
- **Network + benefit steerage:** guide members in-network with real-time estimates + prior-auth rules
- **Faster prior auth + claims audits:** records assembled automatically → fewer provider callbacks and faster AI-assisted review
- **High-risk member support:** proxy/caregiver workflows improve outcomes for seniors and complex chronic populations

---

# But the Hub Flywheel Is Broken

- **No provider automation → bad flow:** fragmented portals + inconsistent APIs → incomplete/late records, manual retrieval
- **Bad flow → high CAC:** payers won't subsidize until value is reliable
- **High CAC → no scale:** hubs can't reach mass adoption
- **No scale → no provider automation:** providers won't invest in record exchange, messaging, scheduling

Providers also need HHS clarity on trust/liability (HIPAA, provenance, responsibility) before they invest.

**Bottom line:** Private actors can't break this flywheel — **HHS can.**

---

# What Ideal Flow Looks Like

1. **User registers with a hub**
2. **Hub redirects user to payer** to confirm approval
3. **User approves hub** on payer site (revocable)
4. **Payer pushes approval** to the user's providers
5. **Providers auto-exchange records + messages** with the hub
6. **Patients get coordinated care; payers cut costs.**

**Missing piece:** a registry that makes discovery + authorization universal.

---

# healthhubregistry.gov

**A lightweight discovery + authorization layer that makes the ideal flow universal.**

- The core protocol fits in a handful of appendix slides  
- The registry never handles PHI — it only routes endpoints + approvals  
- It relies on two open primitives designed for reuse beyond healthcare:
  - **[STP](https://github.com/alex137/state-transfer-protocol):** State Transfer Protocol (streaming tables over HTTP)
  - **[EMTP](https://github.com/alex137/ephemeral-match-token-protocol):** Ephemeral Match Tokens (privacy-preserving matching)

**Spec + reference implementation:**  
https://github.com/alex137/health-hub-registry

**Bottom line:** This is a buildable system, not a research project.

----

# Registry Participant Requirements

- Hubs/payers/providers post hashed identifiers for patient matching
- Beneficiaries approve/revoke matched hub PHI access via their payer
- Payers share plan + network + cost sharing data with approved hubs
- Providers obtain their patients' approved hubs from their payers
- Providers & approved hubs exchange FHIR records + Direct messages
- Hubs post provider record-delivery performance reports

---

# Enforcement and Adoption

- Registry never handles PHI

- Treat payer-confirmed approval as HIPAA safe harbor for PHI exchange

- Use hub reports to automate information-blocking enforcement at scale

- Make hubs a covered digital benefit; tie to quality metrics for hub-enabled workflows (care transitions, prior-auth)

**Bottom line:** Payment incentives + scalable enforcement can create the first universal, patient-controlled interoperability layer.

---
# What Universal Hubs Enable

Once hubs work across providers,

here's what becomes possible at scale.


---

# Hubs: Proxy + Emergency Access

**Proxy usage:** Hubs may let users designate proxies to approve record exchange and manage care on their behalf — useful for seniors and complex chronic care (ongoing or emergency-only, optionally with delay).

**Provider authorization policy:** Hubs may require user confirmation or auto-approve provider requests based on patient preferences + hub policy (e.g., provider reputation, prior relationship, context). Requests using an **emergency provider TLS certificate** may follow a different policy.

**Audit + notice:** Hubs should log proxy/emergency flows and notify users via multiple channels.

*Immediate access to allergies, meds, directives, and proxy designations is a strong adoption driver.*

---

# Benefit: Speeding Prior Authorization

Prior auth delays are mostly **documentation delays** that hubs can solve.

Payer investigators request access via a **Consent Request Direct Message** *(Appendix)*. Upon user approval, hubs issue a **Consent Grant** enabling **time-limited, scoped access** to the aggregate record *solely* for prior-auth and claims-audit review.

- **Patients:** faster approvals, less stress
- **Providers:** less doc churn, lower audit burden, less non-payment risk
- **Payers:** lower admin cost, faster and more consistent decisions

**Bottom line:** Prior-auth relief creates a near-term reason for payers and providers to adopt hub workflows.

---

# Hub-Era Provider Direct Messaging

When records are universal, messaging becomes **contextual, routable, and attachable**.

As hubs make cross-provider records ubiquitous, Direct messages MUST identify **sender type** and **patient/record context** for fast triage.

**Provider↔Provider (record questions):** Providers MUST include a **patient- or record-specific messaging endpoint** in FHIR Provenance; other providers MUST use it when present.

**Hub↔Provider (patient-authorized):** Providers MUST accept messages from **approved hubs** at the same endpoint used for FHIR subscription fulfillment; replies route to sender endpoint.

Required metadata (sender_role, message_category) enables triage, routing, and response tracking (Appendix).


# Hub-Era Provider Direct Messaging

As hubs make cross-provider records ubiquitous, Direct messages MUST identify **sender type** and **patient/record context** for fast triage.

**Provider↔Provider (record questions):** Providers MUST include a **patient- or record-specific messaging endpoint** in FHIR Provenance; other providers MUST use it when present.

**Hub↔Provider (patient-authorized):** Providers MUST accept messages from **approved hubs** at the same endpoint used for FHIR subscription fulfillment; replies route to sender endpoint.

Required metadata (sender_role, message_category) enables triage, routing, and response tracking (Appendix).

---

# Hubs as the Primary Patient Channel

Hubs can become the default place patients communicate about care — replacing fragmented portals.

- Providers and pharmacies SHOULD accept hub-mediated threads for clinical questions, refills, substitutions, and follow-ups.

- Payers SHOULD support hub-mediated threads for coverage questions, prior-auth status, claims issues, and appeals.

- Hubs SHOULD mediate scheduling and care-transition coordination across providers.

- HHS SHOULD grant SMS/WhatsApp safe harbor for hub-mediated delivery under defined safeguards.

---

# Benefit: Targeted Direct Messages

Today, recalls, safety signals, protocol changes, and research requests are posted to websites — and affected patients/providers often never see them.

**Targeted Direct Messages (TDMs)** solve this. They are a Direct Messaging extension where a message is addressed not to a specific recipient, but instead to a deterministic targeting rule (e.g. a boolean predicate of RxNorm, ICD10, timeframe, etc.).

Publishers (FDA/CDC / ONC-approved entity) pull the hub list from the registry and send the TDM to each hub. Hubs match locally (possibly using AI to refine) and deliver to the right providers.

**Result:** safety-critical messages reach the right providers (via provenance endpoints) — and attach to the right records — automatically.

---

# Benefit: Real-Time Real-World Evidence

Research hubs enable near-real-time adverse event capture, real-world controls, and rapid trial recruitment — without years of data-sharing negotiation.

1. Recruit via `research_request` **Targeted Direct Messages** containing a **Consent Request**.

2. Upon approval, the user's hub posts a **Consent Grant** (user contact endpoint + identity hashes) to the Consent Request URL.

3. Research hub registers like any other hub; after payer approval, providers deliver records via standard FHIR subscriptions.

---

# Completing the Data Plane: Pharmacy Participation

*Medications are the most frequent and error-prone part of care — but today's interoperability layer misses the dispense reality.* Today, neither providers nor hubs can reliably know whether a prescribed medication was **filled, substituted, refilled, or abandoned**.

HHS should require pharmacies to operate as **registry-certified provider-like endpoints**, so hubs can FHIR subscribe and receive:

- **Fill + refill status** (including non-pickup / abandonment)
- **Substitutions + med changes** (dispensed NDC mapped to RxNorm)
- **Adherence signals** (late refills, gaps, early discontinuation)

**Result:** safer prescribing, fewer errors, better chronic disease management; the med list reflects what happened, not just what was ordered.

---

# Pharmacy Unlocks: Safety + Automation

**Care transitions:** discharge meds become verifiable and shareable → fewer readmissions + reconciliation errors

**Prior auth + audits:** medication history and proof-of-fill can be assembled automatically → less documentation churn *(and enables non-adherence detection for high-risk conditions like schizophrenia)*

**Targeted safety alerts:** pharmacies and hubs should receive **TDMs** for recalls + safety signals + substitution/formulary changes

**Messaging:** pharmacies SHOULD support Direct messaging with providers + hub-mediated patients for refill coordination and substitution clarification

**Bottom line:** Without pharmacy participation, the "universal health hub" is missing the most time-sensitive part of the record.

---

# Conclusion: Patient-Controlled Healthcare

Patient-chosen hubs create a **universal information bus** for healthcare—where patients control the aggregation point and the system routes data, messaging, safety signals, and research through it.

When that layer exists, providers coordinate from a shared record, prescriptions reflect dispense reality, recalls reach affected patients fast, and real-world evidence becomes continuous—with privacy patients can trust.

**HHS can make this happen. Hubs already exist. The path is clear.**

---

# Questions?

S. Alexander Jacobson
alex@137ventures.com

---

# Appendix ToC (1 of 2)

1. [Common Questions](#common-questions)
2. [Protocol Assumptions](#protocol-assumptions)
3. [Identifier Hash System](#identifier-hash-system)
4. [SyncURL Protocol](#syncurl-protocol)
5. [SyncURL Push Option](#syncurl-push-option)
6. [Endpoint→Hash Tables](#endpoint-hash-tables)
7. [Registry Match Tables](#registry-match-tables)
8. [Polling Responsibilities](#polling-responsibilities)

---

# Appendix ToC (2 of 2)

1. [Payer Beneficiary Endpoint (Hub View)](#beneficiary-endpoint-hub-view)
2. [Payer Beneficiary Endpoint (Provider View)](#beneficiary-endpoint-provider-view)
3. [Registry Trust Establishment](#registry-trust-establishment)
4. [Trust Enforcement + Revocation](#trust-enforcement-revocation)
5. [Required Direct Message Metadata](#required-direct-message-metadata)
6. [Consent Request + Grant](#consent-request-grant)
7. [Targeted Direct Message Headers](#tdm-headers)

---

<a id="common-questions"></a>

# Appendix: Common Questions

- How does the registry prevent a national patient ID?
- Is this just TEFCA with extra steps?
- What about patients without insurance?

---

# How Does the Registry Prevent a National Patient ID?

Participants generate rotating HMAC identifier sets locally using an ONC-published algorithm and time-limited keys. The registry matches only ephemeral hashes and never receives demographics or stores a permanent identifier. Key rotation and variant expansion prevent the system from becoming a national patient ID.

---

# Is This Just TEFCA With Extra Steps?

No. TEFCA is institution-to-institution exchange—it helps providers share records with each other, but leaves patients navigating multiple portals and requesting records episodically.

This framework is patient-authorized endpoint enforcement. Patients designate hubs; providers must fulfill continuously to those hubs. The enforcement locus shifts from institutional negotiation to patient rights.

---

# What About Patients Without Insurance?

Patients without payer coverage won't have payers to confirm hub authorizations. Options for these patients:

- State Medicaid agencies could serve as authorization-only participants for uninsured residents
- ACA healthcare navigators could operate confirmation interfaces while helping patients enroll in coverage
- This creates a pathway to both hub access and coverage enrollment

This is a policy decision, not a protocol requirement.

---
<a id="protocol-assumptions"></a>

# Appendix: Protocol Assumptions

- All system-to-system communication uses **HTTPS + mTLS**.
- Participants are authorized by **certificate Policy OIDs**.
- Control plane: **SyncURL** (routing, approvals, endpoint manifests).
- Data plane: **FHIR** (records/benefits/subscriptions) + **Direct**.
- Hubs subscribe promptly to newly discovered provider endpoints.
- Missing payer endpoints or outages are not revocations; prior status remains authoritative until explicit update.

---

<a id="registry-trust-establishment"></a>

# Appendix: Registry Certificates

- **Trust anchor bundle:** Registry root URL serves a PEM bundle of trusted CA roots for authenticating system participants.

- **mTLS required:** All system-to-system communication MUST use mutual TLS and reject connections that fail chain validation.

- **Role-based certificates:** Participant certificates MUST include a **Policy OID** in `Certificate Policies` identifying role:
  `payer | hub | provider | emergency_provider | tdm_publisher | direct_distributor`

- **Provider identity binding:** Provider certificates MUST encode **NPI** in `SubjectAltName.otherName` using the designated NPI OID.

---

<a id="trust-enforcement-revocation"></a>

# Appendix: Trust Enforcement + Revocation

- **Role enforcement:** Systems MUST authorize requests based on certificate role (Policy OID) and reject invalid role usage.

- **Revocation:** Registry publishes revoked certificate serial numbers via SyncURL at:
  `[rootURL]/crl`
  Participants MUST reject connections involving revoked serials.

- **OID registry:** The registry publishes the authoritative list of role Policy OIDs (and the NPI OID) in the open-source hash/spec repository.

----


<a id="identifier-hash-system"></a>

# Appendix: Identifier Hashes (Not NPIs)

Payers, providers, and hubs MUST use the Registry **hashing function** (source code at [registryRoot]/code) to generate the matchable **HMAC identifier hashes** they post with endpoint URLs.

The function generates hashes of **name, DOB, phone, address tuple variants** using current + prior **registry keys.**

Each month, the Registry distributes **rotating HMAC keys** to **Credentialed Participants** (HIPAA entities / BAs). Restricted key access is a **privacy circuit-breaker**: the Registry can revoke keys for misuse.

**Rotating keys + no demographics → ephemeral hashes; no de facto NPI.**

---

<a id="endpoint-hash-tables"></a>

# Appendix: Endpoint→Hash Tables (Registry Inputs)

**Schema (payers/providers/hubs):**

`[SeqNo] \t [TS] \t [+/-] \t [Endpoint_URL] \t [Identity_Hashes...]`

- Primary key = Endpoint_URL
- Record = whitespace-separated HMAC hashes (hex)
- `-` Endpoint_URL revokes the endpoint/hash binding

---

<a id="registry-match-tables"></a>

# Appendix: Registry Match Tables

- **Payer match stream:** [Beneficiary_Endpoint_URL] → [Hub_User_Endpoint_URLs...]
- **Provider match stream:** [Patient_Endpoint_URL] → [Payer_Beneficiary_Endpoint_URLs...]
- **Hub match stream:** [User_Endpoint_URL] → [Payer_Beneficiary_Endpoint_URLs...]

The match streams are authoritative for which endpoints exist for a given participant.

---

<a id="syncurl-protocol"></a>




# Appendix: SyncURL Streaming Tables 

**Format:** HTTP `GET` returns TSV rows:
`[SeqNo] \t [RFC3339 UTC Time Stamp] \t [+/-] \t [Primary Key] \t [Record]`

**Ordering + auditability:** Servers MUST return rows in strictly increasing `SeqNo` order and retain the full append-only stream.  Clients MUST tolerate duplicate rows (same `SeqNo`) and process idempotently.

**Content-Type:** `application/syncurl+tsv; schema=<schema_id>; version=<n>`

**Actions:** + = add/replace, - = delete.

**Delta sync:** `?since_id=N` returns rows with SeqNo > N.  `?since_id=-N` returns the last N rows. If absent, treat as `since_id=0`.

**Compact view:** `?view=active` MAY omit keys with latest row `-`.

**Long-poll:** Servers SHOULD stream until timeout or no rows available, then close; clients reconnect with last seen SeqNo.

---

<a id="syncurl-notify-option"></a>

# **Appendix: SyncURL Notify**

Participants MAY expose **notify URLs** that peers can POST to in order to announce a **new table** the recipient should begin monitoring, or signal that an existing table **has new rows**.

POST <notify_url>
Content-Type: application/x-www-form-urlencoded
Body MUST include: table=<SyncURL_Table_URL>

`table` MUST be a SyncURL table URL. Recipients track last processed `SeqNo` and GET with `since_id` as needed to retrieve new rows and recover gaps.

Notify POSTs are idempotent and may be retried.

---

<a id="polling-responsibilities"></a>

# Appendix: Polling Responsibilities

The registry match stream is the authoritative mapping from identifier hashes → endpoint URLs. Clients MUST long-poll their registry match stream and begin monitoring newly returned endpoints.

- **Hubs** receive **Beneficiary_Endpoint_URLs** per user and MUST monitor each for approval status (`Pending | Approved | Denied`).

- **Providers** receive **Beneficiary_Endpoint_URLs** per patient and MUST monitor each for hub approvals/revocations (`+/- Hub_User_Endpoint_URL`).

- **Payers** receive **Hub_User_Endpoint_URLs** per beneficiary and MUST provide approval/denial user interface (also reachable via `Pending → Payer_Approval_URL`).

---

<a id="beneficiary-endpoint-hub-view"></a>

# Appendix: Payer Beneficiary Endpoint (Hub View)

`[SeqNo] \t [TS] \t [+/-] \t [Pending|Approved|Denied] \t [URL]`

- `Pending → Payer_Approval_URL` (not revocation)
- `Approved → FHIR_Plan_URL` (subscribe)
- `Denied → Reason_URL` (denied/revoked)

If `FHIR_Plan_URL` changes, hub MUST re-subscribe.

Delete user records + terminate provider subscriptions only when Denied at all payer endpoints returned by the registry.

---

<a id="beneficiary-endpoint-provider-view"></a>

# Appendix: Payer Beneficiary Endpoint (Provider View)

Provider-facing SyncURL table returned based on provider mTLS identity:

`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_Endpoint_URL] \t [optional metadata]`

- Approved hubs appear via `+ Hub_User_Endpoint_URL`
- Revocation is `- Hub_User_Endpoint_URL` (**explicit**)

**Semantics**

- Begin/maintain exchange when + Hub_User_Endpoint_URL appears.
- Terminate *only* when `- Hub_User_Endpoint_URL` is seen from all payer endpoints returned by the registry.

---

<a id="endpoint-manifest"></a>

# Appendix: Provider↔Hub Endpoint Exchange

Providers and hubs exchange relationship endpoints via SyncURL "manifest" tables.

`[SeqNo]\t[TS]\t+\t[endpoint_type]\t[URL]`

**Endpoint types:** `fhir_subscribe` | `fhir_read` | `direct_message` | `manifest_notify`

**Change propagation:** When a participant updates its manifest, it POSTs to the peer’s `manifest_notify` URL with `table=Manifest_URL`. Peers may re-GET the manifest (authoritative).

Unknown `endpoint_type` values MUST NOT break clients.

----

<a id="endpoint-manifest-example"></a>

# Appendix: Endpoint Manifest — Example

**Provider discovers:** `Hub_User_Endpoint_URL`

1) **Provider → Hub (announce + give manifest URL)**  
`POST Hub_User_Endpoint_URL?table=Provider_Manifest_URL` 

2) **Hub → Provider (GET provider manifest)**  
`GET Provider_Manifest_URL?since_id=0`

Returns (SyncURL rows):  
`+ fhir_subscribe   https://prov.com/fhir/sub`  
`+ fhir_read        https://prov.com/fhir/read`  
`+ direct_message   https://prov.com/direct`  
`+ manifest_notify  https://prov.com/notify`  

3) **Provider → Hub (GET hub manifest)**  
`GET Hub_User_Endpoint_URL?since_id=0`

**If hub endpoints change:**  
Hub `POST https://prov.com/notify?table=Hub_Manifest_URL` → Provider re-GETs `Hub_Manifest_URL` *(authoritative)*.
---

<a id="required-direct-message-metadata"></a>

# Appendix: Required Direct Message Metadata

`sender_role: provider | hub | patient | proxy | payer | pharmacy | emergency_provider`

`message_category: clinical | scheduling | administrative | billing | coverage | prior_auth | claims | appeal | refill | pharmacy | other`

Unknown values MUST be displayed but MUST NOT cause rejection.

---

<a id="consent-request-grant"></a>

# Appendix: Consent Request + Grant

**Used for prior-auth, audit, and research**

**Requests:** `message_category: consent_request` MUST include: `requestor_id`, `purpose`, `scope`, `expires_at`, `consent_request_url`
`consent_request_url` MUST return canonical terms and accept SyncURL POSTs.

**Grants:** Upon approval, hub POSTs SyncURL rows:
`[SeqNo] \t [Time] \t + \t [Hub_User_Endpoint_URL] \t [Identity_Hashes...]`
(Optional: `table=Hub_Grant_Stream_URL` for replay/polling.)

Hubs MUST support immediate revocation + audit logging.

---

<a id="tdm-headers"></a>

# Appendix: TDM Required Headers

- `schema_version`: targeting semantics version (e.g., v1)
- `filter`: deterministic predicate over coded fields *(RxNorm, ICD10/SNOMED, CPT, LOINC, demographics, timeframe)*
- `message_type`: `recall | safety_signal | advisory | protocol_change | research_request | payer_policy_change`
- `deliver_to`: `patient | product_provider | treating_providers` *(product_provider = prescriber / ordering / implanting clinician)*
- `valid_until`: expiration timestamp
- `context` (optional): free-text rationale / instructions

**Matching:** filter MUST be applied deterministically; AI MAY refine only after a filter hit. Unknown keys MUST be ignored.
