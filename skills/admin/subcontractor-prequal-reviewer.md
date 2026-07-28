---
name: "Subcontractor Prequalification Reviewer"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45-90 min/sub"
version: 1.2
last_eval_score: 9.2
---

# 🛡 Subcontractor Prequalification Reviewer

## Purpose

Review a subcontractor's prequalification submission — certificate of insurance (COI), safety metrics (EMR, TRIR, OSHA 300 logs), financial snapshot, bonding capacity, licensing, and references — and produce a go / no-go recommendation with specific gaps, risk flags, and coverage deltas vs. the GC's minimum requirements.

## When to Use

Use this skill when a GC or CM is onboarding a new sub, refreshing an annual prequal, or qualifying a sub for a specific project whose risk profile (e.g., high-rise, occupied facility, public works) demands more coverage than the GC's baseline. It is especially useful when a prequal packet arrives as a stack of PDFs and the risk manager wants a two-page read-out instead of opening every attachment. Do not use this skill to replace the legal review of subcontract terms, the underwriter's independent verification of insurance, or the surety's assessment of bonding capacity.

## Required Input

Provide the following. The **GC minimum requirements** (item 1) — baseline insurance minima, required endorsements, EMR/TRIR/DART ceilings, bonding and surety-rating floors, the prequal platform, and the two-tier upset thresholds — are **supplied by `config.yml` when configured** — do not re-enter them; the skill applies the configured baseline and names it on the memo's "Applied config" line. You still provide the sub's packet (items 3–9) and the **project-specific uplift** (item 2) that differs from the configured baseline.

