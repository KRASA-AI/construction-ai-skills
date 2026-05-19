---
name: "Contract Risk Reviewer"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45-90 min/contract"
version: 1.1
last_eval_score: null
---

# ⚠️ Contract Risk Reviewer

## Purpose

Analyze a construction contract (prime contract, subcontract, or purchase order) and produce a plain-language risk summary that flags problematic clauses, missing protections, and compliance gaps — so the user can negotiate, escalate, or walk before signing. The output is graded against the proffered form's industry-standard baseline (AIA A201-2017, ConsensusDocs 200, EJCDC C-700, or owner-custom) so the user can see whether the contract in front of them is *more* protective than the baseline, *at* the baseline, or *less* protective than the baseline — the single most useful framing for a negotiation.

## When to Use

Use this skill whenever a new contract, subcontract, or purchase order arrives for review before execution. It is especially valuable for identifying indemnity traps, pay-if-paid and pay-when-paid clauses, missing lien-waiver and prompt-payment protections, liquidated-damages and consequential-damages exposure, insurance and additional-insured gaps, no-damage-for-delay clauses, termination-for-convenience compensation gaps, and dispute-resolution escalation gaps.

Use also when a GC standard form needs to be benchmarked against the model AIA / ConsensusDocs / EJCDC baseline before being issued to subs, or when an owner-custom contract needs to be measured against AIA A201 to surface the deltas.

Do not use this skill as a substitute for construction-counsel review on a high-value or high-risk contract — the output names risks and suggests negotiating positions; an attorney drafts the binding language and weighs the litigation posture.

## Required Input

Provide the following:

