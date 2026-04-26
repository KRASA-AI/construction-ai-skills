# WIP Reporting & Over/Under Billing — Reference

> Reference for skills that read or produce monthly Work-in-Progress (WIP) schedules
> and over/under billing analyses for construction contractors.

## Why WIP Reporting Matters

A WIP schedule reconciles three numbers for every active job:

1. **Earned revenue** — how much of the contract value the contractor has earned based on progress
2. **Billed revenue** — how much the contractor has invoiced the owner (typically via AIA G702/G703 or equivalent)
3. **The difference (over- or under-billing)** — the cash-flow signal

Sureties, lenders, CFOs, and external CPAs read the WIP schedule monthly. It is the single most important contractor financial document outside the year-end financials. In 2026, sureties will accept AI-generated WIP schedules **provided** the percentage-of-completion methodology is documented and ASC 606 inputs are clearly traceable.

## ASC 606 Five-Step Model (Construction Application)

Effective for all contractors on US GAAP, ASC 606 *Revenue from Contracts with Customers* governs how revenue is recognized over time. The five steps applied to a typical construction contract:

1. **Identify the contract** — Owner-prime contract or GC-subcontract; the parties, the price, the payment terms.
2. **Identify performance obligations** — Most construction contracts contain a single integrated performance obligation (the completed building / system / scope), even when broken into many SOV line items. Distinct, separable obligations (e.g., a separate maintenance period after substantial completion, or a clearly distinct training deliverable) are accounted for separately.
3. **Determine the transaction price** — Contract sum + executed change orders + variable consideration estimates (unapproved COs, claims, incentive fees) reduced for any constraint on variable consideration.
4. **Allocate the transaction price** — For a single performance obligation this is a single number; otherwise allocate by relative standalone selling prices.
5. **Recognize revenue over time** — For most construction contracts, revenue is recognized **over time** (not at completion) because the work creates an asset the customer controls as it is created (most construction work) or because the work is custom and the contractor has the right to payment.

The cost-to-cost (input) method is the default measurement of progress for most general-contractor and subcontractor work. Output methods (units delivered, milestones) are appropriate for repetitive work or contracts with explicit progress milestones.

## Cost-to-Cost Percentage of Completion

For each active job:

```
Costs Incurred to Date
─────────────────────────────────  =  Percent Complete
Estimated Total Cost (ETC) at Completion
```

Then:

```
Earned Revenue to Date  =  Percent Complete × Total Contract Value
Over/Under Billing      =  Billings to Date − Earned Revenue to Date
```

A **positive** value (billings > earned) is **overbilled** — billing has run ahead of cost; cash-positive but creates a liability on the balance sheet (billings in excess of costs).
A **negative** value (billings < earned) is **underbilled** — costs have run ahead of billing; cash-negative and creates an asset on the balance sheet (costs in excess of billings).

Both conditions are normal in healthy construction; the question is the *trend* and the *magnitude relative to the contract*.

## Estimated Total Cost (ETC) — The Most Critical Input

The accuracy of the WIP schedule depends entirely on the ETC. ETC must be **revised** every period based on:

- Actual production rates vs. budget
- Subcontractor change orders (executed and pending)
- Realized loss exposure on fixed-price scope
- Approved owner change orders (which adjust contract value but may also change ETC)
- Cost reports from the field, not just AP postings

A stale ETC produces a misleading WIP. The most common contractor mistake is treating the original budget as the ETC, even after the project has materially evolved. Sureties scrutinize "ETC = original budget for 6 consecutive months" as a red flag.

## Uninstalled Materials (Stored Materials)

Per ASC 606, the cost of **uninstalled materials** that are *not* customizing the project (e.g., generic switchgear, stock fixtures, raw steel awaiting erection) is **excluded** from the cost-to-cost numerator and the ETC denominator. Revenue is recognized only at the cost of those materials (zero margin) when transferred. This is one of the most-missed ASC 606 changes from legacy percentage-of-completion accounting and a frequent finding in CPA reviews.

Uninstalled materials that *are* customized for the project (custom curtain wall, fabricated structural steel, custom millwork) **remain** in the cost-to-cost calculation.

## Standard WIP Schedule Columns

A complete WIP schedule includes, per job:

| Column | What it is |
|---|---|
| Job number, job name, job type, PM | Identity |
| Original contract value | Pre-CO contract sum |
| Approved CO total | Executed change orders only |
| Adjusted contract value | Original + approved COs |
| Original budget | Pre-CO budgeted cost |
| Approved CO budget | Cost portion of executed COs |
| Adjusted budget | Original + approved COs |
| Costs incurred to date | Direct + indirect, period-cumulative |
| Estimated cost to complete (ETC remaining) | Forward-looking |
| Estimated total cost (ETC) | Costs to date + ETC remaining |
| Estimated gross profit | Adjusted contract − ETC |
| Estimated gross profit % | Gross profit / adjusted contract |
| Percent complete | Costs to date / ETC |
| Earned revenue to date | Percent complete × adjusted contract |
| Billings to date | Cumulative G702 line 6 |
| Over/(under) billing | Billings − earned |
| Receivables | A/R for this job |
| Retainage | Held back by owner |

