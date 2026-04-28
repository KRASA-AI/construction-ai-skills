# Backcharge Management — Reference

> Reference for skills that draft, issue, log, or contest backcharges
> on construction projects. Backcharges are the most legally consequential
> and most commonly reversed admin action on a project; the discipline that
> governs them is unglamorous and unforgiving.
>
> This document is not legal advice. Where a backcharge is material or where
> the affected sub is likely to lien, dispute, or sue, retain construction
> counsel licensed in the project state.

---

## Why Backcharge Discipline Matters

Of every admin workflow on a construction project, backcharges have the lowest tolerance for sloppiness. A change order that is poorly drafted may be re-papered. An RFI with the wrong reference may be re-issued. A backcharge that is poorly drafted is often **reversed** — at the next pay app review, in mediation, in arbitration, or by an auditor a year later — because it failed one of a small number of well-known defensibility tests.

Backcharges are reversed for a small set of reasons that recur in every dispute:

1. **No prior written notice** to the responsible party identifying the deficiency and providing an opportunity to cure
2. **Cure window not honored** — the work was self-performed or replacement-contracted before the contractually defined cure window expired
3. **Sub not invited to observe** the corrective work
4. **Costs not traceable** — a round number with no timesheet, invoice, or quote behind it
5. **Wrong contract clause** — the deduction-from-payment clause was not cited; or the cited clause does not authorize the action taken
6. **Silent accumulation** — backcharges held in a binder until closeout and dumped on a final pay app
7. **Misclassification** — punch-list items, warranty items, or out-of-scope work treated as backcharges
8. **Coercive use** — the backcharge appears to be leverage on an unrelated change order or price concession

The four-document chain (Notice of Deficient Work → Notice of Intent to Cure & Backcharge → Backcharge Notice → Deduction Authorization Letter) and the eight-item defensibility self-check used in `admin/backcharge-notice-drafter.md` are the durable, codifiable shape of the workflow. This reference documents the practitioner-level rules that the skill draws on.

---

## Backcharge vs. Adjacent Workflows

A backcharge is a **deduction from payment** for work the upper-tier had to perform or pay for because the lower-tier failed. It is not the same as any of the following:

| Workflow | What it does | Why it is not a backcharge |
|---|---|---|
| **Change order** | Adds scope and adjusts contract sum | Adds; backcharges deduct |
| **Punch-list item** | Closeout-cycle correction under the prime contract | Pre-substantial-completion sub-default; backcharge runs against the deduction-from-payment clause, not the punch-list / closeout clause |
| **Warranty claim** | Post-substantial-completion correction under the warranty clause | Different clause, different remedy posture |
| **Delay / impact claim** | Time and quantum recovery | Backcharges may include a delay component, but the delay claim is its own document with its own elements |
| **Demand letter / termination for default** | Escalation to terminate | Backcharge is in-flight; termination is the next escalation rung |
| **Setoff / recoupment** | Equitable accounting between parties on the same contract | Setoff is broader; backcharge is the specific contractual mechanism |

Misclassification is the cheapest backcharge to reverse — drafters who run a punch-list item through the backcharge chain almost always lose because the contract's deduction-from-payment clause does not authorize the action the punch-list clause does.

---

## The Four-Document Chain

The chain is the durable shape of the workflow. Every document references the prior one; the chain is what reconstructs the timeline in any later dispute.

### Document 1 — Notice of Deficient Work (issued at discovery)

The single most important document in the chain. Without a written notice issued before any remediation, every later step is exposed.

- Identifies the specific defect: location, quantity, spec / drawing reference, photo numbers
- Cites the subcontract clause that defines acceptable work
- States the cure window (commonly 24, 48, 72 hours, or 7 days, per the contract)
- States the consequence of non-cure
- Invites the sub to inspect and propose a cure plan
- Sent by the contract-required notice method (certified mail / email / project-management-platform notification — whichever the contract specifies; do not substitute)
- Proof of delivery preserved

### Document 2 — Notice of Intent to Cure & Backcharge (issued after cure window expires)

The most-overlooked document in the chain. Many backcharges have a Document 1 and a Document 3, with no Document 2 — and that gap is what gets the backcharge reversed in mediation. Document 2 is the link that says "we are about to cure on your behalf, and you may attend."

- References Document 1 and the expired cure window
- States who will perform the cure (in-house, named replacement contractor) and when
- Invites the sub to attend, observe, and document
- States the basis on which costs will be calculated
- Reserves rights to additional consequential costs (delay, A/E re-review, owner-pass-through)

### Document 3 — Backcharge Notice (issued after cure is complete and costs are documented)

