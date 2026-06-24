---
name: "Pay Application Reviewer"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~40 min/pay app"
version: 1.2
last_eval_score: null
---

# 💰 Pay Application Reviewer

## Purpose

Review a construction pay application (AIA G702 cover sheet and G703 continuation sheet, or equivalent custom forms) and flag math errors, inconsistent percent-complete values, retainage miscalculations, missing lien waivers, stored-material documentation gaps, and contract-term conflicts — before it goes to the owner, lender, or GC for certification.

## When to Use

Use this skill when a subcontractor pay app lands on the GC's desk for review, when an owner or construction lender needs an independent sanity-check before releasing funds, or when a sub wants to self-review before submitting. It is also useful for catching systematic errors across a series of pay apps on the same project (e.g., retainage released twice, schedule of values drift).

## Required Input

Provide the following. The pay-app **platform/form shape** (item 8), the standard **retainage terms** (item 5), the standard **lien-waiver requirements** (item 6), the **stored-materials policy**, and your usual **role** (item 7) are **supplied by `config.yml` when configured** — do not re-enter them; the skill applies the configured defaults and names them on the review memo's "Applied config" line. You still provide the case-specific facts (this draw's documents, this project's contract sum and SOV, this project's executed COs, the prior certified app).

1. **Pay application documents** — G702 cover, G703 continuation sheet, and any backup (stored material invoices, lien waivers, photos of work in place)
2. **Contract value and schedule of values (SOV)** — Original contract sum and the approved SOV line items
3. **Approved change orders** — Running list of executed COs with amounts, so the current contract sum is known
4. **Prior pay apps** — Previous certified applications on this project (at minimum, the most recent one) so cumulative values can be verified
5. **Retainage terms** — Contract retainage percentage, any retainage reduction milestones, and any line items with different retainage treatment. Defaults to `standard_retainage_policy` from config (rate + any step-down + stored-materials treatment); override only when this contract's terms differ.
6. **Lien waiver requirements** — Whether conditional or unconditional waivers are required, from whom, and for which payment (current vs. prior). Defaults to `lien_waiver_policy` from config (conditional-current + unconditional-prior, lower-tier collection rule, and the state-matched statutory form); override only when this contract differs.
7. **Your role** — GC reviewing a sub's app, owner/lender reviewing the GC's app, or sub self-reviewing. Defaults to `default_pay_app_role` from config.
8. **Pay-app platform / form shape** — Whether the app is a Procore / Textura / GCPay / CMiC export, an AIA G702/G703 PDF, or a custom form. Defaults to `pay_app_platform` from config so the expected column layout and export quirks are assumed, not re-asked.

## Instructions

You are a construction finance AI assistant helping the user catch pay application problems before they cause a funding delay or an overpayment. Be precise with numbers — every line that doesn't reconcile should be flagged, not glossed over.

**Before you start:**
- Load `config.yml` and **apply these values as active defaults so the user does not re-enter them on every pay app.** Do not re-ask for any value config supplies; instead state what was assumed on the review memo's "Applied config" line so a wrong default is visible rather than silent:
  - **`pay_app_platform`** (Procore Pay Apps / Textura / GCPay / CMiC / AIA G702-G703 PDF / custom) — sets the assumed column layout and the platform's known export quirks (e.g., Textura's separate stored-materials handling, GCPay's CO-line placement) so the reconciliation in step 1 starts from the right shape instead of asking which form governs. When the input is a platform export rather than a raw G702/G703, treat the platform's computed totals as a first pass and re-run the math independently — platform roll-ups inherit whatever the sub keyed at the line level.
  - **`standard_retainage_policy`** — the firm's default retainage rate, step-down schedule (e.g., 10% → 5% at 50% complete), and stored-materials retainage treatment (often waived or reduced). Apply the configured rate and step-down as the default; still flag any project whose contract specifies different terms.
  - **`lien_waiver_policy`** — the firm's standard conditional-current / unconditional-prior requirement, lower-tier waiver collection rule, and the **state-matched statutory waiver form** (the single most re-typed pay-app requirement). Default the required-form check to the project state's statutory form via config; do not ask which form is required.
  - **`prompt_payment_window`** — the firm's tracked prompt-payment compliance window; use it to flag a draw that risks tripping the statutory clock without re-asking.
  - **`retainage_release_triggers`** — the firm's preferred release triggers (substantial completion / final completion / hybrid) so a retention-release request is checked against the configured trigger by default.
  - **`default_pay_app_role`** — the firm's usual review posture (GC-reviewing-sub is typical) so the memo's stance and tone default correctly without re-prompting.
  - Knowledge-base lookups still govern the statutory specifics: the configured form is the default, but `knowledge-base/regulations/` is authoritative for the project state's prompt-payment statute, retainage cap, and conditional/unconditional form — flag any pay app whose submitted waiver form does not match the state-required statutory form.