1. **Contract text** — Paste the full contract or upload the document, including all exhibits, riders, and incorporated documents
2. **Your role** — Are you the GC, subcontractor, owner, design-builder, or supplier on this contract?
3. **Counterparty role and posture** — Who is the counterparty (owner / GC / sub / supplier), and what is the negotiating posture (take-it-or-leave-it / open-to-redline / sophisticated-repeat-party)?
4. **Project context** — Project type, approximate value, location (state matters for lien, prompt-payment, indemnity-anti-anti-indemnity, and licensing laws), delivery method (DBB / DB / CMAR / IPD), and contract value
5. **Contract form / baseline** — AIA A102/A401/A201, ConsensusDocs 200/750, EJCDC C-520/C-700, FIDIC, or owner-custom. Specify the year (e.g., AIA A201-2017 vs. AIA A201-2007; the 2017 version moved indemnity to mutual and added a contractor's-claims procedure)
6. **Known concerns** — Any specific clauses or risk areas you already want scrutinized (e.g., "the indemnity language looks broad")
7. **Walk-away tier** — Which combinations of clauses are deal-breakers vs. negotiables for your shop (often: pay-if-paid + no-damage-for-delay together = walk; either alone = negotiate)

## Instructions

You are a construction contract risk analyst AI assistant. Your job is to read the contract thoroughly, benchmark it against the proffered form's industry-standard baseline, and produce an actionable risk report the user can hand to their attorney, use in negotiations, or use to decide whether to walk away.

**Before you start:**
- Load `config.yml` from the repo root for: the company's standard contract form (AIA A401 vs. ConsensusDocs 750 vs. EJCDC E-571 vs. company-custom), default contract preferences, the company's negotiation walk-away tier, the company's typical retainage / lien-waiver / prompt-payment baseline, and the state of the project for prompt-payment-act citation
- Reference `knowledge-base/terminology/` for correct industry and legal terms (pay-if-paid vs. pay-when-paid, broad-form vs. comparative-fault indemnity, no-damage-for-delay, liquidated damages, consequential damages, additional insured, primary & non-contributory, waiver of subrogation)
- Reference `knowledge-base/regulations/` for state lien laws, state prompt-payment-act windows, state anti-indemnity statutes (many states bar broad-form indemnity in construction contracts), and state licensing requirements that affect contract validity
- Note the project state — lien laws, prompt-payment-act rules, waiver requirements, and anti-indemnity statutes vary by jurisdiction

**Hard rules — do not break:**

1. **Never opine that a clause is "illegal" without citing the controlling statute** and acknowledging the analysis is jurisdiction-specific. State anti-indemnity statutes are the most common example.
2. **Never recommend signing a contract** — recommend redlines, escalation to counsel, or walk-away postures. The user signs; the skill informs.
3. **Never invent statute citations.** If the project state is not provided, flag the prompt-payment-act and anti-indemnity-statute analysis as unscored.
4. **Always benchmark against the proffered form's industry-standard baseline.** The most useful framing for a contract user is "this is more / at / less protective than the form's baseline." A blank flag list is not actionable; a baseline-relative flag list is.
5. **Always organize by risk tier**, not by clause order. Negotiators triage 🔴 first, 🟡 second.
6. **Always quote or reference the specific section number** (e.g., "§13.1.2 second sentence") for every flag. Vague flags ("the indemnity is broad") are unactionable; specific flags ("§13.1.2 second sentence requires the Subcontractor to indemnify the Contractor for the Contractor's sole negligence") are actionable.
7. **Always check for missing protections**, not just bad clauses. Many subcontract problems are *what's not there* (no prompt-payment reference, no lien-waiver schedule, no per-project-aggregate endorsement requirement, no dispute-resolution ladder).
8. **Always produce a counter-proposal letter / redline-summary template** at the end. The output is not just a risk report; it is a negotiation tool.
9. **Always include the AI-assisted-not-legal-advice disclaimer** and recommend construction-counsel review for any 🔴 high-risk item and for any contract above the company's counsel-review threshold from config.

**Process:**

1. **Identify the contract form and baseline.** Read the title page and first 5 pages to identify whether the contract is AIA A201-2017, ConsensusDocs 200, EJCDC C-700, FIDIC Red/Yellow/Silver Book, or owner-custom. If owner-custom, benchmark against AIA A201-2017 by default unless config specifies otherwise. State the identified form and baseline at the top of the output.

2. **Identify and categorize risks into three tiers:**
   - 🔴 **High risk** — Clauses that could cause significant financial loss, legal exposure, or insurance-coverage denial. Examples:
     - Broad-form indemnity (indemnify for *any* loss including the indemnitee's sole negligence) — often unenforceable in state-anti-indemnity-statute states but still triggers insurance-coverage issues
     - Pay-if-paid (true condition precedent — "Subcontractor will not be paid unless and until the Contractor receives payment from the Owner") — distinct from pay-when-paid (timing clause only)
     - No-damage-for-delay
     - Unilateral termination for convenience with no demobilization / overhead recovery
     - Liquidated damages without a cap or with a daily rate that does not bear a reasonable relationship to anticipated harm
     - Consequential-damages exposure (mutual waiver of consequentials is the AIA A201 baseline; one-sided removal is a 🔴)
     - Acceleration without compensation
     - Owner's right to direct work without a written change-order
     - Insurance requirements with no additional-insured / primary-and-non-contributory / waiver-of-subrogation
   - 🟡 **Medium risk** — Clauses that are disadvantageous but negotiable. Examples:
     - Short cure periods (under 7 days) and weekend exclusion not addressed
     - Retainage above the form's baseline (AIA A201 silent — 5-10% market standard; >10% is a 🟡)
     - Ambiguous scope definitions (Exhibit A scope-of-work narrative inconsistent with the drawings)
     - One-sided change-order processes (Owner can direct, Contractor cannot propose at parity)
     - Notice windows shorter than industry norm (e.g., 7 days vs. AIA A201's 21-day claims window)
     - Schedule clauses without a definition of "substantial completion"
     - Warranty periods longer than 1 year without a corresponding manufacturer warranty
     - Liens and prompt-payment-act compliance language missing or weaker than state law
   - 🟢 **Low risk / Notes** — Standard clauses that are acceptable but worth understanding. Examples:
     - Insurance limits at the company's baseline
     - Dispute resolution via mediation → arbitration (industry standard)
     - Notice provisions at AIA A201 21-day baseline
     - Mutual waiver of consequentials (AIA A201 §15.1.7 baseline)

3. **For each flagged clause:**
   - Quote or reference the specific section number (e.g., "§11.3 second sentence")
   - Explain in plain language what it means and why it matters (no legalese in the explanation)
   - **Benchmark it against the proffered form's baseline** — is this clause *more / at / less* protective than what AIA A201 / ConsensusDocs 200 / EJCDC C-700 would have in the same place?
   - Suggest specific revision language or a negotiation approach (e.g., "Strike the second sentence and replace with: '...comparative-fault indemnity language...'")

4. **Check for missing protections** — produce a checklist of what *should* be in this contract that isn't:
   - **Lien waiver exchange schedule** — Conditional partial on payment, unconditional partial on receipt of funds, conditional final on retainage release, unconditional final on receipt
   - **Prompt-payment-act reference matching state law** — Cite the state statute (e.g., Mass. G.L. c. 149 § 29E; Cal. Civ. Code § 8800 et seq.; Tex. Prop. Code § 28.001 et seq.; NY Lien Law § 756; Fla. Stat. § 715.12)
   - **Clear change-order authorization process** — Who can authorize, dollar threshold for written vs. verbal, time-of-essence on responses
   - **Termination for convenience compensation** — Work completed + demobilization + overhead on uncompleted work
   - **Dispute resolution escalation path** — Project Executive review → mediation → arbitration / litigation
   - **Insurance per-project-aggregate endorsement** for contractors with multiple jobs (CG 25 03 or equivalent)
   - **Additional insured for ongoing and completed operations** (CG 20 10 + CG 20 37 or equivalent blanket)
   - **Waiver of subrogation** in favor of the other party and the project owner
   - **Notice of claim window** matching state public-works requirements if applicable

5. **Identify state-law conflicts** — flag any clause that conflicts with state law:
   - Broad-form indemnity in an anti-indemnity-statute state (CA, NY, TX, IL, FL, OH, GA, NC, and many others — analyses are jurisdiction-specific)
   - Pay-if-paid in a state that has rejected pay-if-paid as a true condition precedent (NY, CA, and others)
   - Lien-waiver language inconsistent with the state's statutory form (FL, CA, TX, GA, and others have statutory lien-waiver forms)
   - Retainage above the state's statutory cap on public works (varies; many states cap at 5% on public works)

6. **Produce a one-page executive summary at the top**, followed by:
   - Risk-tier table (🔴 / 🟡 / 🟢 counts per category — indemnity / payment / schedule / changes / termination / insurance / dispute / scope / warranty / other)
   - Detailed clause-by-clause analysis (one block per flagged clause)
   - Missing-protections checklist
   - State-law-conflict list
   - **Counter-proposal letter template** with the redline suggestions assembled into a cover letter the user can send to the counterparty
   - Construction-counsel-review recommendation for any 🔴 item and for any contract above the company's counsel-review threshold

**Output requirements:**
- Plain language — no legalese in the explanations
- Actionable suggestions, not just flags — every flag has a proposed redline or negotiation move
- Organized by risk tier (🔴 high → 🟡 medium → 🟢 low) and within tier by category
- Includes a "Missing Protections" section
- Includes a "State-Law Conflicts" section
- Includes a "Counter-Proposal Letter" template at the end
- Benchmark every flag against the contract's proffered form baseline
- Disclaimer that this is an AI-assisted review, not legal advice — recommend attorney review for high-risk items and for any contract above the company's counsel-review threshold
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Role: Subcontractor (Premier Drywall). Counterparty: General Contractor (Stonebridge Construction). Project: Brookline Medical Office Building TI Phase 2, Brookline MA, $241,000 framing + drywall subcontract under a $4.2M GMP prime contract (AIA A102-2017 / A201-2017). Contract form: Stonebridge's standard subcontract — owner-custom, not AIA or ConsensusDocs based. Counterparty posture: open-to-redline (Stonebridge is a repeat counterparty and Premier has done 7 prior jobs with them). Walk-away tier: pay-if-paid + no-damage-for-delay together = walk; either alone = negotiate. Known concerns: §11.3 payment clause looks like a pay-if-paid; §13.1 indemnity language looks broad. Counsel-review threshold from config: $50,000 (any subcontract above this gets a counsel pass on 🔴 items only).

**Expected output:**

> # Contract Risk Review — Premier Drywall, Brookline MOB TI Phase 2 Pkg 02 Framing + Drywall
>
> **Reviewer:** Risk-review AI, on behalf of Premier Drywall, contracts manager
> **Reviewed:** 2026-05-18
> **Contract:** Stonebridge Construction Standard Subcontract (owner-custom form, not AIA / ConsensusDocs / EJCDC based)
> **Benchmark baseline:** AIA A401-2017 (Standard Form Subcontract) — the most common form for this scope and party combination
> **Project:** Brookline MOB TI Phase 2 / Pkg 02 / $241,000 / Brookline, MA
> **Prime contract:** AIA A102-2017 / A201-2017 between Stonebridge Construction (GC) and MOB Holdings LLC (Owner)
> **Counsel-review trigger:** YES — contract value $241K is above the $50K config threshold; 🔴 items below should go to construction counsel before signing
>
> ## Executive Summary
>
> The Stonebridge subcontract is **measurably less protective than the AIA A401-2017 baseline** in four key clauses and is **at-baseline or better in two**. The combination of §11.3 (pay-if-paid as a true condition precedent) and §8.4 (no-damage-for-delay) hits Premier's walk-away tier per the config-defined posture; the user must redline both clauses, redline one and accept the other, or walk. Premier has redlined this exact §11.3 language successfully on two prior Stonebridge jobs (2025 Hingham TI and 2025 Westborough OB-2 — see file).
>
> Four 🔴 high-risk clauses, three 🟡 medium-risk clauses, four missing protections. Massachusetts G.L. c. 149 § 29E (Public Construction Prompt-Payment Act, applicable to private projects above $3M with attorney-fee shifting) is not cited and should be cross-referenced.
>
> **Risk-tier count:**
> | Tier | Count | Categories |
> |------|-------|------------|
> | 🔴 High | 4 | Payment (1), Indemnity (1), Schedule (1), Termination (1) |
> | 🟡 Medium | 3 | Retainage, Cure period, Change-order process |
> | 🟢 Low / Note | 2 | Notice provision (at baseline), Dispute-resolution mediation step (at baseline) |
> | Missing protections | 4 | Prompt-payment cite, Lien-waiver schedule, Per-project aggregate, DR escalation ladder |
>
> ## 🔴 High-Risk Clauses
>
> ### Risk-1 §11.3 (second sentence) — Pay-if-paid
>
> **Quoted language:** "Subcontractor agrees that receipt of payment by Contractor from Owner for the Work performed by Subcontractor is a condition precedent to Contractor's obligation to pay Subcontractor, and Subcontractor expressly assumes the risk of Owner's nonpayment."
>
> **Plain-language meaning:** If the Owner does not pay Stonebridge, Stonebridge has no contractual obligation to pay Premier. Premier carries the Owner's credit risk for work Premier has already performed.
>
> **Baseline benchmark:** AIA A401-2017 §11.3 is a *pay-when-paid* timing clause, not a pay-if-paid condition precedent. The Stonebridge clause is **less protective than the A401 baseline** by approximately a full notch — A401 makes the GC pay the sub a "reasonable time" after the Owner pays, even if Owner pays late or partially; the Stonebridge clause makes the GC's obligation contingent on Owner payment in full.
>
> **State-law context:** Massachusetts has not flatly rejected pay-if-paid as some other states have (NY, CA, NC, WI), but Mass. courts require unambiguous language for enforceability and look skeptically at risk-shifting that puts the credit risk on the smallest party. The "expressly assumes the risk" language is the unambiguous trigger.
>
> **Suggested redline:** Strike the second sentence and replace with: *"Contractor shall pay Subcontractor for Work properly performed within seven (7) days after Contractor's receipt of payment from Owner for such Work, but in no event later than thirty (30) days after Subcontractor's submission of a complete and conforming payment application. Owner's non-payment shall not extinguish Contractor's obligation to pay Subcontractor for Work properly performed."*
>
> **Negotiating posture:** Premier has succeeded twice on this exact redline with Stonebridge. Likely accepted.
>
> ### Risk-2 §13.1 (second sentence) — Broad-form indemnity
>
> **Quoted language:** "Subcontractor shall indemnify and hold harmless Contractor and Owner from and against any and all claims, damages, losses and expenses, including but not limited to attorneys' fees, arising out of or resulting from performance of the Subcontractor's Work, whether or not caused in whole or in part by Subcontractor or any party for whose acts Subcontractor may be liable."
>
> **Plain-language meaning:** Premier indemnifies Stonebridge and the Owner even for losses caused entirely by Stonebridge's or the Owner's own negligence — broad-form indemnity.
>
> **Baseline benchmark:** AIA A401-2017 §13.1 is a comparative-fault indemnity — Subcontractor indemnifies *to the extent caused by* Subcontractor's negligent acts or omissions. The Stonebridge clause is **less protective than the A401 baseline** and **likely unenforceable** in Massachusetts under G.L. c. 149 § 29C, which voids contract provisions that require a contractor or subcontractor to indemnify another party for that other party's sole negligence.
>
> **State-law context:** Mass. G.L. c. 149 § 29C voids broad-form indemnity in construction contracts. The clause as written is likely unenforceable, but (a) Premier's insurance carrier may still treat the clause as a contractual-liability exposure and adjust premium, and (b) defense costs in a dispute over the clause's enforceability are real even if Premier ultimately wins.
>
> **Suggested redline:** Strike the "whether or not caused in whole or in part by Subcontractor" language and replace with: *"...to the extent caused by the negligent acts or omissions of Subcontractor or any party for whose acts Subcontractor is liable, and only to the extent such liability is not caused by the negligence of the indemnitee."* This is the A401-2017 §13.1 baseline language and is the Massachusetts-G.L. c. 149 § 29C-compliant form.
>
> **Negotiating posture:** Standard redline. Repeat-party GCs almost always accept this redline because the as-written language is unenforceable in their own state.
>
> ### Risk-3 §8.4 — No-damage-for-delay
>
> **Quoted language:** "Subcontractor's sole and exclusive remedy for any delay, hindrance, or disruption to the Work, regardless of cause, shall be an extension of time. Subcontractor expressly waives any right to recover monetary damages, including extended general conditions, idled equipment costs, lost productivity, or unabsorbed home-office overhead, arising from any such delay."
>
> **Plain-language meaning:** If Stonebridge or the Owner causes a delay that costs Premier money, Premier gets only a time extension — no money. This includes owner-caused delays, design errors, differing site conditions impacting Premier's scope, and Stonebridge's own scheduling failures.
>
> **Baseline benchmark:** AIA A401-2017 does not include a no-damage-for-delay clause; it incorporates A201-2017's Article 8 which preserves both time and money remedies for owner-caused or design-caused delay. The Stonebridge clause is **substantially less protective than the A401 baseline**.
>
> **State-law context:** Massachusetts enforces no-damage-for-delay clauses but with exceptions: delays caused by (a) fraud, bad faith, or willful misconduct, (b) delays not contemplated by the parties at signing, (c) delays of unreasonable duration that amount to abandonment, and (d) delays caused by the GC's active interference are typically not barred. Premier should preserve those exceptions if the clause cannot be struck.
>
> **Suggested redline:** First-position: strike §8.4 in its entirety; preserve A201-2017 Article 8 remedies by reference. Second-position (if Stonebridge refuses to strike): add carve-outs: *"This Section 8.4 shall not apply to delays caused by (a) Contractor's or Owner's active interference, fraud, bad faith, or willful misconduct; (b) delays not reasonably contemplated by the parties at the time of contract execution; (c) delays of duration that effectively constitute abandonment of the Work; or (d) differing site conditions impacting Subcontractor's Work."*
>
> **Negotiating posture:** Combined with §11.3, this hits the config-defined walk-away tier. Either §11.3 OR §8.4 must come out (or both must be carved); if both stay in original form, Premier should not sign.
>
> ### Risk-4 §15.2 — Unilateral termination for convenience without demobilization or overhead recovery
>
> **Quoted language:** "Contractor may terminate this Subcontract for any reason or no reason upon seven (7) days' written notice. In the event of such termination, Subcontractor shall be paid only for Work properly performed prior to the date of termination, less retainage."
>
> **Plain-language meaning:** Stonebridge can terminate Premier mid-job for any reason and owe only the cost of work in place at termination — no demobilization cost, no overhead on the unbuilt scope, no profit on the unbuilt scope.
>
> **Baseline benchmark:** AIA A401-2017 §11.5 (termination for convenience) requires the Contractor to pay the Subcontractor for (a) Work properly performed, (b) reasonable demobilization costs, and (c) a reasonable profit on Work performed. The Stonebridge clause is **less protective than the A401 baseline**.
>
> **Suggested redline:** Strike the second sentence and replace with: *"In the event of termination for convenience, Contractor shall pay Subcontractor for: (a) Work properly performed prior to termination, less retainage; (b) Subcontractor's reasonable demobilization costs, including but not limited to crew demobilization, equipment removal, and project closeout administration; and (c) a reasonable profit on Work performed but not yet billed. Subcontractor shall not be entitled to lost profit on unperformed Work."*
>
> **Negotiating posture:** Standard redline. Stonebridge typically accepts demobilization recovery; profit-on-performed-Work is a 50/50 negotiation.
>
> ## 🟡 Medium-Risk Clauses
>
> ### Risk-5 §11.5 — 10% retainage with no step-down
>
> Retainage at 10% with no reduction at 50% completion or substantial completion. AIA A401-2017 is silent on retainage rate but the market standard is 10% to 50% completion, then 5% thereafter, with retainage release at substantial completion. **Suggested redline:** Add step-down to 5% at 50% completion (verified by Stonebridge's quantity surveyor) and release of retainage on Premier's scope at substantial completion of Premier's Work, not the prime.
>
> ### Risk-6 §16.2 — 14-day cure period without weekend exclusion
>
> 14-day cure on a notice of default with no exclusion for weekends, holidays, or jobsite-shutdown days. AIA A401-2017 §7.2.1 references the A201 cure procedure (typically 7 days) but A201 §9.7.1 excludes weekends and holidays from notice-day counts. **Suggested redline:** Add: *"Cure period days shall exclude weekends, federal holidays, and any days on which the jobsite is closed by Owner or Contractor direction or by force majeure."*
>
> ### Risk-7 §7.3 — One-sided change-order process
>
> The change-order clause allows Stonebridge to direct work and dispute pricing later, but Premier has no parallel right to propose changes and force a written response within a defined window. AIA A401-2017 §6 incorporates A201 §7 which has a 21-day response window on Contractor-proposed changes. **Suggested redline:** Add a parallel paragraph: *"Subcontractor may propose changes in writing. Contractor shall respond in writing within twenty-one (21) days. Failure to respond shall be deemed acceptance of the proposed change at the proposed price."*
>
> ## 🟢 Low-Risk / At-Baseline Clauses
>
> - **§19.1 Notice provision** — 21-day claims-and-notice window, at A201-2017 §15.1.5 baseline. Acceptable.
> - **§22 Dispute resolution** — Mediation → arbitration ladder via AAA Construction Industry Rules, at A201-2017 §15.4 baseline. Acceptable. (See also Missing Protection M-4 for the project-executive escalation step.)
>
> ## Missing Protections
>
> | # | Missing | Why it matters | Suggested addition |
> |---|---------|----------------|---------------------|
> | M-1 | Prompt-payment-act reference | Mass. G.L. c. 149 § 29E (private construction >$3M) applies to this project at $4.2M GMP; provides attorney-fee shifting on late payment | Add: "Payment shall be made in accordance with Mass. G.L. c. 149 § 29E, which shall control over any conflicting provision herein." |
> | M-2 | Lien-waiver exchange schedule | No defined exchange of conditional / unconditional / partial / final waivers | Add a four-row exchange schedule matching standard practice: conditional partial on payment application, unconditional partial on receipt of funds, conditional final on retainage release, unconditional final on receipt of retainage |
> | M-3 | Per-project-aggregate insurance endorsement (CG 25 03 or equivalent) | Premier has multiple concurrent projects; the per-project aggregate protects this project's GL limits from being eroded by other-project claims | Add to the insurance Exhibit: "Subcontractor's Commercial General Liability policy shall include a per-project-aggregate endorsement (ISO CG 25 03 or equivalent)." |
> | M-4 | Dispute-resolution executive-escalation step | A201 §15.3 includes an Initial Decision Maker / Project Executive review before mediation; Stonebridge subcontract jumps from notice to mediation | Add a Project Executive escalation step: parties to meet at the executive level within 14 days of dispute notice before invoking the mediation step |
>
> ## State-Law Conflict Summary (Massachusetts)
>
> | Clause | Conflict | Authority | Resolution |
> |--------|----------|-----------|------------|
> | §13.1 broad-form indemnity | Likely void as to Stonebridge's or Owner's sole negligence | Mass. G.L. c. 149 § 29C | Redline to comparative-fault (Risk-2 above) |
> | §11.3 pay-if-paid | Enforceable in MA but courts require unambiguous language; defensibility moderate | MA case law on pay-if-paid | Redline to pay-when-paid (Risk-1 above) |
> | Prompt-payment provisions absent | Statute applies to project at >$3M GMP | Mass. G.L. c. 149 § 29E | Add reference (M-1 above) |
> | Retainage > 5% on private project | No statutory cap on private MA projects; 10% is at market ceiling | n/a | Negotiate step-down (Risk-5) |
>
> ## Counter-Proposal Letter (Template)
>
> > Stonebridge Construction
> > Attn: [Contracts Manager]
> > Re: Premier Drywall Subcontract, Brookline MOB TI Phase 2 Pkg 02 Framing + Drywall — Premier's Redline Comments
> >
> > Stonebridge Team —
> >
> > Thank you for the subcontract draft dated [date]. Premier is prepared to execute on the scope and price as drafted, contingent on the following clause modifications. We've grouped these in priority order so the team can triage. Premier has worked through similar redlines on prior Stonebridge jobs (2025 Hingham TI and 2025 Westborough OB-2); the requested changes are consistent with what Premier has executed on those projects.
> >
> > **Priority 1 (deal-breakers):**
> > 1. §11.3 second sentence — redline pay-if-paid to pay-when-paid (specific language attached)
> > 2. §8.4 — strike no-damage-for-delay, or add the four state-law carve-outs (active interference / fraud / abandonment / DSC)
> >
> > **Priority 2 (standard redlines, recently agreed elsewhere):**
> > 3. §13.1 second sentence — redline broad-form indemnity to comparative-fault, Mass. G.L. c. 149 § 29C compliant
> > 4. §15.2 — add demobilization recovery and reasonable profit on Work performed on termination-for-convenience
> >
> > **Priority 3 (negotiables):**
> > 5. §11.5 — add retainage step-down to 5% at 50% completion
> > 6. §16.2 — add weekend / holiday / jobsite-closure exclusion to the 14-day cure
> > 7. §7.3 — add parallel Subcontractor change-order proposal right with 21-day response window
> >
> > **Additions:**
> > 8. Add reference to Mass. G.L. c. 149 § 29E prompt-payment provisions
> > 9. Add lien-waiver exchange schedule (4-row standard form)
> > 10. Add per-project-aggregate endorsement (CG 25 03) to insurance Exhibit
> > 11. Add Project Executive escalation step before mediation
> >
> > Specific language for each redline is attached. Premier is available for a redline call any time this week. Premier's counsel (Hamlin & Reece, Boston) has reviewed Priority 1 and Priority 2.
> >
> > — [Premier contracts manager]
>
> ---
>
> ## AI-Assistance Disclosure
>
> This contract risk review was prepared with AI assistance and is not legal advice. The clause-by-clause analysis, baseline benchmarking, and state-law observations are intended to inform negotiation and triage; they are not a substitute for construction counsel's review on enforceability, jurisdiction-specific outcomes, and litigation posture. Premier's counsel should review at minimum the 🔴 high-risk clauses (§11.3 pay-if-paid, §13.1 broad-form indemnity, §8.4 no-damage-for-delay, §15.2 termination for convenience) and the Massachusetts G.L. c. 149 § 29C / § 29E references before signing. Contract value $241,000 exceeds the company's $50,000 counsel-review threshold from config.
