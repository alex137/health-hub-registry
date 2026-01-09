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

# Hubs as the Primary Patient Channel

HHS should also grant safe harbor for hub-mediated delivery (SMS, WhatsApp, email) under defined safeguards.
Authorized, record-aware hubs become the default coordination channel — replacing portals.

* **Unified threads:** persistent hub-mediated conversations across providers (thread_id)
* **Care coordination:** scheduling, referrals, transitions, discharge follow-up
* **Medication + pharmacy workflows:** refills, substitutions, adherence outreach
* **Coverage workflows:** prior-auth status, benefits questions, appeals

Result: one record-aware channel for patients and providers.

---

# What Universal Hubs Enable

Once hubs work reliably across providers,
the system gains new capabilities — beyond record access.

Emergency continuity, faster prior auth, safety alerts, real-world evidence,
and pharmacy integration all become automatic.


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

# Provider Messaging Becomes Record-Linked Collaboration

When hubs make cross-provider records universal, messaging stops being “fax in disguise.”

**Messages can point to the exact record context:**
- “Here’s the abnormal lab” *(opens that lab + trend + meds)*
- “Why was anticoagulation stopped?” *(opens discharge note + orders)*
- “Please confirm allergy status” *(opens allergy history + recent reactions)*

Providers communicate with **shared context**, not summaries.

**Result:** fewer mistakes, less back-and-forth, faster decisions.

---

# Patient-Scoped Care Channels 
###Across Health Systems

If providers attach messages to the shared record, every patient gains a persistent care channel:

- A single thread shared across the care team (even across health systems)
- Visible to nurses, MAs, care managers, and specialists involved in care
- Messages persist with the record — not trapped in one portal

This creates **common knowledge**: everyone sees the same aggregate record *and* the same conversation history.

**Result:** care coordination becomes continuous, not episodic.

---

# AI-Ready Triage + Coordination

Once messaging is record-linked and shared across the care team:

- AI agents can surface relevant record context directly in the thread
- Route messages to the right team member automatically
- Draft replies with one-click send
- Monitor labs, refills, and transitions and alert when something changes

This enables **automation without fragmentation** — 
because every action is grounded in shared record context.

**Result:** better outcomes, lower clinician burden, fewer coordination failures.

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

# Completing Data:  Pharmacy Participation

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

# Contact / Next Steps

S. Alexander Jacobson \<alex@137ventures.com\>

This is a draft in active iteration — I’d love:  
- questions on what this is really solving / how it should work  
- suggestions to improve the design (technical or policy)  
- opportunities to walk through it and discuss adoption paths  

---
# Appendix

