---
marp: true
theme: default
paginate: true
style: |
  /* ---------- Base slide typography / layout ---------- */
  section {
    font-family: Arial, sans-serif;
    padding: 40px;
    line-height: 1.35;
    max-width: 1100px;        /* helps reduce ugly wraps on wide bullet slides */
    margin: 0 auto;
  }

  h1 {
    color: #1a5276;
    font-family: Georgia, serif;
    font-size: 1.65em;
    margin-bottom: 0.6em;
  }

  h2 {
    color: #1a5276;
    font-family: Georgia, serif;
    margin-bottom: 0.5em;
  }

  h3 {
    color: #1a5276;
    margin-bottom: 0.4em;
  }

  strong {
    color: #1a5276;
  }

  /* ---------- Links ---------- */
  a {
    color: #1a5276;
    text-decoration: none;
  }
  a:hover {
    text-decoration: underline;
  }

  /* ---------- Title slide ---------- */
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

  /* ---------- Blockquotes ---------- */
  blockquote {
    background: #1a5276;
    color: white;
    padding: 20px 30px;
    border-radius: 8px;
    border-left: none;
    font-size: 1.1em;
    margin: 18px 0;
  }
  blockquote strong {
    color: white;
  }

  /* ---------- Soft containers (used via .card class) ---------- */
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

  /* ---------- GLOBAL LIST CLEANUP (fixes bullet noise + indent) ---------- */
  section ul,
  section ol {
    margin-top: 14px;
    margin-bottom: 0;
    padding-left: 1.05em;   /* much less indent than default */
  }

  section li {
    margin: 10px 0;         /* gives breathing room */
    line-height: 1.35;
  }

  section li::marker {
    color: #1a5276;         /* makes marker feel intentional but not loud */
    font-size: 0.9em;
  }

  /* Reduce hanging-indent ugliness on wrapped lines */
  section li {
    padding-left: 0.15em;
  }

  /* Better spacing between paragraphs and lists */
  section p {
    margin: 0.6em 0;
  }

  /* ---------- OPTIONAL: "cards list" mode for dense bullet slides ---------- */
  /* Use by adding: <!-- _class: cards --> */
  section.cards ul,
  section.cards ol {
    list-style: none;
    padding-left: 0;
    margin-left: 0;
  }

  section.cards li {
    background: #f0f4f7;
    border-radius: 8px;
    padding: 10px 14px;
    margin: 12px 0;
    line-height: 1.35;
  }

  /* Add subtle emphasis for bold lead-ins inside card bullets */
  section.cards li strong {
    color: #1a5276;
  }

  /* ---------- OPTIONAL: tighter "dense" mode if you ever need it ---------- */
  /* Use by adding: <!-- _class: dense --> */
  section.dense {
    padding: 32px;
  }

  section.dense li {
    margin: 7px 0;
    line-height: 1.25;
  }
---

<!-- _class: title -->

# Patient-Chosen Health Hubs

**A Patient-Controlled Interoperability Layer**

January 2026

---

# Consumer Health Hubs in the Market

These hubs are already creating patient value — and they could unlock even bigger payer value if they were reliable at scale.

Millions use Apple Health, Guava, Picnic, OneRecord, and others to:

- **Aggregate + organize** medical records across providers  
- **Help patients interpret** results and manage conditions (AI-assisted)  
- **Enable access** to async care, virtual visits, and home diagnostics  
- **Keep clinicians informed** (especially in transitions & emergencies)  
- **Support proxies** for seniors and complex chronic care  

---

<!-- _class: cards -->
# The Promise of Hubs At Scale for Payers

**Better outcomes, lower medical + admin cost.**

- **Lower total cost of care:** better self-management + navigation → fewer avoidable ED visits + better chronic control
- **Administrative deflection:** shift portal + call-center volume to record-aware self-service workflows
- **Network + benefit steerage:** guide members in-network with real-time estimates + prior-auth rules
- **Faster prior auth + claims audits:** records assembled automatically → fewer provider callbacks and faster AI-assisted review
- **High-risk member support:** proxy/caregiver workflows improve outcomes for seniors and complex chronic populations

---

<!-- _class: cards -->
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
-https://github.com/alex137/health-hub-registry

**Bottom line:** This is a buildable system, not a research project.

----

<!-- _class: cards -->
# Registry Participant Requirements

- Hubs/payers/providers post hashed identifiers for patient matching
- Beneficiaries approve/revoke matched hub PHI access via their payer
- Payers share plan + network + cost sharing data with approved hubs
- Providers obtain their patients' approved hubs from their payers
- Providers & approved hubs exchange FHIR records + Direct messages
- Hubs post provider record-delivery performance reports

