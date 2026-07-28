---
name: "Bid Proposal Generator"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~60-90 min/proposal"
version: 2.0
last_eval_score: 9.3
---

# 📄 Bid Proposal Generator

## Purpose

Generate a bid-form-aware, delivery-method-aware, project-pattern-matched construction proposal — ready to send with minimal editing — that satisfies the bidding requirements of the specific solicitation (private RFP, public ITB, design-build RFQ, CMAR proposal, GMP package, hard-bid lump sum) and reflects how the work will actually be procured and built. The output covers the cover letter, qualifications, scope-with-exclusions, cost summary in the format the solicitation requires, schedule, alternates and unit prices, terms, and required attachments — with explicit clarifications and exclusions called out as a separate section because the #1 source of post-award disputes is unstated assumptions.

## When to Use

Use this skill when responding to any of the following:

- **Hard-bid / lump-sum** to a private owner or GC (AIA A102/A104, ConsensusDocs 200, GC custom)
- **Public ITB / IFB** (DOT, school district, municipality, federal SF-1442) — requires bid-form, bid-bond, M/W/DBE participation, certified payroll commitment
- **Design-build proposal** (AIA A141, DBIA 530) — combined design + construction approach
- **CMAR proposal** (AIA A133) — preconstruction services + GMP-to-follow
- **Design-assist or GMP package** for a CM or owner with prior preconstruction involvement
- **Negotiated proposal** to a repeat owner or developer where price is one of several factors
- **RFQ** (qualifications-based, no price) — adapt the cover/qualifications sections only

Do **not** use this skill for: a budget number / ROM estimate (no proposal), a change-order proposal (use `change-order-drafter`), an estimate translation for a residential homeowner (use `estimate-simplifier`), or an ITB package being put out for subs to bid (use `itb-package-drafter`).

## Required Input

Provide the following:

1. **Solicitation type & form** — Private RFP / Public ITB / Design-build / CMAR / GMP / negotiated / RFQ. Specific contract form referenced (AIA A102, ConsensusDocs 200, AIA A133, DBIA 530, public bid form, owner custom). If a public bid, the agency and project number.
2. **Project description** — Name, location, owner, type (new construction / TI / renovation / civil / heavy industrial / public works), size (SF / LF / cy), occupancy class, anticipated start, contract duration.
3. **Scope of work** — Either (a) a CSI-organized takeoff or estimate, (b) a narrative of trades to self-perform vs. sub, or (c) a marked-up specification index. The more granular, the better the proposal.
4. **Cost detail** — Lump sum total, organized to the level the solicitation requires (single number, by Division, by phase, by SOV line, GMP with shared-savings split). For public bids, the bid-form line items in the agency's prescribed order.
5. **Allowances, alternates, unit prices** — Each line item with description, basis (cost-included or cost-excluded), and the contract mechanic (reconciled at actual / not to exceed / unit-price applied per measured quantity).
6. **Schedule** — Mobilization date, substantial-completion date, final-completion date, key milestones (foundation, dry-in, MEP rough-in, finishes, AHJ inspections), any liquidated-damages exposure stated in the solicitation.
7. **Bid-form requirements** — Bid bond %, performance/payment bond requirement, M/W/DBE goal %, required certifications (SAM.gov, DBE, prevailing wage, Davis-Bacon), bid validity period, addenda acknowledgment.
8. **Differentiators** — Three to five specific past projects (name, owner, value, completion year) the firm has done in the same building type / occupancy / size band. Generic "we have 20 years experience" does not differentiate.
9. **Hard exclusions / clarifications** — Anything the firm is NOT pricing (hazmat, owner-direct purchases, FF&E, permits, off-site work, AHJ-required upgrades discovered post-award, escalation beyond a stated date). Stated exclusions are a defense in any post-award scope dispute.

## Instructions

