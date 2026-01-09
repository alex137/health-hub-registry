---
marp: true
theme: default
paginate: true
style: |
/* =========================
   Global slide layout
   ========================= */

section {
  font-family: Arial, sans-serif;
  padding: 18px 34px 26px 34px;   /* tighter margins */
  line-height: 1.25;
  font-size: 26px;
}

/* Dense slides */
section.dense {
  padding: 12px 28px 18px 28px;
  font-size: 25px;
  line-height: 1.10;
}

/* Remove extra top margin from first element */
section > :first-child {
  margin-top: 0 !important;
}

/* Tighten paragraph spacing */
section p {
  margin: 0.32em 0;
}

/* =========================
   Headings
   ========================= */

h1 {
  color: #1a5276;
  font-family: Georgia, serif;
  font-size: 1.55em;
  margin: 0 0 0.18em 0;
  line-height: 1.08;
}

h2 {
  color: #1a5276;
  font-family: Georgia, serif;
  font-size: 1.2em;
  margin: 0.12em 0 0.30em 0;
  line-height: 1.12;
}

h3 {
  color: #1a5276;
  font-size: 1.05em;
  margin: 0.1em 0 0.25em 0;
}

/* =========================
   Links + emphasis
   ========================= */

strong { color: #1a5276; }

a {
  color: #1a5276;
  text-decoration: none;
  font-weight: 600;
}
a:hover { text-decoration: underline; }

/* =========================
   Title slide
   ========================= */

section.title {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
section.title h1 {
  font-size: 2.4em;
  margin-bottom: 0.2em;
}

/* =========================
   Bullets
   ========================= */

ul {
  margin: 0.4em 0 0.1em 0;
  padding-left: 1.0em;
}

li { margin: 0.22em 0; }

li::marker { color: #1a5276; }

ul ul {
  margin-top: 0.2em;
  padding-left: 0.95em;
  font-size: 0.95em;
  opacity: 0.95;
}

/* =========================
   Slide class: cards
   ========================= */

section.cards ul {
  list-style: none;
  padding-left: 0;
  margin-top: 0.5em;
}

section.cards li {
  background: #f0f4f7;
  border-radius: 10px;
  padding: 12px 16px;
  margin: 10px 0;
  line-height: 1.22;
}

section.cards li::marker { content: ""; }

/* =========================
   Blockquotes + callouts
   ========================= */

blockquote {
  background: #1a5276;
  color: white;
  padding: 16px 22px;
  border-radius: 10px;
  border-left: none;
  font-size: 1.05em;
  margin: 0.6em 0;
}
blockquote strong { color: white; }

/* Bottom line callout */
.bottomline {
  background: #e8f1f5;
  border-left: 4px solid #1a5276;
  padding: 12px 16px;
  border-radius: 0 8px 8px 0;
  margin-top: 14px;
}

/* =========================
   Code blocks
   ========================= */

pre, code {
  font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
  font-size: 0.85em;
}
pre {
  padding: 10px 14px;
  border-radius: 8px;
  background: #f6f8fa;
  line-height: 1.2;
}
---

<!-- _class: title -->

# Patient-Chosen Health Hubs

**A Patient-Controlled Interoperability Layer**

### Implementation Notes 

The core mechanism is intentionally small.  
These slides describe the protocol in implementer-ready form.

January 2026

----

<a id="appendix-map"></a>

# System Map (How the Pieces Fit)

1) **Match (EMTP)**  
Participants publish EMTP tables (SURLs) → notify Registry root (NURL)

2) **Crosswalk (Registry STP)**  
Registry matches token overlap → serves participant match streams (SURLs)

3) **Approve (Payer STP)**  
Participants follow payer beneficiary NURLs → receive scoped approval SURLs

4) **Connect + Exchange (Manifests + Data Plane)**  
Approved parties exchange manifests (SURL↔NURL) → FHIR + Direct (+ optional claims)

---
<a id="protocol-assumptions"></a>

# Protocol Assumptions

