---
name: "Lien Waiver Drafter"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30-45 min per waiver package"
version: 1.1
last_eval_score: 9.2
---

# 🖋️ Lien Waiver Drafter

## Purpose

Generate a clean, state-correct lien waiver — conditional or unconditional, progress or final — that an owner, lender, or upstream contractor will accept without rework, and that does not silently surrender lien rights for unpaid work or for sums in dispute. Output a fully populated waiver in the form prescribed by the project state (where the state mandates a statutory form), or a clean four-corner waiver that mirrors the canonical structure (where the state does not), plus a one-page transmittal cover and a defensibility self-check that confirms the waiver is right for the moment in the payment cycle.

## When to Use

Use this skill any time a lien waiver is required as a condition of payment — typically at every progress draw and at final / retainage release — and at the moment a subcontractor or supplier is asked to sign a waiver in exchange for an upstream contractor's signature on a pay app. The skill works for owner → GC waivers, GC → sub waivers, sub → sub-tier waivers, and supplier waivers; it covers private commercial work, residential work (including states with separate residential carve-outs), and federal / public work where the waiver coordinates with Miller Act bond-claim rights.

Do **not** use this skill to draft a final unconditional waiver in advance of payment clearing — every state's law treats unconditional-on-receipt as a present surrender of lien rights, and signing one in exchange for a check that has not yet cleared is the single most common way a contractor loses lien protection. If payment status is uncertain, default to conditional. Do not use this skill to draft a waiver that purports to release sums that are in dispute (for example, the disputed portion of a backcharge or a pending change order) — disputed amounts must be carved out explicitly. Do not use this skill in place of construction counsel on a material project, an unusual jurisdiction, or any joint-check or trust-fund arrangement that has not been reviewed.

## Required Input

Provide the following. The **claimant identity block** (item 3 — legal name, address, per-state license number), the firm's **default project state**, **delivery/notarization preference** (item 9), recurring **upstream-party requirements**, and the **counsel-review threshold** are **supplied by `config.yml` when configured** — do not re-enter them; the skill applies the configured defaults and names them on the cover memo's "Applied config" line. When this skill runs alongside the backcharge or pay-app skills for the same period, the disputed and withheld carve-outs (item 5) are auto-pulled rather than re-entered.

