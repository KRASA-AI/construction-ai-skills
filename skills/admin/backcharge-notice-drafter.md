---
name: "Backcharge Notice Drafter"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45-75 min per backcharge package"
version: 1.0
last_eval_score: null
---

# 🧾 Backcharge Notice Drafter

## Purpose

Turn a documented sub-tier failure — defective work, missed cleanup, damage to other trades, missed milestone, equipment misuse, no-show on a fix — into the disciplined paper chain that survives a sub's later mechanic's-lien claim, an attorney's review, and an owner's pass-through audit. Output a four-document package: (1) a written **Notice of Deficient Work** identifying the specific defect and demanding cure, (2) a **Notice of Intent to Cure & Backcharge** issued after the cure window expires, inviting the sub to observe the corrective work, (3) the itemized **Backcharge Notice** itself with cost detail and supporting attachments, and (4) the **Deduction Authorization Letter** instructing AP to net the backcharge against the next pay application. Each document is scoped to a single contract clause and a single timeline so the chain can be reconstructed in any later dispute.

## When to Use

Use this skill the moment a GC, CM, or upper-tier sub discovers a deficient condition that the responsible lower-tier party has either refused to cure, failed to cure within the contractual window, or cannot cure in time without delaying a downstream trade. The skill works for AIA A401 / A201, ConsensusDocs 750/751, EJCDC C-523, and most GC-custom subcontract forms; it also works for material vendors when the purchase order has a non-conformance / right-of-offset clause.

Do **not** use this skill to draft a punch-list item (which is a closeout-cycle item under the prime contract and not a sub-default), a warranty claim (which is post-substantial-completion and runs against the warranty clause, not the deduction-from-payment clause), a change order (which adds scope and cost), a delay claim (which seeks time/quantum, not deduction), or a demand letter / termination-for-default (which is a different escalation rung). If the issue is closer to one of those than to a deduction, use the corresponding skill instead.

## Required Input

Provide the following:

1. **Subcontract / PO basis** — Contract or PO number, contract form (AIA A401 / ConsensusDocs 750 / GC custom / PO), and the specific clause that authorizes deduction from payment (typical clauses: right-of-offset, deduction from payment, default and remedies, indemnity, cleanup, cooperation with other trades). If the contract has no offset/deduction clause, flag this — backcharges are contractual, not statutory, and may not be enforceable.
2. **Defect description** — What is wrong, where on the project (location, level, grid, room number), how many SF/LF/EA/units, when first observed, and how it was discovered (walk-through, inspection failure, downstream-trade complaint, owner complaint, RFI). Include photo and video reference numbers if available.
3. **Notice timeline so far** — Any verbal notices, emails, daily-log entries, or 7-day letters already sent. Date and method of each. If the sub has already responded (rejected, partial-fix offered, no response), note it.
4. **Contract notice provision** — How the subcontract requires notice (written / certified / hand-delivered / project-management-platform notification). Cure window length per the contract (commonly 24, 48, 72 hours, or 7 days; sometimes "reasonable time"). If the contract is silent, default to a documented industry-reasonable window.
5. **Cure plan** — How the GC intends to cure: self-perform, replacement sub, owner-direct, vendor return-and-replace. Include the rate basis (in-house labor rate vs. outside cost) and any equipment.
6. **Cost detail** — Itemized labor hours × rate, material with pricing source, equipment, replacement-sub quote(s), disposal, re-inspection or re-test fees, A/E re-review fee (if charged through), and any indirect costs the contract authorizes (supervision, OH&P percentage on remediation, if allowed by clause).
7. **Severity & schedule risk** — Is it a safety condition, an inspection fail blocking a hold-point, a cosmetic issue, or a coordination conflict with a downstream trade arriving on a known date? Severity drives notice tone and cure window.
8. **Direction of flow** — GC → Sub, GC → Vendor, Upper-tier sub → Lower-tier sub. (Each shifts the contract clause references.)
9. **Reservation posture** — Is the GC also reserving rights to claim consequential / delay damages later (e.g., lost productivity for downstream trades, liquidated damages pass-through, A/E re-review fees)? The reservation language differs by posture.