- All system-to-system communication uses **HTTPS + mTLS**.
- Participants are authorized by **certificate Policy OIDs** (role-based certs).
- **[EMTP](https://github.com/alex137/ephemeral-match-token-protocol/)** provides privacy-preserving identity matching (token overlap; rotating keys).
- **[STP](https://github.com/alex137/state-transfer-protocol)** is the control-plane primitive (streaming state tables + notifications).
- **FHIR + Direct** are the data-plane primitives (records + messaging).
- Missing payer endpoints or outages are **not revocations**; last known status remains valid until explicitly updated.



---

<a id="registry-trust-establishment"></a>

# Registry Certificates

- **Trust anchor bundle:** Registry root URL serves a PEM bundle of trusted CA roots for authenticating system participants.

- **Role-based certificates:** Participant certs include a **Policy OID** identifying role:
  `payer | hub | provider | emergency_provider | tdm_publisher | direct_distributor | sponsor`

- **Provider identity binding:** Provider certs encode **NPI** in `SubjectAltName.otherName` using the designated NPI OID.

---

<a id="trust-enforcement-revocation"></a>

# Trust Enforcement + Revocation

- **Role enforcement:** Systems authorize requests based on certificate role (Policy OID) and reject invalid role usage.

- **Revocation feed:** Registry publishes revoked certificate serial numbers via STP at: `[rootURL]/crl`

- **OID registry:** The registry publishes the authoritative list of role Policy OIDs (and the NPI OID) in the open-source spec repository.

----

<a id="emtp"></a>

# EMTP (Ephemeral Match Tokens)

Participants post privacy-preserving match tokens derived from identifier tuples (name, DOB, phone, address, optional ID digits). Tokens rotate over time and are computed locally using registry-distributed keys.

Keys are distributed only to credentialed participants and rotate on a fixed schedule (e.g., monthly).

**No de facto NPI:** The registry matches tokens and returns endpoint crosswalks, but never receives demographics or stores persistent identifiers.

Link: **[EMTP spec + reference code](https://github.com/alex137/ephemeral-match-token-protocol/)**

---

<a id="stp"></a>

# STP (State Transfer Protocol)

The registry uses **STP** to serve and synchronize tables as **append-only change logs over HTTP**, with:

- **Monotonic sequence numbers** for auditability + replay  
- **Delta sync** (`since_id`) and **gap recovery**  
- **Idempotent processing** (clients tolerate duplicates)

Participants MAY expose **Notify URLs** (**NURLs**) that peers POST to when a new **State URL** (**SURL**) is available or when an existing SURL has updates.

Link: **[STP spec + reference implementations](https://github.com/alex137/state-transfer-protocol)**.

---
<a id="surl-nurl-terms"></a>

# STP Terms (SURLs + NURLs)

To keep the protocol compact, we use two STP URL roles:

- **SURL (State URL):** a URL you **GET** to read a streaming STP table  
- **NURL (Notify URL):** a URL you **POST** to send an STP notification

**Notify format:**  `surl=<SURL>&<event>=<NURL>`

A notification can include:
- the **SURL** to follow, and/or
- one or more callback **NURLs** (for `match`, `manifest`, `grant`, etc.)

*In this appendix, “SURL” always means “STP table URL,” and “NURL” means “STP Notify endpoint.”*

---

<a id="endpoint-token-tables"></a>


# Bootstrap (EMTP Tables)

Participants (providers, payers, sponsors, hubs) publish EMTP match-token tables as STP **State URLs (SURLs)**.

The registry root is an STP **Notify URL (NURL)**. Participants notify:
`surl=<EMTP_Table_SURL>&match=<Match_NURL>`

`match` is the NURL the registry uses to notify the participant of its corresponding streaming **Registry Match SURL**.

**SURL schema:** `emtp_table`  
`[SeqNo] \t [TS] \t [+/-] \t [Subject_NURL] \t [EMTP_Tokens...]`

- `Subject_NURL`: stable per-person identifier (and PrimaryKey) at that participant.
- `EMTP_Tokens`: whitespace-separated tokens for identifier tuples.

---

<a id="registry-match-tables"></a>

# Registry Match SURLs

**Crosswalk URLs from matching EMTP tokens**

The registry serves participant-specific **match streams** as SURLs.

**SURL schema:** `registry_match_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Subject_NURL] \t [Matched_NURLs...]`

- `Matched_NURLs`: whitespace-separated NURLs matched via EMTP token overlap.
- **Payers:** hub users, sponsor member/employees, and patients
- **Hubs & Providers** payer beneficiaries 
- **Sponsors**: beneficiaries and providers. 

Match streams are authoritative for which foreign URLs are in-scope.

---
<a id="payer-authorization"></a>

# Payer Approval Stream Serving

Payers expose **Beneficiary NURLs** as stable entry points for approval state.

Providers/Hubs/Sponsors notify the Beneficiary NURL with a callback `notify=<NURL>`.  
The payer replies by notifying that callback with a requester-scoped **SURL**.

Returned SURLs deliver: approved hubs (providers), approval status (hubs), claims (sponsors).  
SURLs are scoped to requester mTLS identity and may be migrated via re-notify.


---

<a id="beneficiary-endpoint-hub-view"></a>

# Hub Approval Stream (Hub SURL)

Payers serve these streams to authorized hubs to report user approval status.

**SURL schema:** `hub_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_NURL] \t [Status] \t [Action_URL]`

- `Status ∈ {Pending | Approved | Denied}`

- `Pending`: approval UI URL
- `Approved`: relationship manifest SURL
- `Denied`: denial/revocation reason URL

If `Manifest_SURL` changes, the hub re-fetches the manifest and updates subscriptions.  
Delete records + terminate subscriptions only when **Denied across all active payers**.

---

<a id="beneficiary-endpoint-provider-view"></a>

# Provider SURLs

Provider SURLs deliver patient-approved hub sets.

**STP schema:** `provider_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Patient_NURL] \t [Hub_User_NURLs...]`

- `Hub_User_NURLs...` = whitespace-separated approved hub user NURLs
- Approval is revoked when a new row omits a hub from the list.

- Begin/maintain exchange when a hub appears in the list.
- Terminate only when the hub is absent from **all active payer** lists.

---

<a id="finance-policy"></a>

# Finance SURLs (Who Serves What)

`finance_surl` is an optional manifest endpoint that exposes an STP **finance mirror**
(`finance_event_stream`), scoped by requester mTLS identity.

**Recommended exposure**
- **Payers SHOULD** expose `finance_surl` to **hubs + sponsors**
- **Providers SHOULD** expose `finance_surl` to **hubs + payers** *(auto-generated from billing / outbound X12 logs)*
- **Sponsors MAY** expose `finance_surl` to **payers** *(funding + expectations)*

Finance mirrors do **not** replace X12 — they make billing + adjudication **auditable, replayable, and disputable**.

---

<a id="finance-stream"></a>

# Finance Event Stream (Schema)

Finance mirrors represent transaction state as an append-only STP log.

**SURL schema:** `finance_event_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Txn_ID] \t [Event_Type] \t [Action_URL] \t [KV]`

- `Txn_ID`: stable identifier *(claim / bill / payment / funding item)*
- `Action_URL` (optional): scoped details / documentation link
- `KV`: whitespace-separated `key=value` metadata *(amounts, codes, dates, IDs)*

---

<a id="finance-event-types"></a>

# Finance Event Types (Unified)

Finance mirrors use a shared event vocabulary across payers, providers, and sponsors.

**Event_Type ∈ {**`submitted | accepted | denied | adjusted | appealed | paid | refunded`**}**

**Canonical `KV` keys:**  
`billed_amount`, `allowed_amount`, `paid_amount`, `patient_responsibility`, `copay_due`,  `denial_code`, `service_date`, `provider_id`

Unknown keys MUST be ignored.
Sponsors encode premium/funding semantics via txn_kind= and related KV keys.

---
<a id="manifest-init-registry"></a>

# Manifest Initiation (From Registry Match)

When a participant learns a new **foreign NURL** from its **Registry Match SURL**, it SHOULD initiate a manifest exchange.

It sends an STP Notify to the foreign NURL:

`surl=<Sender_Manifest_SURL>&manifest_nurl=<Sender_Manifest_NURL>`

- `surl`: sender’s relationship manifest SURL  
- `manifest_nurl`: where the receiver notifies back with its manifest SURL

Receivers treat the **most recently notified `surl`** as the sender’s current manifest.

----
<a id="manifest-init-payer"></a>

# Manifest Initiation (From Payer Approvals)

Payers return **Hub_User_NURLs** to providers and sponsors to indicate an approved hub relationship.

When a party receives a new approved **Hub_User_NURL**, it SHOULD notify:

`surl=<Sender_Manifest_SURL>&manifest_nurl=<Sender_Manifest_NURL>`

The hub fetches the sender’s manifest (SURL) and replies (via `manifest_nurl`)
with hub-user–specific Direct/FHIR/Finance endpoints.

---

<a id="endpoint-manifest"></a>

# Relationship Manifest (SURL)

**SURL schema:** `endpoint_manifest`  
`[SeqNo] \t [TS] \t [+/-] \t [endpoint_type] \t [URL]`

**endpoint_type values:**  
`fhir_subscribe | fhir_read | direct_message | finance_surl`

- `finance_surl`: `finance_event_stream` *(payer/provider/sponsor-issued)*
- Unknown `endpoint_type` values MUST NOT break clients.

----
<a id="manifest-example"></a>

# Manifest Exchange (Example)

**Provider learns approved `Hub_User_NURL` → initiates exchange**

1) Provider → Hub_User_NURL  
`surl=Provider_Manifest_SURL&manifest_nurl=Provider_Manifest_NURL`

2) Hub GETs Provider_Manifest_SURL → learns:  
`fhir_subscribe, direct_message, finance_surl`

3) Hub → Provider_Manifest_NURL  
`surl=Hub_Manifest_SURL&manifest_nurl=Hub_Manifest_NURL`

Later: either party re-notifies → **last notified `surl` wins**.

----

<a id="direct-message-recommended-metadata"></a>

# Direct Message Metadata (Recommended)

To enable cross-system collaboration, Direct messages SHOULD include:

- `thread_id`: stable identifier for a conversation thread
- `patient_ref`: reference to patient identity context shared by both systems
- `record_pointer` (optional): pointer to relevant record context  
  *(FHIR Resource reference + Provenance or equivalent)*

Providers MAY route or triage messages differently based on `sender_role` + `message_category`.

----

<a id="consent-request-grant"></a>

# Consent Request + Grant

**Used for prior-auth, audit, and research**

**Requests:** `message_category: consent_request` MUST include:  `requestor_id`, `purpose`, `scope`, `expires_at`, `consent_request_notify_url`

**Grants:** Upon approval, hub exposes an **STP grant table** and sends an **STP Notify** to `consent_request_notify_url`.

**Grant Schema:**
`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_Endpoint_URL] \t [EMTP_Match_Tokens..]`

Hubs MUST support immediate revocation + audit logging.

---
<a id="tdm-headers"></a>

# TM Required Headers

- `schema_version`: targeting semantics version (e.g., v1)
- `filter`: deterministic predicate over coded fields *(RxNorm, ICD10/SNOMED, CPT, LOINC, demographics, timeframe)*
- `message_type`: `recall | safety_signal | advisory | protocol_change | research_request | payer_policy_change`
- `deliver_to`: `patient | product_provider | treating_providers` *(product_provider = prescriber / ordering / implanting clinician)*
- `valid_until`: expiration timestamp
- `context` (optional): free-text rationale / instructions

**Matching:** filter MUST be applied deterministically; AI MAY refine only after a filter hit. Unknown keys MUST be ignored.
