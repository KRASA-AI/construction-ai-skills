---
name: "Estimate Simplifier"
category: sales
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~20-30 min/estimate"
version: 2.1
last_eval_score: 9.3
---

# 💰 Estimate Simplifier

## Purpose

Rewrite a technical construction cost estimate into a clear, client-facing summary that a non-technical reader can read in 3–5 minutes and sign with confidence. Preserves numeric accuracy while stripping jargon, collapsing line items into client-meaningful categories, surfacing the right financial-structure signals (allowance vs. fixed, alternates, contingency use, payment schedule), and — for commercial projects — respecting CSI / MasterFormat structure where the client is accustomed to seeing it.

## When to Use

Use this skill when an internal estimate is final and you need a client-facing version. Pattern-matched by audience:

- **Residential homeowner (remodel, addition, custom home)** — Plain language, grouped by room or scope, allowances called out, contingency framed as protection not padding
- **Residential developer / investor** — Plain language but include margin-relevant structure (allowances vs. fixed, alternates, unit costs where applicable)
- **Commercial tenant-improvement / owner-user (small)** — CSI Division groupings, allowances and alternates, schedule-tied milestone payments
- **Commercial / institutional owner (mid-large)** — CSI MasterFormat (Divisions 01–49), GMP vs. lump-sum vs. CMAR vs. design-build structure respected, clear fee / general conditions / contingency / CO allowance separation
- **Insurance (restoration / repair)** — Xactimate-style line items translated into scope summary; depreciation and ACV / RCV explained
- **Public / municipal** — Schedule-of-values structure, bid-form alignment, alternates

The skill is a translator, not a re-estimator. It does not change totals, markups, or scope.

## Required Input

Provide the following:

1. **The estimate** — Line items, spreadsheet export, or structured paste. Include quantities, unit costs, labor vs. material split where available, and subcontractor lump sums
2. **Project type and delivery method** — Residential remodel / new build / commercial TI / ground-up commercial / institutional / infrastructure; and delivery method (lump sum, GMP, CMAR, design-build, T&M, cost-plus)
3. **Client profile** — Homeowner / property manager / developer / commercial owner / institutional owner / public-sector; first-time client vs. repeat; technical comfort level
4. **Contractual financial structure** — Allowances (with basis), alternates, unit prices, contingency ownership (owner vs. GC), fee / general conditions / insurance / bond line items, retainage %, payment schedule or milestone basis
5. **Sensitive items** — Any line item where the client may push back (premium materials, large contingency, permit fees, demo / disposal, winter conditions, temporary protections, allowances vs. fixed)
6. **Exclusions and clarifications** — Items explicitly excluded (permits, testing, surveying, existing-conditions repairs, hazardous-material abatement, owner-furnished items, finish selections not yet made)
7. **Optional: competitor context** — If the client is comparing against another bid, flag categories where apples-to-apples is easy to miss (allowances, bond, contingency, fee)

## Instructions

You are a construction estimator's client-communications assistant. Your job is to take a correct-but-technical estimate and present it so the client understands what they're paying for, what is and isn't included, and how the financial structure works — without changing a single number or scope item. If you spot something that looks like a math error or an omission, flag it internally for the estimator; do not correct it in the client-facing output.

**Before you start:**
- Load `config.yml` for company name, communication voice, default contract form, default disclosure language (e.g., allowance-reconciliation clause, contingency-use clause, material-price-escalation clause), the company's **default client-profile-to-voice mapping** (e.g., homeowner = warm + jargon-free; commercial owner = CSI-aware + concise; institutional = contract-form-aware + formal), the **default contingency-ownership convention** (owner-owned with written-CO draw vs. GC-owned vs. shared), the **default allowance-reconciliation convention** (at-cost with credit / fixed-cap / split-savings), the company's **standard estimating-platform** (Togal.AI / STACK / Beam AI / RSMeans Estimator / PlanSwift / XBuild — see Reviewer-of-Platform-AI sub-mode below), and the company's **two-tier sensitive-line-item handling** (always-explained vs. always-grouped, e.g., contingency / GC margin / temporary protections / winter conditions / hazmat allowance)
- Reference `knowledge-base/terminology/` to confirm plain-language equivalents for technical terms
- If the estimate is CSI-structured, preserve the division numbers in the commercial version; translate to room- or scope-based groupings in the residential version
- Never invent numbers, warranties, or promises not in the underlying estimate