1. **GC minimum requirements** — The GC's baseline for insurance (GL per occurrence / aggregate, auto, umbrella, WC, professional, pollution, cyber if relevant), additional insured endorsement, waiver of subrogation, primary & non-contributory, EMR ceiling, minimum years in business, bonding capacity threshold. **Defaults entirely from config** (`gc_insurance_baseline`, `safety_ceilings`, `bonding_requirements`, `surety_rating_floor`) — supply this item only to override the configured baseline for a specific GC entity.
2. **Project-specific requirements** — Any uplift vs. baseline (e.g., $5M umbrella for a hospital project, pollution policy for demolition, builder's risk waiver of subrogation). **This is the main thing you provide** — the project's risk profile and the uplift it drives on top of the configured baseline.
3. **Sub's COI** — Acord 25 or equivalent, with all pages including endorsements
4. **Sub's safety package** — EMR letter (3 years ideally), TRIR / DART calculations, OSHA 300/300A logs (most recent 3 years), written safety program table of contents
5. **Sub's financial snapshot** — CPA-compiled or reviewed financials (balance sheet, income statement), bank reference, D&B score if available, bonding letter with single & aggregate limits
6. **Sub's licensing** — Contractor license in the project state, specialty trade licenses, business entity registration
7. **Sub's project history** — Similar-scope projects, GC references with contact info, completed-project values
8. **Sub's organization** — Years in business, ownership, key personnel resumes, MBE/WBE/DBE certification if applicable
9. **Scope they are bidding** — Trade + rough contract value (to check bonding and coverage adequacy)

## Instructions

You are a construction risk manager's AI assistant. Your job is to read every page of a prequal packet, cross-check it against the GC's standard, and flag every gap clearly enough that the sub can respond in one email. Be pedantic about expiration dates and coverage language — these are the details that blow up projects.

**Before you start:**
- Load `config.yml` and **apply these values as active defaults so the user does not re-enter the GC's standing requirements on every prequal.** Do not re-ask for any value config supplies; instead state what was assumed on the memo's "Applied config" line so a wrong default is visible rather than silent. The user supplies the sub's packet and the project-specific uplift; config supplies the standing baseline the packet is measured against:
  - **`gc_insurance_baseline`** — the GC's standard GL / Auto / Umbrella / WC / Pro / Pollution per-line minima, additional-insured endorsement-form preference (CG 20 10 / CG 20 37 editions), waiver-of-subrogation requirement, primary-and-non-contributory requirement, and per-project-aggregate requirement. Populate the "GC Standard" column of the requirements-vs-submitted matrix directly from this; do not ask the user to restate baseline minima.
  - **`safety_ceilings`** — EMR ceiling and TRIR / DART ceilings **by trade family**; apply the trade-matched ceiling to the sub's metrics automatically based on the scope being bid.
  - **`bonding_requirements`** and **`surety_rating_floor`** — the single/aggregate bonding multipliers against contract value and backlog, and the surety-rating floor (typically A- VIII or better); apply as the default pass/fail test on the bonding letter.
  - **`prequal_platform`** — the GC's prequalification platform (TradeTapp / Procore Prequalification AI / Highwire / Avetta / ISNetworld / BROWZ / COMPASS); when set, assume the input may be a platform-AI summary and pre-load that platform's known gap pattern in the Reviewer-of-Platform-AI sub-mode below without re-asking which platform produced it.
  - **`prequal_thresholds`** — the GC's two-tier upset thresholds ("Approved with conditions" vs. "Not approved at this time") so the headline recommendation uses the firm's wording, not a generic scale.
  - **`license_verification_states`** and **`mbe_wbe_dbe_convention`** — the GC's project-state list for state-specific license verification and the firm's diversity-tracking convention.
- Reference `knowledge-base/terminology/` for correct insurance and construction risk language (Acord form numbers, endorsement codes — CG 20 10 ongoing-ops, CG 20 37 completed-ops, CG 24 04 waiver-of-subrogation, CG 25 03 per-project aggregate, WC waiver state-specific forms)
- Reference `knowledge-base/best-practices/subcontractor-risk/` if present, for the GC's standard risk matrix
- Note that insurance endorsement language (additional insured, waiver of subrogation, primary & non-contributory) must be matched literally — "on file" or "as required by contract" on the COI is not acceptance. The endorsement form must be attached and the language read.

**Process:**

1. Build a requirements-vs-submitted matrix:
   - One row per required item (coverage line, endorsement, safety metric, license, reference)
   - Columns: Required / Submitted / Delta / Action
2. Parse the COI:
   - Carriers and AM Best ratings (flag anything below A-)
   - Policy effective and expiration dates (flag any expiring within 60 days)
   - Coverage limits per line (GL, Auto, Umbrella, WC, Pro, Pollution)
   - Deductibles or SIRs (flag high SIRs that could bankrupt a small sub)
   - Required endorsements present with correct language:
     - Additional Insured on a blanket basis (CG 20 10 / CG 20 37 or equivalent) covering ongoing and completed operations
     - Waiver of Subrogation (CG 24 04 or WC-specific)
     - Primary and Non-Contributory
     - Per-project aggregate (CG 25 03) for contractors with multiple jobs
   - Named insured matches the entity that will sign the subcontract (flag mismatches)
3. Audit safety metrics:
   - EMR for the most recent three years — flag trend (rising vs. falling)
   - TRIR and DART vs. industry/BLS benchmarks for the trade
   - OSHA 300 logs: number of recordables, DART cases, severity (fatalities, hospitalizations)
   - OSHA citations in the last 5 years (willful / repeat / serious)
   - Written safety program completeness (key programs: fall protection, confined space, LOTO, hot work, hazcom, silica, crane/rigging for relevant trades)
4. Audit the financial snapshot:
   - Working capital and current ratio — flag negative or very thin
   - Debt-to-equity — flag > 3:1 without explanation
   - Revenue trend (last 3 years)
   - Backlog vs. bonding capacity (flag over-committed subs)
   - Is the financial review independent (CPA compiled vs. reviewed vs. audited)?
   - Bonding letter: single job limit, aggregate limit, surety rating (flag < A-), and whether the letter references the current project
5. Audit licensing:
   - Contractor license active and in the project state
   - Specialty trade license if required (electrical, plumbing, mechanical, roofing in some states)
   - Business entity in good standing (not suspended)
6. Audit project history and references:
   - Similar scope (trade + dollar size + complexity) within the last 3–5 years
   - Reference contacts current and verifiable
   - Flag large gaps between past largest project and the proposed contract value (more than 2x jump is a warning)
7. Score the sub on a simple matrix:
   - Insurance: Pass / Conditional / Fail
   - Safety: Pass / Conditional / Fail
   - Financial: Pass / Conditional / Fail
   - Licensing: Pass / Conditional / Fail
   - Experience: Pass / Conditional / Fail
8. Produce a prequal review memo:
   - Headline recommendation: Approved / Approved with conditions / Not approved at this time
   - Required actions (numbered, each with an owner and a 3-to-10-business-day deadline)
   - Conditions the GC should embed in the subcontract (e.g., weekly safety audit, monthly financials during the job, retainage at 10% until 50% complete)
   - Risk notes for the PM (what to watch for in execution)

**Output requirements:**
- Open the memo header with an **"Applied config"** line naming the standing baseline the review assumed (e.g., "Applied config: GC baseline GL $1M/$2M, Umbrella $5M, CG 20 10 + CG 20 37 blanket (gc_insurance_baseline); EMR ceiling 1.00, mech/plumbing TRIR ceiling 3.0 (safety_ceilings); surety floor A- VIII (surety_rating_floor); TradeTapp platform (prequal_platform); thresholds Approved-with-conditions / Not-approved-at-this-time (prequal_thresholds)") so any wrong default is visible rather than silent. Do not re-ask the user for any baseline value config supplied.
- Markdown memo with (a) headline, (b) requirements-vs-submitted table, (c) insurance detail section, (d) safety detail section, (e) financial detail section, (f) licensing & experience, (g) required actions with owners, (h) subcontract conditions to consider
- Every flag cites the specific document and page where the issue was found (e.g., "COI page 2, Auto coverage expires 2026-06-01")
- Plain-language risk summary for the PM and the estimator at the top — do not bury the lede
- Include a disclaimer that this is an AI-assisted prequal review, that insurance endorsements must be verified with the carrier, and that financial and bonding conclusions are not underwriting opinions
- Saved to `outputs/` if the user confirms

## Reviewer-of-Platform-AI-Output Sub-Mode

Many GCs in 2026 have adopted platform-based prequal-management systems with AI-assisted intake and scoring: **TradeTapp** (Procore Prequalification, AI-summarized risk score + COI parsing), **Highwire** (AI-assisted compliance scoring with carrier-verification add-on), **Avetta** (AI-summarized contractor profile + automated coverage-gap flagging), **ISNetworld** (AI-driven RAVS-Plus scoring), **BROWZ / Veriforce** (AI-assisted regrade triggers), and **COMPASS Subcontractor Compliance** (AI-assisted endorsement-language parsing). These platforms produce an AI-generated risk summary and a green/yellow/red flag set; the GC's risk manager is then the reviewer-of-AI-output rather than the original abstractor. This sub-mode produces a redline of the platform's AI summary before it is accepted into the GC's subcontract package.

When the input is a platform-AI summary (not raw documents), apply this six-point redline check before accepting the platform's recommendation:

1. **Endorsement-language literal-text check.** Platforms frequently mark the additional-insured / waiver-of-subrogation / primary-and-non-contributory boxes as "compliant" based on a yes/no field set by the carrier or broker — without parsing the actual endorsement form attached. Pull the endorsement PDF (CG 20 10 04 13, CG 20 37 04 13, CG 24 04 05 09, CG 25 03 05 09, or equivalent), read the language, and verify it actually covers ongoing AND completed operations on a blanket basis. Platforms over-index on the form-number match and miss the date-edition or scheduled-vs-blanket distinction.
2. **EMR-and-TRIR trend reading.** Platforms typically score the most-recent year's EMR and TRIR; they do not score the trend. A 1.05 EMR after three years at 0.78 / 0.91 / 1.05 is a deteriorating-trend flag the platform will miss. Re-read the three-year history.
3. **Bonding-letter currency.** Platforms accept a bonding letter at upload and rarely re-verify single-job and aggregate limits against the proposed contract value or the sub's current backlog. Re-verify: does the bonding letter reference the current project? Are the single-job and aggregate limits adequate against the proposed contract value and the sub's currently-bonded backlog?
4. **Financial-statement independence reading.** Platforms record "financial statement on file" without distinguishing CPA-compiled vs. reviewed vs. audited. The independence level changes the weight the GC should put on the working-capital, current-ratio, and debt-to-equity figures. Re-classify and lower confidence on a compiled statement vs. an audited statement.
5. **State-specific licensing verification.** Platforms typically verify license-number existence but not in-good-standing status, in the project state, with the right classification, and not currently suspended or under disciplinary action. Re-verify with the state licensing board's online lookup; the platform's last-verified date is often months stale.
6. **Project-fit reading.** Platforms produce a generic-risk score, not a project-fit score. Re-score the sub against the specific project's risk profile: high-rise vs. low-rise, occupied vs. unoccupied, public vs. private, hospital / data center / school / multifamily / retail-TI (the GC's risk uplift on the baseline insurance, safety, and financial requirements changes the sub's effective prequal status from "Approved" to "Approved with conditions" or vice versa).

Sub-mode output: (a) platform's original AI-generated risk summary + score (preserved verbatim), (b) redline applied to each of the six points, (c) final GC-accepted recommendation that may agree or disagree with the platform, (d) provenance footer noting which platform produced the summary, which version of its AI was used (if known), what the redline changed, and which the GC accepted.

## Example Output

**Example input scenario:** Brookline MOB TI Phase 2 (GC = Stonebridge Construction, owner = Brookline Health Partners, 32,000 SF medical-office build-out, $4.2M total contract). The GC is qualifying **Acme Mechanical & Plumbing, LLC** for Pkg 06 (HVAC + plumbing rough-in + plumbing finish, scope budget $612,000) as a new sub on the GC's approved-vendor list. Acme submitted a 47-page prequal packet (COI + Acord 25 with 4 endorsement PDFs, 3-year EMR letter from MEMIC, OSHA 300/300A for 2023/2024/2025, CPA-reviewed financials for FYE 2025, bonding letter from Liberty Mutual Surety, MA contractor license + plumbing license + sheet-metal license, 6 reference projects).

**Expected output:**

> # PREQUALIFICATION REVIEW MEMO
>
> **Subject:** Acme Mechanical & Plumbing, LLC — Pkg 06 HVAC + Plumbing, Brookline MOB TI Phase 2
> **Project:** 2026-031 Brookline MOB TI Phase 2 (Brookline Health Partners, Brookline MA)
> **Trade / Scope:** HVAC + Plumbing rough-in + Plumbing finish
> **Proposed Contract Value:** $612,000
> **Reviewed by:** Risk Manager (AI-assisted), Stonebridge Construction
> **Review Date:** 2026-05-26
>
> ## HEADLINE RECOMMENDATION
>
> **Approved with conditions.** Acme Mechanical & Plumbing meets the GC's baseline insurance, safety, financial, and licensing thresholds for the Brookline MOB TI Phase 2 scope, with three conditions to clear before NTP and two execution-phase conditions to embed in the subcontract. The proposed contract value ($612,000) is within 1.4× the sub's prior-largest similar-scope project ($435,000 MGH OR-suite renovation, 2025) — within the GC's 2× warning threshold per config.yml.
>
> **Required actions before NTP:** 3 (resolve in 5 business days).
> **Subcontract execution conditions:** 2 (embed in §00 7300 supplementary conditions).
> **Pre-mobilization conditions:** 1 (state plumbing license verification refresh).
>
> ## REQUIREMENTS-VS-SUBMITTED MATRIX
>
> | # | Requirement | GC Standard | Project Uplift (Brookline MOB) | Submitted | Delta | Action | Doc / Page |
> |---|---|---|---|---|---|---|---|
> | 1 | GL per occurrence | $1M | — | $1M | ✓ Meets | None | COI p.1 |
> | 2 | GL aggregate | $2M | $4M (occupied healthcare uplift) | $2M | **⚠ Short** | Increase to $4M or add CG 25 03 per-project aggregate | COI p.1 |
> | 3 | Auto liability CSL | $1M | — | $1M | ✓ Meets | None | COI p.1 |
> | 4 | Umbrella / Excess | $5M | $10M (occupied healthcare uplift) | $5M | **⚠ Short** | Increase umbrella to $10M or layer with project-specific excess | COI p.1 |
> | 5 | WC / EL | Statutory / $1M EL | — | Statutory / $1M EL | ✓ Meets | None | COI p.1 |
> | 6 | Professional liability | Not required for HVAC/plumbing | — | Not carried | ✓ N/A | None | — |
> | 7 | Pollution liability | Required if scope incl. demolition / refrigerant recovery | $1M (refrigerant recovery on existing AHUs) | Not carried | **🔴 Missing** | Procure $1M contractors-pollution policy before NTP; non-negotiable | COI p.1 |
> | 8 | Add'l Insured — ongoing ops | CG 20 10 04 13 blanket, owner + GC + lender | — | CG 20 10 04 13 blanket present | ✓ Meets | None | Endorsement PDF p.1 |
> | 9 | Add'l Insured — completed ops | CG 20 37 04 13 blanket, owner + GC + lender | — | **Not attached** | **🔴 Missing** | Request CG 20 37 04 13 blanket endorsement; "on file" notation on COI p.2 is not acceptance per GC policy | COI p.2 |
> | 10 | Waiver of Subrogation (GL+WC) | CG 24 04 + WC state-specific | — | CG 24 04 + MA WC waiver attached | ✓ Meets | None | Endorsement PDF p.2-3 |
> | 11 | Primary & Non-Contributory | Required | — | CG 20 01 04 13 attached | ✓ Meets | None | Endorsement PDF p.4 |
> | 12 | Per-Project Aggregate | Required for multi-job subs | — | Not attached | **⚠ Short** | Resolves with #2 above (CG 25 03 satisfies both) | — |
> | 13 | EMR (3-yr trend) | Ceiling 1.00 | — | 0.81 / 0.78 / 0.83 (2023/2024/2025) | ✓ Meets, improving-then-flat | None — note slight 2025 uptick for execution-phase watch | MEMIC EMR letter |
> | 14 | TRIR (most recent) | Ceiling 3.0 (mech/plumbing BLS 2024 = 2.7) | — | 1.9 | ✓ Meets (below industry) | None | OSHA 300A 2025 |
> | 15 | DART (most recent) | Ceiling 1.5 | — | 0.9 | ✓ Meets | None | OSHA 300A 2025 |
> | 16 | OSHA citations (5-yr) | Zero willful / repeat / serious-with-injury | — | Zero willful / repeat; 1 serious (2023, abated, $4,400) | ✓ Conditional Meets | Note in risk file; not disqualifying | OSHA 300 2023 |
> | 17 | Written safety program | Fall protection, LOTO, hot work, hazcom, silica, confined space | + infection control risk assessment (ICRA) for healthcare | TOC submitted; ICRA not addressed | **⚠ Short** | Submit ICRA program addendum (ASHE / Joint Commission compliant) before NTP | Safety program TOC |
> | 18 | Working capital | > $500K for $600K+ contract | — | $1.8M | ✓ Meets | None | CPA reviewed FYE 2025 p.4 |
> | 19 | Current ratio | > 1.3 | — | 1.9 | ✓ Meets | None | CPA reviewed FYE 2025 p.4 |
> | 20 | Debt-to-equity | < 3:1 | — | 1.4:1 | ✓ Meets | None | CPA reviewed FYE 2025 p.5 |
> | 21 | Financial independence | CPA-reviewed minimum | — | CPA-reviewed (Smith & Co., Boston) | ✓ Meets | None — note: not audited, treat working-capital figure with normal review-level confidence | CPA cover letter |
> | 22 | Bonding capacity (single / aggregate) | Single ≥ 1.5× contract; Aggregate ≥ 4× backlog | Single ≥ $920K (1.5 × $612K) | Single $1.5M / Aggregate $7M from Liberty Mutual Surety (A.M. Best A XV) | ✓ Meets | None — bonding letter references this specific project | Bonding letter |
> | 23 | MA contractor license | Active, in good standing | — | HIC license active to 2027-03-15 | ✓ Meets | None | MA HIC verified 2026-05-23 |
> | 24 | MA master plumbing license | Active, qualifying license-holder identified | — | License #MPL-22417 (John Acme, qualifying); last verified 2026-02-12 | **⚠ Stale** | Re-verify online with MA Board of State Examiners of Plumbers before NTP (3-month-stale verification per GC policy) | License copy |
> | 25 | MA sheet-metal license | Active | — | License #SM-9821 active to 2027-06-30 | ✓ Meets | None | License copy |
> | 26 | Similar-scope reference (healthcare TI) | ≥ 1 in last 3 yrs | — | MGH OR-suite renovation $435K (2025); BWH lab fit-out $370K (2024) | ✓ Meets | Reference checks complete — both PMs gave positive recommendations | Reference list |
> | 27 | Single-project size jump | ≤ 2× prior largest similar | — | $612K vs. $435K = 1.41× | ✓ Meets | None | — |
>
> ## INSURANCE DETAIL
>
> **Carrier:** The Hartford (GL/Auto/Umbrella), MEMIC (WC), MA. AM Best ratings: Hartford A+ XV, MEMIC A IX — both above GC's A- VIII floor. Policy period 2026-01-01 to 2027-01-01 (no expirations within 60 days).
>
> **Critical gaps:**
> 1. **🔴 Missing — Contractors Pollution Liability** (refrigerant recovery on existing AHUs triggers Brookline MOB project uplift; non-negotiable before NTP).
> 2. **🔴 Missing — CG 20 37 04 13 Completed-Operations Additional Insured** (only ongoing-operations endorsement attached; completed-ops needed for retainage-release-to-completion warranty period).
> 3. **⚠ Short — GL aggregate ($2M submitted vs. $4M project-uplift required)** + **⚠ Short — Umbrella ($5M submitted vs. $10M project-uplift required)** — both addressable by either raising the underlying or adding a CG 25 03 per-project aggregate plus a $5M project-specific excess; broker to confirm cost and recommend route.
>
> ## SAFETY DETAIL
>
> 3-yr EMR trend 0.81 / 0.78 / 0.83 — slight 2025 uptick (one DART case at MGH project, abated). TRIR 1.9 (well below industry 2.7). DART 0.9 (below GC ceiling 1.5). Zero willful / repeat citations; one serious citation in 2023 (housekeeping at a non-healthcare project, abated, $4,400 penalty). Written safety program covers all GC-required programs **except infection control risk assessment (ICRA)** — required for the occupied healthcare project per Brookline Health Partners' supplementary conditions and per ASHE / Joint Commission expectations. **⚠ ICRA addendum required before NTP.**
>
> **Execution-phase watch:** the 2025 EMR uptick + one DART case in a healthcare environment warrants pre-mobilization safety pre-construction meeting with the GC's safety director and the sub's safety lead; recommend weekly ICRA-zone audits during construction with photo-anchored documentation (cross-reference `operations/safety-plan-builder.md` reviewer sub-mode).
>
> ## FINANCIAL DETAIL
>
> CPA-reviewed (not audited) FYE 2025 — Smith & Co., Boston MA. Working capital $1.8M, current ratio 1.9, debt-to-equity 1.4:1, revenue trend 2023 $4.2M / 2024 $5.1M / 2025 $5.8M (healthy upward, 12-15% YoY). Bonding capacity single $1.5M / aggregate $7M from Liberty Mutual Surety (A.M. Best A XV). Current bonded backlog $4.1M per surety letter, leaving $2.9M aggregate headroom against the $612K Brookline MOB project. **No financial gap; CPA-reviewed (not audited) status noted — treat working-capital figure with review-level confidence per GC policy, no derate.**
>
> ## LICENSING & EXPERIENCE
>
> All three required MA licenses (HIC general, master plumbing, sheet-metal) active and in qualifying-license-holder good standing. **⚠ Master plumbing license last verified 2026-02-12 (>3 months stale per GC policy) — re-verify with MA Board of State Examiners of Plumbers online lookup before NTP.** Two similar-scope healthcare TI references both above $350K (MGH OR-suite $435K 2025; BWH lab fit-out $370K 2024); both PM references contacted by the GC's risk team 2026-05-22 and 2026-05-23 — both gave positive recommendations with no qualifying notes. Size jump from prior-largest ($435K) to proposed ($612K) is 1.41× — within the GC's 2× warning threshold.
>
> ## SCORE MATRIX
>
> | Dimension | Score |
> |---|---|
> | Insurance | **Conditional** (4 gaps; all curable in 5 business days with broker action) |
> | Safety | **Conditional** (ICRA addendum required for healthcare scope) |
> | Financial | **Pass** |
> | Licensing | **Conditional** (re-verify master plumbing license currency) |
> | Experience | **Pass** |
> | **Overall** | **Approved with Conditions** |
>
> ## REQUIRED ACTIONS BEFORE NTP
>
> 1. **Owner:** Acme Mechanical broker (The Hartford / MEMIC, named on COI). **Action:** Procure $1M Contractors Pollution Liability policy; provide COI with Stonebridge Construction + Brookline Health Partners + Eastern Bank named as additional insureds. **Deadline:** 2026-06-02 (5 business days). **Verification:** Stonebridge risk manager review of CPL policy declarations page.
> 2. **Owner:** Acme Mechanical broker. **Action:** Issue CG 20 37 04 13 Completed-Operations Additional Insured endorsement (blanket basis, including Stonebridge Construction + Brookline Health Partners + Eastern Bank); raise GL aggregate to $4M and Umbrella to $10M via CG 25 03 per-project aggregate + $5M project-specific excess (or equivalent). **Deadline:** 2026-06-02 (5 business days). **Verification:** revised COI + endorsement PDFs reviewed against requirement matrix.
> 3. **Owner:** Acme Mechanical safety lead (John Acme, qualifying license holder). **Action:** Submit ICRA program addendum (ASHE / Joint Commission compliant; covers Class I-IV ICRA precautions, anteroom requirements, HEPA filtration, daily wet-vacuuming protocols) per Brookline MOB §01 3540. **Deadline:** 2026-06-02 (5 business days). **Verification:** Stonebridge safety director review + sign-off.
>
> ## PRE-MOBILIZATION CONDITIONS
>
> 1. **Re-verify MA master plumbing license** (license #MPL-22417, qualifying holder John Acme) with MA Board of State Examiners of Plumbers online lookup; last verified 2026-02-12, >3 months stale per GC policy. Verification date and result to be recorded in the prequal file before mobilization.
>
> ## SUBCONTRACT EXECUTION CONDITIONS (Embed in §00 7300 Supplementary Conditions)
>
> 1. **Monthly OSHA 300 + EMR update during construction** (per GC's healthcare-project standard; the 2025 EMR uptick to 0.83 and one DART case warrant execution-phase monitoring).
> 2. **Weekly ICRA-zone audit with photo-anchored documentation** during occupied-healthcare-adjacent work (cross-reference `operations/safety-plan-builder.md` reviewer sub-mode + `operations/daily-log-generator.md` reviewer sub-mode for the photo-documentation standard).
>
> ## RISK NOTES FOR THE PM
>
> - **Healthcare ICRA discipline is the dominant execution risk** — Acme has solid mechanical / plumbing healthcare experience but ICRA program is missing from the written-program TOC; this is curable pre-NTP but warrants a Day 1 pre-mob meeting to confirm protocol understanding.
> - **CPL is a hard gate** — refrigerant recovery on the existing AHUs (specified in §23 0900 demolition + refrigerant recovery) is the trigger; the sub may push back on CPL cost — hold the line, this is a non-negotiable owner requirement per Brookline Health Partners' RFP §11.
> - **Bonding headroom is adequate but not deep** ($2.9M aggregate headroom vs. $612K project — 4.7× coverage); if the sub picks up another large public-works project mid-construction, re-verify aggregate availability at 50% completion.
> - **CPA-reviewed (not audited) financials** — if Stonebridge requires audited statements for subs above $500K per a corporate-level policy update, flag for re-prequalification; current GC policy accepts CPA-reviewed at this contract size.
>
> ## DISCLAIMER
>
> This is an AI-assisted prequalification review. Insurance endorsements must be verified with the carrier and the carrier's claims representative before the subcontract is executed; "on file" or "as required by contract" notations on the COI are not acceptance. Bonding capacity and financial conclusions are not underwriting opinions and should be confirmed with the GC's surety and the sub's CPA. State-specific licensing must be verified via the state licensing board's online lookup at the verification date, not relied on from prior prequalification cycles. The risk manager should spot-check this memo against the raw documents before relying on it for subcontract execution.

## Example Output — Reviewer-of-Platform-AI-Output Sub-Mode (TradeTapp / Procore Prequalification)

**Example input scenario:** The GC's prequalification platform (TradeTapp, integrated with Procore Prequalification) has produced an AI-generated risk summary for **Acme Mechanical & Plumbing, LLC** (same sub as above) that reads:

> **TradeTapp Risk Score: 78 / 100 (Yellow — Approved with Conditions)**
> Coverage compliance: 100% (all required lines present). Endorsements: Compliant. EMR: 0.83 — compliant. TRIR: 1.9 — compliant. Financial: Strong (working capital, current ratio, debt-to-equity all within thresholds). Bonding: Adequate. Licensing: All licenses verified.
> **Yellow-flag reasons:** EMR slight uptick 2024→2025 (0.78→0.83); 1 OSHA serious citation in 2023 (abated).
> **Recommendation:** Approve with standard conditions; monitor EMR through 2026.

The GC risk manager is the reviewer-of-AI-output. Re-read this summary against the raw documents using the six-point redline.

**Expected output:**

> # PREQUAL PLATFORM-AI OUTPUT REVIEW — REDLINE
>
> **Platform:** TradeTapp (integrated with Procore Prequalification), AI version per 2026-Q2 release notes
> **Subject:** Acme Mechanical & Plumbing, LLC — Pkg 06, Brookline MOB TI Phase 2
> **Reviewed by:** Risk Manager (AI-assisted), Stonebridge Construction
> **Review Date:** 2026-05-26
>
> ## PLATFORM AI SUMMARY (PRESERVED VERBATIM)
>
> *TradeTapp Risk Score: 78 / 100 (Yellow). Coverage compliance: 100%. Endorsements: Compliant. EMR: 0.83 — compliant. TRIR: 1.9 — compliant. Financial: Strong. Bonding: Adequate. Licensing: All licenses verified. Yellow-flag reasons: EMR slight uptick; 1 OSHA serious citation in 2023 (abated). Recommendation: Approve with standard conditions; monitor EMR through 2026.*
>
> ## SIX-POINT REDLINE
>
> **1. Endorsement-Language Literal-Text Check — ❌ FAILS PLATFORM SUMMARY.** TradeTapp scored "Endorsements: Compliant" based on the broker's checkbox attestation in the upload form. Pulled the endorsement PDFs: CG 20 10 04 13 (ongoing-operations AI) is present and blanket; **CG 20 37 (completed-operations AI) is NOT attached** — only "on file" notation on the COI. **Per GC policy, "on file" is not acceptance — this is a 🔴 missing endorsement, not a green flag.**
>
> **2. EMR-and-TRIR Trend Reading — ⚠ PLATFORM UNDERSTATES.** TradeTapp flagged the EMR uptick yellow but presented it as cosmetic. Three-year trend reading: 0.81 (2023) → 0.78 (2024) → 0.83 (2025). The 2025 uptick is associated with one DART case (housekeeping injury at MGH OR-suite, abated). **For the Brookline MOB occupied-healthcare uplift, this trend warrants the execution-phase ICRA-zone weekly audit condition embedded in the subcontract — not just "monitor through 2026." Upgrade from monitoring to active execution-phase condition.**
>
> **3. Bonding-Letter Currency — ✓ PLATFORM IS CORRECT.** Re-read bonding letter — single $1.5M / aggregate $7M, A.M. Best A XV surety, **letter explicitly references "Brookline MOB TI Phase 2"** and was dated 2026-05-19 (well within the 60-day window). No redline.
>
> **4. Financial-Statement Independence Reading — ⚠ PLATFORM OBSCURES.** TradeTapp scored "Financial: Strong" — accurate at the metric level but **does not distinguish CPA-compiled vs. reviewed vs. audited**. The submitted statements are CPA-**reviewed** (Smith & Co., Boston) — review-level assurance, not audited. The working-capital and current-ratio figures should be accepted at review-level confidence, not audit-level. **Net effect: same recommendation, but the PM should know the assurance level when reading the working-capital figure.**
>
> **5. State-Specific Licensing Verification — ❌ FAILS PLATFORM SUMMARY.** TradeTapp scored "Licensing: All licenses verified" based on its last platform-side verification date. **The MA master plumbing license (#MPL-22417) was last verified on the platform 2026-02-12 — >3 months stale per GC policy.** Re-verify with MA Board of State Examiners of Plumbers before NTP; the platform's "verified" status is not currency-acceptable for execution.
>
> **6. Project-Fit Reading — ❌ FAILS PLATFORM SUMMARY.** TradeTapp produced a generic risk score (78 / Yellow). It does not know that Brookline MOB is an occupied-healthcare TI with project-specific insurance uplift (GL aggregate $4M not $2M; umbrella $10M not $5M; CPL $1M required for refrigerant recovery; ICRA program required). **Re-scored against the Brookline MOB project-specific risk profile: the sub is Approved-with-Conditions but with three additional pre-NTP conditions (CPL procurement, GL/Umbrella uplift, ICRA addendum) that the platform's generic risk score missed entirely.**
>
> ## FINAL GC-ACCEPTED RECOMMENDATION
>
> **Approved with Conditions** (matches platform recommendation directionally) **— but with five pre-NTP conditions where the platform identified zero:**
>
> 1. CPL $1M policy (platform missed — generic risk score)
> 2. CG 20 37 completed-ops endorsement (platform marked compliant on broker checkbox; redline corrected)
> 3. GL aggregate $4M + Umbrella $10M (platform missed — project-specific uplift)
> 4. ICRA program addendum (platform missed — project-specific uplift)
> 5. Re-verify MA master plumbing license currency (platform marked verified on stale date; redline corrected)
>
> Plus two execution-phase subcontract conditions (monthly OSHA 300 + EMR update; weekly ICRA-zone audit) that elevate the platform's "monitor through 2026" suggestion to an enforceable subcontract obligation.
>
> ## PROVENANCE
>
> - **Platform:** TradeTapp + Procore Prequalification, AI version per 2026-Q2 release notes
> - **Platform risk score:** 78 / 100 (Yellow — Approved with Conditions)
> - **Redline changes:** 4 of 6 dimensions adjusted (endorsement literal-text; EMR trend escalated; licensing currency stale; project-fit re-scored). 1 of 6 dimensions confirmed (bonding currency). 1 of 6 dimensions noted-but-accepted (financial independence — review-level vs. audit-level).
> - **Final GC recommendation:** Approved with Conditions, 5 pre-NTP + 2 execution-phase (vs. platform's "standard conditions; monitor EMR").
> - **Disclaimer:** This redline is AI-assisted; insurance endorsements still require carrier verification before subcontract execution.
