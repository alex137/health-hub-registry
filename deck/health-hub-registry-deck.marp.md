---
marp: true
theme: default
paginate: true
style: |
/* =========================
   Global slide layout
   ========================= */
 
 /* =========================
    Marp default theme overrides
    ========================= */
 
 /* Force the slide content box tighter */
 section {
   padding-top: 20px !important;
   padding-bottom: 26px !important;
 }
 
 /* Remove extra top margin from the first element on every slide */
 section > :first-child {
   margin-top: 0 !important;
 }
 
 /* Tighten h1 spacing (Marp theme often overrides this) */
 section h1 {
   margin-top: 0 !important;
   margin-bottom: 0.4em !important;
 }
 
 /* Tighten h2/h3 too */
 section h2 {
   margin-top: 0.15em !important;
   margin-bottom: 0.35em !important;
 }
 section h3 {
   margin-top: 0.15em !important;
   margin-bottom: 0.3em !important;
 }
 
 /* Optional: reduce paragraph spacing slightly */
 section p {
   margin-top: 0.35em;
   margin-bottom: 0.35em;
 }

section {
  font-family: Arial, sans-serif;
  padding: 20px 34px 30px 34px;   /* less top padding */
  line-height: 1.25;
  font-size: 26px;                 /* base size for body text */
}

/* Extra room for dense / appendix slides */
section.dense {
  padding: 14px 28px 22px 28px;   /* noticeably tighter */
  font-size: 26px;
  line-height: 1.22;
}

/* =========================
   Headings
   ========================= */

h1 {
  color: #1a5276;
  font-family: Georgia, serif;
  font-size: 1.55em;
  margin: 0 0 0.10em 0;
  line-height: 1.08;
}

h2 {
  color: #1a5276;
  font-family: Georgia, serif;
  font-size: 1.2em;
  margin: 0 0 0.45em 0;
  line-height: 1.15;
}

h3 {
  color: #1a5276;
  font-size: 1.05em;
  margin: 0.2em 0 0.4em 0;
}

/* =========================
   Links + emphasis
   ========================= */

strong {
  color: #1a5276;
}

a {
  color: #1a5276;
  text-decoration: none;
  font-weight: 600;
}

a:hover {
  text-decoration: underline;
}

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
   Bullets: reduce indentation + noise
   ========================= */

ul {
  margin: 0.45em 0 0.1em 0;
  padding-left: 1.05em;            /* tighter indent */
}

li {
  margin: 0.28em 0;
}

li::marker {
  color: #1a5276;                  /* subtle brand color bullets */
}