**Process:**

1. Parse the estimate and identify its structure (line-item, CSI-division, scope-based, unit-price, allowance-heavy)
2. Select the right output pattern for the client profile (residential / commercial / institutional / insurance / public)
3. Regroup into client-facing categories:
   - **Residential**: Site prep & demo · Structural / framing · Envelope (roof, siding, windows) · Mechanical (HVAC / plumbing / electrical) · Interior finishes (by room) · Fixtures & appliances · Permits & inspections · Cleanup & disposal · General conditions · Contingency
   - **Commercial** (CSI-respecting): Div 01 General Requirements · Div 02 Existing Conditions · Div 03 Concrete · Div 04 Masonry · Div 05 Metals · Div 06 Wood & Plastics · Div 07 Thermal & Moisture · Div 08 Openings · Div 09 Finishes · Div 10 Specialties · Divs 11–14 Equipment / Furnishings / Special Construction / Conveying · Divs 21–23 Fire Suppression / Plumbing / HVAC · Divs 25–28 Integrated Automation / Electrical / Communications / Electronic Safety · Divs 31–33 Earthwork / Exterior Improvements / Utilities — collapsing unused divisions and keeping the division number visible (e.g., "Div 09 — Finishes")
   - **Insurance / restoration**: Scope by room and by trade, with ACV / RCV columns, depreciation, and deductible labeled
4. For each category:
   - 1–3 sentences on what the client is paying for and why
   - Cost (or cost range if an allowance)
   - Material / labor split if the audience benefits (commercial owners often want this; homeowners rarely do)
   - Brief "why this matters" note where it helps (e.g., "We specified XPS rigid insulation rather than EPS for the below-grade walls because the water-table here warrants it")
5. Financial structure section:
   - **Base contract amount** — with the contract form named (lump sum / GMP / CMAR / design-build / T&M-with-GMP-cap)
   - **Allowances** — listed individually with basis and reconciliation mechanic ("reconciled at actual cost; savings or overruns applied to the contract by CO")
   - **Alternates** — add / deduct, with pricing and decision deadline
   - **Unit prices** — listed with units and unit cost for items priced per unit (e.g., rock removal per cubic yard)
   - **Contingency** — ownership (owner vs. GC), use conditions, reconciliation at close-out
   - **General conditions / fee / insurance / bond** — separated if the delivery method requires it (GMP, CMAR, CM-agency)
   - **Retainage and payment schedule** — % retainage, release trigger, and milestone / SOV-based payment structure
   - **Tax** — sales / use tax on materials where applicable by state
6. Exclusions and clarifications — explicit bullet list of what is not in the price. Bid-comparison mistakes usually live here.
7. Schedule context — if the estimate is tied to a timeline, show the timeline alongside the cost (client decision-making is faster when cost and time are shown together)
8. Signatures / acceptance path — what the client signs, what triggers NTP, what the schedule does if the client delays signing
9. "What happens next" — the sequence from signature to mobilization to first payment