Some contractors track unapproved change orders, claims, and pending COs in separate columns under "variable consideration" rather than mixing them into adjusted contract value — this is the conservative ASC 606 treatment.

## Health Bands (Heuristics, Not Rules)

| Indicator | Healthy | Investigate | Action Required |
|---|---|---|---|
| Variance vs. last month's ETC | ±5% | ±5–10% | >10% |
| Gross profit fade (vs. original) | <2 pts | 2–5 pts | >5 pts |
| Overbilling as % of contract | <15% | 15–25% | >25% — possible front-loading or understated cost |
| Underbilling as % of contract | <5% | 5–10% | >10% — billings are lagging earned |
| Job over 90% billed but <90% complete | n/a | flag | flag — common late-project front-load |
| Job under 50% complete with >2 pts profit fade | n/a | flag | flag — early profit erosion typically worsens |

Surety underwriters typically focus on **profit fade** (a job whose estimated gross profit % is dropping period over period) and **overbilling concentration** (a few large jobs holding most of the overbilling — when those jobs close, cash flow inverts).

## Surety / CPA Disclosure Requirements

Most contractors submitting financials to a surety provide a WIP schedule that complies with the AICPA *Audit and Accounting Guide for Construction Contractors* and discloses:

- The percentage-of-completion method used (cost-to-cost is presumed unless stated)
- The treatment of uninstalled materials
- The treatment of variable consideration (unapproved COs, claims, incentive fees)
- A description of any significant judgments (constraint on variable consideration, performance obligation determination)
- The two backlog metrics: **total backlog** (signed contract less earned) and **gross profit in backlog**
- A reconciliation of **billings in excess of costs** (liability) and **costs in excess of billings** (asset) to the trial balance

For private contractors not reporting under US GAAP, an **OCBOA** (other comprehensive basis of accounting — typically the income tax basis or modified cash basis) WIP schedule is acceptable, but most sureties prefer GAAP.

## Common WIP Mistakes

1. **Stale ETC** — never re-forecasting; treating budget as ETC.
2. **Including pending or unapproved COs in adjusted contract value** without applying ASC 606 variable-consideration constraint.
3. **Including unapproved CO costs in costs incurred but not in adjusted contract value** — inflates costs, deflates margin.
4. **Double-counting retainage** — once as a receivable, once as a deduction in the WIP.
5. **Mixing job types in one schedule** — T&M and lump-sum mechanics differ; T&M jobs should be separately reported or carved out, since cost-to-cost is not the right measure for T&M.
6. **Stored material cost in cost-to-cost** without the ASC 606 carve-out for uninstalled non-custom material.
7. **Closing out jobs that still have warranty or punch-list cost exposure** — leaves cost-to-complete underestimated.
8. **Ignoring loss-job recognition** — under ASC 606, an estimated total contract loss must be recognized **immediately** in the period it becomes probable, not amortized.

## Variance Categories for Variance Reports

When generating a monthly cost variance report alongside the WIP, use these categories:

- **Timing** — Cost incurred earlier or later than budget; usually self-correcting.
- **Volume** — Quantity installed differs from quantity budgeted.
- **Rate / Price** — Unit cost differs from budget; often driven by labor productivity, material market, or sub buyout.
- **Scope** — Work added or removed via change order or constructive change.
- **One-time** — Non-recurring (rework, accident, mobilization shift).
- **Structural** — A pattern that will repeat (under-budgeted activity, missing scope).

Color coding by convention: **green** = favorable, **red** = unfavorable, **yellow** = within ±5% (no action).

## Cash-Flow Implications

Overbilling generates cash today at the cost of a future cash drag. A contractor whose business is *in aggregate* significantly overbilled is borrowing from future projects to fund current operations. When that pipeline shrinks, the cash flow inverts.

Underbilling, conversely, ties up working capital. Subs and GCs with persistent underbilling on multiple jobs often have weak billing discipline (slow invoicing, delayed schedule of values updates after change orders, slow lien waiver assembly delaying owner approval).

## Useful References

- AICPA Audit and Accounting Guide — Construction Contractors
- FASB ASC 606 Revenue from Contracts with Customers
- AICPA Construction Contractor Industry Guide (annual updates)
- AGC Financial Issues Forum (industry CPA group)
- Construction Financial Management Association (CFMA) — Annual Financial Survey

## Glossary (Quick Reference)

- **Backlog** — Signed contract value not yet earned. Total backlog = adjusted contract − earned revenue across all open jobs.
- **Billings in excess of costs (BIEC)** — Liability; appears on the balance sheet when overbilled.
- **Costs in excess of billings (CIEB)** — Asset; appears on the balance sheet when underbilled.
- **Gross profit fade** — Decline in estimated gross profit % from one period to the next on the same job.
- **Percentage-of-completion (POC)** — Revenue recognition method that recognizes revenue over time as the contractor performs.
- **Substantial completion** — The point at which the owner can use the work for its intended purpose; typically triggers retainage release and warranty start.
- **Variable consideration** — Contract amounts not yet fixed (unapproved COs, claims, incentives, liquidated damages); recognized only to the extent it is probable a significant reversal will not occur.

---

*Last updated: 2026-04-25. References AICPA construction guide and ASC 606 as in effect April 2026.*
