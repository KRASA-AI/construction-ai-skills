---
name: "Value Engineering Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90-120 min/package"
version: 2.1
last_eval_score: 9.2
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

- Load `config.yml` for company defaults, preferred subs by trade, regional labor-rate awareness, default markup applied to VE savings (the GC's share of saved cost), any standard exclusions, the **owner's typical hold-period default by project type** (residential-developer-flip 0-yr / commercial-TI tenant-fitout 5–10 yr / corporate-owner-occupier 15-yr / institutional-owner-occupier 30-yr), the **company's LCC-discipline posture** (always-surface-LCC-on-owner-occupier / surface-only-when-asked / never-LCC-for-flip), the **company's CM-contingency policy** (don't-VE-contingency-without-fee-offset / accept-contingency-trade / never), the company's **VE-platform choice** (Procore Datagrid VE / Beam AI cost-reduction / ALICE optioneering / Trunk Tools / general-LLM workflows — see Reviewer-of-Platform-AI sub-mode below), and the company's **buyout-watchlist commitment posture** (e.g., "we commit to a 90-day post-GMP buyout watchlist to chase additional savings during buyout" — used as a closing offer on partial-bundle closes).
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
> Recommended path: take the $171k likely bundle; absorb the remaining $76k into owner contingency with a 90-day buyout-watchlist commitment from CM to find additional savings during sub buyout (per config.yml buyout-watchlist-posture default).
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

## Reviewer-of-Platform-AI-Output Sub-Mode

Construction platforms in 2026 increasingly produce AI-generated VE candidate lists from the same estimate / spec / model the GC is already working in: **Procore Datagrid AI VE agent** (summer-2026 broader-availability trajectory; produces VE candidates with savings ranges from line-item estimate + spec parse), **Beam AI cost-reduction recommendations** (estimating-platform-side VE list from the takeoff + estimate), **ALICE Technologies optioneering** (schedule-VE: phasing / sequencing alternates that compress GC duration — McKinsey partnership 35+ clients), **Trunk Tools VE workflow** (spec-substitution candidates from the spec parse), **Document Crunch / Trimble Construction One** (post-acquisition: spec relaxation candidates from CDs + AHJ amendments), **Autodesk Construction Cloud + AI Assistant** (spec + drawing-parse VE candidates), **Togal.AI** (quantity / coverage reduction candidates from the AI takeoff), **STACK** (assembly-substitution VE candidates), and general LLM workflows where the chief estimator pastes the estimate into ChatGPT / Claude and accepts a VE candidate list. The chief estimator / preconstruction lead is then the reviewer-of-AI-output. This sub-mode produces a redline of the platform's VE candidate list before it goes into the VE workshop materials.

When the input is a platform-AI VE list (not a raw estimate), apply this six-point redline check before accepting candidates into the recommended bundle:

1. **Phase-altitude alignment.** Platforms produce VE candidates without checking whether the altitude matches the project phase. A CD-phase project that gets SD-altitude candidates (system change: VRF → packaged rooftop) will mostly reject those candidates; the redline downsizes to phase-appropriate altitude per the Phase / VE-able table above. Flag and drop any candidate whose altitude is one or more tiers above the current phase (e.g., system change proposed at CD; concept-level shape change proposed at DD).
2. **Life-safety / structural / seismic exclusion check.** Platforms occasionally propose VE candidates that touch life-safety, structural, seismic, smoke evacuation, or egress (e.g., "reduce fire-rating from 2-hr to 1-hr at corridor partition," "reduce shear-wall thickness," "substitute fire-sprinkler heads to less-expensive model without re-running hydraulics"). The redline drops these unconditionally and surfaces them in the "Do Not VE" section. The hard rule applies — no exceptions without EOR review and AHJ re-submission flagged as a required step.
3. **Owner-constraint compliance.** Platforms do not read the owner's stated constraints (LEED level, occupancy date, accessibility commitments, brand-specific finishes the owner chose, M/W/DBE participation goal). Cross-check every platform candidate against the owner's stated constraints from the input and drop any candidate that breaches a stated constraint. Flag explicitly so the workshop materials show what the platform missed.
4. **LCC-impact disclosure (the v2.0 seventh category, enforced here).** Platforms typically report first-cost savings without computing the LCC delta over the owner's hold period. For owner-occupier and institutional-owner projects (per config.yml LCC-discipline posture), compute the 20-year (or owner-hold-period) LCC delta for every platform candidate and flag any that are **first-cost-positive / LCC-negative** (e.g., porcelain → LVT in a high-traffic break room over a 15-year hold; lower-SEER HVAC over a 20-year hold; lower-efficacy LED over a 10-year hold). For developer-flip projects, this check is neutralized per config.yml posture.
5. **Savings-basis credibility.** Platforms generate savings ranges with named or unnamed bases. The redline reads each candidate's basis and rates it H / M / L credibility: H = vendor-specific quote or regional bid-spread within 90 days; M = RSMeans / national-database reference within the current quarter; L = engineer estimate / "industry typical" with no anchor. Any candidate with L credibility is held until a vendor quote or sub-of-record confirmation is in hand; the workshop materials present these as "candidate — pending verification" not "recommended — proceed."
6. **Approval-path completeness.** Platforms often surface the savings without the implementation path (architect substitution-request / EOR re-stamp / AHJ re-submission / spec-section approved-equal). The redline fills in the missing approval path per the spec section, the project's delivery method (DBB / DB / CMAR / IPD changes who has authority), and the implementation lead time (1 wk substitution request / 4 wk re-design / 8 wk AHJ re-submission). Any candidate whose approval-path lead time exceeds the available pre-NTP window is dropped to "next-tier" rather than "recommended."

Sub-mode output: (a) platform's original AI-generated VE candidate list (preserved verbatim, including savings ranges and any narrative the platform produced), (b) redline applied to each of the six points with phase-altitude downsizing / hard-rule drops / owner-constraint drops / LCC-impact annotations / credibility ratings / restored approval paths, (c) final estimator-accepted VE log ready for the workshop, with **pre-redline-vs-post-redline candidate-count delta** (e.g., platform proposed 24 candidates → 18 accepted-as-is + 4 downsized-by-phase + 2 dropped-on-owner-constraint), (d) provenance footer noting which platform produced the list, which version of its AI (if known), what the redline changed, what the estimator accepted, and a pattern-notes feedback-loop for vendor-config calibration over time (e.g., "platform consistently proposes structural VE on healthcare projects — adjust prompt to exclude structural Pareto items upstream").

## Example Output — Reviewer-of-Platform-AI-Output Sub-Mode (Procore Datagrid AI VE Agent)

**Example input scenario:** Same Brookline MOB TI Phase 2 post-bid GMP-reconciliation as above ($247K gap on $4,797K GMP, 15-yr owner-occupier hold, ICRA Class III/IV maintained, med-gas + slab-to-deck rated joint detail off-limits). The Stonebridge preconstruction lead ran the GMP-reconciliation estimate through Procore Datagrid AI's VE candidate agent (private-beta cohort access). Datagrid produced an 18-candidate VE list:

> **Procore Datagrid AI VE Candidates — Brookline MOB TI Phase 2**
> 1. Demountable glass partitions → conventional gyp throughout (all 18 walls): $74K
> 2. Solid-surface countertops → laminate throughout (incl. exam): $24K
> 3. Carpet tile alternate manufacturer (Shaw → Mohawk): $11K
> 4. Lighting alternate (Eaton → Lithonia approved-equal): $18K
> 5. VAV system → packaged rooftop (system change): $89K
> 6. Reduce demising wall rating from 2-hr to 1-hr at non-corridor locations: $34K
> 7. Reduce med-gas spec from oxygen-cleaned copper to general copper: $42K
> 8. Painting 1 prime + 1 finish in all spaces: $14K
> 9. Door hardware Grade 1 → Grade 2 throughout (incl. main corridor): $19K
> 10. Casework laminate veneer throughout (incl. exam): $28K
> 11. Defer break-room flooring porcelain → LVT: $9K
> 12. Defer interior signage: $14K
> 13. Reduce CM contingency 3% → 2%: $44K
> 14. Reduce GC contingency 5% → 3%: $91K
> 15. Slab-on-grade thickness 5" → 4": $11K
> 16. Reduce LEED documentation effort (project is not LEED): $3K
> 17. Compress GC duration 1 wk via single night shift: $11K
> 18. Substitute fire-sprinkler heads to less-expensive model: $9K

The preconstruction lead is the reviewer-of-AI-output. Apply the six-point redline before accepting into the workshop bundle.

**Expected output:**

> # VE PLATFORM-AI OUTPUT REVIEW — REDLINE
>
> **Platform:** Procore Datagrid AI VE agent (private-beta cohort, May 2026)
> **Subject:** Brookline MOB TI Phase 2 — VE candidate list — Post-bid GMP reconciliation
> **Reviewed by:** Preconstruction Lead (AI-assisted), Stonebridge Construction
> **Review Date:** 2026-04-27
> **Project posture per config.yml:** owner-occupier 15-yr hold = LCC-discipline ON; CM-contingency policy = don't-VE-contingency-without-fee-offset; phase = post-bid GMP reconciliation (system change is mostly out of altitude)
>
> ## PLATFORM VE CANDIDATE LIST (PRESERVED VERBATIM)
>
> *18 candidates as listed by Procore Datagrid AI, $574K nominal total at the high end if all accepted.*
>
> ## SIX-POINT REDLINE
>
> **1. Phase-Altitude Alignment — 1 candidate downsized, 1 dropped.**
> - Candidate 5 (VAV → packaged rooftop) is a **system change** — SD altitude, proposed at post-bid GMP reconciliation phase. **Dropped to "next-tier — would require re-design 8 weeks + EOR re-stamp + AHJ re-submission; not feasible inside NTP window."** Surface in the workshop materials as "platform-proposed, infeasible at this phase" with the rationale.
> - Candidate 17 (compress GC duration via single night shift) — sequencing / productivity altitude, in-phase. Accept.
>
> **2. Life-Safety / Structural / Seismic Exclusion — 3 candidates dropped to "Do Not VE."**
> - Candidate 6 (reduce demising wall rating from 2-hr to 1-hr at non-corridor locations) — fire-rating reduction; UL U419 listing condition; owner-stated constraint also explicit ("no compromise on slab-to-deck rated joint detail at demising walls"). **Dropped — Do Not VE.** Hard rule + owner constraint.
> - Candidate 7 (reduce med-gas spec from oxygen-cleaned copper to general copper) — NFPA 99 condition; owner-stated constraint also explicit. **Dropped — Do Not VE.** Hard rule + owner constraint + code.
> - Candidate 18 (substitute fire-sprinkler heads to less-expensive model) — fire-suppression system; hard rule says no without EOR review + AHJ re-submission; hydraulic-calc impact not evaluated by platform. **Dropped — Do Not VE.** Hard rule.
> - Candidate 15 (slab-on-grade thickness 5" → 4") — structural; outside ICRA Class III/IV demolition / repour during occupied operations is not viable; even if structurally OK, the candidate touches the structural design. **Dropped — Do Not VE.** Hard rule.
>
> **3. Owner-Constraint Compliance — 2 candidates dropped (overlapping with #2).**
> - Already captured in #2: candidates 6 + 7 breach explicit owner constraints. No additional candidate drops at this point.
> - Candidate 16 (reduce LEED documentation effort) — project is not LEED per the input; the platform proposed a candidate that does not apply. **Dropped — does-not-apply (no actual savings to capture).**
>
> **4. LCC-Impact Disclosure — 4 candidates LCC-annotated.**
> - Candidate 1 (demountable → gyp, all 18 walls): platform proposed *all* walls. The v2.0 example carved 12 non-exam + 6 exam (retain demountable at exam for reconfigurability over 15-yr hold). The platform's full-stripout would deprive owner of $42K NPV reconfigurability benefit at exam over 15-yr hold. **Downsize to non-exam only (12 walls) — accept $58K of the $74K platform claim; LCC-aligned.**
> - Candidate 2 (solid-surface → laminate throughout, incl. exam): exam-room counters drive cleanability; LCC penalty of laminate edge-wear over 15-yr at exam stations exceeds the first-cost saving. **Downsize to non-exam only — accept $18K of the $24K platform claim; LCC-aligned.**
> - Candidate 10 (casework laminate veneer throughout, incl. exam): exam casework drives medical-cleanability; same LCC reasoning. **Downsize to non-exam only — accept $13K of the $28K platform claim; LCC-aligned.**
> - Candidate 11 (defer break-room flooring porcelain → LVT): **flag as first-cost-positive / LCC-negative over 15-yr hold** (porcelain 25-yr vs. LVT 10-15-yr; $4-8K LCC penalty against $9K likely first-cost saving). Surface to owner with the LCC framing; not auto-accepted.
>
> **5. Savings-Basis Credibility — 3 candidates dropped or held.**
> - Candidate 13 (CM contingency 3% → 2%, $44K) — not VE; risk transfer. Per config.yml CM-contingency policy "don't-VE-contingency-without-fee-offset," **hold and surface as risk-transfer-not-VE to the owner** with the recommended GC-fee bump offset.
> - Candidate 14 (GC contingency 5% → 3%, $91K) — not VE; risk transfer; same posture. **Hold; not recommended at the workshop without offsetting risk-allocation discussion.** Additionally, dropping owner's contingency from 5% to 3% on a TI of this complexity (occupied healthcare adjacencies; ICRA discipline; med-gas; rated demising) leaves only $137K cushion on a $4.55M cap — historically tight.
> - Candidate 9 (door hardware Grade 1 → Grade 2 throughout, including main corridor) — main corridor hardware is the spec floor (Grade 1 in main corridor + exam; Grade 2 acceptable in back-of-house). Platform over-reached. **Downsize to non-corridor only — accept $6K of the $19K platform claim.**
>
> **6. Approval-Path Completeness — Restored on accepted candidates.**
> - Candidates 1 (demountable substitution), 2 (countertop substitution), 3 (carpet manufacturer), 4 (lighting alternate), 5 (already dropped), 9 (door hardware grade), 10 (casework veneer): architect via CSI 13.1 substitution request; 1–2 weeks each.
> - Candidate 8 (painting 1 prime + 1 finish in mech / storage only — downsize from "all spaces"; retain 1+2 in occupied per spec): architect + owner sign-off on sample; 1 week.
> - Candidate 12 (defer signage): owner-direct contract post-occupancy; 1 day.
> - Candidate 17 (compress GC duration via shift change): CM operational decision; 1 day to commit.
>
> ## ACCEPTED VE LOG (POST-REDLINE)
>
> | VE# | Title | Savings (low/likely/high) | Notes |
> |---|---|---|---|
> | VE-001 | Demountable → gyp at 12 non-exam offices (downsized from platform's "all 18 walls") | $48k / $58k / $68k | LCC-aligned per redline |
> | VE-002 | Solid-surface → laminate at non-exam only (downsized) | $14k / $18k / $22k | LCC-aligned per redline |
> | VE-003 | Carpet tile alternate (Shaw → Mohawk) | $8k / $11k / $14k | Accept as-platform |
> | VE-004 | Lighting alternate (Eaton → Lithonia) | $14k / $18k / $22k | Accept; +1wk lead shorter |
> | VE-006 | Painting 1 prime + 1 finish in mech / storage only (downsized from "all spaces") | $5k / $7k / $9k | Retain 1+2 in occupied per spec |
> | VE-007 | Door hardware Grade 1 → Grade 2 at non-corridor only (downsized) | $4k / $6k / $8k | Main corridor + exam retain Grade 1 |
> | VE-008 | Casework laminate veneer at non-exam only (downsized) | $9k / $13k / $17k | LCC-aligned |
> | VE-009 | Defer break-room porcelain → LVT (flagged LCC-negative) | $6k / $9k / $12k | Surface to owner with LCC framing |
> | VE-010 | Defer interior signage (post-occupancy) | $11k / $14k / $17k | Accept |
> | VE-012 | Compress GC duration 1 wk via single night shift | $8k / $11k / $14k | Accept; -7 days schedule |
>
> **Total likely savings (post-redline):** $165K (vs. platform's $574K nominal max) — closes ~67% of $247K gap with the recommended-or-flagged set. Pair with owner contingency for the residual ~$82K + 90-day buyout watchlist commitment per config.yml.
>
> ## DO NOT VE (RESTORED FROM REDLINE)
>
> - **Candidate 5 — VAV → packaged rooftop:** dropped on phase-altitude (SD altitude proposed at post-bid; 8-wk re-design + EOR + AHJ infeasible inside NTP window)
> - **Candidate 6 — demising wall rating reduction:** owner constraint + UL listing + code
> - **Candidate 7 — med-gas spec relaxation:** owner constraint + NFPA 99
> - **Candidate 15 — SOG thickness reduction:** structural + ICRA occupied-operations re-pour infeasibility
> - **Candidate 16 — LEED documentation reduction:** does not apply (project is not LEED)
> - **Candidate 18 — sprinkler-head substitution:** life-safety; hard rule; hydraulic re-calc impact not evaluated
>
> ## HOLD — RISK TRANSFER (NOT VE)
>
> - **Candidate 13 — CM contingency 3% → 2%:** $44K savings; surface as risk-transfer with recommended GC-fee bump offset
> - **Candidate 14 — GC contingency 5% → 3%:** $91K savings; not recommended at this complexity
>
> ## PROVENANCE + PATTERN NOTES
>
> - **Platform:** Procore Datagrid AI VE agent (private-beta cohort, May 2026)
> - **Pre-redline candidate count:** 18
> - **Accepted (recommended or discuss):** 10
> - **Downsized (LCC or scope):** 5 (candidates 1, 2, 8, 9, 10)
> - **Dropped to Do Not VE:** 6 (candidates 5, 6, 7, 15, 16, 18)
> - **Held — risk transfer (not VE):** 2 (candidates 13, 14)
> - **Pattern notes for Procore Datagrid AI VE feedback-loop:**
>   - Datagrid consistently proposes structural / fire-rating VE on healthcare projects — feed back the rule "exclude life-safety, structural, seismic, fire-rating candidates" upstream
>   - Datagrid did not weight the owner's 15-yr hold against LCC — feed back the owner-hold-period parameter so LCC-negative candidates get auto-annotated
>   - Datagrid did not respect the owner-stated-constraint list (med-gas, rated joint) — feed back the constraint list as input filter
>   - Datagrid proposed contingency reduction as VE — re-label as risk-transfer-not-VE
>   - Datagrid over-applied substitutions to all spaces (demountable / hardware / casework / countertops) when the right answer was non-exam / non-corridor only — feed back the "downsize-by-zone" rule
> - **Disclaimer:** This redline is AI-assisted. VE candidates require formal architect substitution-request approval, EOR re-stamp where applicable, and AHJ re-submission where applicable. The platform's first-pass savings reduction (~$574K → $165K accepted) reflects the LCC-discipline, hard-rule, and owner-constraint filters that distinguish a VE workshop from a candidate-generation exercise.