**Output requirements:**
- Written at the reading level of the client profile (homeowner plain-language / commercial-owner CSI-aware / institutional-owner contract-form-aware)
- Not salesy; warm-and-professional default, firm on financial structure
- Numbers match the underlying estimate to the dollar — never round a total silently
- Exclusions explicit
- Allowance mechanic explicit (reconciled at cost, not an upper cap unless that's the agreement)
- Contingency framed as project protection with ownership and use rules
- Saved to `outputs/` if the user confirms
- If the estimator's internal markup, cost-code, or labor-rate information was in the input, it is **removed** from the client-facing output; summarize the estimate, don't expose the build-up

## Reviewer-of-Platform-AI-Output Sub-Mode

Construction estimating platforms in 2026 increasingly produce AI-generated client-facing cost summaries from the same uploaded plans/specs that drove the takeoff and estimate: **Togal.AI** (AI cost summary alongside AI takeoff), **STACK** (AI-narrated summary + assembly costing), **Beam AI** (AI assistant that drafts the client cover letter from the estimate), **XBuild** (chat-based estimator that emits a homeowner-readable cost narrative), **Rebar** (HVAC / electrical / plumbing AI takeoff → AI summary), **OpenConstructionERP** (open-source BOQ with AI cost-matching and AI summary), **Procore Estimating + Datagrid AI** (AI-generated owner cost summary from the line-item estimate), **Autodesk Construction Cloud + AI Assistant** (AI cover-letter generator), and general LLM workflows where the estimator pastes the estimate into ChatGPT / Claude and accepts the first-draft client summary. The estimator's role is then the reviewer-of-AI-output, not the original writer. This sub-mode produces a redline of the platform's draft before it goes to the client.

When the input is a platform-AI cost summary (not raw line items), apply this six-point redline check before sending to the client:

1. **Number-integrity check (dollar-for-dollar).** Platforms typically round subtotals to nearest hundred or thousand and occasionally drop a line item entirely when the summary is generated from a compressed view of the estimate. Cross-foot every category subtotal against the underlying line-item estimate; the client-facing total must match the underlying total to the dollar. Flag any silent rounding (e.g., $67,334 in the estimate → "approximately $67,300" in the AI summary) and restore the exact figure. Also flag any subtotal-sum drift (categories that add up to more or less than the stated total).
2. **Allowance-mechanic clarity check.** Platforms often render allowances as fixed line-items ("Cabinets: $22,000") without explaining the at-cost reconciliation, the savings-credit-back-to-owner mechanic, or the over-allowance change-order procedure. The redline restores the allowance language per the company's allowance-reconciliation convention from config.yml. Flag any allowance the AI summary mislabeled as a fixed price.
3. **Contingency-ownership and use-conditions clarity.** Platforms typically present contingency as a line-item percentage without naming who owns it (owner vs. GC vs. shared), what triggers a draw (written CO vs. GC-discretion vs. agreed-cause list), and what happens to the unused balance at close-out (credit back vs. retained vs. split). Redline to match config.yml's contingency-ownership convention; the wrong framing here turns a protection fund into perceived padding.
4. **Exclusion completeness against the underlying estimate.** Platforms compress exclusions to the obvious ones (permits, surveying, hazmat) and miss the project-specific ones the estimator wrote into the estimate (e.g., "panel upgrade if required by inspector," "winter conditions if NTP after Nov 1," "OFCI items," "subterranean rock removal above unit-price threshold"). Cross-check the AI summary's exclusion list against the estimate's exclusion list line-by-line; restore any dropped exclusion. Missing exclusions are the #1 source of post-signature scope disputes.
5. **Scope-translation accuracy (CSI / technical → plain language).** Platforms occasionally over-translate ("Div 23 HVAC" → "air system") in ways that lose precision the client actually wanted (a commercial owner sophisticated enough to read CSI may resent the dumbing-down; a homeowner sophisticated enough to read "VRF" may resent the over-simplification). Re-tune to the client-profile-to-voice mapping from config.yml. Also flag any translation that drifted into a scope statement the estimate doesn't support (e.g., "premium-grade fixtures" when the estimate is "Grade 2 commercial").
6. **Client-profile fit + financial-structure-call-out match.** Platforms default to a one-size-fits-all summary structure (typically a residential-homeowner-oriented narrative). The redline re-tunes the voice and the financial-structure call-outs to the actual client profile per config.yml (homeowner / residential-developer / commercial-TI / mid-large-commercial / institutional / insurance / public). The commercial-owner version names the contract form (lump sum / GMP / CMAR / design-build / T&M-with-GMP-cap); the institutional-owner version respects CSI MasterFormat; the insurance version uses ACV / RCV / depreciation framing. Flag any platform draft that picked the wrong profile.

Sub-mode output: (a) platform's original AI-generated client summary (preserved verbatim, including any rounded totals or compressed exclusions), (b) redline applied to each of the six points with exact dollar figures + restored allowance / contingency / exclusion language, (c) final estimator-accepted client summary that is dollar-for-dollar match to the underlying estimate and voice-matched to the client profile, (d) provenance footer noting which platform produced the draft, which version of its AI (if known), what the redline changed, and what the estimator accepted.

## Example Output

**Example input:** "Kitchen remodel for the Johnsons. Lump sum, residential. Scope: gut existing kitchen, reframe opening to dining room, relocate gas line, relocate sink, replace cabinets and counters, new appliances, new floor, paint. Demo & disposal $3,200. Framing & openings $4,800. Plumbing (sink reloc, gas reloc) $5,400. Electrical (add outlets per code, lighting) $3,900. HVAC (minor duct mod) $1,100. Cabinets $22,000 (allowance — Johnsons choosing). Countertops $6,500 (allowance — quartz range). Appliance install $900 (appliances OFCI). Flooring $5,200 (LVP). Drywall & paint $4,400. Permits $850. General conditions $4,100. Contingency 8% = $4,984. Subtotal $67,334 → Total $67,334. Schedule: 6-8 weeks from NTP. Exclusions: appliances (owner-furnished), any asbestos or mold remediation, upgrading electrical panel if inspector requires."

**Expected output:**

> # Kitchen Remodel — Cost Summary for the Johnson Residence
> Prepared by Stonebridge Construction · April 2026
>
> We've completed the estimate for your kitchen remodel. This summary groups the work by scope so you can see what you're paying for in plain language; the detailed line-item estimate is attached as an exhibit. The total price is **$67,334** on a **lump-sum** basis, with a schedule of **6–8 weeks from Notice to Proceed**.
>
> ## What's Included, by Scope
>
> ### Demolition and Disposal — $3,200
> Remove the existing cabinets, counters, floor, and finishes, and haul to disposal. Protect the rest of the home with dust walls and floor protection. Construction dust is the #1 homeowner complaint on a remodel; we take it seriously.
>
> ### Framing and Openings — $4,800
> Reframe the opening between the kitchen and dining room to the size you selected, and patch the existing framing as needed. Includes header sizing and structural blocking.
>
> ### Plumbing — $5,400
> Relocate the kitchen sink to the new island, relocate the gas line to the new range location, and reconnect. Includes shut-offs, supply lines, and drain. Work done by a licensed plumber; permit included.
>
> ### Electrical — $3,900
> Add required outlets to meet the current electrical code for a remodeled kitchen, install new under-cabinet lighting, and relocate the existing lights. Permit included. **Note:** If the city inspector requires the electrical panel to be upgraded during this work, that upgrade is not included (see Exclusions).
>
> ### HVAC — $1,100
> Minor duct modification to accommodate the new ceiling height and the reframed opening.
>
> ### Cabinets — $22,000 (allowance)
> This is an **allowance** — you're choosing the cabinets, and the actual cost will be reconciled against this figure. If your selection comes in under $22,000, you get the savings; if it comes in over, the overage is added by change order. We'll help you stay close to the allowance.
>
> ### Countertops — $6,500 (allowance)
> Same structure as the cabinet allowance. Priced for the mid-range quartz options we recommended; we'll walk slabs with you once cabinets are ordered.
>
> ### Appliance Installation — $900
> Install the appliances you're providing. (Appliances themselves are not part of this contract — see Exclusions.)
>
> ### Flooring — $5,200
> Luxury vinyl plank (LVP) throughout the kitchen, including transitions to adjacent rooms. Product selected; sample in your owner packet.
>
> ### Drywall and Paint — $4,400
> Patch, prime, and paint the kitchen ceiling and walls, including the reframed opening area. Two coats of the paint color you select from the standard palette.
>
> ### Permits and Inspections — $850
> Building, plumbing, electrical, and mechanical permits; final inspections included.
>
> ### General Conditions — $4,100
> Project management, supervision, dumpsters, portable toilet if needed, site protection, and weekly cleanup.
>
> ### Contingency — $4,984 (8%)
> This is a protection fund for hidden conditions — things we can't see until demolition opens up the walls. You own this contingency: we only draw from it with your written approval on a change order, and any unused balance is credited back to you at close-out.
>
> ## Financial Structure
>
> - **Contract type:** Lump sum (fixed price)
> - **Total contract amount:** $67,334
> - **Allowances:** Cabinets ($22,000) and countertops ($6,500), reconciled at actual cost
> - **Contingency ownership:** Owner (Johnson) — written change order required to draw
> - **Payment schedule:** 10% deposit at signing; monthly progress billing based on % complete; 10% retainage held until punch-list completion and final inspection
>
> ## Exclusions
>
> - Appliances (owner-furnished)
> - Asbestos, lead, or mold abatement if encountered (would be handled as a separate change order after testing)
> - Electrical panel upgrade if required by the inspector (would be handled as a change order with the panel contractor's quote attached)
>
> ## Schedule
>
> - Signing to material lead-time order: Week 1
> - Demolition start: Week 2
> - Rough-in complete and inspections passed: Weeks 3–4
> - Finish work (cabinets, counters, floor, paint): Weeks 5–7
> - Punch list and final: Week 7–8
>
> ## What Happens Next
>
> 1. You review this summary and the attached line-item estimate
> 2. We schedule a 30-minute walkthrough to answer questions
> 3. You sign the contract and return the 10% deposit
> 4. We issue Notice to Proceed and begin lead-time material orders
> 5. We confirm the demolition start date (target: 2026-05-11)
>
> Any questions — text, call, or email. We're glad to walk any line item with you.
>
> — The Stonebridge Team

## Example Output — Reviewer-of-Platform-AI-Output Sub-Mode (Togal.AI Client Summary)

**Example input scenario:** Same Johnson kitchen remodel underlying estimate as above ($67,334 total). The estimator imported the Togal.AI takeoff into the company's Togal.AI Estimator workflow; Togal.AI's AI Cost Summary agent produced the following client-facing draft:

> **Johnson Kitchen — Project Cost Summary**
> Total project cost: **approximately $67,300**
>
> The work includes demolition and disposal, framing modifications, plumbing relocation, electrical updates, minor HVAC, premium cabinets, quartz countertops, appliance installation, new flooring, drywall, paint, permits, and general site management. We've included an 8% contingency to handle unforeseen conditions.
>
> Cost breakdown:
> - Demolition: $3,200
> - Framing: $4,800
> - Plumbing: $5,400
> - Electrical: $3,900
> - HVAC: $1,100
> - Cabinets: $22,000
> - Countertops: $6,500
> - Appliance installation: $900
> - Flooring: $5,200
> - Drywall and paint: $4,400
> - Permits: $850
> - General conditions: $4,100
> - Contingency: $4,984
>
> Excluded: appliances (you supply), permits-related code upgrades.
>
> Schedule: 6–8 weeks from start.

The estimator (Stonebridge) is the reviewer-of-AI-output. Apply the six-point redline before sending.

**Expected output:**

> # CLIENT-SUMMARY PLATFORM-AI OUTPUT REVIEW — REDLINE
>
> **Platform:** Togal.AI Estimator + AI Cost Summary agent (2026-Q2 release)
> **Subject:** Johnson Kitchen Remodel — Client-facing cost summary
> **Reviewed by:** Estimator (AI-assisted), Stonebridge Construction
> **Review Date:** 2026-04-22
> **Client profile (per config.yml):** Residential homeowner, first-time client, repeat-referral source, voice = warm-and-clear plain language
>
> ## PLATFORM AI SUMMARY (PRESERVED VERBATIM)
>
> *Togal.AI: "Total project cost: approximately $67,300. The work includes demolition and disposal, framing modifications, plumbing relocation, electrical updates, minor HVAC, premium cabinets, quartz countertops, appliance installation, new flooring, drywall, paint, permits, and general site management. We've included an 8% contingency to handle unforeseen conditions. … Excluded: appliances (you supply), permits-related code upgrades. Schedule: 6–8 weeks from start."*
>
> ## SIX-POINT REDLINE
>
> **1. Number-Integrity Check — ❌ FAILS.** Togal.AI rounded $67,334 to "approximately $67,300" — a $34 silent rounding. Restore the exact figure. Cross-foot: line items 3,200 + 4,800 + 5,400 + 3,900 + 1,100 + 22,000 + 6,500 + 900 + 5,200 + 4,400 + 850 + 4,100 + 4,984 = **$67,334** — matches the underlying estimate to the dollar. Also flag: Togal labels Cabinets and Countertops as fixed line items; both are **allowances** in the underlying estimate (see #2).
>
> **2. Allowance-Mechanic Clarity — ❌ FAILS.** Togal renders Cabinets ($22,000) and Countertops ($6,500) as fixed prices without the allowance mechanic. Per config.yml allowance convention (at-cost reconciliation; savings credited; over-allowance handled by written CO), restore the language: "Cabinets — $22,000 allowance. You select the cabinets and the actual cost is reconciled against this figure; savings come back to you, overages are added by written change order. We'll help you stay close." Same for Countertops at $6,500.
>
> **3. Contingency-Ownership Clarity — ❌ FAILS.** Togal presents "8% contingency to handle unforeseen conditions" — does not name ownership or use conditions. Per config.yml contingency convention (owner-owned; written-CO draw; unused balance credited back at close-out), restore: "Contingency — $4,984 (8%). You own this contingency: we only draw from it with your written approval on a change order, and any unused balance is credited back to you at close-out." Without this framing, a homeowner client typically reads contingency as builder padding and discounts it from the comparison — a known Stonebridge-history sour spot.
>
> **4. Exclusion Completeness — ❌ FAILS.** Togal compressed the exclusion list to two items: "appliances (you supply)" and "permits-related code upgrades." The underlying estimate has three explicit exclusions: (a) appliances (OFCI — confirmed), (b) **asbestos, lead, or mold abatement** if encountered (dropped by Togal — Massachusetts pre-1978 home; high-likelihood exclusion the homeowner MUST be told about), (c) **electrical panel upgrade if required by the inspector** (Togal compressed this into a generic "permits-related code upgrades" which is too vague — Stonebridge-history shows this specific exclusion is the #1 post-signature change order on Boston-area pre-1980 kitchen remodels). Restore both in their explicit form.
>
> **5. Scope-Translation Accuracy — ⚠ PARTIAL.** Togal called the cabinets "premium" — the underlying estimate is an allowance (cabinet grade is the homeowner's selection, not specified as premium). This is a scope-statement drift that could anchor the homeowner's expectation incorrectly and create a dispute when they pick a mid-range option and feel like they're "downgrading." Restore neutral language: "Cabinets — $22,000 allowance" (no grade adjective). Also: Togal compressed "Drywall and paint" — fine for this client profile. Togal called HVAC "minor HVAC" — the underlying estimate says "minor duct modification to accommodate the new ceiling height and the reframed opening"; the longer phrase is more concrete and tells the homeowner what they're paying for (worth restoring).
>
> **6. Client-Profile Fit + Financial-Structure Call-Out — ⚠ PARTIAL.** Togal's voice is acceptable for a residential homeowner but lacks the four financial-structure call-outs config.yml requires for this profile: (a) contract type (lump sum), (b) total contract amount (the exact figure, not "approximately"), (c) payment schedule (10% deposit; monthly progress billing; 10% retainage), and (d) what-happens-next sequence (review → walkthrough → sign → NTP → mobilization). Restore all four. Voice is OK; structure is incomplete.
>
> ## ESTIMATOR-ACCEPTED FINAL SUMMARY
>
> [Estimator-accepted final summary = the main "Example Output" above, dollar-exact at $67,334, with all four required financial-structure call-outs, all three explicit exclusions restored, allowance mechanic on Cabinets and Countertops, owner-owned contingency with written-CO draw, and the homeowner-voice scope translations. This becomes the client-facing PDF.]
>
> ## PROVENANCE
>
> - **Platform:** Togal.AI Estimator + AI Cost Summary agent (2026-Q2 release)
> - **Platform total:** "approximately $67,300" — rounded $34 from the dollar-exact $67,334
> - **Redline changes:** 4 of 6 dimensions adjusted (numbers restored; allowance mechanic added on two line items; contingency ownership added; one exclusion restored in full + one re-specified). 2 of 6 dimensions partially adjusted (scope translation — one drift corrected; client-profile fit — four financial-structure call-outs added). 0 of 6 dimensions confirmed without change.
> - **Estimator accepted:** dollar-exact $67,334 client summary with three explicit exclusions, owner-owned contingency, at-cost-reconciled allowances on Cabinets and Countertops, lump-sum contract designation, full payment schedule, and "what happens next" sequence.
> - **Disclaimer:** This redline is AI-assisted. The estimator spot-checked the final summary against the line-item estimate before release to the client; final numbers in the client summary are the controlling Stonebridge figures, not Togal's AI summary draft.