The deduction document. References Documents 1 and 2; itemized cost worksheet; attachments list; reservation language; specific pay-app from which the deduction will be taken.

### Document 4 — Deduction Authorization Letter (internal — to AP)

Internal-only routing. Project / sub / contract / pay-app / amount; lien-waiver coordination note; approvals per company policy.

---

## The Eight-Item Defensibility Self-Check

Every backcharge passes through this list before issuance. For each item, the answer must be yes — for any "no", the gap is flagged in the cover memo and the corrective step is recommended.

1. Was a written notice of deficient work issued before any remediation?
2. Did the sub have a documented opportunity to inspect and to cure?
3. Was the sub invited to be present during the corrective work?
4. Is every cost line backed by a timesheet, invoice, or quote (not a round number)?
5. Does the subcontract or PO contain a clause that authorizes deduction from payment?
6. Is the backcharge being issued contemporaneously with the cure (not silently accumulated)?
7. Is the defect properly classified (not a punch-list item, warranty item, or coercion of an unrelated change)?
8. Does the package preserve the sub's right to dispute within the contractual window?

---

## Seven-Class Deficiency Taxonomy

The first decision in any backcharge is to classify the deficiency, because the contract clause that authorizes the deduction varies by class:

| Class | Description | Typical Authorizing Clause |
|---|---|---|
| **Defective workmanship** | Work fails contract spec | Deduction-from-payment / right-of-offset |
| **Non-conforming material** | Material does not match approved submittal | Non-conformance + replacement |
| **Missed cleanup** | Sub failed to remove debris / sweep / haul | Cleanup (often a per-occurrence rate or pro-rata of GC labor) |
| **Damage to other trades' work** | Sub's work or equipment damaged another trade's installed work | Indemnity + cooperation |
| **Missed milestone / no-show on a fix** | Sub failed to staff the cure on time | Delay / coordination |
| **Equipment misuse / unauthorized access** | Sub used GC equipment without authorization or accessed restricted areas | Equipment-use / site-security / restoration |
| **Re-inspection or re-test fees** | AHJ or A/E re-review charged because of the sub's failure | Costs of reinspection (if contract has one); otherwise deduction-from-payment |

A backcharge that does not match any of these classes is usually not a backcharge — it is something else (a change order, a warranty item, a punch-list item, a claim).

---

## Cost Substantiation Discipline

The single fastest way to lose a backcharge is to issue a round number. Every line in the itemized cost worksheet must trace to a source:

- **In-house labor** — Foreman / craft / laborer hours × burdened rate, with timesheet number
- **Replacement-sub costs** — Invoice from the replacement contractor, with invoice number
- **Material** — Pricing source (vendor invoice, internal stock-issue ticket), unit price × quantity, with sales tax handled per company policy
- **Equipment** — Rental rate × duration, or internal-equipment standard rate × duration, with rental ticket or internal time-use record
- **Third-party costs** — Disposal tickets; AHJ re-inspection receipts; A/E re-review invoices passed through
- **OH&P on remediation** — Only if the contract authorizes it; cite the clause; do not apply silently

For the costs that look high vs. industry norms (e.g., labor hours that imply 4× the original install hours), flag for the GC's review before sending; do not sandbag the worksheet but do not pad it either. Backcharges that are obviously inflated read as bad faith and reverse on that ground alone.

---

## Lien-Waiver Coordination

Backcharges and lien-waivers are tightly coupled. The mechanic that operates underneath is simple: a sub who is backcharged retains lien rights for the disputed amount, even after signing a progress-payment lien waiver, **only if** the waiver carves out the disputed amount.

