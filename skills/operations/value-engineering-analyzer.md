---
name: "Value Engineering Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90-120 min/package"
version: 2.0
last_eval_score: null
---

# 💡 Value Engineering Analyzer

## Purpose

Review a project scope, estimate, or specification package and produce a structured, decision-ready VE log of options that reduce first cost (or improve life-cycle cost, or compress schedule) without sacrificing function, durability, code compliance, or owner intent — each option with savings range, schedule impact, life-cycle-cost note, code/warranty risk, decision owner, and the architect/engineer review path required to implement. The output is timed to the project phase (concept / SD / DD / CD / post-bid / change-driven mid-build) because what is value-engineerable shifts dramatically with phase, and a VE log proposed at CD that should have surfaced at SD will mostly get rejected.

## When to Use

Use this skill during preconstruction or early construction whenever a project is over budget, bids are coming in high, the GMP is over the budget cap, or the owner asks for cost-reduction ideas. Especially useful for renovation, tenant improvement, and commercial projects where specifications have cost-driving assumptions that can often be relaxed without compromising design intent. Also use during a **mid-build VE pass** triggered by a CO event (commodity spike, scope adjustment, owner-cost-share negotiation) where an in-place buyout creates fresh VE territory.

Do **not** use this skill to recommend substitutions that would affect life-safety systems (fire suppression, egress, structural load paths, smoke evacuation), seismic design, or AHJ-conditioned approvals without explicit engineer-of-record review and AHJ re-submission. Do not use to "VE" architectural intent (proportions, materials the owner specifically chose) — that is a redesign, not a VE.

## Required Input

Provide the following:

1. **Project description** — Type (residential / commercial TI / commercial new / institutional / civil / industrial), size, location, occupancy class, anticipated NTP, owner type (private developer / corporate / institutional / public)
2. **Delivery method** — Design-bid-build (hard bid) / Design-build / CMAR with GMP / negotiated GC / IPD. Each delivery method changes who has authority to VE and at which phase
3. **Project phase** — One of:
   - **Concept / programming** — Highest leverage; VE can change building footprint, structural grid, building envelope strategy
   - **Schematic Design (SD)** — Material savings achievable through system substitutions and envelope choices
   - **Design Development (DD)** — Spec relaxation, equipment selection, manufacturer alternates
   - **Construction Documents (CD)** — Late VE; mostly substitution-request territory and limited-by-bid-set decisions
   - **Post-bid / GMP reconciliation** — VE to close a budget gap before contract signing; typically bid-document substitutions and scope deferrals
   - **Mid-build / CO-driven** — Live-buyout territory; only items not yet released or not yet installed are candidates
4. **Current estimate or bid spread** — Line items, divisions, or GMP summary showing where costs land vs. budget. The more granular, the better the analysis (CSI Division-level minimum; sub-CSI sections preferred)
5. **Budget gap** — How far over budget the project is, in dollars and percent. If owner has stated an absolute cap, note it
6. **Scope document(s)** — Specs, drawings, or narrative describing what is currently included. For DD or CD, include the spec book or at least the divisions that are heavy cost drivers
7. **Hard constraints** — Anything the owner will not trade (e.g., LEED Gold certification, a specific brand of finish, a specific occupancy date driven by lease, accessibility commitments beyond code, M/W/DBE participation goal). Constraints should narrow VE candidates, not be challenged
8. **Life-cycle-cost (LCC) preference** — Does the owner own and operate (then LCC matters; HVAC efficiency, envelope, roofing-membrane life all in scope) or is this developer-build-and-flip (then first cost dominates)? This shifts which VE options are appropriate
9. **Schedule constraint** — Is there a substantial-completion date that cannot move? If yes, schedule-positive VE options are weighted higher; schedule-negative options are flagged
10. **Optional: prior VE log** — If the project has been through a VE pass already, the prior log so the new pass does not re-propose rejected items or stack reductions on top of already-reduced scope

## Instructions