---

<!-- _class: cards -->
# Enforcement and Adoption

- Registry never handles PHI

- Treat payer-confirmed approval as HIPAA safe harbor for PHI exchange

- Use hub reports to automate information-blocking enforcement at scale

- Make hubs a covered digital benefit; tie to quality metrics for hub-enabled workflows (care transitions, prior-auth)

**Bottom line:** Payment incentives + scalable enforcement can create the first universal, patient-controlled interoperability layer.

---

<!-- _class: cards -->
# Hubs as the Primary Patient Channel

HHS should also grant safe harbor for hub-mediated delivery (SMS, WhatsApp, email) under defined safeguards.
Authorized, record-aware hubs become the default coordination channel — replacing portals.

* **Unified threads:** persistent hub-mediated conversations across providers (thread_id)
* **Care coordination:** scheduling, referrals, transitions, discharge follow-up
* **Medication + pharmacy workflows:** refills, substitutions, adherence outreach
* **Coverage workflows:** prior-auth status, benefits questions, appeals

Result: one record-aware channel for patients and providers.

---
# Patient Channel + Financial Channel

Once hubs are authorized and reliably record-aware, they become the natural place patients manage the **financial side of care** — with the same context as the clinical record.

- **Unified out-of-pocket tracking** across providers + pharmacies  
- **Record-linked bills + explanations** (“what was this charge for?”)  
-	**Payer claims + adjudication updates** — denials, adjustments, patient responsibility — in the same thread
- **Appeals + disputes** with the right clinical context attached  
- **Payment plans + financing** (HSA, employer benefits, charity care routing)

**Result:** patients manage costs in real time, with full record context.

---
# What Universal Hubs Enable

Once hubs work reliably across providers,
the system gains new capabilities — beyond record access.

Emergency continuity, faster prior auth, safety alerts, real-world evidence,
and pharmacy integration all become automatic.


---

<!-- _class: dense -->
# Hubs: Proxy + Emergency Access

**Proxy usage:** Hubs may let users designate proxies to approve record exchange and manage care on their behalf — useful for seniors and complex chronic care (ongoing or emergency-only, optionally with delay).

**Provider authorization policy:** Hubs may require user confirmation or auto-approve provider requests based on patient preferences + hub policy (e.g., provider reputation, prior relationship, context). Requests using an **emergency provider TLS certificate** may follow a different policy.

**Audit + notice:** Hubs should log proxy/emergency flows and notify users via multiple channels.

*Immediate access to allergies, meds, directives, and proxy designations is a strong adoption driver.*

---

<!-- _class: dense -->
# Benefit: Speeding Prior Authorization

Prior auth delays are mostly **documentation delays** that hubs can solve.

Payer investigators request access via a **Consent Request Direct Message** *(Appendix)*. Upon user approval, hubs issue a **Consent Grant** enabling **time-limited, scoped access** to the aggregate record *solely* for prior-auth and claims-audit review.

- **Patients:** faster approvals, less stress
- **Providers:** less doc churn, lower audit burden, less non-payment risk
- **Payers:** lower admin cost, faster and more consistent decisions

**Bottom line:** Prior-auth relief creates a near-term reason for payers and providers to adopt hub workflows.

---

# Benefit: Auditable Claims + Sponsor Oversight

Prior auth is slow because documentation is slow.
So are audits and sponsor–carrier disputes.

With hubs at scale, payers can expose auditable claim state streams:
	•	Near-real-time claim lifecycle visibility (submitted → denied → adjusted → paid)
	•	Faster audits + dispute resolution (append-only, replayable history)
	•	Earlier fraud/waste detection (duplication, upcoding, contract violations)
	•	Better sponsor oversight of TPAs, PBMs, and delegated risk groups
	•	Clear reconciliation between what providers billed, what was allowed, and what was paid

Result: accountable spend, lower admin cost, fewer drawn-out disputes.

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

<!-- _class: dense -->
# Benefit: Targeted Direct Messages

Today, recalls, safety signals, protocol changes, and research requests are posted to websites — and affected patients/providers often never see them.

**Targeted Direct Messages (TDMs)** solve this. They are a Direct Messaging extension where a message is addressed not to a specific recipient, but instead to a deterministic targeting rule (e.g. a boolean predicate of RxNorm, ICD10, timeframe, etc.).

Publishers (FDA/CDC / ONC-approved entity) pull the hub list from the registry and send the TDM to each hub. Hubs match locally (possibly using AI to refine) and deliver to the right providers.

**Result:** safety-critical messages reach the right providers (via provenance endpoints) — and attach to the right records — automatically.