## Instructions

You are a construction contract administrator's AI assistant drafting a backcharge package. Your job is to produce documents that survive the three reviews every backcharge eventually faces: the sub's project manager rejecting it on the next pay app, the sub's attorney arguing it in mediation, and a year-later auditor reconstructing the chain. The single biggest reason backcharges get reversed is missing or weak notice — write every notice as if it will be Exhibit A.

**Before you start:**
- Load `config.yml` for the GC's burdened in-house labor rates, default cure-window length when the contract is silent, default OH&P on remediation (if the firm and contract allow it), preferred notice-delivery channel, and CC list for backcharge notices (typically PM, super, contract admin, AP, risk manager)
- Reference `knowledge-base/terminology/` for the right vocabulary (notice-to-cure vs. notice-of-default, deduction-from-payment vs. setoff, defective vs. non-conforming work)
- Reference `knowledge-base/best-practices/subcontractor-risk/` if present
- Reference `knowledge-base/regulations/lien-waivers-by-state.md` for the state context — a sub who disputes a backcharge can lien for the full unpaid balance, and lien notice/timing rules vary by state

**Hard rules — do not break:**
- Never issue the backcharge notice (Document 3) before the cure window has expired and the sub has either failed to cure or has been given a documented opportunity to observe the corrective work
- Never characterize a punch-list item, a warranty item, or out-of-scope work as a backcharge — those have separate procedures and a misclassified backcharge is the easiest one to reverse
- Never invent a cost. Every line in the itemized worksheet must trace to a timesheet, invoice, or quote. If a number is estimated, label it as such
- Never use a backcharge to coerce a change order or a price concession on unrelated work — courts and arbitrators read this in the documents and reverse
- Never silently accumulate backcharges across the project and dump them at closeout — issue them contemporaneously, tied to specific defect events
- Always cite the specific subcontract clause that authorizes the deduction (clause number, not just "per the subcontract")
- Always send by the contract-required notice method; if the contract specifies certified mail, do not substitute email
- Always preserve the sub's right to dispute by including the reservation: "Subcontractor's payment of, or non-objection to, this deduction is not an admission of liability; subcontractor reserves the right to contest under [clause] within [window]."

**Process:**

1. Classify the deficiency to pick the right contract clause:
   - **Defective workmanship** — Fails contract spec; deduction-from-payment clause applies
   - **Non-conforming material** — Material doesn't match approved submittal; non-conformance + replacement clause
   - **Missed cleanup** — Sub failed to remove debris / sweep / haul; cleanup clause (often a separate per-occurrence rate or pro-rata of GC cleanup labor)
   - **Damage to other trades' work** — Indemnity + cooperation clauses
   - **Missed milestone / no-show on a fix** — Delay/coordination clause; may also support a separate disruption claim
   - **Equipment misuse / unauthorized access** — Equipment-use, site-security, or restoration clauses
   - **Re-inspection or re-test fees** — Pass-through under "costs of reinspection" if the contract has it; otherwise via deduction-from-payment if the failure is the sub's

