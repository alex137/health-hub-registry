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
/* Dense slides */
section.dense {
  padding: 12px 28px 18px 28px;
  font-size: 24px;
  line-height: 1.10;
}

section.dense ul { margin-top: 0.25em; }
section.dense li { margin: 0.15em 0; }

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

These hubs are already creating patient value

Millions use Apple Health, Guava, Picnic, OneRecord, and others to:

- **Aggregate + organize** medical records across providers  
- **Help patients interpret** results and manage conditions (AI-assisted)  
- **Enable access** to async care, virtual visits, and home diagnostics  
- **Keep clinicians informed** (especially in transitions & emergencies)  
- **Support proxies** for seniors and complex chronic care  

They could unlock even bigger payer value if they were reliable at scale.

---

<!-- _class: cards -->

# The Promise of Hubs At Scale for Payers

- **Lower total cost of care**  
  Better self-care + navigation → fewer avoidable ED visits, better chronic control

- **Lower admin cost**  
  Shift portal + call-center volume to record-aware self-service workflows

- **Better steerage**  
  Guide in-network care with real-time estimates + prior-auth rules

- **Faster prior auth + audits**  
  Records assembled automatically → fewer provider callbacks, faster review

- **Risk reduction & prevention**  
  Caregiver-enabled workflows + early coordination for complex members

---
<!-- _class: cards -->
# But the Hub Flywheel Is Broken

- **No provider automation → bad user flow**  
  Fragmented portals + inconsistent APIs → incomplete records, manual retrieval

- **Bad user flow → no payer pull**  
  Unreliable value → payers won’t subsidize or recommend

- **No payer pull → no business model → no scale**  
  Most users won’t pay → hubs can’t reach mass adoption

- **No scale + unclear HIPAA/liability → no provider automation**  
  Providers won’t invest in record exchange + messaging needed to fix the flow

**Bottom line:** Private actors can’t fix this flywheel — **HHS can.**

---
<!-- _class: cards -->
# How HHS Can Fix the Flywheel

*Launch a registry that makes approved hub↔provider discovery easy:

1. User registers with a hub to authorize PHI access
2. Hub redirects user to payer for member confirmation 
3. User confirmes hub phi authorization (revocable)
4. Payer publishes authorization to the user’s providers
5. Payers share plan / network / cost-sharing data with approved hubs  
6. Providers auto-exchange records + messages with the hub
7. Patients get coordinated care; payers cut costs


----
<!-- _class: dense -->
# How this registry can work

This provisional implementation spec ([PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-impl-deck.pdf)) is designed for ease of  implemention. It proposes a lightweight system:

Registry-certified organizations share **token ↔ endopint URL pairings** with registry:
*	Endpoint URL: member-scoped service URL (actionable, replaceable)
* Token: derived from local identifiers using a **shared time-bounding algorithm** 

**Registry matches participant endpoints by token overlap (no PHI):**
- Enables **payers** to discover matched **hub endpoints**
- Enables **hubs / providers / sponsors** to discover matched **payer endpoints**

**Privacy property:** the registry never receives demographics or PHI. URLs/tokens are time-bounded + replaceable — so can’t become a persistent identifier.

---

# Outside the Registry

The registry only enables **discovery + authorization routing**.  
All clinical + financial workflows run **between participants** using existing standards:

**Providers & hubs:** Pull approvals from payers; records + messaging via **FHIR + Direct**
**Payers/sponsors/providers:** Finance coordination via **X12-compatible mirrors** 
  
  (transactions stay X12)

HHS mainly needs to **standardize + certify + enforce** adoption.

---

<!-- _class: cards -->
# Enforcement and Adoption
### Make hub exchange enforceable at scale

- Treat **payer-confirmed hub authorization** as a HIPAA safe harbor for PHI exchange
-	Require providers to retrieve approved hubs from payers
- Require providers to initiate continuous exchange to approved hubs
- Require hubs to publish **provider record-delivery performance reports**
- Use hub reports to automate **information-blocking enforcement** at scale
- Make hubs a **covered benefit** tied to hub-enabled quality measures
- Allow hub-mediated delivery (SMS, WhatsApp, email) under defined safeguards

---

# What Universal Hubs Unlock

The next slides show what becomes possible once hubs are universal and reliably record-aware.

Coordination becomes continuous: shared messaging + emergency continuity + pharmacy reality + targeted safety outreach — all grounded in the same aggregate record.

---
<!-- _class: cards -->
# Hubs as the Primary Patient Channel

Record-aware hubs become the default coordination channel — replacing portals.

* **Unified threads:** persistent hub-mediated conversations across providers 
* **Care coordination:** scheduling, referrals, transitions, discharge follow-up
* **Pharmacy workflows:** refills, substitutions, adherence
* **Coverage workflows:** prior-auth status, benefits questions, appeals

Result: one record-aware channel for patients and providers.

---

<!-- _class: dense -->
# Hubs: Proxy + Emergency Access
*Allergies, meds, directives — and trusted proxies when it matters.*

**Proxy usage:** Hubs can let users designate proxies to manage care and approvals (ongoing or emergency-only, optionally with delay) — especially for seniors and complex chronic care.

**Emergencies:** On a request from a **registry-certified emergency provider**, hubs should:
- grant immediate access to a **user-selected minimum emergency dataset**
- notify the user and designated emergency proxies via multiple channels
- allow emergency proxy access after a configured delay
- apply heightened logging + audit trails to deter abuse

**Non-emergency requests:** Hubs follow the user’s standard consent settings.

---
# Provider Messaging
*Shared record + shared thread across health systems — with AI-ready context.*

