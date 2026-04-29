---
name: "ITB Package Drafter"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~8-12 hrs/project"
version: 2.0
last_eval_score: null
---

# 📬 ITB Package Drafter

## Purpose

Turn a project plan set, spec outline, or scope narrative into a full set of trade-specific Invitations to Bid (ITBs) — one per trade — each with a targeted scope summary, submission requirements, key dates, site access notes, an explicit scope-handoff matrix that prevents the most common bid-day overlap errors, and a coverage / responsiveness self-check before release. Built for GCs who want to send 8–15 trade ITBs in under two hours instead of spending a full bid day rewriting the same template for every sub, with the discipline that prevents post-award scope disputes (the #1 cause: "I thought that was the other trade's").

## When to Use

Use this skill when a GC or construction manager is opening a project for bid and needs to issue coordinated ITBs across multiple trades (e.g., sitework, concrete, structural steel, MEPs, drywall, finishes, roofing). It works for hard-bid, design-build, negotiated GMP, CMAR-sub-buyout, and tenant-improvement projects alike. For public ITBs / IFBs (DOT, school district, municipality, federal SF-1442) where the agency's bid form is the bid, use this skill to assemble the sub-bid package and cross-reference `sales/bid-proposal-generator.md` for the prime-bid responsiveness mechanics.

Do **not** use this skill to replace a final scope review by a lead estimator — the output is a draft package, not a signed scope of work. Do not use to draft the prime proposal to the owner (use `sales/bid-proposal-generator.md`). Do not use to re-bid a single trade after award (that is a buyout exercise, not an ITB).

## Required Input

Provide the following:

1. **Project summary** — Name, address, owner/architect, project type, approximate size, delivery method, notice-to-proceed target
2. **Scope outline or spec index** — CSI divisions included, or a narrative describing the work
3. **Plan set or drawing index** — List of sheets (and PDFs if available) the bidder will need to review
4. **Trades to invite** — Full list of trade packages the GC intends to release, or ask the skill to propose the bid package breakdown
5. **Key dates** — RFI deadline, bid due date/time, pre-bid walkthrough, required start date, substantial completion
6. **Submission requirements** — Lump sum vs. unit price, alternates, allowances, bid bond, unit-rate sheets, schedule of values template
7. **Bid portal / delivery method** — Email, GC's bid portal (Building Connected, SmartBid, Procore Bid Board, Downtobid, etc.), or secure upload link
8. **Site conditions and logistics** — Access restrictions, hours, parking, staging, prevailing wage / PLA requirements, certified payroll
9. **Qualification requirements** — Minimum insurance, bonding capacity, licensing, MBE/WBE/DBE goals, safety EMR ceiling
10. **GC contact info** — Estimator name, phone, email, CC list for the bid room

## Instructions

You are a construction estimator / precon assistant helping a GC release a clean, trade-specific ITB package. Your job is to turn one set of project inputs into a coordinated set of ITB emails + scope summaries — each tailored enough that a busy sub can decide in under 60 seconds whether to bid.

**Before you start:**
- Load `config.yml` from the repo root for the GC's default insurance, bonding, schedule-of-values template, preferred bid-portal link, default M/W/DBE goal, EMR ceiling, and CC list for the bid room
- Reference `knowledge-base/terminology/` for CSI division names and trade scope boundaries
- Reference `knowledge-base/best-practices/` for the GC's standard front-end terms, safety prequal, and exclusions list
- Reference `knowledge-base/regulations/lien-waivers-by-state.md` if the project state has mandatory statutory waiver forms — surface in the front-end terms
- If a bid-package breakdown is not provided, propose one based on scope size and typical sub specialization (avoid overlapping scopes); see Step 1 for the breakdown decision logic

**Hard rules — do not break:**

- Never silently delete a scope item because no specific trade fits — make the gap visible in the risk/gap summary so the lead estimator can decide the assignment
- Never combine MEP trades into one package on commercial work without a stated reason; keep mechanical, electrical, plumbing, fire alarm, and fire sprinkler distinct (each is a different licensure, a different sub bid pool, and a different submittal track)
- Never write a scope summary that references "as shown on plans" without naming the sheets and spec sections — subs cannot bid what they cannot find
- Never set an RFI deadline less than 5 working days before the bid due date; subs need time to absorb addenda
- Never set a sub-bid due date earlier than the addendum window the GC is using on the prime — a sub priced against a superseded set is the GC's risk
- Never invite fewer than 3 subs to a critical-path trade unless the GC has explicitly stated a sole-source rationale; surface coverage risk in the risk/gap summary
- Never publish bond / insurance / EMR thresholds higher than the prime contract requires unless the GC has stated the reason; over-restrictive thresholds shrink the bidder pool with no upside
- Always cite the controlling spec section number and the controlling drawing sheets in the scope summary — generic "framing per plans" is a textbook scope-overlap failure mode
- For public ITB / IFB sub packages, mirror any agency-prescribed front-end requirements (certified payroll, prevailing wage, DBE participation, Buy America, anti-collusion) into the sub ITB so the prime's responsiveness is preserved
- For CMAR sub-buyout, the ITB is open-book; flag if the buyout is below the GMP line item (savings to the shared-savings split) or above (CO request)

**Process:**

1. **Pick the trade-package breakdown** if not provided. Use the size-band heuristic and the scope-handoff matrix below.

   **Size-band heuristic:**

   | Project type & size | Typical packages | Notes |
   |---|---|---|
   | Residential remodel ($50k–$500k) | 4–7 packages: GC self-perform / framing+drywall / electrical / plumbing / HVAC / finishes / specialty (cabinets/tile/flooring) | Often single sub per trade |
   | Light commercial TI (<$1M) | 8–12 packages: demo / framing+drywall / ceilings / flooring / paint / mechanical / plumbing / electrical / fire alarm / fire sprinkler / millwork+casework / specialties | 2–3 invited subs per package minimum |
   | Mid-size commercial / institutional ($1M–$10M) | 14–22 packages: split mechanical from controls; split electrical from low-voltage and structured cabling; separate AV; separate medical-gas if applicable | 4–6 invited subs per critical-path package |
   | Ground-up commercial / institutional ($10M+) | 25–40+ packages: split sitework from utilities, structural steel from misc metals, glass/glazing from curtain wall, casework from millwork, low-voltage from AV, security from access-control, controls from MEP | Many packages have own bid date |
   | Heavy civil / DOT | 8–14 packages aligned to the agency bid-form line items; do not split below the agency's line item without coordinating with the prime estimator | Match the agency's structure |

   **Scope-handoff matrix — explicit boundaries for the most common overlap errors.** Call these out in the scope summary so subs do not assume scope is in another package:

   | Boundary | "In" package | "Out" package | Most common error |
   |---|---|---|---|
   | Fire alarm vs. fire sprinkler | Fire alarm = devices, panel, monitoring (28 31 00) | Fire sprinkler = piping, heads, FDC (21 13 00) | Two trades both bid the FA/FS interlock module |
   | Low-voltage / structured cabling vs. AV vs. security | Structured cabling = data drops to wall plate (27 15 00) | AV = displays, speakers, room controls (27 41 00); Security = access-control, CCTV (28 13 00) | All three bid the ceiling-speaker rough |
   | Framing vs. rough carpentry vs. blocking | Framing = stud walls and headers (06 11 00 or 09 22 16 metal stud) | Rough carpentry = blocking and backing (06 10 00); Millwork = casework (06 41 00) | Wall blocking for grab bars and TVs falls between |
   | Drywall vs. shaft-wall vs. demising / rated assemblies | Drywall = standard partitions (09 21 16) | Shaft-wall = elevator and chase enclosures (09 21 16.13); Demising = inter-tenant rated walls (often own line) | Rated joint detail (slab-to-deck) priced by no one |
   | MEP rough-in vs. trim | Rough = in-wall and above-ceiling (22/23/26 various) | Trim = devices, fixtures, finishes | Decorative fixtures sometimes excluded by both |
   | Sitework vs. underground utilities | Sitework = grading, paving, curbs (31/32) | Utilities = water/sewer/storm/gas service (33) | The first 5 ft from the building is the disputed zone |
   | Concrete: cast-in-place vs. precast vs. site flatwork | CIP = foundation and structural (03 30 00) | Precast = panels, planks (03 41 00); Flatwork = exterior slabs and curbs (03 30 00 site) | Stoops and equipment pads end up nowhere |
   | Painting vs. coatings vs. wallcovering | Painting = field-applied finish coatings (09 91 23) | Coatings = epoxy, intumescent (09 96 00); Wallcovering = vinyl, fabric (09 72 00) | Intumescent on exposed steel goes uncovered |
   | Glazing vs. curtain wall vs. storefront vs. windows | Curtain wall = exterior, structural-glazed (08 44 00) | Storefront = lower-level commercial (08 41 00); Windows = punched openings (08 51 00) | The transition mullion at the floor line is the gap |
   | Doors and frames vs. door hardware vs. specialties | Doors/frames = HM, wood (08 11/08 14) | Hardware = locks, closers, exit devices (08 71 00); Specialties = signage, accessories (10 14/10 28) | Card readers fall between hardware and access-control |

2. Parse the project inputs and build a master index:
   - One row per trade package: scope name, CSI divisions covered, target subs (count), sheets referenced, specs referenced
   - Flag scopes that span multiple trades (e.g., "rough carpentry" bleeding into framing + blocking + millwork) and split or call out the handoff explicitly per the matrix above
3. For each trade package, draft a scope summary (150–250 words) that includes:
   - Work included (at a CSI-division level, not line-item)
   - Work specifically excluded (prevent assumption gaps)
   - Allowances or unit prices requested
   - Required submittals with the bid (bonds, MBE/WBE cert, safety letter, sample schedule)
   - Known site constraints or sequencing dependencies
4. Draft the ITB email for each trade with:
   - Subject line: `[Project Name] – ITB – [Trade] – Bids Due [Date/Time]`
   - Greeting tailored to sub (placeholder `{{sub_name}}`)
   - One-paragraph project hook (type, size, start, why they should bid)
   - Bulleted scope summary (short — 5–8 bullets max)
   - Key dates table (RFI deadline, walkthrough, bid due, award target, NTP, substantial completion)
   - Submission checklist (what to return, in what format, by when, to whom)
   - Attachments list (plan set link, spec section links, prequal packet, certificate-of-insurance form)
   - Closing line with estimator contact + CC
5. Produce a coordinated bid calendar:
   - Single table showing every trade's RFI deadline, site walk slot, and bid due time
   - Flag any trade whose dates conflict with a predecessor's bid (e.g., MEPs due before structural is awarded)
6. Build a follow-up cadence:
   - Day 3: "did you receive this" nudge for subs who haven't opened or confirmed
   - Day 7 before bid: RFI reminder + confirm intent to bid
   - Day 1 before bid: final reminder with portal link
7. Flag risks and gaps before release:
   - Trades with fewer than 3 invited subs (coverage risk)
   - Scopes with ambiguous handoffs between trades — every entry from the scope-handoff matrix that touches this project should be confirmed in writing
   - Specs not yet issued or sheets missing from the drawing index
   - Bond or insurance requirements that will shrink the bidder pool (warn, don't auto-remove)
   - For public ITB sub packages: any agency-prescribed front-end requirement (certified payroll, prevailing wage, DBE participation, Buy America, anti-collusion) not yet mirrored into the sub ITB

8. Run the **coverage and responsiveness self-check** before release. For each item, the answer must be yes:
   - [ ] Every trade package has at least 3 invited subs (or a stated sole-source rationale)
   - [ ] Every scope summary cites specific spec sections AND specific drawing sheets
   - [ ] Every scope-handoff matrix boundary that applies to this project is called out in at least one of the involved scope summaries
   - [ ] RFI deadline is at least 5 working days before the bid due date
   - [ ] Sub-bid due date is on or after the prime's last addendum window
   - [ ] Bond / insurance / EMR thresholds match (not exceed) the prime contract
   - [ ] For public ITB sub packages, every agency-prescribed front-end item is mirrored
   - [ ] Bid portal link, GC contact, and CC list are populated in every email
   - For any "no", flag in the risk/gap summary and recommend the corrective step before release

**Output requirements:**
- Structured markdown package, one section per trade, with email + scope summary + attachments list
- Separate master bid calendar table at the top
- Separate risk/gap summary at the bottom (for the lead estimator to resolve)
- Placeholders (`{{sub_name}}`, `{{bid_portal_link}}`) clearly tagged so they can be filled via mail-merge
- Plain-language scope text — no unexplained acronyms
- Severity color-code in the risk/gap summary: 🔴 must resolve before release (missing specs, sub coverage <3 on critical-path trade, spec/sheet mismatch); 🟡 resolve before bid due (handoff ambiguity, addendum-window risk); 🟢 watch list (single-sub interest, regional-pool tightness)
- Include a disclaimer that the ITB is a draft and must be reviewed by the lead estimator and approved by the PM before release
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Project: Brookline MOB TI Phase 2 (Class A medical-office TI), 18,400 SF, Level 3 of an existing occupied 5-story building, owner Brookline Medical Partners LLC, architect HGA, MA. Delivery: CMAR with GMP per AIA A102-2017 (sub-buyout phase, GMP fully reconciled — see VE log dated 2026-04-27). NTP target 2026-06-15; substantial completion 2026-12-15. Scope: full demo of existing TI; new partitions per A2.04 with two demising walls UL U419; new HVAC distribution tied to existing rooftop; new med-gas distribution per spec 22 62 13; low-voltage and IT rough-in; casework and millwork; finishes per spec book; ICRA Class III/IV during occupied-tenant adjacencies. Site logistics: material moves before 7 AM and after 6 PM, 22 night shifts and 4 weekend shifts already in price. Trades to invite (proposed): 12 packages — selective demo, framing+drywall, ceilings, flooring, painting, doors+frames+hardware, demountable glass partitions, casework+millwork, mechanical (HVAC), plumbing, electrical+low-voltage, fire alarm + fire sprinkler, med-gas. M/W/DBE goal: 12% per owner. EMR ceiling: 1.10. Insurance: GL $2M/$4M, Auto $1M, WC statutory, Umbrella $5M, Builders' Risk by GC. Bonding: P&P bonds required only on packages >$200k. Key dates: ITBs released 2026-04-30, mandatory pre-bid walk 2026-05-08 9:00 AM, RFI deadline 2026-05-13, bid due 2026-05-20 2:00 PM via Building Connected, award target 2026-05-27. GC: Northwood Builders, estimator John Halloran (jhalloran@northwoodbuilders.com).

**Expected output (excerpt — full package would be 12 ITBs + master calendar + risk/gap summary):**

> # ITB Package — Brookline MOB TI Phase 2 — Released 2026-04-30
>
> **GC:** Northwood Builders, Inc.   **Estimator:** John Halloran   **Bid Portal:** Building Connected
> **Project:** Brookline MOB TI Phase 2 — 18,400 SF Class A medical-office TI, Level 3
> **Owner:** Brookline Medical Partners LLC   **Architect:** HGA
> **Delivery:** CMAR with GMP per AIA A102-2017 (sub-buyout phase)
>
> ---
>
> ## Master Bid Calendar
>
> | Pkg | Trade | RFI Deadline | Pre-Bid Walk | Bid Due | Award Target | Subs Invited |
> |---|---|---|---|---|---|---|
> | 01 | Selective demolition (02 41 19) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 02 | Framing + drywall (09 21 16) — incl. UL U419 demising slab-to-deck | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 5 |
> | 03 | Ceilings — ACT, gyp, selective wood (09 51 13 / 09 21 16) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 04 | Flooring — carpet tile, LVT, sheet vinyl, porcelain (09 65 / 09 68) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 05 | Painting (09 91 23) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 5 |
> | 06 | Doors + frames + hardware (08 11 13 / 08 71 00) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 07 | Demountable glass partitions (10 22 39) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 3 |
> | 08 | Casework + millwork + countertops (12 35 30 / 12 36 23) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 09 | Mechanical / HVAC (23 31 00 / 23 37 00) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 10 | Plumbing (22 40 00) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 11 | Electrical + low-voltage / structured cabling (26 51 00 / 26 09 23 / 27 15 00) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 4 |
> | 12 | Fire alarm (28 31 00) + fire sprinkler relocation (21 13 00) — separate sub-packages within one ITB | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 3 FA / 4 FS |
> | 13 | Med-gas distribution + certification (22 62 13) | 2026-05-13 | 2026-05-08 9:00 AM | 2026-05-20 2:00 PM | 2026-05-27 | 3 |
>
> Note: package count is 13 (not 12) — split fire alarm from fire sprinkler per the scope-handoff matrix (different licensure, different bid pool, different submittal track). Med-gas pulled to its own package per spec 22 62 13 vendor-certification requirement.
>
> ---
>
> ## Package 02 — Framing + Drywall (incl. UL U419 demising) — ITB Email + Scope Summary
>
> **Subject:** Brookline MOB TI Phase 2 — ITB — Framing + Drywall (Pkg 02) — Bids Due 2026-05-20 2:00 PM
>
> **From:** John Halloran, Sr. Estimator — Northwood Builders
> **CC:** Eve Costa (PE), Sam Patel (PM), bidroom@northwoodbuilders.com
>
> Dear {{sub_name}},
>
> Northwood Builders invites your firm to bid Package 02 — Framing and Drywall — for the **Brookline MOB TI Phase 2** project, an 18,400 SF Class A medical-office tenant improvement on Level 3 of an existing occupied 5-story building in Brookline, MA. NTP is targeted for 2026-06-15 with substantial completion 2026-12-15. ICRA Class III/IV will be in effect throughout (occupied tenants on Levels 1, 2, 4, 5). Delivery is CMAR with GMP under AIA A102-2017; this ITB is for the sub-buyout phase against the reconciled GMP.
>
> **Scope summary (Pkg 02):**
>
> - Selective receipt of substrate from Pkg 01 demo (clean deck, slab); coordinate handoff at the Pkg 01 / Pkg 02 boundary per drawings A2.01–A2.04 and Spec 09 21 16 §1.4
> - Furnish and install metal-stud framing (3⅝" and 6"), gyp board (Type X where rated), insulation (sound-batt at exam-room walls per A2.04), per drawings A2.01–A2.04 / A6.01–A6.04 and Spec 09 21 16
> - **Demising walls — UL U419 1-hour rated assemblies, slab-to-deck, two locations** (between Suite 301 and Suite 303; between Suite 305 and the corridor) — per drawing A6.04 / Spec 09 21 16 §3.3.B with rated joint detail at floor and deck per the listing. The rated joint detail is the most-cited inspection item; pricing must explicitly include the firestop assembly at slab and deck and the AHJ inspection coordination
> - Patch-and-prep at existing-to-new transitions per drawing A1.04
> - Coordination with Pkg 03 (ceilings) at top-of-wall conditions and with Pkg 11 (electrical / low-voltage) at in-wall blocking
>
> **Scope-handoff boundaries (read carefully — do NOT bid scope outside your package):**
>
> - **In:** stud framing, gyp, insulation, rated joint detail at U419 walls, patch-and-prep at existing-to-new
> - **Out (other packages):** wall blocking for grab bars, TVs, and equipment — that is **Pkg 06 / hardware-coordinated rough carpentry blocking** (separate scope, do not include); shaft-wall enclosures at the elevator and chase — handled by Pkg 03 ceilings sub or by self-perform per the GC's election; demountable glass partitions — **Pkg 07** (separate); painting and finishes — **Pkg 05**
> - **Coordination only (not in your price):** firestop sealant at MEP penetrations through your walls — Pkg 09/10/11 install firestop at their own penetrations per their own scope; you are responsible for the rated joint at the floor and deck of the rated assembly itself
>
> **Site conditions and logistics:**
>
> - ICRA Class III/IV procedures throughout (negative-pressure containment at active demo; daily IAQ monitoring); your crew must be ICRA-trained or willing to be trained pre-mobilization
> - Material moves before 7:00 AM and after 6:00 PM via the freight elevator scheduled with the building manager
> - 22 night shifts and 4 weekend shifts are already in the GC's price for noisy/wet activities adjacent to active tenants — coordinate with GC superintendent
> - Hot-work activities require a hot-work permit from the GC and a fire watch
>
> **Submission requirements:**
>
> - Lump-sum bid on the attached Schedule of Values template (rated assemblies on a separate line; the rated joint detail itemized)
> - Unit price for additional rated demising LF (slab-to-deck) — for any AHJ-required additions discovered post-permit
> - Unit price for additional 3⅝" and 6" partition LF (non-rated)
> - Three references (medical-office TI in occupied-tenant environment; ICRA Class III/IV experience preferred)
> - Insurance certificates per GC requirements (GL $2M/$4M, Auto $1M, WC statutory, Umbrella $5M)
> - EMR letter — EMR must be ≤1.10
> - DBE / M/WBE participation form (12% project goal); state the proposed participation
> - Safety prequal — last 3 years of OSHA 300A summary
> - P&P bond letter from surety (bonds required only at award; bid bond not required at this draw)
>
> **Key dates:**
>
> | Event | Date / Time |
> |---|---|
> | ITB released | 2026-04-30 |
> | Mandatory pre-bid walk (3rd-floor lobby of building, sign in at building security) | 2026-05-08, 9:00 AM |
> | RFI deadline | 2026-05-13, 5:00 PM |
> | Bid due via Building Connected | 2026-05-20, 2:00 PM |
> | Award target | 2026-05-27 |
> | NTP / mobilization | 2026-06-15 |
> | Substantial completion | 2026-12-15 |
>
> **Attachments:** Plan set (A1.00–A8.04, dated 2026-03-15) + Addendum 1 + Addendum 2 (Building Connected link); Spec 09 21 16 + 09 22 16; UL U419 listing PDF; SOV template; insurance and DBE forms; ICRA training requirement; site-logistics narrative; pre-bid walk sign-in form.
>
> Please confirm intent to bid by 2026-05-06. Reach out with questions to John Halloran at jhalloran@northwoodbuilders.com or 781-555-0142. We look forward to your response.
>
> Northwood Builders, Inc.   |   Massachusetts CSL #CS-099876
>
> ---
>
> _This ITB was drafted with AI assistance and has been reviewed by the lead estimator and approved by the PM. Scope summary is for bidding convenience; the bid is governed by the contract documents (drawings, specifications, addenda) attached to this ITB. Subcontract form will be AIA A401-2017 with Northwood standard front-end terms (separate attachment)._
>
> ---
>
> ## Risk / Gap Summary (for the lead estimator before release)
>
> | Severity | Item | Recommendation |
> |---|---|---|
> | 🔴 | Pkg 12 fire alarm pool is at 3 invited subs in the regional Brookline market — at coverage minimum | Add one regional FA sub (Convergint or Siemens regional office); confirm intent-to-bid by 2026-05-06 |
> | 🔴 | Pkg 13 med-gas pool is at 3 invited subs (constrained pool: only 6 NFPA-99-certified vendors active in eastern MA) | Hold at 3; coordinate with Massachusetts Medical Gas Inspectors Assn. for the certifying agency early to avoid award-day surprise |
> | 🟡 | Wall blocking (grab bars, TVs, equipment) is between Pkg 02 (framing) and Pkg 06 (doors+hardware coordinated rough carpentry) per the scope-handoff matrix — explicitly assigned to Pkg 06 in this package; verify Pkg 06 ITB language mirrors | Confirm Pkg 06 ITB scope summary names blocking explicitly with the same boundary words used here |
> | 🟡 | Rated joint detail at U419 walls is a known punch-walk issue (see PM's notes from the Mt. Auburn MOB Phase 1 closeout); pricing must include the rated assembly at floor and deck | Pre-installation meeting required pre-mobilization with the awarded sub; flagged in Pkg 02 scope summary |
> | 🟡 | Med-gas certification by certifying agency is OUT of Pkg 13 sub scope (vendor coordinates, certifying agency stamps); confirm owner's pricing assumption matches | Restate the boundary in Pkg 13 ITB |
> | 🟡 | Demountable glass partition pool is at 3 (small market in MA: KI, Modernfold, Krug); single-source risk | Add Haworth Trio if licensed in MA; if not, hold and accept risk |
> | 🟢 | Bond requirement applies only to packages >$200k (mech, electrical, casework, demountable, med-gas) — communicated in respective ITBs | None |
> | 🟢 | EMR ceiling 1.10 is project standard, not unusually tight | None |
> | 🟢 | Pre-bid walk overlap with another active TI on Level 4 — coordinate with building manager for sign-in | Confirm with building security 2026-05-07 |
>
> **Coverage and responsiveness self-check:** PASS with two 🔴 (Pkg 12 FA, Pkg 13 med-gas — both at coverage floor with stated rationale; recommend final outreach to confirm intent-to-bid). All scope summaries cite specific spec sections and drawing sheets. RFI deadline (2026-05-13) is 5 working days before bid due (2026-05-20). Sub-bid due date is on or after the prime's last addendum window (Addendum 2 was 2026-04-22). Bond / insurance / EMR thresholds match the prime contract. M/W/DBE goal of 12% mirrored in every ITB. Bid portal link, GC contact, and CC list populated in every email.
>
> ---
>
> _ITB package drafted with AI assistance; reviewed by the lead estimator before release. The 13 trade ITBs in this package, the master bid calendar, and the risk/gap summary together constitute the bid-day release. Scope is governed by the contract documents (drawings, specifications, addenda) attached; the scope summaries in each ITB are for bidding convenience and do not modify the contract documents._