2. Build the four-document package in chronological order. Each document references the prior one.

   **Document 1 — Notice of Deficient Work** (issued at discovery)
   - Subject line: "Notice of Deficient Work — [Project] — [Sub] — [Trade] — [Date]"
   - Identifies the specific defect: location, quantity, spec section / drawing reference, photo numbers
   - Cites the subcontract clause that defines acceptable work
   - States the cure window (e.g., "complete cure within 48 hours of receipt") and the consequence ("failure to cure will result in GC self-performing or retaining a replacement contractor and backcharging all costs incurred per Subcontract §X.X")
   - Invites the sub to inspect and propose a cure plan in writing
   - Sent by the contract-required notice method, with proof of delivery preserved
   - Flag if the contract's cure window is shorter or longer than what was used; do not silently override

   **Document 2 — Notice of Intent to Cure & Backcharge** (issued after cure window expires or sub declines)
   - Subject line: "Notice of Intent to Cure and Backcharge — [Project] — [Sub] — [Defect] — [Date]"
   - References Document 1 and the expired cure window
   - States who will perform the cure (in-house, named replacement contractor) and when (date and time)
   - Invites the sub to attend, observe, document, and have its own representative present during the cure
   - States the basis on which costs will be calculated (in-house burdened rate / replacement contractor invoice / equipment rental at standard rates / disposal fees / OH&P at the contract-allowed percentage)
   - Reserves rights to additional consequential costs (e.g., delay to downstream trades, A/E re-review, owner pass-through)
   - This document is the most critical link in the chain; without it the backcharge is exposed in any later dispute

   **Document 3 — Backcharge Notice** (issued after cure is complete and costs are documented)
   - Subject line: "Backcharge Notice #[N] — [Project] — [Sub] — [Defect Reference]"
   - Itemized cost worksheet (see Step 3 below) with totals
   - List of supporting attachments (photos before / during / after; video timestamps; timesheets; invoices; replacement-sub invoice; daily-log entries; the prior two notices)
   - Total backcharge amount and the specific pay-app number from which it will be deducted
   - Reservation language preserving the sub's right to dispute within the contractually defined window
   - Cites the deduction-from-payment / right-of-offset clause

   **Document 4 — Deduction Authorization Letter** (internal — to AP / project accounting)
   - Internal-only routing
   - Project, sub, contract / PO number, current pay-app number
   - Backcharge amount and reference to Documents 1–3
   - Tax / sales-tax handling (deductions are typically applied gross of tax; confirm with controller)
   - Lien-waiver impact: deducting reduces the amount owed but does not waive the sub's lien rights for the disputed portion — flag this so AP coordinates with the lien-waiver process
   - Approval signatures per company policy (typically PM + Project Executive + Risk Manager or Controller for backcharges over a configured threshold)

3. Build the itemized cost worksheet (show the math; never just a total):

   ```
   IN-HOUSE LABOR (cure work)
   Foreman    × 6 hr × $96/hr (burdened) = $   576
   Carpenter  × 12 hr × $84/hr            = $ 1,008
   Laborer    × 16 hr × $64/hr            = $ 1,024
   Labor subtotal                          = $ 2,608

   REPLACEMENT SUB (if used instead of self-perform)
   ABC Drywall — Invoice 2026-1184       = $ 4,250

   MATERIAL
   5/8" Type X gyp, 32 sheets @ $14.80   = $   474
   Joint compound, tape, fasteners       = $   118
   Sales tax (7.5%)                      = $    44
   Material subtotal                     = $   636

   EQUIPMENT
   Boom lift — 2 days @ $410/day          = $   820
   Equipment subtotal                     = $   820

   THIRD-PARTY COSTS
   Disposal — 1 dump trailer load         = $   180
   A/E re-review fee (per A102 §4.2.x)   = $   320
   Re-inspection fee (AHJ)                = $   125
   Third-party subtotal                   = $   625

   DIRECT REMEDIATION COST                = $ 8,939

   GC OH&P on remediation
   (per Subcontract §12.4: 10% on direct
   remediation cost, capped at $X)        = $   894

   TOTAL BACKCHARGE                       = $ 9,833
   ```

   - Show source for every line (timesheet number, invoice number, equipment-rental ticket)
   - If OH&P or supervision markup is being applied, cite the clause that authorizes it; if the clause is silent, do not apply
   - Flag any line where the cost looks high vs. industry norms (e.g., labor hours that imply 4× the original install hours) — the GC may want to scrub before sending
   - Never round upward "just in case"; round to actuals

