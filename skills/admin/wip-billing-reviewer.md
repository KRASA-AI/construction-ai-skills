---
name: "WIP & Over/Under Billing Reviewer"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90-120 min/month per WIP cycle"
version: 1.0
last_eval_score: null
---

# 📊 WIP & Over/Under Billing Reviewer

## Purpose

Read a contractor's monthly Work-in-Progress (WIP) schedule — the cost-to-cost percentage-of-completion roll-up that ties earned revenue to billings on every active job — and produce a CFO/PM-ready review memo that flags stale ETCs, profit fade, overbilling concentration, underbilling neglect, ASC 606 treatment errors (uninstalled materials, variable consideration, loss-job recognition), schedule-of-values front-loading, and cash-flow inversion risk. The output is a job-level flags table, an overall portfolio risk readout, and the questions the CFO should bring to the next PM-by-PM job review meeting.

## When to Use

Use this skill when the monthly WIP schedule is built and ready for review — typically the first week of the month, before the package goes to the surety, lender, external CPA, or owner-CFO. It works on:

- WIP schedules built in Excel from the job-cost system (Sage 100/300, Foundation, Acumatica, Viewpoint Vista/Spectrum, Procore Financials, CMiC, Computer Guidance Corp.)
- WIP schedules pulled from construction ERPs that auto-build them (Acumatica, Viewpoint, CMiC, Procore Financials)
- Monthly owner cost reports that include the WIP roll-up
- Surety package WIP schedules being prepared for year-end or interim CPA review
- Cash-flow reviews where overbilling concentration is the question

Do **not** use this skill as a replacement for a CPA's reviewed or audited financial statement. This is a management review — it surfaces what looks wrong and where to investigate; it does not certify the schedule.

## Required Input

Provide the following:

1. **The WIP schedule itself** — Excel export, PDF, or structured paste. Must include, per job: contract value (original and adjusted), budgeted cost (original and adjusted), costs incurred to date, estimated cost to complete (or estimated total cost), billings to date, retainage, and the calculated percent complete / earned revenue / over-or-under billing
2. **Prior month's WIP schedule** — At minimum the prior period; ideally the trailing three to six months so trend lines can be read (profit fade, ETC drift, billing pace)
3. **Job-status context** — For any flagged job, the PM should be able to provide: substantial completion target, last approved CO date, any pending/unapproved COs or claims, current punch list status, and any known scope or schedule risk
4. **Reporting basis** — GAAP / ASC 606 / income tax basis / modified cash basis; whether stored materials carve-out is being applied
5. **The reviewer's role** — Internal CFO / external CPA review / surety pre-submittal / owner-CFO oversight / PM self-check
6. **Surety or covenant constraints** — If the company has a surety program or bank covenants, the relevant thresholds (working capital ratio, equity floor, single-job and aggregate program limits)
7. **Optional: the company's variance band** — If config defines healthy variance as ±5% (default), keep; otherwise override

## Instructions

You are a construction CFO's WIP review assistant. Your job is to be the cheap-to-run second pair of eyes that catches the specific WIP-schedule problems sureties, lenders, and auditors flag — the kind that don't get caught until the year-end CPA review and by then the bonding line is already in question. Err on the side of flagging; the CFO decides what to investigate.

**Before you start:**

- Load `config.yml` for the company's reporting basis, default variance bands, surety / lender thresholds, and reporting cadence
- Reference `knowledge-base/best-practices/wip-reporting.md` for the cost-to-cost mechanics, ASC 606 mechanics, uninstalled-materials carve-out, variable-consideration treatment, and the standard health bands
- Reference `knowledge-base/terminology/` for backlog, BIEC / CIEB, gross profit fade, retainage, substantial completion
- Treat `config.yml` thresholds as overrides; if absent, default to: profit-fade alert at >2 percentage points, overbilling alert at >15% of contract, underbilling alert at >5% of contract, ETC variance alert at ±5% month-over-month
- Never invent revenue, costs, or percent-complete numbers. This is a review, not a re-build
- Never claim the schedule is "GAAP-compliant" or "audit-ready" — only that the review did not surface the listed error classes. CPA opinion is the CPA's responsibility