/* Make nested bullets less ugly */
ul ul {
  margin-top: 0.25em;
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

section.cards li::marker {
  content: "";
}

section.cards li strong {
  color: #1a5276;
}

/* =========================
   Blockquotes + callouts
   ========================= */

blockquote {
  background: #1a5276;
  color: white;
  padding: 18px 24px;
  border-radius: 10px;
  border-left: none;
  font-size: 1.05em;
  margin: 0.65em 0;
}

blockquote strong {
  color: white;
}

/* Card blocks */
.card {
  background: #f0f4f7;
  padding: 14px 18px;
  border-radius: 8px;
  margin: 12px 0;
}

/* Bottom line callout */
.bottomline {
  background: #e8f1f5;
  border-left: 4px solid #1a5276;
  padding: 14px 18px;
  border-radius: 0 8px 8px 0;
  margin-top: 18px;
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

/* =========================
   Tables (if used)
   ========================= */

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.9em;
}

th, td {
  padding: 8px 10px;
  border-bottom: 1px solid #d9e2e8;
}

th {
  text-align: left;
  color: #1a5276;
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

**A lightweight discovery + authorization layer to makes ideal flow universal.**

- The core protocol fits in a handful of appendix slides  
- The registry never handles PHI — it only routes endpoints + approvals  
- It relies on two open primitives designed for reuse beyond healthcare:
  - **[STP](https://github.com/alex137/state-transfer-protocol):** State Transfer Protocol (streaming tables over HTTP)
  - **[EMTP](https://github.com/alex137/ephemeral-match-token-protocol):** Ephemeral Match Tokens (privacy-preserving matching)

Link: **[Spec + reference implementation](https://github.com/alex137/health-hub-registry)**  


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

- Make hubs a covered benefit tied to hub-enabled quality measures

**Bottom line:** Payment incentives + scalable enforcement can create the first universal, patient-controlled interoperability layer.

---

<!-- _class: cards -->
# Hubs as the Primary Patient Channel

HHS should also grant safe harbor for hub-mediated delivery (SMS, WhatsApp, email) under defined safeguards. Authorized, record-aware hubs become the default coordination channel — replacing portals.

* **Unified threads:** persistent hub-mediated conversations across providers 
* **Care coordination:** scheduling, referrals, transitions, discharge follow-up
* **Pharmacy workflows:** refills, substitutions, adherence
* **Coverage workflows:** prior-auth status, benefits questions, appeals

Result: one record-aware channel for patients and providers.

---
# Patient Channel + Financial Channel

Once hubs are authorized and reliably record-aware, they become the natural place patients manage the **financial side of care** — with the same context as the clinical record.

- **Unified out-of-pocket tracking** across providers + pharmacies  
- **Record-linked bills + explanations** (“what was this charge for?”)
- **Claim status + responsibility updates** (denied, adjusted, what you owe)
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

*Immediate access to allergies, meds, directives, & proxies drives adoption.*

---

<!-- _class: dense -->
# Benefit: Speeding Prior Authorization

Prior auth delays are mostly **documentation delays** that hubs can solve.

Payer investigators request access via a **Consent Request Direct Message** *(Appendix)*. Upon user approval, hubs issue a **Consent Grant** enabling **time-limited, scoped access** to the aggregate record *solely* for prior-auth and claims-audit review.

- **Patients:** faster approvals, less stress
- **Providers:** less doc churn, lower audit burden, less non-payment risk
- **Payers:** lower admin cost, faster and more consistent decisions

** Bottom line:** Prior-auth relief is a another near-term adoption driver. 

---

# Benefit: Auditable Claims + Sponsor Oversight

When documentation is slow, so are prior auth, audits, and disputes.

With hubs at scale, payers can expose **auditable claim state streams**:

- **Near-real-time lifecycle visibility** (submitted → denied → adjusted → paid)  
- **Faster audits + dispute resolution** (append-only, replayable history)  
- **Earlier fraud/waste detection** (duplication, upcoding, contract violations)  
- **Sponsor oversight** of TPAs, PBMs, and delegated risk groups  
- **Reconciliation** between provider billing mirrors and payer adjudication streams  

*Transactions stay X12. Auditable mirror for disputes + oversight.*

**Result:** accountable spend, lower admin cost, fewer drawn-out disputes.

---

# Benefit: Auditable Billing Mirrors  

*Low provider burden. High value for payers, sponsors, and patients.*

Providers already generate claims and patient bills.  
With hubs at scale, they can expose an **auditable mirror** of billing events:

- **No new format:** auto-generated from billing systems or outbound X12 logs  
- **Auditable + replayable:** “what was billed when — and what changed”  
- **Record-linked transparency:** bills + denials attach to clinical context  
- **Fewer disputes + faster payment** (providers, payers, sponsors)  

**Result:** billing becomes transparent & stateful — without new workflow burden.

---

# Provider Messaging 
### Record-Linked Collaboration

Universal cross-provider records means messaging stops being “fax in disguise.”

**Messages can point to the exact record context:**
- “Here’s the abnormal lab” *(opens that lab + trend + meds)*
- “Why was anticoagulation stopped?” *(opens discharge note + orders)*
- “Please confirm allergy status” *(opens allergy history + recent reactions)*

Providers communicate with **shared context**, not summaries.

**Result:** fewer mistakes, less back-and-forth, faster decisions.

---

# Persistent Patient-Scoped Care Channels  
### Shared-Record Messaging

- One thread shared across the care team (even across health systems)  
- Visible to nurses, MAs, care managers, and specialists  
- Messages persist with the record — not trapped in one portal  

This creates **common knowledge**: shared record + shared conversation.

**Result:** coordination becomes continuous, not episodic.

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
# Benefit: Targeted Messages (TMs)

Today, recalls, safety signals, protocol changes, and research requests are posted to websites — and affected patients/providers often never see them.  
**Targeted Messages (TMs)** solve this.

A TM is addressed to a deterministic targeting rule (RxNorm, ICD10, timeframe, etc.) — not a specific recipient.

Publishers (FDA / CDC / product developers) pull the hub list from the registry and send the TM to each hub.  Hubs match locally, then **translate the TM into Direct Messages (DMs)** to the right providers and attach to the right records.

**Result:** safety-critical messages reach the right clinicians automatically.

---

# Benefit: Real-Time Real-World Evidence

Research hubs enable near-real-time adverse event capture, real-world controls, and rapid trial recruitment — without years of data-sharing negotiation.

1. Recruit via `research_request` **Targeted Message Consent Requests**.

2. Upon approval, the user’s hub issues a **Consent Grant** to the research hub.

3. After payer confirmation, providers deliver records via standard FHIR subscriptions — and research advances.

---
<!-- _class: dense -->
# Benefit: Gaining Pharmacy Participation

*Medications are the most frequent & error-prone part of care — but today’s interoperability layer misses the dispense reality.*  Providers and hubs rarely know whether a prescription was **filled, substituted, refilled, or abandoned**.

HHS should require pharmacies to operate as **registry-certified provider-like endpoints**, so hubs can FHIR subscribe and receive:

- **Fill + refill status** (including non-pickup / abandonment)
- **Substitutions + med changes** (dispensed NDC mapped to RxNorm)
- **Adherence signals** (late refills, gaps, early discontinuation)

**Result:** safer prescribing, fewer errors, better chronic disease management; the med list reflects what happened, not just what was ordered.

---

<!-- _class: cards -->
# Pharmacy Unlocks: The Dispense Reality

Once hubs work reliably across providers, pharmacies can finally plug into the same universal layer — so the record includes what actually happened.

- **Care transitions:** discharge meds become verifiable + shareable → fewer reconciliation errors + readmissions  
- **Prior auth + audits:** proof-of-fill + med history assemble automatically → less documentation churn  
- **Targeted safety alerts:** pharmacies + hubs receive Targeted Messages for recalls, safety signals, formulary changes  
- **Messaging:** record-aware refill + substitution coordination with providers + hub-mediated patients  

**Bottom line:** Universal hub access enables universal pharmacy participation — and access to the most time-sensitive part of the record.

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

Latest Version Links:
* **Policy Deck:** [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-deck.pdf) & [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-deck.marp.md)

* **Implementation Deck:**  [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-impl-deck.pdf) & [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-impl-deck.marp.md)

---

<a id="common-questions"></a>
# Appendix: Answers to Common Questions

- How the Registry Prevents a National Patient ID  
- Why TEFCA Can’t Solve This  
- Options for Patients Without Insurance

---

# How the Registry Prevents a National Patient ID

Participants generate **rotating HMAC match tokens** locally using an ONC-published algorithm and time-limited keys.

The registry matches only **ephemeral tokens** — it never receives demographics and never stores a permanent identifier. Key rotation + variant expansion prevent the system from becoming a national patient ID.

**Importantly:** a functional registry also removes much of the policy pressure for creating one.

---

# Why TEFCA Can’t Solve This

TEFCA is institution-to-institution exchange. It helps providers share records with each other, but still leaves patients navigating multiple portals and requesting records episodically.

This framework is **patient-authorized endpoint enforcement**:
patients designate hubs, and providers must fulfill continuously to those hubs.

The enforcement locus shifts from institutional negotiation to patient rights.

---

# Options for Patients Without Insurance

Patients without payer coverage won’t have a payer to confirm hub authorizations. Options include:

- State Medicaid agencies acting as authorization-only participants for uninsured residents  
- ACA healthcare navigators providing confirmation while helping with enrollment  
- A pathway that connects hub access to coverage enrollment

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
Participants follow payer beneficiary NURLs → receive scoped approval SURLs

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

Link: **[EMTP spec + reference code](https://github.com/alex137/ephemeral-match-token-protocol/)**

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
<a id="surl-nurl-terms"></a>

# Appendix: STP Terms (SURLs + NURLs)

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
- **Payers:** hub users, sponsor member/employees, and patients
- **Hubs** payer beneficiaries 
- **Providers**: beneficiaries
- **Sponsors**: beneficiaries and providers. 

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
Delete records + terminate subscriptions only when **Denied across all active payers**.

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

<a id="finance-policy"></a>

# Appendix: Finance SURLs (Who Serves What)

`finance_surl` is an optional manifest endpoint carrying an STP finance stream
(`finance_event_stream`), scoped by mTLS identity.

**Recommended exposure:**
- **Payers SHOULD** expose `finance_surl` to **hubs + sponsors**  
- **Providers MAY** expose `finance_surl` to **hubs + payers**  
- **Sponsors MAY** expose `finance_surl` to **payers** *(premium + coverage expectations)*

Finance streams do **not** replace X12; they provide an auditable state mirror.

---

<a id="finance-stream"></a>

# Appendix: Finance Event Stream (Schema)

Finance streams mirror **transaction state** as an append-only log (claims, bills, payments, funding).

**SURL schema:** `finance_event_stream`  
`[SeqNo] \t [TS] \t [+/-] \t [Txn_ID] \t [Event_Type] \t [Action_URL] \t [KV...]`

- `Txn_ID`: stable transaction identifier *(claim / bill / payment / funding item)*
- `Event_Type`: from unified vocabulary *(next slide)*
- `Action_URL` (optional): scoped detail / documentation link
- `KV...`: whitespace-separated `key=value` metadata *(amounts, codes, dates, IDs)*

*(See next slide for event vocabulary.)*

---

<a id="finance-event-types"></a>

# Appendix: Finance Event Types (Unified)

Finance streams share a small common vocabulary usable by **providers, payers, and sponsors**.

**Event_Type ∈ {**
- `submitted` — record created *(claim / bill / invoice / funding request)*
- `accepted` — received / accepted for processing
- `denied` — rejected *(include `denial_code`)*
- `adjusted` — amounts changed *(contract, correction, coordination, recoupment)*
- `appealed` — dispute / appeal opened
- `paid` — payment issued or received
- `refunded` — reversal / refund  
**}**

`KV...` uses `key=value` pairs. Canonical keys:  
`billed_amount`, `allowed_amount`, `paid_amount`, `patient_responsibility`, `copay_due`, `denial_code`, `service_date`, `provider_id`  
Unknown keys MUST be ignored.

---
<a id="manifest-init-registry"></a>

# Appendix: Manifest Initiation (From Registry Match)

When a participant learns a new **foreign NURL** from its **Registry Match SURL**, it SHOULD initiate a manifest exchange.

It sends an STP Notify to the foreign NURL:

`surl=<Sender_Manifest_SURL>&manifest_nurl=<Sender_Manifest_NURL>`

- `surl`: sender’s relationship manifest SURL  
- `manifest_nurl`: where the receiver notifies back with its manifest SURL

The receiver uses the most recently notified `surl` as the sender’s current manifest.

----

<a id="manifest-init-payer"></a>

# Appendix: Manifest Initiation (From Payer Approvals)

Payers return **Hub_User_NURLs** to providers and sponsors to indicate an approved hub relationship.

When a party receives a new approved **Hub_User_NURL**, it SHOULD send an STP Notify:

`surl=<Sender_Manifest_SURL>&manifest_nurl=<Sender_Manifest_NURL>`

The hub fetches the sender’s manifest (SURL) and replies (via `manifest_nurl`)
with hub-user–specific endpoints for Direct, FHIR, and Finance.

---

<a id="endpoint-manifest"></a>

# Appendix: Relationship Manifest (SURL)

**Manifest SURL schema:** `endpoint_manifest`  
`[SeqNo] \t [TS] \t [+/-] \t [endpoint_type] \t [URL]`

**endpoint_type values:**  
`fhir_subscribe` | `fhir_read` | `direct_message` | `finance_surl`

- `finance_surl` serves `finance_event_stream`
- Unknown `endpoint_type` values MUST NOT break clients.

----

# Appendix: Manifest Exchange — Example

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
<a id="tdm-headers"></a>

# Appendix: TM Required Headers

- `schema_version`: targeting semantics version (e.g., v1)
- `filter`: deterministic predicate over coded fields *(RxNorm, ICD10/SNOMED, CPT, LOINC, demographics, timeframe)*
- `message_type`: `recall | safety_signal | advisory | protocol_change | research_request | payer_policy_change`
- `deliver_to`: `patient | product_provider | treating_providers` *(product_provider = prescriber / ordering / implanting clinician)*
- `valid_until`: expiration timestamp
- `context` (optional): free-text rationale / instructions

**Matching:** filter MUST be applied deterministically; AI MAY refine only after a filter hit. Unknown keys MUST be ignored.
