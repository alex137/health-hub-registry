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
  line-height: 1.2;
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

**Latest version links:**  
- **Policy Deck:** [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-deck.pdf) · [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-deck.marp.md)  
- **Implementation Deck:** [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-impl-deck.pdf) · [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-impl-deck.marp.md)

---

<a id="common-questions"></a>
# Answers to Common Questions

- How the Registry Prevents a National Patient ID  
- Why TEFCA Can’t Solve This  
- Options for Patients Without Insurance

---

# How the Registry Prevents a National Patient ID

Participants generate **rotating HMAC match tokens** locally using an ONC-published algorithm and time-limited keys.

The registry matches only **ephemeral tokens** — it never receives demographics and never stores a permanent identifier. Key rotation + variant expansion prevent the system from becoming a national patient ID.

**Importantly:** a functional registry removes policy pressure for creating one.

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
# END