4. Run the **defensibility self-check** before output. For each item, the answer must be yes:
   - [ ] Was a written notice of deficient work issued before any remediation?
   - [ ] Did the sub have a documented opportunity to inspect and to cure?
   - [ ] Was the sub invited to be present during the corrective work?
   - [ ] Is every cost line backed by a timesheet, invoice, or quote (not a round number)?
   - [ ] Does the subcontract or PO contain a clause that authorizes deduction from payment?
   - [ ] Is the backcharge being issued contemporaneously with the cure (not silently accumulated)?
   - [ ] Is the defect properly classified (not a punch-list item, warranty item, or coercion of an unrelated change)?
   - [ ] Does the package preserve the sub's right to dispute within the contractual window?
   - For any "no", explicitly flag the gap in the output and recommend the next step (e.g., "No prior written notice — recommend issuing Notice of Deficient Work and resetting the cure window before proceeding")

5. Output and flag. The skill should produce four named documents, plus a short cover memo summarizing the chain and the defensibility-self-check result.

**Output requirements:**

Markdown package containing four documents in sequence:

```
# Backcharge Package — [Project] — [Sub] — [Defect Reference]

## Cover Memo
- Defect: [one-sentence description with location and quantity]
- Contract clause(s) cited: [§X.X — title]
- Cure window: [duration; whether contract-defined or industry-reasonable]
- Cure performed by: [in-house / replacement sub name]
- Total backcharge: $[amount]
- Defensibility self-check: [pass / flagged items]
- Documents in package: 1) Notice of Deficient Work; 2) Notice of Intent to Cure & Backcharge; 3) Backcharge Notice; 4) Deduction Authorization Letter (internal)

---

## Document 1 — Notice of Deficient Work
[Standard letter format; cites clause, defect, cure window, consequences]

---

## Document 2 — Notice of Intent to Cure & Backcharge
[Standard letter format; references Document 1, expired cure window, cure plan, invitation to observe]

---

## Document 3 — Backcharge Notice #[N]
[Header; references Documents 1–2; itemized cost worksheet; attachments list; deduction reference; reservation language]

---

## Document 4 — Deduction Authorization Letter (Internal)
[Internal-only routing; pay-app reference; AP instructions; lien-waiver coordination note; approval signatures]

---

_This package was prepared with AI assistance. Cost figures and contract-clause citations should be verified by the contract administrator before transmission. Sending of formal notices should follow the contract's prescribed delivery method. Where the dispute is material or the sub is likely to lien or sue, construction-counsel review is recommended before issuing Documents 1–3._
```

- Name the specific contract clause for every authority cited (clause number + title); never just "per the subcontract"
- Include the proof-of-delivery method on every external notice
- Severity color-code in the cover memo: 🔴 safety / hold-point fail, 🟡 coordination conflict / cosmetic-but-spec-fail, 🟢 housekeeping / cleanup
- Where the contract is silent on cure-window length, default to 48 hours for non-emergency conditions and document the basis
- Always include the standard reservation: the deduction is not a final liquidation of damages; either party may seek further remedies under the contract
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> GC: Northwood Builders. Project: Lakeside Office Tower TI, contract 2026-018. Sub: Premier Drywall, subcontract 026-PD (AIA A401 base). Defect: Premier installed 32 sheets of 5/8" Type X gyp on a 1-hour rated demising wall (Level 4, between Suites 401 and 403, grid B-7 to D-9, ~640 SF) over open joints in the rated assembly — fire-rated joint detail per drawing A6.04 / spec 09 21 16 §3.3.B was not followed, and the AHJ failed inspection on 2026-04-22. We discovered it the same day. Issued a verbal notice that afternoon and a written notice 2026-04-23 (email + Procore notification) requiring cure within 48 hours per Subcontract §12.4. Premier responded 2026-04-24 stating they could not return to site until 2026-04-29 due to other work; we needed it cured before MEP rough-in resumed Monday 2026-04-26. We retained replacement sub Apex Acoustical to cure on 2026-04-25 (Saturday). Premier was invited by email and Procore to attend; they did not. Apex completed on 2026-04-25; AHJ re-inspected and passed 2026-04-26. Apex invoice $4,250. Our supervision: foreman 6 hrs, no in-house labor needed. Disposal $180. AHJ re-inspection fee $125. A/E re-review billed through at $320. Subcontract §12.4 allows 10% OH&P on remediation. Reservation posture: also reserve rights to charge for any delay to MEP rough-in (none observed; MEP started Monday on schedule, so delay reservation only).