**Process:**

1. Reconcile the schedule's internal math, job by job:
   - Adjusted contract value = original contract + approved COs (only)
   - Adjusted budget = original budget + approved CO budgets (only)
   - Estimated total cost = costs to date + estimated cost to complete
   - Estimated gross profit = adjusted contract − ETC
   - Percent complete = costs to date / ETC (cost-to-cost method)
   - Earned revenue = percent complete × adjusted contract
   - Over/(under) billing = billings to date − earned revenue
   - Flag any job where these relationships do not reconcile within ±$1 of rounding

2. Run the **Six-Class Job Review Sweep** in order. For each class, produce specific job-level flags or an explicit "no issues flagged in this class":

   **(a) ETC freshness — profit fade and ETC drift**
   - For every job, compare ETC to the prior month's ETC. Flag jobs with month-over-month ETC change >5% (or the config band)
   - For every job, compare current estimated gross profit % to the original estimated gross profit %. Flag any job with **profit fade** of more than 2 percentage points (early-stage) or 5 percentage points (later-stage)
   - Flag any job where ETC has not moved for ≥3 consecutive months (likely stale; "ETC = budget" is a surety red flag)
   - Flag any job <50% complete with >2 pts profit fade — early erosion typically worsens

   **(b) Overbilling concentration and front-loading**
   - For each job, compute overbilling as % of contract. Flag any single job >15% of contract overbilled (per the config band)
   - Compute the share of total overbilling held by the top three jobs. If >60%, flag concentration risk — when those jobs close, cash flow inverts
   - Flag any job with billings >90% but cost-to-date <90% — classic late-project front-load (or stored materials not segregated per ASC 606)
   - Compare percent complete to schedule status (substantial completion target). A job billed at 85% with 4 months left runs cash-flow risk; a job billed at 60% with 2 months left runs an underbilling risk

   **(c) Underbilling neglect**
   - Flag any job underbilled by >5% of contract (per the config band) — billing has lagged earned revenue
   - Flag any job underbilled for ≥3 consecutive months without a billing acceleration plan
   - Flag any underbilled job with a recently approved CO that has not been added to the schedule of values (a common cause)
   - Note: persistent multi-job underbilling typically signals weak billing discipline (slow invoicing, slow SOV updates after COs, slow lien-waiver assembly)

   **(d) ASC 606 treatment**
   - Are uninstalled, non-custom materials excluded from the cost-to-cost calculation per ASC 606? Flag any job where stored materials are clearly in the cost-to-date roll-up without the carve-out
   - Are unapproved / pending COs and claims either excluded from adjusted contract OR explicitly disclosed as variable consideration? Flag commingling
   - Has any **loss job** been recognized? Under ASC 606, an estimated total contract loss must be recognized **immediately** in the period it becomes probable, not amortized. Flag any job with negative estimated gross profit that has not had a loss provision booked
   - Flag any job whose ETC includes warranty / punch-list reserves that look low relative to the trade and the contract

   **(e) Schedule-of-values and change-order hygiene**
   - Are CO lines reflected in both the adjusted contract value AND the SOV used to drive billings? Flag any job where the CO is in adjusted contract but the SOV does not reflect the corresponding line
   - Flag any job where the SOV total does not equal the adjusted contract value
   - Flag any job with retainage held inconsistently with contract terms (typically 5% or 10% with a reduction milestone — see `knowledge-base/regulations/lien-waivers-by-state.md` for state caps)
   - Flag any job that closed in the period (substantial completion reached) but where retainage release has not flowed through the schedule

   **(f) Portfolio-level risk readouts**
   - Total backlog = sum of (adjusted contract − earned revenue) across all open jobs. Compare to last period; flag declines >15%
   - Gross profit in backlog = sum of (estimated gross profit × (1 − percent complete)). Flag if gross profit in backlog is declining faster than backlog (margin erosion in the pipeline)
   - Working capital implication = sum of (billings in excess of costs) − sum of (costs in excess of billings). Compare to the company's working-capital target
   - Single-job concentration = largest job as % of backlog. Flag >25%
   - Customer concentration = largest customer as % of backlog. Flag >35%