1. [Common Questions](#common-questions)
2. [Technical Appendix](#technical-appendix)
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

<a id="technical-appendix"></a>

# Appendix: Technical Appendix

Detailed protocol and implementation slides.

(Everything below is optional reading for implementers.)

---
<a id="protocol-assumptions"></a>

# Appendix: Protocol Assumptions

- All system-to-system communication uses **HTTPS + mTLS**.
- Participants are authorized by **certificate Policy OIDs**.
- Control plane: **STP** (routing, approvals, endpoint manifests).
- Data plane: **FHIR** (records/benefits/subscriptions) + **Direct**.
- Providers promptly STP notify newly discovered approved hub user urls.
- Missing payer endpoints or outages are not revocations; prior status remains authoritative until explicit update.

---

<a id="registry-trust-establishment"></a>

# Appendix: Registry Certificates

- **Trust anchor bundle:** Registry root URL serves a PEM bundle of trusted CA roots for authenticating system participants.

- **Role-based certificates:** Participant certs include a **Policy OID** identifying role:
  `payer | hub | provider | emergency_provider | tdm_publisher | direct_distributor`

- **Provider identity binding:** Provider certs encode **NPI** in `SubjectAltName.otherName` using the designated NPI OID.

---

<a id="trust-enforcement-revocation"></a>

# Appendix: Trust Enforcement + Revocation

- **Role enforcement:** Systems authorize requests based on certificate role (Policy OID) and reject invalid role usage.

- **Revocation feed:** Registry publishes revoked certificate serial numbers via STP at: `[rootURL]/crl`

- **OID registry:** The registry publishes the authoritative list of role Policy OIDs (and the NPI OID) in the open-source spec repository.

----

<a id="emtp"></a>

# Appendix: EMTP (Ephemeral Match Tokens)

Participants post privacy-preserving match tokens derived from identifier tuples (name, DOB, phone, address, optional ID digits). Tokens rotate over time and are computed locally using registry-distributed keys.

Keys are distributed only to credentialed participants and rotate on a fixed schedule (e.g., monthly).

**No de facto NPI:** The registry matches tokens and returns endpoint crosswalks, but never receives demographics or stores persistent identifiers.

**Full spec + reference code:** see EMTP repo.

---
<a id="stp"></a>

# Appendix: STP (State Transfer Protocol)

The registry uses **STP** to serve and synchronize tables as **append-only change logs over HTTP**, with:

- **Monotonic sequence numbers** for auditability + replay  
- **Delta sync** (`since_id`) and **gap recovery**  
- **Idempotent processing** (clients tolerate duplicates)

Participants MAY also expose **STP Notify URLs** to announce new tables or signal table updates.

**Full spec + reference implementations:** see STP repo.

*In this deck, “STP URL” means a URL that serves STP rows via HTTP GET.*


---

<a id="endpoint-token-tables"></a>

# Appendix: Bootstrap (EMTP Tables)

Participants are providers, payers, and hubs.  
Participants STP notify the registry root of STPs containing EMTP match tokens.
These STPs must also take STP notification of Registry Match STPs.

**STP schema:** `emtp_table`  
`[SeqNo] \t [TS] \t [+/-] \t [URL] \t [EMTP_Tokens...]`

- `URL` uniquely identifies an individual at that participant.
- `EMTP_Tokens`: whitespace-separated tokens for identifier tuples.




---
<a id="registry-match-tables"></a>

# Appendix: Registry Match STPs

**Crosswalk URLs from matching EMTP tokens**

**STP schema:** `registry_match_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Subject_URL] \t [Matched_URLs...]`

- `Matched_URLs`: whitespace-separated; matched via EMTP token overlap.

**Streams:**
- **Payer:** `Beneficiary_URL → Hub_User_URLs...`
- **Provider:** `Patient_URL → Payer_Beneficiary_URLs...`
- **Hub:** `User_URL → Payer_Beneficiary_URLs...`

Match streams are authoritative for which foreign URLs are in-scope.

---
<a id="payer-authorization"></a>

# Appendix: Payer Approval Stream Serving

Payers expose **beneficiary URLs** that act as stable entry points for approval state.

- Providers beneficiary URLs redirect to **Provider_STP** streams.
- Hubs beneficiary URLs redirect to  **Hub_STP** streams.

**Authorization:** Streams MUST scope results to client mTLS identity:
- Providers see only hubs approved for their patients.
- Hubs see only approval status for their users.

Payers should keep Beneficiary_URL redirect stable; migrate streams by issuing new ones for their beneficiaries. 

---

<a id="beneficiary-endpoint-hub-view"></a>

# Appendix: Hub STPs

Hubs deliver updates on hub user approval statuses.

**STP schema:** `hub_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_URL] \t [Status] \t [URL]`

- `Status ∈ {Pending | Approved | Denied}`
- `Pending → Payer_Approval_URL`
- `Approved → FHIR_Plan_URL`
- `Denied → Reason_URL`

If `FHIR_Plan_URL` changes, hub re-subscribes.  
Delete records + terminate provider subscriptions only when **Denied across all active payers**.

---

<a id="beneficiary-endpoint-provider-view"></a>

# Appendix: Provider STPs

Provider_STPs deliver updates on patient-approved hubs.

**STP schema:** `provider_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Patient_URL] \t [Hub_User_URLs...]`

- `Hub_User_URLs...` is whitespace-separated approved hub URLs.
- Approval is revoked when a hub disappears from the list.

**Semantics**
- Begin/maintain exchange when a hub appears in the list.
- Terminate only when the hub drops from **all active payers** lists.

---

<a id="endpoint-manifest"></a>

# Appendix: Manifest Exchange

Providers and hubs exchange relationship endpoints via STP manifest tables:

**STP schema ** `endpoint_manifest`: `[SeqNo]\t[TS]\t+\t[endpoint_type]\t[URL]`

**Endpoint types:** `fhir_subscribe` | `fhir_read` | `direct_message` | `notify`

**Change propagation:** When a participant updates its manifest, it sends an STP Notify to the peer’s `notify` URL with `table=<sender_manifest_url>`. Peers re-GET the manifest (authoritative).

Manifests SHOULD include `notify` for change propagation w/o polling.
Unknown `endpoint_type` values MUST NOT break clients.

----

<a id="endpoint-manifest-example-1"></a>

# Appendix: Manifest — Example (1/3)

**Goal:** Provider discovers a new `Hub_User_URL` and shares its manifest.

### 1) Provider → Hub (announce + give manifest table)

`POST Hub_User_URL`
`Content-Type: application/x-www-form-urlencoded`

`table=Provider_Manifest_URL`

---

# Appendix: Manifest — Example (2/3)

### 2) Hub → Provider (fetch provider manifest)

`GET Provider_Manifest_URL?since_id=0`

Returns rows:  
`+ fhir_subscribe   https://prov.com/fhir/sub`  
`+ fhir_read        https://prov.com/fhir/read`  
`+ direct_message   https://prov.com/direct`  
`+ notify           https://prov.com/notify`

---

<a id="endpoint-manifest-example-2"></a>

# Appendix: Manifest — Example (3/3)

### 3) Provider → Hub (fetch hub manifest)

`GET Hub_User_URL?since_id=0`

Hub returns its manifest rows (same schema).

### If the hub manifest changes later:

Hub notifies the provider’s notify URL:  
`POST https://prov.com/notify`
`table=Hub_Manifest_URL`

Provider re-GETs `Hub_Manifest_URL` *(authoritative)*.

---

<a id="direct-message-required-metadata"></a>

# Appendix: Direct Message Metadata (Required)

Direct messages MUST include:

- `message_id`: stable identifier for the message object (may be a URL)
- `sender_role`: provider | hub | patient | proxy | payer | pharmacy | emergency_provider
- `message_category`: clinical | scheduling | administrative | billing | coverage | prior_auth | claims | appeal | refill | pharmacy | other

Unknown values MUST be displayed and MUST NOT cause rejection.

----

<a id="direct-message-recommended-metadata"></a>

# Appendix: Direct Message Metadata (Recommended)

To enable cross-system collaboration, Direct messages SHOULD include:

- `thread_id`: stable identifier for a conversation thread
- `patient_ref`: reference to patient identity context shared by both systems
- `record_pointer` (optional): pointer to relevant record context  
  *(FHIR Resource reference + Provenance or equivalent)*

Providers MAY route or triage messages differently based on `sender_role` + `message_category`.

----

<a id="consent-request-grant"></a>

# Appendix: Consent Request + Grant

**Used for prior-auth, audit, and research**

**Requests:** `message_category: consent_request` MUST include:  `requestor_id`, `purpose`, `scope`, `expires_at`, `consent_request_notify_url`

**Grants:** Upon approval, hub exposes an **STP grant table** and sends an **STP Notify** to `consent_request_notify_url`.

**Grant Schema:**
`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_Endpoint_URL] \t [EMTP_Match_Tokens..]`

Hubs MUST support immediate revocation + audit logging.

---


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