- **Deep-link record context across systems:**  
  “Here’s the abnormal lab” *(lab + trend + meds)* · “Why stopped anticoag?” *(discharge note + orders)* · “Confirm allergy?” *(allergy history)*

- **Persistent shared threads:** conversations live with the aggregate record → **common knowledge** across teams

- **AI becomes practical:** full-context threads enable better triage + routing, drafted replies, lab/refill/transition monitoring, and proactive alerts

**Result:** fewer callbacks + errors; faster decisions; lower coordination burden.

---

<!-- _class: dense -->
# Gaining Pharmacy Participation

*Medications are the most frequent & error-prone part of care — but today’s interoperability layer misses the dispense reality.*  Providers and hubs rarely know whether a prescription was **filled, substituted, refilled, or abandoned**.

HHS should require pharmacies to operate as **registry-certified provider-like endpoints**, so hubs can FHIR subscribe and receive:

- **Fill + refill status** (including non-pickup / abandonment)
- **Substitutions + med changes** (dispensed NDC mapped to RxNorm)
- **Adherence signals** (late refills, gaps, early discontinuation)

**Result:** safer prescribing, fewer errors, better chronic disease management; the med list reflects what happened, not just what was ordered.

---

<!-- _class: dense -->
# Pharmacy Unlocks: The Dispense Reality

With dispense status flowing into hubs:

- **Care transitions:** discharge meds become verifiable + shareable → fewer reconciliation errors + readmissions  
- **Prior auth + audits:** proof-of-fill + med history assemble automatically → less documentation churn  
- **Targeted safety alerts:** pharmacies + hubs receive TMs for recalls + safety signals + formulary changes  
- **Messaging:** record-aware refill + substitution coordination w/ providers + patients  

---

<!-- _class: dense -->
# Targeted Messages (TMs)

Today, the FDA, CDC, and product developers can’t reliably reach the right patients or clinicians with recalls, safety signals, or protocol changes. They’re limited to website posts and press releases.

**Targeted Messages (TMs)** solve this.

1. TMs target rules-based filters (RxNorm, ICD10, timeframe) — not specific recipients.
2. Publishers pull the hub list from the registry and send the TM to each hub.
3. Hubs match locally & deliver to the right clinicians — linked to the relevant record.

**Result:** safety-critical outreach reaches the right clinicians fast — automatically.

*This same mechanism also supports `research_request` recruitment (next slide).*

---

# Real-Time Real-World Evidence

Research hubs enable near-real-time adverse event capture, real-world controls, and rapid trial recruitment — without years of data-sharing negotiation.

1. Recruit via **Targeted Messages** that include a **Consent Request** (opt in to a research hub).

2. If the user approves, their hub sends a **Consent Grant** to the research hub (so it can request payer confirmation).

3. After payer confirmation, providers deliver records via standard FHIR subscriptions — and research can run continuously.

**Bottom line:** Research becomes an opt-in default — not a one-off data-sharing project.

---


# A System Upgrade for Financial Coordination

The same universal layer improves financial flow for every party:

- **Patients:** faster access to covered care + real-time cost clarity
- **Providers:** faster reimbursement + fewer payment disputes
- **Payers:** lower admin cost + better documentation + earlier anomaly detection
- **Sponsors:** delegated entity oversight via auditable claim mirrors

Next: prior auth, auditable mirrors, and the patient financial channel.


---

# Patient Channel + Financial Channel

Record-aware hubs become the natural place patients manage the **financial side of care** — with the same context as the clinical record.

- **Unified out-of-pocket tracking** across providers + pharmacies  
- **Record-linked bills + explanations** (“what was this charge for?”)
- **Claim status + responsibility updates** (denied, adjusted, what you owe)
- **Appeals + disputes** with the right clinical context attached  
- **Payment plans + financing** (HSA, employer benefits, charity care routing)

**Result:** patients manage costs in real time, with full record context.

---


<!-- _class: dense -->
# Speeding Prior Authorization & Claims Review 

Prior auth delays are mostly **documentation delays** that hubs can eliminate.

Payer reviewers request access via a **Consent Request Direct Message**. Upon user approval, hubs issue a **Consent Grant** enabling **time-limited, scoped access** to the aggregate record solely for prior auth and case-level review.

- **Patients:** faster approvals, less stress
- **Providers:** less documentation churn, lower audit burden, less non-payment risk
- **Payers:** lower admin cost, faster and more consistent decisions

**Hub-based consent → faster approvals for patients — and faster payments for providers.**
----
<!-- _class: dense -->
# Auditable Finance Mirrors  
*Stateful, replayable billing + claim status — across providers, payers, and sponsors.*

X12 remains the transaction layer. The registry makes it easy for participants to expose a small **auditable mirror** of finance state:

- **Payers publish claim/adjudication mirrors** for **sponsors + providers**
- **Providers publish billing mirrors** for **payers**
- **Reconciliation becomes automatic:** “what was billed, allowed, paid”
- **Faster audits + disputes:** append-only history, replayable and timestamped
- **Less waste + friction:** earlier anomaly detection + fewer callbacks and appeals

**Transparent + stateful finance → lower admin cost, fewer disputes, faster payments.**

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

**Latest version links:**  
- **Policy Deck:** [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-deck.pdf) · [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-deck.marp.md)  
- **Implementation Deck:** [PDF](https://github.com/alex137/health-hub-registry/releases/latest/download/health-hub-registry-impl-deck.pdf) · [Marp source](https://github.com/alex137/health-hub-registry/blob/master/deck/health-hub-registry-impl-deck.marp.md)