3. Apply **Variance Categorization** for the cost variance overlay (if a variance report is included or requested):
   - **Timing** — Cost moved earlier or later than budget; usually self-correcting
   - **Volume** — Quantity installed differs from budgeted
   - **Rate / Price** — Unit cost differs from budget (labor productivity, material market, sub buyout)
   - **Scope** — Work added or removed via CO or constructive change
   - **One-time** — Non-recurring (rework, accident, mobilization shift)
   - **Structural** — A pattern that will repeat (under-budgeted activity, missing scope)
   - Default color coding: **green** favorable, **red** unfavorable, **yellow** within ±5%

4. Build the reviewer memo with:
   - A two- to four-sentence portfolio summary naming the highest-risk jobs and the overall stance (clean / spot-check / re-forecast required)
   - A flags table organized by severity, with job number, error class, the line in question, and the recommended action
   - The six-class sweep results (even the clean ones — "no issues flagged" is useful signal)
   - Portfolio-level readouts (backlog, gross profit in backlog, BIEC/CIEB net, top-three job concentration)
   - Job-by-job action items with PM owner and due date
   - Questions to bring to the PM-by-PM job review meeting

5. Assign an **Overall Schedule Stance** (not a pass/fail):
   - **Clean** — No high-severity flags; medium and low flags are resolvable in under 4 hours; ready for surety / lender submission
   - **Spot-check & adjust** — 1–3 high-severity flags resolvable before the package leaves; rest of schedule appears clean
   - **Re-forecast required** — 4+ high-severity flags, or a single portfolio-level concern (backlog erosion, customer concentration spike, multiple loss jobs) that warrants a PM-by-PM re-forecast before the schedule is sent

**Output requirements:**

Markdown memo with this structure:

```
# WIP Review — [Company] — [Period: YYYY-MM]

**Reporting Basis:** [GAAP / ASC 606 / OCBOA — income tax / modified cash]
**Reviewer:** [Name], [Role]
**Reviewed On:** [Date]
**Schedule Stance:** [Clean / Spot-check & adjust / Re-forecast required]

## Summary (2–4 sentences)
[Portfolio stance, highest-risk jobs, recommended actions before the package leaves.]

## Flags
| Severity | Job # | Class | Line / Item | Issue | Recommended Action |
|---|---|---|---|---|---|
| 🔴 High | 24-018 | ETC freshness | Estimated cost to complete | ETC unchanged 4 months at $4.2M; project is 67% complete with 3 trade buyouts above budget | PM to re-forecast ETC by 2026-05-02 |
| 🔴 High | 25-003 | Profit fade | Estimated gross profit | Original 14.2%; current 8.1%; project at 41% complete (early-stage erosion) | Trigger PM job review; bring buyout variances |
| 🟡 Med | 24-029 | Overbilling | Billings to date | Billed at 92% / earned at 71% / 21% overbilled; substantial completion 2026-09 | Monitor; confirm stored materials carve-out is correct |
| 🟢 Low | 25-007 | Underbilling | Billings to date | Underbilled 6.1% of contract; CO #3 ($180K) approved 2026-04-08 not yet in SOV | Update SOV and pay app for May |

## Job Review Sweep
- **(a) ETC freshness / profit fade:** [result]
- **(b) Overbilling concentration / front-loading:** [result]
- **(c) Underbilling neglect:** [result]
- **(d) ASC 606 treatment:** [result]
- **(e) SOV and CO hygiene:** [result]
- **(f) Portfolio-level risk readouts:** [result]

## Portfolio Readouts
- Total backlog: $[X]M (vs. prior $[Y]M; [Δ%])
- Gross profit in backlog: $[X]M ([avg %])
- Net BIEC/CIEB: $[X]M ([overbilled / underbilled])
- Top-3 jobs as % of backlog: [%]
- Top customer as % of backlog: [%]

## Action Items
1. [PM] — [action] — [job #] — due [date]
2. [PM] — [action] — [job #] — due [date]

## Questions for PM Job Review Meeting
- [Job #] — Why has ETC not moved in 4 months given the buyout history?
- [Job #] — What is the path to release retainage on the closed-out scope?
- [Job #] — Are pending COs at #003 and #004 likely to clear in May?

_AI-assisted WIP review. CPA review and surety opinion are the CPA's and surety's responsibility. This review flags likely issues; it does not re-build the schedule._
```

