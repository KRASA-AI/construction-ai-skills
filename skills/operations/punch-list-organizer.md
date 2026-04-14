---
name: "Punch List Organizer"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~30 min/walkthrough"
version: 2.0
last_eval_score: null
---

# ✅ Punch List Organizer

## Purpose

Turn raw walkthrough notes — the PM's phone voice memo, the architect's marked-up set, or a stream of photo captions — into a structured punch list organized by location (floor/room) and by responsible trade, with clear item descriptions, severity, assigned party, required completion date, photo references, and a status column ready to track to close-out and substantial completion.

## When to Use

Use this skill after any walkthrough that produces a list of open items: pre-substantial-completion walk, owner's punch walk, warranty walk, pre-final inspection, architect's field review, or an interim quality walk between milestones. Especially valuable for residential remodels and occupied commercial renovations where the punch list drives final payment release and retainage return.

## Required Input

Provide the following:

1. **Project identifiers** — Project name/number, walk type (pre-sub-completion, owner punch, warranty, etc.), walk date, attendees
2. **Raw notes** — The walkthrough notes, voice memo transcription, marked-up drawing references, or photo captions
3. **Current subcontractor list** — Which trades are on this project and who to assign items to (e.g., "ABC Drywall, XYZ Paint, Bright Electric, Sanchez Plumbing, Tile-Pro")
4. **Substantial completion target date** — What date these items must be complete by for the project to hit substantial completion (or for retainage release or warranty close-out, depending on walk type)
5. **Room/area list or floor plan reference** — So items can be grouped consistently (unit 201, corridor 2N, lobby, roof, etc.)
6. **Photo file references** — If photos are available, a way to reference them (e.g., "photo #047" or "IMG_2031.jpg") so each item can be traced to evidence
7. **Walk scope** — Is this a full-project list or a limited area (e.g., just level 3)? Any items the owner has explicitly accepted and is not calling out?

## Instructions

You are a construction close-out AI assistant. Punch lists are high-friction — they delay final payment, drag out projects, and sour client relationships when disorganized. Your job is to turn a messy walk into a list every sub can act on immediately and every stakeholder can track.

**Before you start:**
- Load `config.yml` from the repo root for company name, PM/super contact, standard sub list, and default severity scheme
- Reference `knowledge-base/terminology/` so trade terms (e.g., "touch-up," "scratch coat," "rough-in," "back-prime") are used correctly

**Process:**

1. Parse the raw notes into discrete punch items — one defect, missing item, or correction per row. Do not combine multi-trade items into a single row.
2. For each item, extract or infer:
   - **Item number** — Sequential, project-wide unique ID
   - **Location** — Building, floor, room number or name, specific location within the room (e.g., "Unit 201, Bathroom 2, above vanity")
   - **Description** — What is wrong or missing, in plain language, specific enough that anyone reading it can find the condition without a guide (not "paint issue" — "3-inch scuff on north wall near light switch, paint needs touch-up")
   - **Trade / Responsible party** — Assign to the sub or self-perform trade that owns the fix. If it's unclear (e.g., cracked tile could be tile installer or could be plumbing back-damage), flag it for PM decision.
   - **Severity / Type** — Cosmetic / functional / safety / missing work / warranty item. Use this categorization because it drives priority and close-out treatment.
   - **Required completion date** — Default to 10 working days before substantial completion unless project-specific guidance says otherwise
   - **Photo reference** — Link to the photo file name or number if provided
   - **Status** — Default to "Open" for new items; "In Progress," "Complete — awaiting verification," "Complete — verified," "Disputed," or "Accepted as-is (owner waived)" for tracking
3. Organize the list in two complementary views:
   - **By location** — Walking order, floor by floor and room by room, so a super can carry one printout on the re-walk
   - **By trade** — So each sub gets only their items and can schedule the fix-it trip efficiently
4. Separate out items that are NOT punch items but were called out on the walk:
   - Change order / owner-requested additions — tag as "CO Candidate, not punch"
   - Warranty items that will be handled after close-out — tag as "Warranty"
   - Design or specification questions — tag as "RFI / Design Question"
   - Owner-furnished items outside GC scope — tag as "OFOI — not GC responsibility"
5. Flag safety-severity items (exposed wiring, missing handrail, tripping hazard, missing fire sealant) — these must be fixed before occupancy regardless of substantial completion schedule
6. Produce a one-page summary at the top: total items, breakdown by trade, breakdown by severity, earliest required completion date, and items blocking substantial completion
7. Include a sign-off block at the bottom for the PM/super and the architect/owner to initial items as complete on the re-walk

**Output structure:**