---
<!-- _class: dense -->
# Benefit: Real-Time Real-World Evidence

Research hubs enable near-real-time adverse event capture, real-world controls, and rapid trial recruitment — without years of data-sharing negotiation.

1. Recruit via `research_request` **Targeted Direct Messages** containing a **Consent Request**.

2. Upon approval, the user's hub posts a **Consent Grant** (user contact endpoint + identity hashes) to the Consent Request URL.

3. Research hub registers like any other hub; after payer approval, providers deliver records via standard FHIR subscriptions.

---
<!-- _class: dense -->
# Completing Data:  Pharmacy Participation

*Medications are the most frequent and error-prone part of care — but today's interoperability layer misses the dispense reality.* Today, neither providers nor hubs can reliably know whether a prescribed medication was **filled, substituted, refilled, or abandoned**.

HHS should require pharmacies to operate as **registry-certified provider-like endpoints**, so hubs can FHIR subscribe and receive:

- **Fill + refill status** (including non-pickup / abandonment)
- **Substitutions + med changes** (dispensed NDC mapped to RxNorm)
- **Adherence signals** (late refills, gaps, early discontinuation)

**Result:** safer prescribing, fewer errors, better chronic disease management; the med list reflects what happened, not just what was ordered.

---

<!-- _class: cards -->
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

**Latest deck + source:**  
- PDF (latest): **[download](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-deck.pdf)**  
- Source (Marp): **[health-hub-registry-deck.marp.md](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-deck.marp.md)**

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

# Appendix: Implementation Notes (Optional)

The core mechanism is intentionally small.  
These slides describe the protocol in implementer-ready form.

*(Everything below is optional reading.)*

----

<a id="appendix-map"></a>

# Appendix: System Map (How the Pieces Fit)

1) **Match (EMTP)**  
Participants publish EMTP tables (SURLs) → notify Registry root (NURL)

2) **Crosswalk (Registry STP)**  
Registry matches token overlap → serves participant match streams (SURLs)

3) **Approve (Payer STP)**  
Participants follow payer beneficiary NURLs → receive scoped approval streams (SURLs)

4) **Connect + Exchange (Manifests + Data Plane)**  
Approved parties exchange manifests (SURL↔NURL) → FHIR + Direct (+ optional claims)

---
<a id="protocol-assumptions"></a>

# Appendix: Protocol Assumptions