- The sub's progress lien-waiver should reflect the **gross** billing less the deduction; the waiver should explicitly **exclude** the disputed deduction amount, the underlying contract dispute, and any related claims
- The waiver should be the conditional form (`Conditional Waiver and Release on Progress Payment` or the state's statutory equivalent), not the unconditional form, because the deduction makes the actual payment a partial payment of the gross billing
- Where the project state requires a statutory waiver form (Arizona, California, Florida, Georgia, Massachusetts, Michigan, Mississippi, Missouri, Nevada, Texas, Utah, Wyoming — see `knowledge-base/regulations/lien-waivers-by-state.md`), the carve-out is added to the carve-out section of the form, **never** to the form's substantive release text
- In Mississippi and Wyoming, the waiver requires notarization to be enforceable; the disputed-deduction carve-out must be in the notarized document

This is the practitioner pattern that ties `admin/backcharge-notice-drafter.md` and `admin/lien-waiver-drafter.md` together.

---

## Hard Rules

- **No silent accumulation.** Issue the backcharge contemporaneously with the cure event; do not hold backcharges in a binder for closeout. Silent-accumulation backcharges are read as bad faith and reverse for that reason.
- **No coercive backcharges.** A backcharge tied to leverage on an unrelated change order, a price concession, or a payment of an undisputed sum will reverse on review.
- **No invented costs.** Every line traces to a source.
- **No imputed cure.** The cure must actually happen — and be observed or invited-to-be-observed by the sub. A "cure" that nobody saw is not a cure.
- **No backcharge without authority.** The deduction-from-payment / right-of-offset clause must exist in the subcontract or PO. Backcharges are contractual, not statutory; without a clause that authorizes the deduction, the deduction may be void.
- **No notice substitution.** If the contract requires certified mail, certified mail is the method. Email is not certified mail. Procore notification is not certified mail.
- **No omitted reservation.** The sub's right to dispute under the contract — typically with a window of 7 to 14 calendar days from receipt — must be preserved in the Backcharge Notice. A waiver of that right is unenforceable in many states.

---

## Severity Triage

Not every backcharge gets the same level of attention. Severity drives notice tone, cure window, and counsel-review threshold:

- **🔴 Safety / hold-point failure / inspection fail blocking a downstream trade** — Immediate notice; cure window measured in hours; counsel review recommended for material amounts; reservation of rights to delay damages and downstream-trade impact must be explicit
- **🟡 Coordination conflict / cosmetic-but-spec-fail / adjacent-trade damage** — Standard notice; cure window per contract; counsel review at the company's threshold
- **🟢 Housekeeping / cleanup / minor restoration** — Routine notice; per-occurrence rate often pre-defined; rarely contested; lowest counsel-review priority

---

## Backcharge Register

Every project should maintain a single backcharge register tracking, at minimum:

| Field | Notes |
|---|---|
| Backcharge number | Sequential per project (e.g., BC-001) |
| Sub / vendor | |
| Defect description and location | |
| Class | One of the seven |
| Notice timeline | Document 1 date, Document 2 date, Document 3 date, Document 4 date |
| Cure window | Length and source (contract clause or industry-reasonable) |
| Cure performed by | In-house / replacement contractor name |
| Cost | Direct + OH&P, with breakdown reference |
| Pay app deducted | Pay app number and period-ending |
| Sub's response | Accepted / contested (with date and reservation reference) |
| Status | Open / contested / closed / reversed |
| Lien-waiver carve-out | Yes (with reference) / no (with reason) |

The register is the second-level audit trail. When a backcharge is contested at closeout or in arbitration, the register answers two questions auditors always ask: did the GC follow the four-document chain on every backcharge issued on this project, and did the GC apply the chain consistently across subs (so no individual sub can argue the GC singled them out).

---

## When to Escalate to Counsel

The skill's default counsel-review recommendation triggers when any of the following is true:

- The backcharge amount exceeds a configured threshold (commonly $25,000 or 5% of the subcontract value, whichever is lower)
- The defect is a safety condition or an inspection fail that may have caused or contributed to a downstream-trade delay
- The sub has already retained counsel, filed a lien, served a stop-payment notice, or threatened arbitration
- The sub's contract is a custom GC-form with an unusual deduction-from-payment clause (not AIA A401, ConsensusDocs 750, EJCDC C-523)
- The cure was delayed or otherwise diverged from the four-document chain
- The project is federal or state public, and the bond-claim mechanics will operate alongside the backcharge

Counsel review is not a sign of weakness; it is the cheapest insurance available against a reversed backcharge.

---

## How Skills Use This Reference

- `admin/backcharge-notice-drafter.md` uses this reference for the seven-class taxonomy, the four-document chain pattern, the eight-item defensibility self-check, the lien-waiver coordination note, and the counsel-escalation thresholds. The skill builds the four documents; this reference is the "why" behind each.
- `admin/lien-waiver-drafter.md` uses this reference for the disputed-deduction carve-out language and for the rule that a sub's lien rights survive a backcharge if and only if the waiver carves out the disputed amount.
- `admin/pay-application-reviewer.md` uses this reference for the pay-app-deduction handling — when a pay app reflects a backcharge deduction, the review confirms the four-document chain is in place and that the lien-waiver coordination has been applied.
- `admin/closeout-documentation-auditor.md` uses this reference at closeout to walk through the project's backcharge register and confirm every open backcharge has either been resolved (paid, closed, or formally contested) or has been carried forward to arbitration / litigation with the appropriate documentation.
- `admin/wip-billing-reviewer.md` uses this reference for the cost-traceability standard — backcharges show up as cost adjustments on the WIP, and a backcharge that does not trace to a documented chain is the kind of WIP item a surety reviewer flags.

The chain is the same in every case. The skills change; the discipline does not.