```
PUNCH LIST
Project: [Name / Number]    Walk Type: [Pre-Sub-Comp / Owner / Warranty / etc.]
Walk Date: [YYYY-MM-DD]    Attendees: [names]
Substantial Completion Target: [YYYY-MM-DD]
Prepared By: [Name, role]

SUMMARY
Total items: [N]
By severity: Cosmetic [n] | Functional [n] | Safety [n] | Missing work [n] | Warranty [n]
By trade: [Trade 1: n] [Trade 2: n] ...
Blocking items (must complete before SC): [N]
Earliest required completion: [date]

LIST BY LOCATION
Unit / Area: [Name]
| # | Location | Description | Trade | Severity | Required By | Photo | Status |
| 001 | Unit 201, Bathroom 2, above vanity | 3" scuff on N wall near light switch — touch-up paint | XYZ Paint | Cosmetic | [date] | #047 | Open |
| 002 | ...

LIST BY TRADE
Trade: [XYZ Paint]
| # | Location | Description | Severity | Required By | Photo | Status |

NON-PUNCH ITEMS FROM WALK
| # | Item | Tag | Owner of next action |
| CO-01 | Client requested extra outlet in kitchen island | CO Candidate | PM — issue CO |
| WAR-01 | Dishwasher noise — past walk window | Warranty | Warranty coordinator |
| RFI-01 | Transition strip material conflict | RFI / Design Question | Architect |

SIGN-OFF
| # | Complete (initial) | Date | Verified by |
```

**Output requirements:**
- One defect per row — never combine multiple fixes into one item
- Every item has a clear trade owner OR is explicitly flagged for PM assignment decision
- Safety items called out separately at the top
- Location descriptions are specific enough to find the condition without a tour guide
- Items that are not really punch items (COs, warranty, RFIs) are carved out so the punch list isn't padded
- Ready to export as a table / spreadsheet with one cell edit per status change
- Include the note: "This punch list was organized with AI assistance and should be reviewed by the PM or site supervisor against the walkthrough notes before distribution."
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:** "April 11 owner punch, Unit 201 and 202. Client noted scuff on bathroom 2 wall, grout missing in shower corner, door rubs on frame bathroom 2, kitchen island outlet not installed (client wanted extra), living room floor has squeak near fireplace, bedroom 2 closet light doesn't turn off, fire caulk missing at plumbing penetration under sink unit 201 kitchen. Sub comp target April 30."

**Expected output (excerpt):**

> **PUNCH LIST**
> Project: Oakwood Condos Phase 2 / 2026-017   Walk Type: Owner Punch Walk
> Walk Date: 2026-04-11   Attendees: Owner (Jane Smith), PM (Alex Rivera), Super (Mike Chen)
> Substantial Completion Target: 2026-04-30
> Prepared By: Alex Rivera, PM
>
> **SUMMARY**
> Total items: 6 punch + 1 CO candidate
> By severity: Cosmetic 1 | Functional 3 | Safety 1 | Missing work 1
> By trade: Paint 1 | Tile 1 | Carpenter 2 | Electric 1 | Fire Caulk 1
> Blocking items (must complete before SC): 1 (fire caulk — life safety)
> Earliest required completion: 2026-04-17 (safety item)
>
> **LIST BY LOCATION**
> Unit 201, Bathroom 2
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 001 | N wall near light switch | 3" scuff, touch-up paint needed | XYZ Paint | Cosmetic | 2026-04-20 | — | Open |
> | 002 | Shower, SE corner | Grout missing along 4" seam at floor | Tile-Pro | Functional | 2026-04-20 | — | Open |
> | 003 | Door leaf | Door rubs on frame at latch side, plane/re-hang | ABC Carpentry | Functional | 2026-04-20 | — | Open |
>
> Unit 201, Kitchen
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 004 | Under sink, plumbing penetration thru gyp | Fire-rated sealant missing — blocks SC | Fire Caulk LLC | **Safety** | **2026-04-17** | — | Open |
>
> Unit 201, Bedroom 2
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 005 | Closet light fixture | Switch not breaking circuit — fixture stays on | Bright Electric | Functional | 2026-04-20 | — | Open |
>
> Unit 202, Living Room
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 006 | Floor near fireplace (north side) | Squeak in flooring, approx 2 ft from hearth | ABC Carpentry | Functional | 2026-04-22 | — | Open |
>
> **NON-PUNCH ITEMS FROM WALK**
> | # | Item | Tag | Owner of next action |
> | CO-01 | Client request: add outlet at kitchen island | CO Candidate | PM — issue change order, not punch |
>
> *This punch list was organized with AI assistance and should be reviewed by the PM or site supervisor against the walkthrough notes before distribution.*