- All system-to-system communication uses **HTTPS + mTLS**.
- Participants are authorized by **certificate Policy OIDs** (role-based certs).
- **[EMTP](https://github.com/alex137/ephemeral-match-token-protocol/)** provides privacy-preserving identity matching (token overlap; rotating keys).
- **[STP](https://github.com/alex137/state-transfer-protocol)** is the control-plane primitive (streaming state tables + notifications).
- **FHIR + Direct** are the data-plane primitives (records + messaging).
- Missing payer endpoints or outages are **not revocations**; last known status remains valid until explicitly updated.



---

<a id="registry-trust-establishment"></a>

# Appendix: Registry Certificates

- **Trust anchor bundle:** Registry root URL serves a PEM bundle of trusted CA roots for authenticating system participants.

- **Role-based certificates:** Participant certs include a **Policy OID** identifying role:
  `payer | hub | provider | emergency_provider | tdm_publisher | direct_distributor | sponsor`

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

Link: **[EMTP spec + reference code](https://github.com/alex137/ephemeral-match-token-protocol/)

---

<a id="stp"></a>

# Appendix: STP (State Transfer Protocol)

The registry uses **STP** to serve and synchronize tables as **append-only change logs over HTTP**, with:

- **Monotonic sequence numbers** for auditability + replay  
- **Delta sync** (`since_id`) and **gap recovery**  
- **Idempotent processing** (clients tolerate duplicates)

Participants MAY expose **Notify URLs** (**NURLs**) that peers POST to when a new **State URL** (**SURL**) is available or when an existing SURL has updates.

Link: **[STP spec + reference implementations](https://github.com/alex137/state-transfer-protocol)**.

---

<a id="endpoint-token-tables"></a>


# Appendix: Bootstrap (EMTP Tables)

Participants (providers, payers, sponsors, hubs) publish EMTP match-token tables as STP **State URLs (SURLs)**.

The registry root is an STP **Notify URL (NURL)**. Participants notify:
`surl=<EMTP_Table_SURL>&match=<Match_NURL>`

`match` is the NURL the registry uses to notify the participant of its corresponding streaming **Registry Match SURL**.

**SURL schema:** `emtp_table`  
`[SeqNo] \t [TS] \t [+/-] \t [Subject_NURL] \t [EMTP_Tokens...]`

- `Subject_NURL`: stable per-person identifier (an NURL) at that participant.
- `EMTP_Tokens`: whitespace-separated tokens for identifier tuples.

---

<a id="registry-match-tables"></a>

# Appendix: Registry Match SURLs

**Crosswalk URLs from matching EMTP tokens**

The registry serves participant-specific **match streams** as SURLs.

**SURL schema:** `registry_match_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Subject_NURL] \t [Matched_NURLs...]`

- `Matched_NURLs`: whitespace-separated NURLs matched via EMTP token overlap.
- **Payers:** hub-user NURLs  
- **Others:** payer-beneficiary NURLs

Match streams are authoritative for which foreign URLs are in-scope.

---
<a id="payer-authorization"></a>

# Appendix: Payer Approval Stream Serving

Payers expose **Beneficiary NURLs** as stable entry points for approval state.

Providers/Hubs/Sponsors notify the Beneficiary NURL with a callback `notify=<NURL>`.  
The payer replies by notifying that callback with a requester-scoped **SURL**.

Returned SURLs deliver: approved hubs (providers), approval status (hubs), claims (sponsors).  
SURLs are scoped to requester mTLS identity and may be migrated via re-notify.


---

<a id="beneficiary-endpoint-hub-view"></a>

# Appendix: Hub Approval Stream (Hub SURL)

Payers serve these streams to authorized hubs to report user approval status.

**SURL schema:** `hub_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_NURL] \t [Status] \t [Action_URL]`

- `Status ∈ {Pending | Approved | Denied}`

- `Pending`: approval UI URL
- `Approved`: relationship manifest SURL
- `Denied`: denial/revocation reason URL

If `Manifest_SURL` changes, the hub re-fetches the manifest and updates subscriptions.  
Delete records + terminate provider subscriptions only when **Denied across all active payers**.

---

<a id="beneficiary-endpoint-provider-view"></a>

# Appendix: Provider SURLs

Provider SURLs deliver patient-approved hub sets.

**STP schema:** `provider_approval_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Patient_NURL] \t [Hub_User_NURLs...]`

- `Hub_User_NURLs...` = whitespace-separated approved hub user NURLs
- Approval is revoked when a new row omits a hub from the list.

- Begin/maintain exchange when a hub appears in the list.
- Terminate only when the hub is absent from **all active payer** lists.

---
<a id="sponsor-stp"></a>

# Appendix: Claims SURLs (Claims STP)

Payers expose **Claims SURLs** to hubs and sponsors as an **auditable mirror stream**
of claim + adjudication state (scoped to requester mTLS identity).

**STP schema:** `claim_event_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Claim_ID] \t [Event_Type] \t [URL] \t [Metadata...]`
- `Event_Type ∈ {submitted | adjudicated | denied | appealed | paid | adjusted | refunded}`
- `URL` links to payer-hosted claim detail / supporting documentation *(scoped)*
- `Metadata` MAY include: allowed_amount, patient_responsibility, copay_due, denial_code, provider_id

**Notes**
- Sponsors can replay claim history and audit changes over time.
- X12 remains the transaction layer; this is the payer-served **state mirror**.

---

<a id="endpoint-manifest"></a>

# Appendix: Manifest Exchange

When a party receives a new approved **Hub_User_NURL** (from a payer), or wants to update relationship endpoints, it sends an STP Notify:

`surl=<Manifest_SURL>&manifest_nurl=<Manifest_NURL>`

-	surl: sender’s manifest SURL (relationship endpoints)
- manifest_nurl: NURL where hub posts its manifest SURL

Last notified surl replaces prior  sender manifest.

**Manifest SURL schema:** `endpoint_manifest`  
`[SeqNo] \t [TS] \t [+/-] \t [endpoint_type] \t [URL]`

**endpoint_type values:**  
`fhir_subscribe` | `fhir_read` | `direct_message` | `claims_surl`

Unknown `endpoint_type` values MUST NOT break clients.

----

Appendix: Manifest Exchange — Example

Provider learns approved Hub_User_NURL
	1.	Provider notifies hub of provider manifest:
surl=Provider_Manifest_SURL&manifest_nurl=Provider_Manifest_NURL
	2.	Hub GETs provider manifest SURL and learns endpoints:
fhir_read, fhir_subscribe, direct_message, claims_surl
	3.	Hub replies via provider manifest_nurl:
surl=Hub_Manifest_SURL&manifest_nurl=Hub_Manifest_NURL

Later: if either manifest moves, sender re-notifies → last notified surl wins.

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