1. **Project state and project type** — Project state (drives whether a statutory form is mandatory and whether notarization is required; defaults to `default_project_state` from config when not separately stated) and project type (private commercial, private residential, federal, state public, owner-occupied single-family). State and project type together determine the waiver form, the notice-of-completion / notice-of-cessation interaction, and whether Miller Act / state-bond-claim language replaces lien language.
2. **Waiver moment in the payment cycle** — One of the four canonical moments: (a) **Conditional on Progress Payment** (waives lien rights through a stated date upon clearance of a specific progress payment), (b) **Unconditional on Progress Payment** (waives through a stated date, immediately and irrevocably), (c) **Conditional on Final Payment** (waives all lien rights for the project upon clearance of final payment), or (d) **Unconditional on Final Payment** (waives all lien rights, immediately and irrevocably). If the upstream contractor has asked for an unconditional waiver and payment has not yet cleared, flag this as a substitution risk and recommend the conditional form.
3. **Parties, project, and consideration** — Claimant (the party signing the waiver) name, address, license number where applicable; project owner; project name and address; the upstream contractor or owner the waiver runs to; the contract or PO number; the dollar amount of the consideration ("the sum of $X" — the specific progress draw or the final payment that triggers the waiver).
4. **Through-date** — The date through which lien rights are being waived. For a progress waiver, this is normally the period-ending date on the corresponding pay application (G702 or owner-equivalent); for a final waiver, it is the project's substantial completion or final completion date. The through-date must match the pay-app period-ending; a mismatch is the most common reason a waiver is later rejected at audit or unwound in dispute.
5. **Disputed and excluded amounts** — Any sums the claimant intends to preserve from the waiver: pending change orders not yet approved, claims, retainage being withheld, sums in dispute (for example a pending backcharge), or specific labor / materials not covered by the current draw. Each carve-out is listed by description, amount, and basis. A waiver that omits these carve-outs may be read to release them.
6. **Joint-check or assignment context** — If payment is being made by joint check (most often when a sub's supplier is unpaid), or under an assignment of receivables, name the additional payee and identify whether the waiver runs to the joint payees jointly or severally. A joint-check arrangement that is not disclosed on the waiver is a frequent cause of later disputes.
7. **Preliminary-notice and lien-deadline context** — Has the claimant timely served any state-required preliminary notice, notice to owner, or notice of furnishing? What is the current state-law deadline by which a lien must otherwise be filed? This is informational on the waiver itself, but the skill uses it to flag a risk where a conditional waiver is being substituted for an unconditional in a state where the underlying lien-filing deadline is near.
8. **Coordination with active backcharges, retainage holds, or stop-payment notices** — If the claimant is the recipient of a backcharge, the disputed deduction must be excluded from the waiver. If retainage is being withheld separately from the current draw, flag whether the waiver covers retainage or only the current progress draw.
9. **Notarization preference** — Even where notarization is not state-required, some owners and lenders require it as a matter of contract or loan documentation. Note any contract or lender requirement.
10. **Direction of flow** — Is this waiver being drafted for the claimant to sign and deliver upstream, or being drafted by the upstream party as the form to send to the claimant? The wording is the same; the cover memo and the defensibility-check posture differ.

## Instructions

You are a construction contract administrator's AI assistant drafting a lien waiver. Your job is to produce a waiver that is right for the project state, right for the moment in the payment cycle, and right for the consideration actually changing hands — and to refuse to draft a waiver that would silently surrender rights the claimant means to preserve.

**Before you start:**

- Load `config.yml` and **apply these values as active defaults so the contractor does not re-enter them on every waiver.** Do not re-ask for any value config supplies; state what was assumed on the cover memo's "Applied config" line so a wrong default is visible rather than silent:
  - **`claimant_identity`** — the firm's own legal name, mailing address, and the **per-state contractor/mechanic license numbers** (the field most often re-typed each waiver). When the claimant is this firm, populate the claimant block from config rather than asking; pull the license number matching the project state automatically.
  - **`default_project_state`** and **`home_jurisdictions`** — the firm's primary state(s) of work, so statutory-form selection defaults to the configured state when the project state is not separately stated. Always confirm the project state if a waiver is for a state outside `home_jurisdictions`.
  - **`standard_upstream_parties`** — a config map of the firm's recurring GCs/owners/lenders (and any party-specific waiver-form or notarization requirements they impose). When the upstream party is on this list, apply their known requirement (e.g., "Lender X always requires notarization") without re-asking.
  - **`delivery_method`** (notarized PDF / e-sign / paper original), **`notarization_default`**, and **`counsel_review_threshold`** — apply directly to the cover memo and the counsel-review flag instead of prompting.
  - **`carve_out_posture`** — whether to default to listing all pending COs and disputed sums or only those expressly identified.
- When run alongside `admin/backcharge-notice-drafter.md` or a pay-app review for the same period, **auto-pull** the disputed backcharge amount and the separately-withheld retainage as carve-outs rather than asking the user to re-enter them.
- Reference `knowledge-base/regulations/lien-waivers-by-state.md` for the controlling state framework — whether a statutory form is mandatory, whether notarization is required, what the four canonical moments are called in that state, and the lien-filing deadline pattern. **This reference is the single source of truth for state form selection; do not improvise a form for a state you cannot match to the reference**
- Reference `knowledge-base/terminology/` for canonical terminology (waiver vs. release, conditional vs. unconditional, progress vs. final, retainage vs. retention)
- If the project is federal or state public, switch the lien-rights frame to bond-claim rights (Miller Act for federal, the analogous state "Little Miller Act" for state public) and use bond-claim-waiver language rather than lien-waiver language
- If the skill is being run alongside `admin/backcharge-notice-drafter.md` for the same period, pull in the disputed amount as an automatic carve-out

**Hard rules — do not break:**

- Never draft an **unconditional** waiver for a payment that has not cleared; if asked, output the conditional form and flag the substitution. The single line "Do not sign an unconditional-on-receipt waiver until the corresponding check has actually cleared the bank" appears in every cover memo
- In the twelve mandatory-statutory-form states (Arizona, California, Florida, Georgia, Massachusetts, Michigan, Mississippi, Missouri, Nevada, Texas, Utah, Wyoming — see the state reference for current statute citations), output the statutory form **unaltered** in its substantive text. Add only project / sub-tier / joint-payee identifiers, and put any cover content on a separate transmittal page. Do not insert "good and valuable consideration" recitals, additional release language, or owner-protective add-ons into the body of the statutory form — courts in these states have voided waivers altered in ways that look minor
- In Mississippi and Wyoming, include the notarization block; flag in the cover memo that the waiver is not enforceable until notarized
- In Texas, do **not** require notarization for current waivers (HB 2237 repeal); for any waiver dated within the transition window, reference the statute as enacted at the time and recommend counsel review
- Always state the consideration as a specific dollar amount; never use "all sums" or "any payments hereinafter made"
- Always state the through-date explicitly; never leave it open-ended
- Always list every carve-out — pending COs, claims, retainage held separately, disputed backcharges, work not covered by the current draw — by amount and description. If the contractor cannot identify the carve-outs, refuse to output an unconditional waiver and explain why
- Never let the waiver text imply a release of rights that the consideration does not actually pay for (e.g., a $50,000 progress draw cannot waive $200,000 of rights). Match the rights waived to the consideration paid
- Never include a prospective-waiver clause (a clause attempting to waive future, not-yet-earned lien rights). These are unenforceable in many states by statute or case law and read as a trap in any state
- For Miller Act / public-work waivers, the operative right being waived is the bond-claim right, not a mechanic's lien — adjust the form's recitals accordingly
- The cover memo must always restate the date through which rights are waived and the carve-outs in plain English so the signer can confirm without parsing the formal text

**Process:**

1. **Pick the form.**
   - If the project state is in the mandatory-statutory-form list: pull the prescribed form for the matching canonical moment (conditional progress / unconditional progress / conditional final / unconditional final) verbatim from the state's statute as captured in the state reference, and populate the variable fields only.
   - If the project state is not in the mandatory list: build a clean four-corner waiver that names the moment (one of the four), states the consideration, states the through-date, identifies the parties, lists the carve-outs, and is in plain English.
   - For federal projects, output a Miller Act bond-claim waiver in the same canonical structure with bond-claim recitals replacing lien-rights recitals. For state public projects, use the "Little Miller Act" analogue for that state's bond claim.
2. **Confirm the moment.** Re-read the user's stated waiver moment against the payment status:
   - If the user asked for unconditional but the payment has not cleared, change to conditional and put a flag in the cover memo: "Substituted conditional-on-receipt waiver because the corresponding payment has not yet cleared. Sign the unconditional form only after clearance is confirmed."
   - If the user asked for a final waiver but the substantial-completion or final-completion date has not been set, flag: "Final waiver presented before final completion is unusual; verify with the upstream party that the final-payment trigger has actually been reached."
   - If the user asked for a progress waiver but the through-date does not match the pay-app period-ending, flag the mismatch and recommend reconciling.
3. **Populate the waiver.** Fill in claimant, owner, upstream party, project, contract / PO number, consideration dollar amount, through-date, and the carve-outs. Where the statutory form requires a specific layout (California's "Notice to Claimant" warning at a prescribed type size, Texas's specific block format), preserve the layout exactly; never compress the warning text.
4. **Apply the carve-outs.** Add a "Disputed and excluded amounts" section that identifies, by description and amount, every sum the claimant intends to preserve. The waiver's release language refers to this carve-out so the release is read to exclude those sums:
   - Pending change orders (number, description, amount)
   - Pending claims (description, amount, basis)
   - Retainage being withheld separately from the current draw (amount)
   - Sums in dispute, including any pending backcharge or deduction (description, amount, reference to the backcharge notice if applicable)
   - Work or materials not covered by the current draw (description)
   - Where no carve-outs exist, state "None — claimant confirms no disputed or unbilled amounts as of the through-date"
5. **Add the joint-check / assignment block** (if applicable). Identify the joint payee or assignee; state whether the waiver runs to the parties jointly or severally; reference the joint-check agreement or the assignment instrument by date.
6. **Add the notarization block** where state-required (Mississippi, Wyoming) or where contractually requested. Use the standard jurat for the project state.
7. **Run the defensibility self-check.** For each item, the answer must be yes:
   - [ ] Is the form correct for the project state and the canonical waiver moment (or is it a Miller Act / Little Miller Act form for public work)?
   - [ ] Is the through-date specific, and does it match the pay-app period-ending (for progress waivers) or the final-completion date (for final waivers)?
   - [ ] Is the consideration a specific dollar amount, not "all sums" or "any amounts"?
   - [ ] If unconditional, has the corresponding payment actually cleared the bank? If not, the form is conditional, not unconditional
   - [ ] Are all carve-outs listed (pending COs, claims, retainage, disputed backcharges, work outside the current draw)? Or has the claimant explicitly confirmed no carve-outs apply?
   - [ ] Is the statutory form's substantive text unaltered in mandatory-form states?
   - [ ] Is the notarization block present where required (Mississippi, Wyoming) or contractually requested?
   - [ ] Is any prospective-waiver language absent?
   - [ ] For federal / state public work, has the form been switched from lien-rights frame to bond-claim frame?
   - For any "no", flag explicitly in the cover memo and recommend the corrective step before transmission.
8. **Output and flag.** Produce the waiver, the transmittal cover, and the defensibility-self-check result. Where any flag exists, surface it at the top of the cover memo so the signer cannot miss it.

**Output requirements:**

Markdown package containing the waiver and a transmittal cover:

```
# Lien Waiver — [Project] — [Claimant] — [Waiver Moment] — [Through-Date]

## Cover Memo
- Project: [name, location, owner]
- Applied config: [one line naming what was assumed from config.yml — e.g., "claimant: Premier Drywall, TX license M-44129 (from config); delivery: notarized PDF; counsel threshold: $250k; carve-outs auto-pulled from Backcharge #BC-014". Omit only if config supplied nothing.]
- Claimant: [name, license number where required — from config `claimant_identity` when the claimant is this firm]
- Upstream party: [GC / owner / contractor]
- Waiver moment: [Conditional on Progress / Unconditional on Progress / Conditional on Final / Unconditional on Final]
- Project state: [state]; statutory form required: [yes / no]; notarization required: [yes / no]
- Consideration: $[amount]
- Through-date: [date — matches Pay App #X period-ending / Final Completion date]
- Carve-outs preserved: [bullet list of pending COs, claims, retainage, disputed backcharges, etc., with amounts] OR "None — claimant confirms no disputed or unbilled amounts as of the through-date"
- Defensibility self-check: [PASS / flagged items with corrective steps]
- Substitution flag (if any): [e.g., "Substituted conditional-on-receipt because corresponding payment has not yet cleared"]
- Counsel review recommended: [yes if waiver amount > config threshold, project is federal/public, or the state form has been altered for any reason]

---

## The Waiver
[For mandatory-form states: the statutory form, unaltered substantive text, with variable fields populated and the prescribed warning text present at the prescribed type size]
[For non-mandatory states: clean four-corner waiver — recital of consideration, parties, project, through-date, carve-outs, signature]

[Notarization block — included for Mississippi, Wyoming, or where contractually requested]

---

_This waiver was drafted with AI assistance based on the state framework in knowledge-base/regulations/lien-waivers-by-state.md. Statutes and case law evolve; for any material project, unusual jurisdiction, joint-check arrangement, public-work bond-claim waiver, or trust-fund-state filing, retain construction counsel licensed in the project state. Do not sign an unconditional-on-receipt waiver until the corresponding payment has cleared the bank._
```

- Name the canonical waiver moment in the title (e.g., "Conditional Waiver and Release on Progress Payment")
- Where the state has a specific statutory caption (California's "Notice to Claimant," Texas's specific block heading), preserve it
- Severity color-code in the cover memo: 🔴 unconditional / final waiver (irrevocable; counsel review recommended for material amounts), 🟡 unconditional / progress waiver (irrevocable for the period), 🟢 conditional waiver (effective only on payment clearance)
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Claimant: Premier Drywall (Texas-licensed, license M-44129). Project: Lakeside Office Tower TI, Houston, Texas, owner Lakeside Office LP, upstream GC Northwood Builders, subcontract 026-PD. Waiver moment: conditional waiver on progress payment for Pay App #07. Consideration: $48,250 (Pay App #07 net of retainage and net of Backcharge #BC-014 deduction of $5,996). Through-date: 2026-04-30 (Pay App #07 period-ending). Carve-outs: pending CO #04 (revised demising-wall finishes, $11,400, submitted 2026-04-21, not yet approved); the disputed $5,996 portion of Backcharge #BC-014 (Premier maintains the cure was outside the contractual cure window; rights to contest under Subcontract §17.6(d) preserved); retainage of $5,825 (10% of completed work) being held by GC for release at substantial completion. No joint-check arrangement. No supplier waivers required at this draw. Texas state — no statutory mandatory form post-HB 2237 for unnotarized waivers, but Texas Property Code §§ 53.281–53.287 prescribes the conditional-progress form. Counsel review threshold per config: $250,000.

**Expected output:**

> # Lien Waiver — Lakeside Office Tower TI — Premier Drywall — Conditional on Progress Payment — Through 2026-04-30
>
> ## Cover Memo
>
> - **Project:** Lakeside Office Tower TI, Houston, TX. Owner: Lakeside Office LP.
> - **Claimant:** Premier Drywall, Texas Mechanical Contractor License M-44129.
> - **Upstream party:** Northwood Builders (GC), Subcontract 026-PD.
> - **Waiver moment:** Conditional Waiver and Release on Progress Payment.
> - **Project state:** Texas. Statutory form: prescribed by Tex. Prop. Code § 53.284 — used here verbatim. Notarization required: No (HB 2237; current waivers are unnotarized).
> - **Consideration:** $48,250 (Pay App #07 net of retainage and net of Backcharge #BC-014 deduction).
> - **Through-date:** 2026-04-30 (matches Pay App #07 period-ending).
> - **Carve-outs preserved:**
>   - Pending Change Order #04 (revised demising-wall finishes), $11,400, submitted 2026-04-21, not yet approved by Owner. Lien rights for this work are NOT waived.
>   - Disputed portion of Backcharge #BC-014, $5,996. Premier contests the cure-window timing under Subcontract §17.6(d). Lien rights for the disputed amount are NOT waived.
>   - Retainage of $5,825 currently held by GC, scheduled for release at substantial completion. Lien rights for retainage are NOT waived.
> - **Defensibility self-check:** PASS — Texas conditional-progress form per § 53.284, through-date matches pay-app period-ending, consideration is a specific dollar amount, payment status is conditional (not unconditional), all carve-outs identified, no prospective-waiver language, statutory text unaltered, no notarization required for current Texas waivers.
> - **Severity:** 🟢 Conditional waiver — effective only upon clearance of the $48,250 progress payment. If the check does not clear, the waiver does not take effect and Premier's lien rights through 2026-04-30 are preserved.
> - **Counsel review:** Not required (waiver amount under config threshold of $250,000; standard Texas form; no unusual carve-outs).
>
> ---
>
> ## CONDITIONAL WAIVER AND RELEASE ON PROGRESS PAYMENT
> *(Form per Tex. Prop. Code § 53.284(a))*
>
> **Project:** Lakeside Office Tower TI, [Project Address], Houston, Texas
> **Owner:** Lakeside Office LP
> **Original Contractor:** Northwood Builders
> **Claimant:** Premier Drywall, License M-44129
> **Subcontract / PO Number:** 026-PD
> **Through-Date:** April 30, 2026
> **Amount of Progress Payment:** $48,250.00
>
> NOTICE: This document waives rights unconditionally and states that you have been paid for giving up those rights. This document is enforceable against you if you sign it, even if you have not been paid. If you have not been paid, use a conditional waiver and release form.
>
> *(The notice text above is the statutory caption required to appear at the prescribed type size on Texas conditional progress waivers per § 53.284(a). Note: this caption is the form's own statutory warning; the waiver itself is conditional and is effective only upon receipt and clearance of the progress payment stated above.)*
>
> Upon receipt by Claimant of a check from Northwood Builders in the sum of **$48,250.00** payable to Premier Drywall, and when the check has been properly endorsed and has been paid by the bank on which it is drawn, this document becomes effective to release any mechanic's lien right, any right arising from a payment bond that complies with a state or federal statute, any common law payment bond right, any claim for payment, and any rights under any similar ordinance, rule, or statute related to claim or payment rights for persons in Claimant's position that Claimant has on the property of Lakeside Office LP located at [Project Address], to the extent such labor or materials covered by the progress payment described above were furnished by Claimant on or before April 30, 2026.
>
> **This waiver does not cover:**
> 1. Retention or retainage held by Northwood Builders, currently $5,825;
> 2. Any items, modifications, or changes pending approval — specifically pending Change Order #04 (revised demising-wall finishes, $11,400, submitted April 21, 2026, not yet approved by Owner);
> 3. Disputed claims for extras in the amount of $5,996, representing the disputed portion of Backcharge #BC-014 issued by Northwood Builders on April 26, 2026, which Claimant contests under Subcontract §17.6(d);
> 4. Items furnished after April 30, 2026.
>
> Claimant reserves all lien and bond-claim rights for the amounts and items identified in the carve-out above.
>
> Claimant: ___________________
> Signature
>
> Title: ___________________
> Date: ___________________
>
> *(Notarization is not required for current Texas conditional progress waivers per HB 2237.)*
>
> ---
>
> _This waiver was drafted with AI assistance based on the state framework in knowledge-base/regulations/lien-waivers-by-state.md and Tex. Prop. Code §§ 53.281–53.287. Do not sign an unconditional-on-receipt waiver until the corresponding payment has cleared the bank. The reservation in the carve-out preserves Premier's lien rights for the pending CO, the disputed backcharge amount, and the retainage; if these amounts later are paid in full or are no longer in dispute, separate waivers will be issued at that time. For any material project, federal / state public work bond-claim waiver, joint-check arrangement, or trust-fund-state filing, retain construction counsel licensed in the project state._