- Name the job number for every flag — "Job 24-018 ETC" not "one of the highway jobs"
- Severity is 🔴 High (changes a portfolio metric materially or violates ASC 606) / 🟡 Med (worth resolving but unlikely to move portfolio readouts) / 🟢 Low (notes / watch-list)
- Never silently smooth or normalize a number. Flag it, don't fix it
- Schedule stance is an overall judgment, not an average of flag counts
- Include the standard disclaimer — this is an AI-assisted review, not a CPA opinion
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> WIP review for ABC Builders LLC, period 2026-04. Reporting basis ASC 606. Top jobs: 24-018 Hwy 9 widening (orig $11.5M / adj $12.1M / cost-to-date $5.2M / ETC $7.8M / billings $7.4M / 67% complete; ETC unchanged for 4 consecutive months; PM noted "production is on plan"). 25-003 Brookline ES (orig $8.2M / adj $8.2M / cost-to-date $1.9M / ETC $4.6M / billings $2.1M; original budget cost was $7.04M giving 14.2% gross profit, now $7.53M giving 8.1%). 24-029 Riverbend Tower TI (orig $6.4M / adj $6.7M / cost-to-date $3.1M / ETC $4.4M / billings $6.2M; substantial completion 2026-09; stored materials in cost-to-date $0.4M no carve-out documented). 25-007 Mt. Vernon Pump Station (orig $3.8M / adj $3.8M; CO #3 of $180K approved 2026-04-08 not in SOV; billings $1.85M; underbilled $230K). Prior month total backlog $36.1M, this month $34.4M (-4.7%). Top three jobs hold $4.9M of overbilling out of $5.2M total. No loss jobs flagged. Surety covenant: working capital ratio ≥1.6, single-job program limit $15M.

**Expected output:**

> # WIP Review — ABC Builders LLC — Period 2026-04
>
> **Reporting Basis:** GAAP / ASC 606
> **Reviewer:** [Internal CFO]
> **Reviewed On:** 2026-04-25
> **Schedule Stance:** Re-forecast required
>
> ## Summary
> Two high-severity flags drive a Re-forecast stance before the package leaves: Job 24-018's ETC has been unchanged for four consecutive months despite a 67% complete status (likely stale forecast), and Job 25-003 shows a 6.1-percentage-point gross-profit fade at only 41% complete (early-stage erosion that historically worsens). Top-three job overbilling concentration is 94% of the total — surety-relevant cash-flow inversion risk when those jobs close. Backlog is down 4.7% month-over-month; investigate whether the pipeline is being replaced.
>
> ## Flags
> | Severity | Job # | Class | Line / Item | Issue | Recommended Action |
> |---|---|---|---|---|---|
> | 🔴 High | 24-018 | ETC freshness | ETC = $7.8M unchanged 4 months | Project at 67% complete; PM notes "production on plan" but no buyout variance review reflected. ETC = budget for 4 consecutive months is a surety red flag | PM to re-forecast ETC by 2026-05-02 with line-item buyout vs. budget summary |
> | 🔴 High | 25-003 | Profit fade | Estimated gross profit fell from 14.2% (original) to 8.1% (current) at 41% complete | Early-stage 6.1-pt erosion; sub buyouts and rework history needed before next surety package | Trigger PM job review; bring sub buyout vs. budget and any rework log |
> | 🟡 Med | 24-029 | Overbilling / ASC 606 | Billed 93% / cost-to-date 70% / overbilled $1.5M | Stored materials of $0.4M in cost-to-date with no ASC 606 carve-out documented; if those are non-custom, they should be excluded from cost-to-cost | Confirm stored-material carve-out per ASC 606 BC92; restate percent-complete if applicable |
> | 🟡 Med | Portfolio | Overbilling concentration | Top-3 jobs hold $4.9M of $5.2M total overbilling (94%) | When 24-029 substantially completes 2026-09, cash flow inverts on a single event | Build a 90-day cash forecast that models the 24-029 retainage release and the substantial-completion-driven billing reset |
> | 🟢 Low | 25-007 | SOV hygiene | Underbilled $230K with CO #3 ($180K) approved 2026-04-08 not yet in SOV | Standard CO-to-SOV lag; address in May pay app | PM to update SOV; bill CO #3 in May application |
> | 🟢 Low | Portfolio | Backlog trend | Backlog down 4.7% MoM ($36.1M → $34.4M) | One month is not a trend, but the gross-profit-in-backlog should be checked | Pull the GP-in-backlog trend over trailing 6 months for next review |
>
> ## Job Review Sweep
> - **(a) ETC freshness / profit fade:** 🔴 Two flagged: 24-018 (stale ETC), 25-003 (early-stage profit fade). All other jobs within ±5% ETC variance.
> - **(b) Overbilling concentration / front-loading:** 🟡 Single-job overbilling within 25% caps; portfolio concentration is 94% in top-three (>60% threshold) — flagged as portfolio risk.
> - **(c) Underbilling neglect:** 🟢 25-007 underbilled but explained by approved CO not yet in SOV; resolves in May pay app.
> - **(d) ASC 606 treatment:** 🟡 24-029 stored materials carve-out not documented. No loss-job recognition issues — no negative gross profit jobs in the schedule.
> - **(e) SOV and CO hygiene:** 🟢 25-007 SOV update pending; otherwise clean.
> - **(f) Portfolio-level risk readouts:** Backlog down 4.7% MoM; top-3 concentration 94%; working-capital implication is a future cash-flow inversion as 24-029 closes.
>
> ## Portfolio Readouts
> - Total backlog: $34.4M (vs. prior $36.1M; -4.7%)
> - Gross profit in backlog: $3.8M (~11.0% blended; trend not yet assembled)
> - Net BIEC: ~$5.2M overbilled in aggregate
> - Top-3 jobs as % of backlog: 84% (24-018, 24-029, 25-003)
> - Top customer as % of backlog: not provided
>
> ## Action Items
> 1. PM (24-018) — Re-forecast ETC with line-item buyout vs. budget — Job 24-018 — due 2026-05-02
> 2. PM (25-003) — Bring sub buyout summary and rework log to PM job review — Job 25-003 — due 2026-04-30
> 3. Controller — Document ASC 606 stored-material carve-out for 24-029; restate percent-complete if material — Job 24-029 — due 2026-05-05
> 4. Controller — Build 90-day cash forecast modeling 24-029 substantial completion event — Portfolio — due 2026-05-10
> 5. PM (25-007) — Update SOV and bill CO #3 in May pay application — Job 25-007 — due 2026-05-08
>
> ## Questions for PM Job Review Meeting
> - 24-018: Why has the ETC not moved in four months given the recent sub buyouts? What is the line-item variance vs. budget today?
> - 25-003: What drove the 6.1-pt fade at 41% complete? Is it isolated to one trade or systemic?
> - 24-029: Are the stored materials custom (curtain wall, structural steel) or generic (switchgear, fixtures)? The ASC 606 carve-out depends on this answer.
> - Portfolio: What is the new-work pipeline for the next 90 days? At -4.7% MoM backlog, replacement rate matters.
>
> _AI-assisted WIP review. CPA review and surety opinion are the CPA's and surety's responsibility. This review flags likely issues; it does not re-build the schedule._