**Expected output:**

> # Backcharge Package — Lakeside Office Tower TI — Premier Drywall — Demising Wall Rated-Joint Failure
>
> ## Cover Memo
> - **Defect:** ~640 SF of 1-hour rated demising wall (Level 4, grid B-7 to D-9, between Suites 401 and 403) installed without fire-rated joint detail per A6.04 / spec 09 21 16 §3.3.B; AHJ failed inspection 2026-04-22
> - **Contract clauses cited:** Subcontract §3.2 (Conformance to Specifications), §12.4 (Default and Remediation), §17.6 (Right of Offset / Deduction from Payment), §12.4(c) (10% OH&P on Remediation)
> - **Cure window:** 48 hours from written notice 2026-04-23 (per §12.4); expired 2026-04-25 with sub's stated unavailability before 2026-04-29
> - **Cure performed by:** Apex Acoustical (replacement sub) on 2026-04-25 with Northwood foreman supervision
> - **Total backcharge:** $5,996
> - **Defensibility self-check:** PASS (all eight items met; written notice issued before remediation, cure window documented, sub invited to observe, costs traceable, contract authorizes deduction, contemporaneous, properly classified, sub's dispute right preserved)
> - **Severity:** 🔴 (life-safety / inspection fail blocking downstream trade)
> - **Documents in package:** 1) Notice of Deficient Work (2026-04-23); 2) Notice of Intent to Cure & Backcharge (2026-04-25 AM); 3) Backcharge Notice #BC-014 (2026-04-26); 4) Deduction Authorization Letter (internal, 2026-04-26)
>
> ---
>
> ## Document 1 — Notice of Deficient Work
>
> **To:** Premier Drywall — Project Manager (Mara Klein) and Field Superintendent (Ron T.)
> **From:** Northwood Builders — [PM name], Project Manager
> **Project:** Lakeside Office Tower TI
> **Subcontract:** 026-PD (AIA A401 base)
> **Date:** 2026-04-23
> **Delivery:** Email (read-receipt requested) + Procore notification + USPS Certified Mail (tracking number to follow)
> **Subject:** Notice of Deficient Work — Demising Wall Rated-Joint Detail — Level 4 Grid B-7 to D-9
>
> 1. **Defect.** On 2026-04-22, the AHJ failed inspection of the 1-hour rated demising wall between Suites 401 and 403 (Level 4, grid B-7 to D-9, approximately 640 SF). Inspection notes (attached) cite missing or improperly detailed fire-rated joint treatment per drawing A6.04 and Specification 09 21 16 §3.3.B. Photos PD-0421-08 through PD-0421-19 document the condition.
>
> 2. **Contract basis.** Subcontract §3.2 (Conformance to Specifications) requires all work to comply with the contract documents including referenced fire-rated assembly details. Subcontract §12.4 (Default and Remediation) authorizes Northwood to issue a notice of default and require cure within 48 hours.
>
> 3. **Required cure.** Premier shall complete the rated-joint detail per A6.04 / 09 21 16 §3.3.B for the entire 640 SF segment, schedule re-inspection with the AHJ, and confirm pass within **48 hours of receipt of this notice** (no later than 2026-04-25, 5:00 PM local).
>
> 4. **Consequence of non-cure.** If Premier fails to cure within the window or declines, Northwood will, per Subcontract §12.4 and §17.6, retain a replacement contractor or self-perform and backcharge all direct and indirect costs against the next pay application. MEP rough-in is scheduled to resume 2026-04-26 (Monday) and depends on this hold-point.
>
> 5. **Inspection / cure plan.** Premier is invited to inspect the condition with the GC superintendent any time before the cure window expires and to submit a written cure plan. Please respond by 2026-04-24, 5:00 PM.
>
> Sincerely,
> [PM name], Project Manager — Northwood Builders
> CC: Northwood Project Executive; Risk Manager; Apex Acoustical (informational)
>
> ---
>
> ## Document 2 — Notice of Intent to Cure & Backcharge
>
> **To:** Premier Drywall — PM and Field Superintendent
> **From:** Northwood Builders — [PM name]
> **Project:** Lakeside Office Tower TI
> **Subcontract:** 026-PD
> **Date:** 2026-04-25, 7:30 AM
> **Delivery:** Email (read-receipt) + Procore notification
> **Subject:** Notice of Intent to Cure and Backcharge — Demising Wall Rated-Joint — Reference Document 1 (2026-04-23)
>
> 1. **Status.** The 48-hour cure window opened by the Notice of Deficient Work dated 2026-04-23 ends today, 2026-04-25, 5:00 PM. Premier's email response of 2026-04-24 (PM Mara Klein) states that the soonest Premier can return to site is 2026-04-29 — four calendar days past the cure deadline. Per Subcontract §12.4(b), Premier's written declination to cure within the window constitutes a waiver of the cure right and triggers the GC's remedy clause. The downstream MEP rough-in is scheduled to resume 2026-04-26 and cannot proceed until the AHJ passes the rated assembly.
>
> 2. **Action.** Per Subcontract §12.4, Northwood is retaining Apex Acoustical to perform the cure beginning today, 2026-04-25, 9:00 AM. Northwood field supervision (foreman) will be on site throughout the cure. The AHJ has been requested for a Monday-morning re-inspection.
>
> 3. **Invitation to observe.** Premier is invited to attend, observe, and document the cure work. A representative may be present at any time during the work; please notify the Northwood superintendent on arrival. If Premier elects not to attend, photos and video of the cure will be made available with the eventual backcharge package.
>
> 4. **Cost basis (preliminary; final detail will follow in the Backcharge Notice).** Apex Acoustical replacement-contractor invoice; Northwood foreman supervision at burdened in-house rate; disposal; AHJ re-inspection fee; A/E re-review fee passed through; OH&P on direct remediation per Subcontract §12.4(c) at 10%.
>
> 5. **Reservation of rights.** Northwood reserves the right to backcharge any consequential costs that emerge — including but not limited to delay to MEP rough-in, lost productivity for downstream trades, owner-pass-through, and liquidated damages exposure — under the applicable subcontract clauses.
>
> Sincerely,
> [PM name], Project Manager — Northwood Builders
> CC: Project Executive; Risk Manager; Contract Admin
>
> ---
>
> ## Document 3 — Backcharge Notice #BC-014
>
> **To:** Premier Drywall — Accounts Receivable, PM, and Field Superintendent
> **From:** Northwood Builders — [PM name]
> **Project:** Lakeside Office Tower TI
> **Subcontract:** 026-PD
> **Date:** 2026-04-26
> **Delivery:** Email + Procore + USPS Certified Mail
> **Subject:** Backcharge Notice #BC-014 — Demising Wall Rated-Joint Cure — Pay App #07 Deduction
>
> 1. **References.** Notice of Deficient Work dated 2026-04-23 (Document 1); Notice of Intent to Cure and Backcharge dated 2026-04-25, 7:30 AM (Document 2). Cure performed 2026-04-25; AHJ re-inspected and passed 2026-04-26.
>
> 2. **Itemized costs.**
>
>    | Item | Source / Reference | Amount |
>    |---|---|---|
>    | Apex Acoustical — replacement-contractor invoice | Invoice 2026-1184 (attached) | $4,250 |
>    | Northwood foreman supervision — 6 hrs @ $96/hr (burdened, per config) | Timesheet TS-04-25 (attached) | $576 |
>    | Disposal — 1 dump trailer load | Disposal ticket DT-04-25 (attached) | $180 |
>    | AHJ re-inspection fee | AHJ receipt 04-26 (attached) | $125 |
>    | A/E re-review fee — passed through per A102 §4.2.x | A/E invoice 2026-A044 (attached) | $320 |
>    | **Direct remediation cost** | | **$5,451** |
>    | OH&P on direct remediation @ 10% per Subcontract §12.4(c) | | $545 |
>    | **Total backcharge** | | **$5,996** |
>
>    *Verify with Controller before transmission. Sales-tax handling on deductions follows company policy; this example shows tax-inclusive material costs.*
>
> 3. **Deduction.** Pursuant to Subcontract §17.6 (Right of Offset / Deduction from Payment), the total backcharge will be deducted from Pay Application #07 (period ending 2026-04-30). Premier's lien-waiver should reflect the gross billing less this deduction; lien rights as to the deducted amount are preserved by Premier per the reservation below.
>
> 4. **Reservation.** Northwood's deduction is not a final liquidation of damages; Northwood reserves the right to assert additional claims (delay, disruption, owner-pass-through) under the applicable subcontract clauses. Premier reserves the right to contest this deduction under Subcontract §17.6(d) by written objection within 10 calendar days of receipt; Premier's payment of, or non-objection to, this deduction is not an admission of liability and Premier reserves all rights and remedies under the subcontract and applicable law.
>
> 5. **Attachments.** (a) Document 1; (b) Document 2; (c) AHJ inspection-fail report 2026-04-22; (d) photos PD-0421-08 through PD-0421-19; (e) Apex Acoustical invoice 2026-1184; (f) Northwood timesheet TS-04-25; (g) disposal ticket DT-04-25; (h) AHJ re-inspection receipt 2026-04-26; (i) A/E re-review invoice 2026-A044.
>
> Sincerely,
> [PM name], Project Manager — Northwood Builders
> CC: Northwood Project Executive; Northwood Controller; Northwood Risk Manager; Premier Drywall (Accounts Receivable)
>
> ---
>
> ## Document 4 — Deduction Authorization Letter (Internal)
>
> **To:** Northwood Accounts Payable / Project Accounting
> **From:** [PM name], Project Manager — Lakeside Office Tower TI
> **Date:** 2026-04-26
> **Distribution:** AP, Project Executive, Controller, Risk Manager (internal only — not for transmission to sub)
> **Subject:** Authorize Deduction — Premier Drywall — Backcharge #BC-014 — Pay App #07
>
> 1. **Reference.** Backcharge Notice #BC-014 (Document 3 of the BC-014 package, dated 2026-04-26, transmitted to Premier same day).
> 2. **Project / Subcontract.** Lakeside Office Tower TI / Subcontract 026-PD / Premier Drywall.
> 3. **Pay app affected.** #07, period ending 2026-04-30.
> 4. **Deduction amount.** $5,996 (gross of sales tax; confirm with Controller per company policy).
> 5. **Lien-waiver coordination.** Premier's progress lien-waiver for Pay App #07 should reflect the gross billing less this deduction. Premier's lien rights as to the deducted $5,996 are preserved per the reservation in Document 3 — coordinate the lien-waiver form language with Risk Manager and reference the state's required waiver form (see knowledge-base/regulations/lien-waivers-by-state.md) before processing.
> 6. **Approvals.** Per company policy, backcharges over $5,000 require PM + Project Executive + Risk Manager signoff. Backcharges over $25,000 also require Controller signoff.
>    - PM: ___________________ Date: _______
>    - Project Executive: ___________________ Date: _______
>    - Risk Manager: ___________________ Date: _______
> 7. **Distribution.** AP applies the deduction; Project Accounting books to job-cost code [code]; Risk Manager logs to the project's backcharge register; Contract Admin updates the dispute-reservation tracker.
>
> ---
>
> _This package was prepared with AI assistance. Cost figures and contract-clause citations should be verified by the contract administrator before transmission. Where the dispute is material or the sub is likely to lien or sue, construction-counsel review is recommended before issuing Documents 1–3._