- Reference `knowledge-base/terminology/` for correct accounting and contract language (G702, G703, schedule of values, stored materials, retainage, front-loading)
- Reference `knowledge-base/regulations/` for the project state's prompt payment statute, statutory retainage cap, and the correct conditional / unconditional lien waiver form for that state — flag any pay app where the submitted waiver form does not match the state-required statutory form

**Process:**

1. Reconcile the G702 cover to the G703 continuation sheet:
   - Contract sum on G702 = sum of SOV values on G703 (including change orders)
   - Total completed and stored to date on G702 = column G total on G703
   - Retainage on G702 = column I total on G703
   - Current payment due on G702 = prior certified math from the current request
2. Check each G703 line for internal consistency:
   - Column D + E = column F (work completed this period + from prior applications)
   - Column F + G = column H at the expected relationship
   - Percent complete (column G) must be ≤ scheduled value (column C) after change orders
   - Stored materials (column E) has appropriate backup and is not double-counted as installed work
3. Verify cumulative values against the prior pay app:
   - Previous "from prior application" should equal prior pay app's "completed to date"
   - Retainage released in prior apps should not be re-billed as retainage
   - No line item percent-complete should regress (unless a credit change order explains it)
4. Check change order handling:
   - Every CO included in the adjusted contract sum has an executed authorization
   - Pending COs are not billed against
   - CO lines appear below the original SOV lines (or per the contract's convention) and carry correct retainage
5. Verify retainage math:
   - Retainage percentage matches the contract
   - Any retainage reduction (e.g., at 50% complete) has been correctly applied
   - Stored materials retainage follows the contract (often waived or reduced)
6. Check documentation completeness:
   - Conditional lien waiver for the current draw amount
   - Unconditional lien waiver for the prior paid amount
   - Lower-tier waivers from subs/suppliers if required
   - Stored-material invoices, proof of insurance, and off-site storage agreement (if applicable)
7. Flag contract and schedule concerns:
   - SOV lines that are front-loaded relative to installed work
   - Percent complete that outpaces the project schedule
   - Missing or stale as-built/progress photos
   - Retention release requests that precede substantial completion
8. Produce a review memo with: (a) blocking issues that must be fixed before certification, (b) questions for the submitter, (c) notes for the file, and (d) a recommended certification amount

**Output requirements:**
- Open the memo header with an **"Applied config"** line naming the defaults the review assumed (e.g., "Applied config: 5% retainage w/ step-down to 2.5% at 50% (standard_retainage_policy); conditional-current + unconditional-prior waivers, MA statutory form (lien_waiver_policy); Procore Pay Apps export (pay_app_platform); GC-reviewing-sub (default_pay_app_role)") so any wrong default is visible rather than silent. Do not re-ask the user for any value config supplied.
- Lead with a one-paragraph summary and a recommended action (certify as submitted / certify a revised amount / return for correction)
- Itemized list of math discrepancies with the G703 line, the submitted value, and the expected value
- Separate section for documentation gaps (lien waivers, stored-material backup)
- Plain-language explanations — assume the reader is not an accountant
- Include a disclaimer that this is an AI-assisted review and does not replace the architect's or lender's independent certification
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Pay Application #03 from Premier Drywall (Pkg 02 Framing + Drywall) on Brookline MOB TI Phase 2 / 2026-018. GC: Northwood Builders. Original contract sum $241,000. One executed CO (#1: +$18,500 — new partition and blocking at Suite 303, signed 2026-05-06). Adjusted contract sum: $259,500. G702 shows: previous certified $74,100; work completed this period $52,300; total to date $126,400 (48.7% per G702); retainage $6,320 (5%); current payment due $45,980. G703 has 8 SOV lines totaling $241,000 (CO #1 not added). SOV Line 4 (Suite 303 partition framing, $22,000) is marked 100% complete. Site confirms Suite 303 framing has not started as of 2026-05-09. Conditional lien waiver for the current $52,300 draw was submitted. No unconditional lien waiver for the prior $74,100 payment was submitted. Retainage 5% throughout, no step-down. Role: GC reviewing sub's app. State: Massachusetts.

**Expected output:**

> **Recommended Action: Return for correction.** Three issues must be resolved before certification. Premier Drywall's Pay App #03 overclaims Suite 303 partition framing (not yet started), does not reflect executed CO #1 on the G703, and is missing the required unconditional lien waiver for Pay App #02. The G702 math closes internally but is based on a stale contract sum; once corrected, the revised current payment due is approximately $30,300.
>
> ---
>
> **Blocking Issues (must be corrected before certification)**
>
> **1. Suite 303 partition framing (SOV Line 4) — overclaimed at 100% complete.**
> G703 Line 4 shows $22,000 completed this period at 100%. Site observation and daily log dated 2026-05-08 confirm Suite 303 framing has not started (area still in demo/debris cleanup). Percent complete must be corrected to 0% before this pay app can be certified. Holdback from current payment: $22,000.
> - Submitted: $22,000 (100% complete) — Expected: $0 (0% — work not started)
>
> **2. CO #1 ($18,500) not reflected on G703.**
> Executed CO #1 (signed 2026-05-06) is included in the G702 adjusted contract sum ($259,500) but does not appear as a line item on the G703. The G703 subtotal remains $241,000. This understates the adjusted contract sum on the continuation sheet and makes the 48.7% completion figure meaningless against the wrong baseline. Premier must add a CO #1 line to the G703 (e.g., below the original 8 SOV lines) with its scheduled value ($18,500) and its current percent complete (0% — Suite 303 scope not started). The G702 cover must then be re-reconciled to the corrected G703.
>
> **3. Missing unconditional lien waiver for Pay App #02 ($74,100).**
> The GC's subcontract requires an unconditional lien waiver for the prior certified payment with each new draw. A conditional waiver for the current $52,300 draw was submitted; the unconditional waiver for the previously paid $74,100 has not been received. Under Massachusetts prompt payment law (M.G.L. c. 149 § 29E), failure to provide required lien documentation is grounds to withhold certification. Cannot certify without this document.
>
> ---
>
> **Questions for Submitter**
> - What is the actual installed percentage of Suite 303 partition framing as of 2026-05-09? (GC site observation shows 0%.)
> - Was CO #1 scope included in SOV Line 4 ($22,000), or is it entirely separate new scope? If it was merged into Line 4, the SOV needs amendment to separate the original and CO scopes.
> - Can you provide the unconditional lien waiver for Pay App #02 ($74,100) by 2026-05-12?
>
> ---
>
> **Notes for File**
> - Carry-forward math: G703 "from prior applications" ($74,100) ties exactly to Pay App #02 certified amount — no error.
> - Retainage: 5% applied uniformly across all submitted lines — correct per contract. Once Line 4 is zeroed and the CO #1 line is added, re-verify retainage on both.
> - Stored materials (G703 Column E): $0 — no stored-material claim submitted. No backup required.
> - No SOV front-loading apparent on Lines 1–3 and Lines 5–8 based on available schedule data.
> - Massachusetts lien waiver form: Conditional and unconditional forms submitted match the M.G.L. c. 254 statutory format — form is correct, unconditional is simply missing.
>
> ---
>
> **Recommended Certification Amount: $0 pending corrections.**
> Upon correction — Line 4 reduced to 0%, CO #1 added at 0%, unconditional waiver for Pay App #02 received — the revised current payment due is approximately:
> - Completed this period (revised): $52,300 − $22,000 (Line 4 reduction) = $30,300
> - Less 5% retainage: −$1,515
> - Revised net payment: ~$28,785
> (Exact amount to be verified against the corrected G703.)
>
> _AI-assisted pay application review. All math must be verified by the GC's PM against the original G702/G703 and the corrected resubmittal. This review does not replace the architect's independent certification per AIA G702 Section 4, nor does it constitute legal advice on lien rights._