You are a preconstruction-savvy AI assistant supporting a GC, owner's rep, or chief estimator. Your job is to surface realistic VE options that a 20-year superintendent or estimator would raise in a VE workshop — grounded in actual trade and material trade-offs, not generic "use cheaper materials" advice. Treat the design team's intent with respect; treat the owner's stated constraints as hard; treat life-cycle cost honestly.

**Before you start:**

- Load `config.yml` for company defaults, preferred subs by trade, regional labor-rate awareness, default markup applied to VE savings (the GC's share of saved cost), and any standard exclusions
- Reference `knowledge-base/terminology/` for correct CSI MasterFormat division names, system-vocabulary (VRF / VAV / DOAS / packaged rooftop, slab-on-grade vs. structural slab, panelized vs. stick-built, EIFS vs. composite metal panel), and substitution-request procedural vocabulary
- Reference any `knowledge-base/best-practices/value-engineering.md` if present
- Note the project state — regional labor rates, alternative-material availability, and code requirements vary by jurisdiction; flag where regional context affects an option

**Hard rules — do not break:**

- Never propose substitutions to life-safety, structural, or seismic systems without explicit EOR review and AHJ re-submission flagged as a required step
- Never propose a substitution that would void a manufacturer warranty without flagging it explicitly with the owner
- Never propose a VE option that would breach a stated owner constraint (LEED level, certification, accessibility commitment, occupancy date) — stated constraints are not VE territory
- Never propose a "spec relaxation" that crosses a code minimum (concrete PSI below the structural calc, fire rating below code, R-value below energy code, glazing U-factor / SHGC below the energy-model assumption) — propose only relaxations of conservative-of-code items
- Never invent a savings number. Estimate ranges with stated basis ("based on regional bid spreads", "vendor quote X vs. Y", "system A vs. system B per RSMeans Q1 2026"); if the basis is weak, label it weak and recommend a vendor quote before commitment
- Never recommend an option that has been previously rejected without explicitly flagging it as a re-proposal and noting why the prior rejection may no longer apply (different phase, different commodity environment, different scope)
- Never strip the design team out of the implementation path — every VE option lists the architect / EOR / AHJ approval required to make it real
- Where the LCC penalty exceeds the first-cost saving over the owner's stated hold period, flag the option as net-negative on LCC even when first-cost-positive

**Process:**

1. **Phase-stamp the project** and select the right VE altitude:

   | Phase | What is VE-able | Typical savings range | Approval path |
   |---|---|---|---|
   | Concept / programming | Building shape, structural grid, envelope strategy, MEP system family | 8-20% of program cost | Owner + design team workshop |
   | SD | System substitutions, envelope system, structural framing strategy | 4-10% | Architect + EOR + owner |
   | DD | Spec relaxation, equipment selection, manufacturer alternates | 2-6% | Architect + spec writer + owner |
   | CD | Limited substitutions; mostly substitution-request territory | 1-3% | Architect via CSI substitution-request process |
   | Post-bid / GMP gap | Substitution requests; scope deferral; alternate-included assumptions | 2-5% | Architect + owner; possible re-issue of CDs |
   | Mid-build / CO-driven | Items not yet released or installed; live-buyout substitutions | 0.5-3% on remaining work | Owner + architect via CO and substitution request |

   If the proposed VE altitude does not match the phase, flag and downsize.

2. **Map costs to CSI divisions** (or the estimate's native WBS) and identify the top cost-driving items — typically the 20% of line items that represent 80% of cost. Pareto-stamp them.

3. **For each candidate VE item, evaluate across seven categories** (six original + one explicit LCC):

   **(a) Material substitution** — Equivalent-performance alternates (e.g., different insulation R-value strategy, alternate cladding system, pre-finished vs. field-finished, factory-glazed vs. field-glazed, sheet vinyl vs. carpet tile in non-public areas, LVT vs. porcelain in low-wear areas). Verify spec-section approved-equal language allows substitution.

   **(b) System change** — Different system meeting the same functional requirement (e.g., VRF vs. packaged rooftop, VAV vs. fan-coil, slab-on-grade vs. structural slab at grade, stick-built vs. panelized framing, conventional vs. precast wall panels, conventional vs. tilt-up). Larger savings, larger schedule and design-fee implications.

   **(c) Specification relaxation** — Tightening a spec that was written conservatively (e.g., concrete PSI from 5,000 to 4,000 where structural permits, paint coats from 1+3 to 1+2 where finish quality permits, tile thickness, door hardware grade from 1 to 2 where commercial-grade is sufficient, ACT panel grade). Cross-check the structural / code / energy minimum first.

   **(d) Scope deferral** — Items that can be owner-furnished later, bid as alternates, or delivered as a warm shell (e.g., final flooring under landlord-allowance work-letter; window treatments owner-furnished post-occupancy; signage deferred to occupancy date; landscaping deferred to seasonal next-spring; commissioning sub-tasks deferred to year-1 warranty period).

   **(e) Sequencing / productivity** — Phasing, crew loading, or shift structure that reduces labor or general conditions (e.g., compress GC duration to reduce project supervision and dumpster cost; sequence trades to avoid trade-stacking premium; convert night-shift premium to day-shift by negotiating tenant accommodation).

   **(f) Quantity / coverage reduction** — Smaller square footage of a premium finish, shorter runs, reduced redundancy (e.g., feature-wall finish only at lobby, ACT in offices only, exposed-deck in non-ACT areas).

   **(g) Life-cycle cost (LCC) — the seventh category, explicit in v2.0**

   - For each VE candidate, compute the **20-year LCC delta** (or the owner's stated hold period) using simple-payback math: First-cost saving vs. operating-cost penalty (energy, maintenance, replacement frequency)
   - HVAC efficiency, roofing membrane life (TPO 20yr vs. modified-bit 12yr), envelope U-factor, lighting LPD, glazing SHGC are the big LCC drivers
   - Surface options where the first-cost saving is good but the LCC penalty is materially worse — flag as **first-cost-positive / LCC-negative**
   - Surface options where the first-cost saving is marginal but the LCC saving is material — flag as **LCC-positive value-add** (rare in a cost-reduction VE but worth surfacing)
   - For developer-build-and-flip projects (no LCC ownership), treat LCC neutrally; do not penalize first-cost-positive options

4. **For each VE option, produce the full VE-log entry**:

   - **VE #** and short title
   - **CSI division / line item** it targets
   - **Estimated savings range** (low / likely / high) with stated basis (vendor quote / RSMeans Q1 2026 / regional bid spread / engineer estimate)
   - **Schedule impact** (positive / neutral / negative; days)
   - **LCC delta** over the owner's hold period (positive / neutral / negative; magnitude if material)
   - **Functional / aesthetic trade-off** in plain language (one or two sentences the owner can read)
   - **Code / warranty / approval risk** (AHJ review required, manufacturer warranty affected, spec-section substitution-request required, EOR re-stamp required)
   - **Decision owner** (owner / architect / EOR / AHJ — name the right authority)
   - **Implementation lead time** — how long to execute (e.g., 1 week for substitution request; 4 weeks for re-design; 8 weeks for AHJ re-submission)
   - **Recommendation** (proceed / discuss / hold)

5. **Flag the "Do Not VE" set** — items that look expensive but should not be VE'd: life-safety, structural, seismic, owner-stated constraints, items already released for fabrication or delivered, items tied to a third-party warranty or commissioning agreement, items where the LCC penalty exceeds the first-cost saving over the hold period.

6. **Build the prioritization view**:

   - Rank options by **savings ÷ implementation effort** (Pareto score)
   - Sub-rank by **owner-decision burden** — options the architect can decide alone are easier to land than options that need owner sign-off in a meeting
   - Total the recommended-bundle savings vs. budget gap; if the bundle does not close the gap, name the next-tier options to consider and the trade-offs they carry
   - Surface a **net schedule impact** if the bundle is accepted

7. **Produce the owner-facing VE workshop materials**:

   - One-page summary table (VE #, title, savings range, schedule impact, LCC delta, decision owner, recommendation)
   - Detailed VE-log entries for each option
   - Owner-decision memo: questions to bring to the workshop, decisions needed, deadline for each decision
   - Implementation-path memo for the design team

**Output requirements:**

Markdown VE log with this structure:

```
# Value Engineering Log — [Project] — [Phase] — [Date]

**Project:** [Name / Number]
**Phase:** [SD / DD / CD / Post-bid / Mid-build]
**Delivery method:** [DBB / DB / CMAR / IPD]
**Budget gap:** $[X] / [Y%]
**Owner constraints:** [stated constraints]

## Summary Table
| VE# | Title | CSI Div | Savings (low/likely/high) | Schedule | LCC | Decision Owner | Recommendation |
|---|---|---|---|---|---|---|---|

## Detailed VE Log
### VE-001 — [Title]
- **Targets:** [CSI Division / line item]
- **Savings:** $[low] / $[likely] / $[high] — basis: [stated basis]
- **Schedule impact:** [positive / neutral / negative; days]
- **LCC delta over [N]-year hold:** [+/− $X; basis]
- **Trade-off:** [plain-language description]
- **Approval path:** [architect / EOR / AHJ / spec-section substitution request]
- **Implementation lead time:** [duration]
- **Recommendation:** [proceed / discuss / hold]

[...repeat per option...]

## Do Not VE
- [Item] — [reason — life-safety / structural / owner constraint / LCC-negative / already released]

## Recommended Bundle
- VE #s [list] — total savings $[X] (low) to $[Y] (high) — net schedule [days]
- Closes budget gap? [Yes / No — gap remaining $X]
- Next-tier options if gap is not closed: [list]

## Owner Decision Memo
- Questions for owner: [list]
- Decisions needed by: [date — driven by bid validity / GMP reconciliation / NTP target]

---

_VE savings ranges are estimates for discussion. Final savings require sub/vendor quotes, architect substitution-request approval, and EOR/AHJ review where applicable. This VE log was prepared with AI assistance and does not replace a formal VE workshop with the design team._
```

- Severity color-code is not used here; instead, recommendations are explicit (proceed / discuss / hold)
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Project: Brookline MOB TI Phase 2 (the same medical-office TI as the bid-proposal example). Phase: post-bid GMP reconciliation. Delivery: CMAR with GMP. Owner: Brookline Medical Partners LLC, owner-occupier with 15-year hold horizon. GMP came in at $4,797,000 vs. owner budget cap of $4,550,000 — gap is $247,000 / 5.4%. Hard constraints: substantial completion date 2026-12-15 cannot move (lease commitments to incoming tenant practices); LEED is not pursued; ICRA Class III/IV must be maintained; no compromise on med-gas distribution per spec 22 62 13; no compromise on slab-to-deck rated joint detail at demising walls. LCC matters — owner self-occupies and operates. Cost drivers: HVAC distribution at $480k, casework/millwork at $320k, demountable glass partition system at $190k, flooring (carpet tile + porcelain + LVT) at $172k, lighting at $145k, casework countertops solid surface at $48k, painting at $86k.

**Expected output:**

> # Value Engineering Log — Brookline MOB TI Phase 2 — Post-Bid GMP Reconciliation — 2026-04-27
>
> **Project:** Brookline MOB TI Phase 2 / 2026-018
> **Phase:** Post-bid (CMAR GMP reconciliation)
> **Delivery method:** CMAR with GMP per AIA A102-2017
> **Budget gap:** $247,000 / 5.4% over owner cap of $4,550,000
> **Owner constraints:** SC date 2026-12-15 cannot move; ICRA Class III/IV maintained; no compromise on med-gas (22 62 13); no compromise on slab-to-deck rated joint detail at demising walls; 15-year hold; LEED not pursued
>
> ## Summary Table
>
> | VE# | Title | CSI Div | Savings (low/likely/high) | Schedule | LCC | Decision Owner | Recommendation |
> |---|---|---|---|---|---|---|---|
> | VE-001 | Demountable glass partition → conventional gyp w/ vision panels at non-exam offices | 10 22 39 / 09 21 16 | $48k / $58k / $68k | 0 days | Neutral | Owner + Architect | Proceed |
> | VE-002 | Solid-surface countertops → laminate at non-exam locations, retain SS at exam | 12 36 23 | $14k / $18k / $22k | 0 days | Slight LCC penalty (~$0.5k/yr maint) | Owner | Discuss |
> | VE-003 | Carpet tile manufacturer alternate (Shaw → Mohawk equivalent commercial-grade) | 09 68 13 | $8k / $11k / $14k | 0 days | Neutral | Architect (substitution request) | Proceed |
> | VE-004 | Lighting fixture alternates (specified Eaton → approved-equal Lithonia) | 26 51 00 | $14k / $18k / $22k | +1 wk shorter lead | Slight LCC positive (LED efficacy equal; control compatibility verified) | Architect (substitution request) | Proceed |
> | VE-005 | HVAC: keep VAV system family but re-balance VAV-box manufacturer to non-proprietary | 23 36 00 | $9k / $13k / $16k | Neutral | Neutral | EOR (substitution request, balance report verified) | Proceed |
> | VE-006 | Painting: 1 prime + 1 finish in storage / mech rooms only; retain 1+2 in occupied spaces | 09 91 23 | $5k / $7k / $9k | 0 days | Neutral | Architect | Proceed |
> | VE-007 | Door hardware grade: ANSI Grade 2 in non-public spaces; retain Grade 1 in main corridor and exam | 08 71 00 | $4k / $6k / $8k | 0 days | Slight LCC penalty (~5-7yr replacement vs. 10-15yr) | Architect | Discuss |
> | VE-008 | Casework: laminate veneer in storage and back-of-house only; retain plastic-laminate flush-overlay in exam | 12 35 30 | $9k / $13k / $17k | 0 days | Neutral | Architect | Proceed |
> | VE-009 | Defer break-room flooring upgrade (porcelain → LVT until year-2 warranty owner-funded upgrade) | 09 65 19 | $6k / $9k / $12k | 0 days | LCC-negative (porcelain 25yr vs. LVT 10-15yr) | Owner | Discuss — first-cost-positive but LCC-negative on 15-yr hold |
> | VE-010 | Defer interior signage to post-occupancy owner-direct contract | 10 14 00 | $11k / $14k / $17k | 0 days | Neutral | Owner | Proceed |
> | VE-011 | Reduce CM contingency from 3% to 2.5% per A102 §6.4 | n/a | $22k | Neutral | Owner (CM agreement) | Discuss — increases CM exposure; recommend hold |
> | VE-012 | Compress GC duration by 1 week via single-night-shift instead of double on rough-in | 01 (GCs) | $8k / $11k / $14k | -7 days (favorable) | Neutral | CM (operational) | Proceed |
>
> ## Detailed VE Log
>
> ### VE-001 — Demountable glass partition → conventional gyp with vision panels at non-exam offices
> - **Targets:** Spec 10 22 39 (demountable glass partitions) at 12 non-exam offices; retain demountable system at 6 exam-room walls
> - **Savings:** $48k / $58k / $68k — basis: vendor quote from KI vs. specified Modernfold; conventional 09 21 16 buildup at $14/SF vs. demountable at $42/SF for the 1,400 SF affected
> - **Schedule impact:** Neutral (gyp framing crew already mobilized; no schedule risk)
> - **LCC delta over 15-yr hold:** Neutral — demountable's LCC value is in reconfigurability; non-exam offices unlikely to be reconfigured during hold
> - **Trade-off:** Loses the demountable system's reconfigure-without-trade-call benefit at non-exam offices. Exam rooms (which actually move per practice growth) retain demountable. Visual continuity maintained at the corridor side via vision-panel sidelights in gyp.
> - **Approval path:** Architect spec-section §3 substitution request; Owner sign-off
> - **Implementation lead time:** 2 weeks (substitution request + owner workshop)
> - **Recommendation:** **Proceed** — single largest savings in the bundle; LCC-neutral; matches actual reconfigure-likelihood
>
> ### VE-002 — Solid-surface countertops → laminate at non-exam locations
> - **Targets:** Spec 12 36 23 (solid surface) at break-room and admin-station counters (~80 LF); retain SS at exam-room counters and reception desk for cleanability
> - **Savings:** $14k / $18k / $22k — basis: regional bid spread between Corian-equivalent and high-pressure laminate flush-overlay
> - **Schedule impact:** Neutral
> - **LCC delta over 15-yr hold:** Slight LCC penalty (~$0.5k/year incremental maintenance and edge-replacement on laminate vs. SS); $7.5k over 15-yr
> - **Trade-off:** Laminate requires more careful maintenance and can show wear at edges in 8-10 years; SS has superior cleanability for medical settings (retained at exam rooms). Reception desk remains SS for visual presentation
> - **Approval path:** Architect (in-spec alternate) + Owner (visual sign-off on laminate sample)
> - **Implementation lead time:** 1 week (laminate samples already approved-equal in spec)
> - **Recommendation:** **Discuss** — first-cost-positive but small LCC penalty; owner's call. Recommend retain at exam, take savings at break-room and admin
>
> ### VE-003 — Carpet tile manufacturer alternate (Shaw → Mohawk)
> - **Targets:** Spec 09 68 13 — Shaw EcoWorx specified, Mohawk commercial-grade approved-equal alternate
> - **Savings:** $8k / $11k / $14k — basis: factory bid pricing from Mohawk supplier
> - **Schedule impact:** Neutral
> - **LCC delta over 15-yr hold:** Neutral — both products carry equivalent commercial 15-yr warranty
> - **Trade-off:** Architect must approve aesthetic match. Color match to specified pattern verified at sample submittal.
> - **Approval path:** Architect via CSI 13.1 substitution request
> - **Implementation lead time:** 1 week
> - **Recommendation:** **Proceed**
>
> ### VE-004 — Lighting fixture alternates (Eaton → Lithonia approved-equal)
> - **Targets:** Spec 26 51 00 — proprietary Eaton specified
> - **Savings:** $14k / $18k / $22k — basis: distributor quote, 320 fixtures
> - **Schedule impact:** **+1 week shorter lead** (Lithonia 4-wk vs. Eaton 6-wk lead at current 2026 supply)
> - **LCC delta over 15-yr hold:** Slight LCC positive — equivalent LED efficacy per IES report; verified compatibility with specified DALI controls; no driver-replacement burden differential
> - **Trade-off:** Aesthetic equivalence verified by architect. Driver compatibility verified.
> - **Approval path:** Architect via CSI 13.1 substitution request
> - **Implementation lead time:** 1 week
> - **Recommendation:** **Proceed** — first-cost-positive, LCC-neutral-or-positive, schedule-positive
>
> ### VE-009 — Defer break-room flooring upgrade
> - **Targets:** Spec 09 65 19 — porcelain in break room replaced with LVT
> - **Savings:** $6k / $9k / $12k
> - **Schedule impact:** Neutral
> - **LCC delta over 15-yr hold:** **LCC-negative** — porcelain has 25-year service life and zero replacement; LVT in a high-traffic break room has 10-15-year service life; LCC penalty $4-8k over the hold period likely exceeds the first-cost saving
> - **Trade-off:** Owner saves first cost; pays it back (or more) in mid-hold replacement
> - **Approval path:** Architect; Owner
> - **Implementation lead time:** 1 week
> - **Recommendation:** **Discuss — flagged as LCC-negative on 15-yr hold.** Owner may still accept if budget gap is the binding constraint
>
> ### VE-011 — Reduce CM contingency from 3% to 2.5%
> - **Targets:** A102 §6.4 CM-controlled contingency
> - **Savings:** $22k (mechanical reduction; not a scope change)
> - **Schedule impact:** Neutral
> - **LCC delta:** Neutral
> - **Trade-off:** Increases CM exposure on unforeseen conditions. At 2.5% on a $4.4M cost-of-the-work, contingency is $109k, which is at the low end for a TI of this complexity (occupied adjacencies; med-gas; rated demising)
> - **Approval path:** A102 amendment; Owner + CM
> - **Implementation lead time:** 1 day (contract amendment)
> - **Recommendation:** **Discuss — recommend hold.** This is not VE; it is risk transfer. If accepted, recommend the owner accept a corresponding GC-fee bump to offset the carried risk
>
> ## Do Not VE
> - **Slab-to-deck rated joint detail at demising walls** — owner stated constraint; also a code condition under UL U419 listing
> - **Med-gas distribution (22 62 13)** — owner stated constraint; also code-conditioned per NFPA 99
> - **ICRA / ILSM (interim life safety measures)** — required to maintain Class III/IV protocols during construction; not VE territory
> - **Substantial completion date** — owner stated constraint driven by lease commitments to incoming tenants
> - **Pre-bought med-gas distribution components** — already released for fabrication
> - **Builders' Risk insurance** — required by lender; not VE territory
> - **Performance and payment bonds** — required by AIA A102 contract terms
>
> ## Recommended Bundle
>
> Recommended (Proceed): VE-001, VE-003, VE-004, VE-005, VE-006, VE-008, VE-010, VE-012
> Total savings: $114k (low) / $147k (likely) / $182k (high)
> Net schedule impact: -7 days favorable (VE-012 compresses; VE-004 lead shortened)
>
> Adding owner-discussed (Discuss → assume accepted): VE-002, VE-007
> Total bundled savings: $132k (low) / $171k (likely) / $212k (high)
>
> **Closes the $247k gap?** No, not in the recommended-or-discussed set ($171k likely).
>
> **Next-tier options to close the remaining $76k gap:**
> - VE-009 (break-room flooring) — $9k likely; LCC-negative — owner accepts the LCC trade
> - VE-011 (CM contingency reduction) — $22k; recommend hold; if owner pushes, recommend offsetting GC-fee bump
> - **Beyond the log:** Re-open a structural-grid VE pass for the demising walls (currently slab-to-deck full UL U419 — could portions revert to plenum-only ratings if AHJ accepts? requires AHJ pre-approval and is high-risk for the schedule). Or owner accepts a $76k gap and absorbs into owner contingency (5% / $228k available).
>
> Recommended path: take the $171k likely bundle; absorb the remaining $76k into owner contingency with a 90-day buyout-watchlist commitment from CM to find additional savings during sub buyout.
>
> ## Owner Decision Memo
>
> **Questions for owner workshop (target date: 2026-05-05):**
>
> 1. **VE-001** (largest savings): accept demountable-to-gyp at non-exam offices? Architect supportive on visual-continuity grounds.
> 2. **VE-002, VE-007** (small LCC penalties): accept LCC trade for first-cost saving? Owner-occupier with 15-year hold — these add up to ~$15k LCC penalty against $24k likely first-cost saving on a 15-year basis (roughly net-positive but tight).
> 3. **VE-009** (LCC-negative): owner's call on whether budget gap pressure overrides 15-year LCC.
> 4. **VE-011** (contingency reduction): owner's call on absorbing CM-side risk via reduced contingency. Not recommended unless paired with offsetting fee adjustment.
> 5. **Remaining gap acceptance** ($76k after recommended bundle): owner-side absorption from owner contingency vs. additional VE rounds?
>
> **Decision deadline:** 2026-05-05 (NTP scheduled 2026-06-15; substitution requests need 2 weeks plus architect review, so VE decisions must close 5 weeks before NTP to avoid schedule slip).
>
> ---
>
> _VE savings ranges are estimates for discussion. Final savings require sub/vendor quotes, architect substitution-request approval, and EOR/AHJ review where applicable. This VE log was prepared with AI assistance and does not replace a formal VE workshop with the design team. CM contingency reduction is a risk-transfer item, not VE; recommend addressing separately from the VE log if pursued._