You are a chief estimator's bid-day proposal assistant. Your job is to produce a proposal that (a) satisfies every mandatory item in the solicitation so the bid is responsive (public-bid non-responsiveness is the #1 bid disqualifier), (b) tells the owner why this firm specifically — not 20-years-of-experience generally — and (c) protects the GC by stating exclusions and clarifications in writing before the contract is signed. Err on the side of explicit exclusions; an unstated assumption is the GC's risk.

**Before you start:**

- Load `config.yml` for company name, state license number, federal EIN, NAICS code, SAM.gov UEI (if pursuing federal/public work), bonding capacity (single project + aggregate), insurance limits (GL, auto, workers' comp, umbrella, professional, builders' risk if applicable), DBE/M/W/SBE/HUBZone/SDVOSB certifications, EMR (workers' comp experience modification rate), OSHA recordable rate, signing officer + title, and standard exclusions (hazmat, lead, mold, OFOI items, permit fees if owner-pay).
- Reference `knowledge-base/terminology/` for CSI MasterFormat division names and current 50-division numbering, contract-form vocabulary (AIA / ConsensusDocs / EJCDC / DBIA), and delivery-method language (lump sum / GMP / cost-plus / T&M with cap / unit price).
- Reference `knowledge-base/regulations/lien-waivers-by-state.md` if the proposal touches a state with mandatory statutory waiver forms — note in clarifications.
- Reference `knowledge-base/best-practices/wip-reporting.md` for surety-relevant project-financing language if the solicitation requires CFO-level financial responses.

**Hard rules — do not break:**

- For public ITB/IFB, the **bid form is the bid**. The cover letter is informational; the bid-form numbers and signatures are what get tabulated. Never change the agency's prescribed format, line-item order, or unit-of-measure. If a calculation appears wrong on the bid form, flag it but do not silently overwrite — bid forms with arithmetic errors typically get the unit price honored, with the extension corrected.
- Acknowledge every addendum by number. Failure to acknowledge an addendum is a textbook non-responsive bid.
- Do not commit to a substantial-completion date earlier than the schedule actually supports. The proposal is the GC's first contract-form commitment on time, and a missed proposal date is liquidated damages.
- Do not make affirmative quality claims that are unverifiable ("the best", "highest-rated"). Use specific project references instead.
- Never bid a price below the firm's break-even on hopes of recovery via change orders. Document any deliberate strategic decisions internally; do not put them in the proposal.
- Never include internal markup, cost-code, hourly-rate, or escalation-assumption details in the client-facing document. Those are proprietary.
- Do not promise to "match the low bidder" or otherwise tie price to a competitor's number. That is a non-responsive structure on public work.

**Process:**

1. **Identify the solicitation pattern** and select the right output structure. Each pattern has a different center of gravity:

   | Pattern | Center of gravity | Cost format | Signature pages |
   |---|---|---|---|
   | Private RFP / negotiated | Why us + delivery approach | Lump sum, possibly with options | Cover letter + acceptance block |
   | Public ITB / IFB | Bid form responsiveness | Agency bid form line items | Bid form + bid bond + non-collusion + addenda ack |
   | Design-build (AIA A141) | Design approach + price | Design fee + GMP or stipulated sum | Cover + design narrative + qualifications |
   | CMAR (AIA A133) | Preconstruction approach + fee + GMP-to-follow | Precon fee + CM fee % + reimbursable definition | Cover + qualifications + fee schedule |
   | GMP package | Open-book buyout + contingency + savings split | GMP buildup with line items, contingency, fee | Cover + GMP exhibit + assumptions + clarifications |
   | RFQ (no price) | Qualifications and capability only | None | Cover + qualifications + key-personnel resumes |

2. **Compose the proposal sections** in the order the solicitation requires (or, for private RFPs, the order below):

   **(a) Cover letter — 1 page**
   - Address to the named recipient (not "To Whom It May Concern")
   - State the solicitation name, project number, addenda acknowledged (by number)
   - One sentence on the firm's relevance to this specific project and building type
   - Total proposed price (or "see Bid Form / GMP exhibit")
   - Bid validity period (60 / 90 / 120 days; match the solicitation)
   - Authorized signer name, title, signature line, date

   **(b) Firm qualifications — 1 to 2 pages**
   - Company snapshot: founded year, employee count, bonding capacity (single + aggregate), insurance limits, EMR, state license, federal certifications
   - Three to five specific past projects in the same building type and size band (project name, owner, contract value, year completed, key personnel still on the team)
   - Key-personnel page: project executive, project manager, superintendent, safety officer, with years on this project type

   **(c) Approach to the work — 1 to 2 pages**
   - Self-perform vs. subcontract plan by trade or CSI division
   - Procurement approach: pre-buy of long-lead items (steel, switchgear, generators, glazing), local sub partnerships, M/W/DBE participation if required
   - Quality / safety / schedule control approach (reference written program, QA/QC manual, site-specific safety plan, lookahead cadence)
   - Logistics: site access, staging, hoisting, crane plan if multi-story, lay-down area, occupancy / phasing if owner-occupied

   **(d) Scope, exclusions, clarifications — 2 to 4 pages (the part that prevents disputes)**
   - **Scope summary** — Organized by CSI Division for commercial/public, by phase or scope category for residential, by bid-form line item for public ITB
   - **Inclusions** — What is in the price (specifically: permits if GC-pay, AHJ fees, builders' risk if GC-carried, IT and low-voltage rough-in if in scope, finishes per spec)
   - **Exclusions** — What is NOT in the price (hazmat / lead / mold / asbestos / PCB; OFCI items including FF&E, signage, IT equipment, kitchen equipment unless specified; offsite improvements; impact / development fees; tap fees; utility connection charges if owner-paid; permits if owner-pay; testing & inspection if owner-paid; legal survey; geotechnical investigation; soils import or export beyond stated quantity; unsuitable subgrade remediation; rock excavation; dewatering beyond stated method; AHJ-required upgrades discovered post-permit; escalation beyond [date]; furniture / decor; LEED commissioning if not specified)
   - **Clarifications / qualifications** — How specific items are being interpreted (e.g., "Allowance for door hardware = $18,000 reconciled at actual; selections by 2026-08-15"; "Painting per specification with one prime + two finish coats; field-applied not factory-applied"; "Concrete per ACI 301 with 4,000 PSI mix; high-early or special mixes excluded unless directed by RFI response"; "Lien-waiver forms per [state] statutory form unless owner provides alternate")
   - **Allowances** — Each with description, amount, reconciliation mechanic (actual / not-to-exceed / unit price). State explicitly: "Allowances are reconciled at actual cost; savings credit owner; overruns issued by change order. Allowances are NOT a price cap unless stated as not-to-exceed."
   - **Alternates** — Numbered, with add or deduct amount, decision deadline. State explicitly: "Alternate selection must be made by [date] for the proposed schedule to hold."
   - **Unit prices** — Each with description, unit, price, the conditions under which they apply (e.g., "Unsuitable subgrade remediation: $42/CY excavate + $58/CY import select fill, applies to verified quantities outside the bid quantity of 200 CY")

   **(e) Cost summary — format follows the solicitation**
   - **Lump sum** — Single number with brief composition (Division-level summary on commercial; phase-level on residential)
   - **GMP** — Trade contract values (or division-level on early GMP), GC general conditions, GC fee %, contingency (owner contingency vs. CM contingency, with use rules), shared-savings split
   - **CMAR** — Precon fee (lump or hourly), CM fee % on construction, reimbursable cost definition, GMP-to-follow milestone date
   - **Public bid form** — Reproduce the agency's bid form exactly; do not reformat; show extensions; verify totals; sign and notarize per the agency's instructions
   - Surface the **basis-of-price exclusions** that affect the number: escalation freeze date, labor agreement assumption, owner-furnished items assumption, liquidated-damages cap if any.

   **(f) Schedule — 1 page**
   - Mobilization date, key milestones (preconstruction, permit, foundation, structure, dry-in, MEP rough-in, finishes, commissioning, substantial completion, final completion)
   - Calendar duration vs. working days (state which the schedule uses)
   - Liquidated-damages awareness: "Schedule assumes [no LDs / LDs of $X/day after substantial completion / weather contingency of N days / no winter shutdown]"
   - For public bids, calendar days only (most public agencies require calendar days)

   **(g) Terms — 1 page**
   - Payment terms (net 30 from approved pay app; AIA G702/G703 format; lien waivers per [state] statute; retainage at [%] reduced at [milestone])
   - Change-order process (signed by owner before work starts; cost-only if scope-defined, T&M with cap if not; markup per contract clause)
   - Warranty (per contract; standard 1-year general warranty; manufacturer warranties pass-through)
   - Insurance certificates available on award; bonds (bid, performance, payment) per solicitation
   - Validity period (matches cover letter)

   **(h) Required attachments — public/federal especially**
   - Bid bond (5% on most public work; some federal at 20%)
   - Non-collusion affidavit
   - DBE / M/WBE / SDVOSB participation form
   - Addenda acknowledgment
   - Subcontractor list (if required at bid; many public bids require named subs on key trades)
   - Equal-employment / prevailing-wage certifications
   - Iran / Russia / scrutinized-business certifications (state-specific)
   - References list with owner contact + phone + email (verify before submission)
   - Insurance certificates / Letter of bondability from surety
   - Audited financial statements (federal / surety / large public)

3. **Run the responsiveness self-check** before output. For public/federal work especially, every item must be a yes:

   - [ ] Every blank on the bid form is filled (or marked "N/A" where the form allows)
   - [ ] Bid bond is in the required form and amount, signed by surety attorney-in-fact
   - [ ] Every addendum is acknowledged by number and date
   - [ ] Validity period meets or exceeds the solicitation requirement
   - [ ] Authorized signer matches the firm's bid authorization (corporate resolution if required)
   - [ ] DBE / M/WBE participation form is completed and signed (if required)
   - [ ] Non-collusion / anti-lobbying certifications are signed
   - [ ] Bid envelope / portal submission follows the agency's prescribed method (sealed, e-bid, two-envelope, etc.)
   - [ ] Bid is being delivered before the deadline (on most public bids, late = automatic disqualification with no exceptions)
   - For private bids, drop the bid bond / DBE / non-collusion items but keep validity, signer, addenda, and submission method.

4. **Internal-only flags** (separate from the proposal document):

   - Where the schedule has thin contingency
   - Where price assumes a sub buyout that hasn't been verified (price exposure)
   - Where escalation is held flat past a date that is unrealistic (commodity exposure)
   - Where exclusions are likely to be challenged (recommend pre-bid clarification call to owner)
   - Where the LD exposure is material vs. fee
   - Where the firm is materially below the next-lowest expected bid (the "winner's curse" check)

**Output requirements:**

Markdown proposal document with this structure for a private/CMAR/GMP/design-build response:

```
# Proposal — [Project Name] — [Solicitation #]

[Cover letter — addressed to recipient by name]

## 1. Firm Qualifications
[Company snapshot, bonding, insurance, certifications, key personnel, three-to-five comparable projects]

## 2. Approach to the Work
[Self-perform vs. sub plan; procurement; QA/QC; safety; schedule control; logistics]

## 3. Scope, Exclusions, and Clarifications
### 3.1 Scope Summary (by CSI Division / Phase)
### 3.2 Inclusions
### 3.3 Exclusions
### 3.4 Clarifications / Qualifications
### 3.5 Allowances
### 3.6 Alternates
### 3.7 Unit Prices

## 4. Cost Summary
[Format matches the solicitation — lump sum / GMP exhibit / CMAR fee schedule / bid form reproduction]

## 5. Schedule
[Milestones; calendar days vs. working days; LD awareness]

## 6. Terms
[Payment, change orders, warranty, insurance, bonds, validity]

## 7. Attachments
[Bid bond, addenda ack, DBE form, non-collusion, sub list, certifications, references, financials, insurance certificates — as applicable]

---

_This proposal was prepared with AI assistance from estimating data supplied by [firm]. Cost figures reflect a complete, conforming bid based on the contract documents listed above, including all addenda acknowledged. Stated exclusions and clarifications are integral to the price and govern over any conflicting interpretation._
```

For public ITB, the proposal is the agency's bid form plus the required attachments — do not invent a different structure.

- Cite the contract form and clauses in clarifications (e.g., "Per AIA A102 §7.3.3, change-order markups apply at..."). Never just "per contract."
- Severity color-code the internal flags only: 🔴 high (price-affecting; recommend resolving pre-bid), 🟡 medium (manage during buyout), 🟢 low (note for award meeting).
- Saved to `outputs/` if the user confirms.

## Example Output

**Example input:**
> Private negotiated proposal. Project: Brookline Medical Office Building TI, Phase 2. Owner: Brookline Medical Partners LLC (Frank Lee, COO). Form: AIA A102-2017 (cost-plus-fee with GMP). Type: 18,400 SF Class A medical-office tenant improvement, Level 3 of an existing 5-story building, occupied tenants on Levels 1-2 and 4-5. Scope: full demo of existing TI, new partitions per A2.04 with two demising walls rated UL U419, new HVAC distribution tied to existing rooftop, new med-gas distribution per spec 22 62 13, low-voltage and IT rough-in, casework and millwork, finishes per spec book. Cost: GMP target $4,650,000 ($253/SF). Schedule: NTP 2026-06-15, substantial completion 2026-12-15, final 2026-12-31. CMAR fee 4.5% on cost; GC contingency 3% of cost (CM-controlled); owner contingency 5% (owner-controlled). Three comparable projects: 2025 Mt. Auburn MOB Phase 1 ($3.9M, 14k SF, completed on schedule); 2024 Newton-Wellesley OBGYN ($5.2M, 22k SF, three weeks early); 2023 Beth Israel Lahey Cardiology ($6.8M, 28k SF, on schedule). EMR 0.78. Bonded to $25M single / $80M aggregate by Liberty Mutual. Massachusetts CSL #CS-099876. 25 employees. Hard exclusions: hazmat / lead / mold / asbestos abatement (assume none present per owner's 2026-04-10 limited survey); FF&E; signage; med-gas certification by med-gas vendor (we coordinate, vendor stamps); after-hours work beyond what is necessary for noisy/wet activities adjacent to occupied tenants (already in cost: 22 night shifts and 4 weekend shifts); escalation held to materials released by 2026-07-30. Allowances: door hardware $42,000; flooring transitions $18,000; window-treatment coordination $12,000. One alternate: Add stone countertops in lieu of solid surface in break room (Add $14,500). One unit price: structured cabling station drops beyond bid quantity of 96, $385/drop installed.

**Expected output (excerpt — full proposal would be ~12 pages):**

> # Proposal — Brookline Medical Office Building TI Phase 2 — RFP-2026-BMP-03
>
> **Northwood Builders, Inc.**
> 14 Industrial Way, Suite 200, Waltham, MA 02451
> Massachusetts CSL #CS-099876 | Federal EIN 04-XXXXXXX | DUNS / SAM UEI: ABCD12345678
>
> 2026-04-27
>
> Frank Lee, COO
> Brookline Medical Partners LLC
> 245 Beacon Street, Brookline, MA 02446
>
> **Subject: AIA A102 CMAR Proposal — Brookline MOB TI Phase 2**
>
> Dear Mr. Lee,
>
> Northwood Builders is pleased to submit this proposal for the Brookline MOB TI Phase 2 project under AIA A102-2017 (CMAR with GMP). We acknowledge Addenda #1 (2026-04-12) and #2 (2026-04-22). Three projects directly comparable to this scope — Mt. Auburn MOB Phase 1, Newton-Wellesley OB/GYN TI, and Beth Israel Lahey Cardiology — were completed on or ahead of schedule, all with active adjacent tenants and live medical-gas systems.
>
> Our **Guaranteed Maximum Price** for the work described in the contract documents and addenda, including the inclusions, exclusions, allowances, alternates, and unit prices set out in Section 3 below, is:
>
> **GMP Target: $4,650,000** (CMAR fee 4.5% on cost; CM contingency 3%; owner contingency 5%)
>
> This proposal is valid for **90 days** from the date above.
>
> John Halloran, President — Northwood Builders, Inc.
>
> Signature: ____________________ Date: ___________
>
> ---
>
> ## 1. Firm Qualifications
>
> | Item | Detail |
> |---|---|
> | Founded | 1998 |
> | Employees | 25 |
> | Bonding | $25M single / $80M aggregate (Liberty Mutual) |
> | EMR | 0.78 |
> | Insurance | GL $2M/$4M; Auto $1M; WC statutory; Umbrella $10M; Builders' Risk available on award |
> | License | Massachusetts CSL #CS-099876 |
>
> **Comparable projects:**
>
> | Project | Owner | Year | Value | Status |
> |---|---|---|---|---|
> | Mt. Auburn MOB Phase 1 (14k SF TI) | Mt. Auburn Partners | 2025 | $3.9M | On schedule, AHJ-passed first review |
> | Newton-Wellesley OB/GYN TI (22k SF) | Newton-Wellesley Hospital | 2024 | $5.2M | 3 weeks early; med-gas certified |
> | Beth Israel Lahey Cardiology (28k SF, occupied adjacencies) | BILH | 2023 | $6.8M | On schedule; zero work-stop notices |
>
> **Key personnel** (resumes attached): Project Executive — Eve Costa (16 yrs MOB/healthcare TI); Project Manager — Sam Patel (11 yrs); Superintendent — Mike Chen (19 yrs, occupied-environment TI specialist); Safety Officer — Linda Reyes (OSHA 30, healthcare-construction certificate).
>
> ## 2. Approach to the Work
>
> - **Self-perform:** Carpentry rough/finish, project supervision, demo, daily protection of occupied adjacencies. **Subcontract:** mechanical, plumbing, electrical, fire alarm, fire sprinkler, med-gas, casework/millwork, painting, flooring, ceilings, low-voltage, glazing.
> - **Procurement:** Pre-buy med-gas distribution components (currently 8-10 wk lead) and main HVAC equipment (currently 14 wk lead); confirm releases by 2026-07-30 to hold escalation freeze.
> - **Quality / safety / schedule:** Healthcare-construction site-specific safety plan with ICRA Class III/IV protocols where applicable; ILSM (Interim Life Safety Measures) plan reviewed with facilities; weekly pull-plan with each trade foreman; six-week look-ahead reviewed with owner monthly; OSHA 10 minimum for all field workers, OSHA 30 for foremen.
> - **Logistics:** Material moves before 7:00 AM and after 6:00 PM; freight elevator scheduled with building manager; negative-pressure containment at demo lines; daily dust/IAQ verification; 22 budgeted night shifts and 4 weekend shifts for noisy/wet activities adjacent to active tenants.
>
> ## 3. Scope, Exclusions, and Clarifications
>
> ### 3.1 Scope Summary (by CSI Division)
>
> Selective demolition of existing TI to deck and slab where required (02 41 19); new 3⅝" and 6" metal-stud partitions including two UL U419 1-hour-rated demising walls slab-to-deck (09 21 16); new ACT, gyp, and selective wood ceilings (09 51 13 / 09 21 16); flooring per finish schedule including carpet tile, LVT, sheet vinyl, and porcelain tile (09 65 / 09 68); painting per spec book one-prime / two-finish (09 91 23); doors, frames, and hardware (08 11 13 / 08 71 00); demountable glass partition system per spec 10 22 39; casework and solid-surface countertops (12 35 30 / 12 36 23); HVAC duct and grille distribution from existing rooftop (23 31 00 / 23 37 00); plumbing distribution including ADA fixtures (22 40 00); electrical distribution from existing panel including new lighting and controls (26 51 00 / 26 09 23); fire alarm extension (28 31 00); fire sprinkler relocation (21 13 00); medical-gas distribution per 22 62 13 with vendor certification; low-voltage rough-in including 96 station drops (27 15 00). All work per architect's drawings A1.00–A8.04 dated 2026-03-15 with addenda 1 and 2.
>
> ### 3.2 Inclusions
> - All trades listed above per contract documents and addenda
> - General conditions: project supervision, site office, dumpsters, temporary protection, parking validations, IAQ monitoring, dust control
> - GC-coordinated permits and AHJ inspection coordination (permit fees pass-through if owner-pay; see exclusions)
> - Builders' Risk on award (rate to be confirmed; pass-through at actual)
>
> ### 3.3 Exclusions
> - **Hazardous materials** of any kind (asbestos, lead-based paint, mold, PCB, mercury). Pricing assumes none present per owner's 2026-04-10 limited environmental survey. Discovered hazmat is a change order.
> - **FF&E**, signage, exam equipment, IT equipment, and millwork beyond what is in the casework specification
> - **Med-gas certification** by certifying agency (vendor performs; vendor stamps; we coordinate)
> - **Tenant relocation, occupied-tenant move services**, and any owner-required interior signage to active tenants
> - **Permit fees** if owner-pay (Brookline TI permit currently $1.10/SF; confirm payor)
> - **Testing & inspection (T&I)** if owner-pay per contract
> - **AHJ-required upgrades** discovered post-permit issuance (path-of-egress, ADA, code-edition mismatch); change-order recovery
> - **After-hours work** beyond the 22 night shifts and 4 weekend shifts already in cost
> - **Escalation** beyond what is captured by material releases by 2026-07-30; commodity exposure on items released later is owner's
> - **LEED, WELL, or other certification** documentation; not specified in this RFP
>
> ### 3.4 Clarifications / Qualifications
> - **Door hardware allowance** ($42,000): reconciled at actual cost; selections by 2026-08-15 to hold the schedule. Allowance is not a not-to-exceed cap.
> - **Flooring transitions allowance** ($18,000): reconciled at actual cost.
> - **Window-treatment coordination allowance** ($12,000): coordination only; window treatments themselves are owner-furnished per 3.3.
> - **Demising wall rated joint detail** (slab-to-deck) per drawing A6.04 / spec 09 21 16 §3.3.B; no spray-applied firestop assumed except at floor and deck conditions.
> - **Fire alarm modifications** assumed to be additive to the existing system; full panel replacement is not in scope.
> - **Liquidated damages**: none stated in solicitation; if added in contract, schedule contingency reduced and price will be revised.
> - **Lien waivers** per Massachusetts statutory form (M.G.L. c.254 §32) per knowledge-base reference.
>
> ### 3.5 Allowances
>
> | Allowance | Description | Amount | Mechanic |
> |---|---|---|---|
> | A1 | Door hardware | $42,000 | Reconciled at actual; CO if over |
> | A2 | Flooring transitions | $18,000 | Reconciled at actual; CO if over |
> | A3 | Window-treatment coordination | $12,000 | Reconciled at actual; CO if over |
>
> ### 3.6 Alternates
>
> | Alt | Description | Cost Impact | Decision Deadline |
> |---|---|---|---|
> | Alt-1 | Stone countertops in break room (in lieu of solid surface) | Add $14,500 | 2026-08-01 |
>
> ### 3.7 Unit Prices
>
> | UP | Description | Unit | Price | Conditions |
> |---|---|---|---|---|
> | UP-1 | Additional structured-cabling station drops | each | $385 installed | Beyond base bid 96 drops |
>
> ## 4. Cost Summary (GMP buildup)
>
> | Item | Amount |
> |---|---|
> | Direct work (CSI Divisions 02–28) — sub buyouts and self-perform | $3,950,000 |
> | General conditions — supervision, temp protection, IAQ, dumpsters, after-hours premium | $295,000 |
> | CM contingency — 3% of cost (CM-controlled per A102 §6.4) | $127,000 |
> | Subtotal cost | $4,372,000 |
> | CMAR fee — 4.5% on cost | $197,000 |
> | **GMP (excludes Owner Contingency)** | **$4,569,000** |
> | Owner contingency — 5% (owner-controlled, additive to GMP per §6.5) | $228,000 |
> | **GMP including Owner Contingency** | **$4,797,000** |
>
> Pricing is open-book per A102. Shared-savings split per §6.7 to be set in the contract (Northwood proposes 25% CM / 75% Owner on savings vs. GMP).
>
> ## 5. Schedule
>
> Calendar days from NTP. Substantial completion includes AHJ inspections passed and all life-safety systems active.
>
> | Milestone | Date |
> |---|---|
> | NTP | 2026-06-15 |
> | Permit issued (target) | 2026-07-01 |
> | Demo complete | 2026-07-22 |
> | Rough-in 70% complete | 2026-09-30 |
> | Above-ceiling sign-off | 2026-10-15 |
> | Finishes start | 2026-10-20 |
> | AHJ life-safety inspection | 2026-12-08 |
> | Substantial completion | 2026-12-15 |
> | Final completion / closeout package delivered | 2026-12-31 |
>
> Schedule assumes no LDs (none stated in RFP), no winter shutdown beyond inability to deliver materials in a Boston-area winter storm event, and material releases by 2026-07-30 to hold escalation.
>
> ## 6. Terms
>
> - Payment per AIA G702/G703, monthly applications, net 30 from approval; retainage 5% reduced to 2.5% at 50% complete per A102 §9.6.4
> - Change orders signed before work proceeds; cost-only when scope-defined; T&M with cap when not; markups per A102 §7.3.3
> - Standard one-year general warranty from substantial completion; manufacturer warranties pass-through
> - Insurance certificates and bonds available on award (performance and payment bonds at 100% of contract per Liberty Mutual)
> - Validity: 90 days from 2026-04-27
>
> ## 7. Attachments
>
> 1. Resumes — Costa, Patel, Chen, Reyes
> 2. Reference list with owner contacts (verified 2026-04-25)
> 3. Insurance certificate sample
> 4. Letter of bondability — Liberty Mutual
> 5. Audited 2024 + 2025 financial statements (under separate confidential cover)
> 6. CMAR fee proposal worksheet (open-book exhibit)
> 7. Site-specific safety / ICRA / ILSM narrative (3 pages)
>
> ---
>
> _This proposal was prepared with AI assistance from estimating data supplied by Northwood Builders. Cost figures reflect a complete, conforming bid based on the contract documents and addenda listed above. Stated exclusions, clarifications, allowances, alternates, and unit prices are integral to the GMP and govern over any conflicting interpretation._
>
> **Internal flags (not for transmission):**
> - 🔴 Med-gas distribution lead time tight; confirm release by 2026-07-30 or escalation moves to owner
> - 🟡 Demising-wall rated joint detail historically a punch-walk issue; pre-installation meeting with drywall sub recommended
> - 🟡 Flooring transition allowance is on the low side for 18,400 SF with three flooring types — pre-buy mockup recommended
> - 🟢 No bid bond required (private CMAR); ensure performance/payment bonds are issued within 10 days of award per §11.5
