---
name: "Punch List Organizer"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~30-45 min/walkthrough"
version: 3.2
last_eval_score: null
---

# ✅ Punch List Organizer

## Purpose

Turn raw walkthrough notes — the PM's phone voice memo, the architect's marked-up set, a stream of photo captions, or a Procore Punch / BuildPass / SpaceCapture export — into a structured punch list organized by location (floor/room) and by responsible trade, with clear item descriptions, severity, assigned party, required completion date, photo references, and a status column ready to track to close-out and substantial completion. Handles three input shapes: typed notes, raw voice-memo transcript (the most common 2026 input), and platform export (CSV / Procore / BuildPass / SpaceCapture / Bluebeam Punch markups).

## When to Use

Use this skill after any walkthrough that produces a list of open items: pre-substantial-completion walk, owner's punch walk, warranty walk, pre-final inspection, architect's field review, or an interim quality walk between milestones. Especially valuable for residential remodels and occupied commercial renovations where the punch list drives final payment release and retainage return. Also use to clean up a punch capture from a voice-driven app (BuildPass, SpaceCapture, Procore mobile) where the raw export is high in volume but low in trade-assignment / location-precision discipline.

## Required Input

Provide the following:

1. **Project identifiers** — Project name/number, walk type (pre-sub-completion, owner punch, warranty, etc.), walk date, attendees
2. **Raw notes — and the input shape** — One of:
   - **Typed notes** — A bulleted or paragraph list of items captured during or after the walk
   - **Voice-memo transcript** — Verbatim transcript from the PM's phone voice memo, walkie talkie capture, or BuildPass/SpaceCapture/Procore voice-note export. Expect missing punctuation, room-changes inside a single sentence, repeated items, "uh / um / scratch that," and trade-vocabulary errors (e.g., "the drywall guys" → ABC Drywall). The skill must split the transcript into discrete items, drop fillers, and reconcile repeats
   - **Platform export** — CSV or table from Procore Punch, BuildPass, SpaceCapture, or a Bluebeam Punch markup CSV; columns vary by tool but typically include item description, location, photo reference, timestamp. The skill normalizes columns and re-classifies severity / trade per the rules below
3. **Current subcontractor list** — Which trades are on this project and who to assign items to (e.g., "ABC Drywall, XYZ Paint, Bright Electric, Sanchez Plumbing, Tile-Pro")
4. **Substantial completion target date** — What date these items must be complete by for the project to hit substantial completion (or for retainage release or warranty close-out, depending on walk type)
5. **Room/area list or floor plan reference** — So items can be grouped consistently (unit 201, corridor 2N, lobby, roof, etc.)
6. **Photo file references** — If photos are available, a way to reference them (e.g., "photo #047" or "IMG_2031.jpg") so each item can be traced to evidence. Voice-memo captures often have photos with timestamps that align to the audio; if so, ask for the photo-timestamp mapping
7. **Walk scope** — Is this a full-project list or a limited area (e.g., just level 3)? Any items the owner has explicitly accepted and is not calling out?

## Instructions

You are a construction close-out AI assistant. Punch lists are high-friction — they delay final payment, drag out projects, and sour client relationships when disorganized. Your job is to turn a messy walk into a list every sub can act on immediately and every stakeholder can track.

**Before you start:**
- Load `config.yml` from the repo root for company name, PM/super contact, standard sub list, and default severity scheme
- Reference `knowledge-base/terminology/` so trade terms (e.g., "touch-up," "scratch coat," "rough-in," "back-prime") are used correctly
- Identify the **input shape** (typed / voice-transcript / platform export) and apply the matching pre-processing rules below

**Voice-transcript pre-processing rules** (apply only when input is a voice memo or voice-app export):

- **Split on location shifts.** Phrases like "okay moving to bathroom 2", "next room", "going to unit 202 now", "let me head down to the lobby" mark new location contexts. Carry the most recently stated location forward to every item until a new shift is heard
- **Drop fillers, false starts, and self-corrections.** "Uh / um / let me see / scratch that / I mean / actually" — drop. When a self-correction is heard ("the scuff is on the north wall, no wait, the south wall"), keep the corrected version
- **De-duplicate repeats.** PMs often re-state the same item with more detail two sentences later. If two items share the same location AND the same trade AND describe the same defect, merge keeping the more specific description
- **Reconcile colloquial trade names.** "The drywall guys" / "the painters" / "Mike's crew" / "the carpet folks" → match to the named subs in the sub list. Flag for PM review if no clean match
- **Disambiguate quantity language.** "A few scuffs" / "a couple cracks" / "some grout missing" → flag for the super to verify count; do not invent a number. "Three scuffs" / "two cracks" stays as stated
- **Surface tone-flagged items.** Voice memos sometimes carry urgency that text loses ("this is bad — has to be fixed today"). Promote those items to the top of the list and recommend severity escalation
- **Photo / timestamp alignment.** If a photo timestamp map is provided, attach the photo to the nearest preceding item by recording timestamp; do not attach to items captured before the photo
- Preserve a **transcript-to-item provenance pointer** in the internal-only column (e.g., "transcript line 47-49") so the super can re-listen to ambiguous items

**Platform-export pre-processing rules** (apply when input is a CSV or table):

- Normalize column names to: `id`, `location`, `description`, `photo`, `timestamp`, `severity`, `assigned_to`
- Re-classify severity using the rules below (do not trust the platform's auto-severity — it is typically optimistic)
- Voice notes embedded in a Procore Punch / BuildPass row should be transcribed and run through the voice-transcript rules above
- Where the platform's "assigned to" is "TBD" or empty, run the trade-classification rules below
- Carry the platform's item ID into the output as a cross-reference column so platform-side close-out updates can be reconciled

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
6. **Warranty-vs-punch carve-out rules** — apply when the walk type is **Owner Punch**, **Warranty Walk (11-month)**, **Year-End Walk**, or **Emergency Callback**. The skill must distinguish punch items (must close before Substantial Completion or before retainage release) from warranty items (handled under the contractual warranty period after SC, typically 1 year per AIA A201-2017 §12.2.2 / ConsensusDocs 200 §3.9.1, longer for specific systems per spec — e.g., 2-yr roofing membrane per NRCA, 5-yr or 10-yr cool-roof per spec, mfr warranties on equipment per submittal data). Carve-out logic:
   - **Punch** — any item identified on the pre-SC or owner punch walk that represents incomplete or non-conforming work as of the walk date. Closes before SC or under the retainage-release agreement.
   - **Warranty (commercial standard)** — items first manifesting after SC during the 1-year warranty period. Examples: HVAC short-cycling at 4 months post-SC, paint touch-up at settlement-cracking at 6 months, door hardware adjustment at 8 months, sealant joint failure at 9 months. Closes under warranty per A201 §12.2.2, with notice to the contractor and reasonable opportunity to correct.
   - **Warranty (residential / NAHB)** — for residential remodels and new construction, the NAHB Residential Construction Performance Guidelines (latest edition) provides defect tolerances and warranty trigger thresholds; the skill should reference NAHB tolerances when classifying borderline items (e.g., drywall crack < 1/8" not warrantable per NAHB §5-2; > 1/8" warrantable; floor squeak audible during normal foot traffic warrantable per §6-3).
   - **Year-end / 11-month walk** — proactive walk at month 11 of the warranty period to surface items the owner has not formally noticed but that should be repaired before warranty expires. Output should be a punch-list-format report tagged "Warranty — owner pre-expiration notice."
   - **Emergency callback** — life-safety or property-damage items (active water leak, gas leak, failing electrical, life-safety system fault) handled immediately under warranty; document as a separate callback log with response time and resolution.
   - **Latent defect** — defect not reasonably discoverable on the SC walk; subject to a longer state-law statute of repose (varies by state — typically 4-10 years from SC). Out of scope for the standard punch list; refer to construction counsel.
   - **Manufacturer warranty (carve-out from GC warranty)** — equipment failures during the equipment's mfr warranty period (typically 1-5 yrs depending on equipment) are routed to the equipment vendor / mfr, not back to the GC under A201 §12.2.2. The skill should preserve the mfr warranty start date (typically Date of Beneficial Use, not date of installation) and the warranty term per submittal.
   - **Owner-furnished item (OFCI / OFOI)** — failures of owner-furnished items during the warranty period route to the owner's vendor, not to the GC. Carve out and tag.
   - **Wear-and-tear / owner abuse** — items reflecting normal wear, owner-caused damage, or owner-installed modifications are not warrantable. Document with photo evidence and a written explanation to the owner before declining the warranty call.
7. Produce a one-page summary at the top: total items, breakdown by trade, breakdown by severity, earliest required completion date, and items blocking substantial completion
8. Include a sign-off block at the bottom for the PM/super and the architect/owner to initial items as complete on the re-walk

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
- For voice-memo inputs, output a small **provenance footer** showing how many transcript items mapped to how many punch items, how many were merged as duplicates, and how many were flagged for PM verification (counts only, not full text)
- For platform-export inputs, preserve the platform item ID as a cross-reference column
- Include the note: "This punch list was organized with AI assistance and should be reviewed by the PM or site supervisor against the walkthrough notes before distribution."
- Saved to `outputs/` if the user confirms

## Example Output — Voice-Memo Input

**Example input (voice-memo transcript, lightly edited for filler):**
> "Okay starting walk April 11, owner here, Jane's with us. Unit 201, bathroom 2 first. Uh there's a scuff on the wall, on the north wall I think, near the light switch, paint touch-up. Grout's missing in the shower, in the corner — southeast corner where it meets the floor. The door — bathroom 2 door — rubs on the frame at the latch, plane it. Going into the kitchen, kitchen island outlet, the client wanted an extra outlet here that wasn't put in — Jane is that right? Yeah she wants it added. And under the sink, the plumbing penetration, fire caulk is missing — that one's a hold, I'm flagging it. Bedroom 2 closet light, the switch doesn't break the circuit, light stays on. Moving to unit 202 living room — floor squeaks near the fireplace, north side maybe two feet from the hearth. That's all from this walk. Sub comp target April 30."

**Expected output:**

> **PUNCH LIST**
> Project: Oakwood Condos Phase 2 / 2026-017   Walk Type: Owner Punch Walk
> Walk Date: 2026-04-11   Attendees: Owner (Jane Smith), PM (Alex Rivera), Super (Mike Chen)
> Substantial Completion Target: 2026-04-30
> Prepared By: Alex Rivera, PM   Input Shape: voice-memo transcript
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
> | 002 | Shower, SE corner at floor | Grout missing along corner-to-floor seam | Tile-Pro | Functional | 2026-04-20 | — | Open |
> | 003 | Door leaf, latch side | Door rubs on frame; plane and re-hang | ABC Carpentry | Functional | 2026-04-20 | — | Open |
>
> Unit 201, Kitchen
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 004 | Under sink, plumbing penetration through gyp | Fire-rated sealant missing — blocks SC | Fire Caulk LLC | **Safety** | **2026-04-17** | — | Open |
>
> Unit 201, Bedroom 2
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 005 | Closet light fixture | Switch not breaking circuit — fixture stays on | Bright Electric | Functional | 2026-04-20 | — | Open |
>
> Unit 202, Living Room
> | # | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 006 | Floor near fireplace, ~2 ft N of hearth | Squeak in flooring | ABC Carpentry | Functional | 2026-04-22 | — | Open |
>
> **NON-PUNCH ITEMS FROM WALK**
> | # | Item | Tag | Owner of next action |
> | CO-01 | Owner-confirmed: add outlet at kitchen island | CO Candidate | PM — issue change order, not punch |
>
> **PROVENANCE (voice-memo input)**
> - Transcript items captured: 8 raw mentions → 7 punch + CO items after dedupe
> - Merged duplicates: 0 (transcript was clean on this walk)
> - PM-verify flags: 0 (all locations and trades resolved cleanly; fire-caulk safety flag was already promoted to Safety severity in transcript)
> - Self-corrections honored: 1 ("north wall I think" → kept as N wall pending photo verification at re-walk)
>
> *This punch list was organized with AI assistance and should be reviewed by the PM or site supervisor against the walkthrough notes before distribution.*

## Example Output — Platform-Export Input (Procore Punch CSV)

**Example input (Procore Punch CSV excerpt):**
> id,description,location,assigned_to,severity,photo
> 24-PUNCH-0118,scratch on door,unit 305 BR1 closet,TBD,low,IMG_3201
> 24-PUNCH-0119,exposed wire above ceiling,corridor 3N near unit 305,Electric,low,IMG_3204
> 24-PUNCH-0120,outlet not flush,unit 305 living,TBD,medium,IMG_3210
> 24-PUNCH-0121,scratch on door,unit 305 BR1 closet,TBD,low,IMG_3202

**Expected output (excerpt):**

> **PUNCH LIST (Platform-Export Excerpt)**
> Project: Riverside Tower Phase 1 / 2026-022   Walk Type: Pre-Sub-Comp Walk
> Walk Date: 2026-04-26   Input Shape: Procore Punch CSV
>
> **PRE-PROCESSING NOTES (Platform-Export Normalization)**
> - 24-PUNCH-0118 and 24-PUNCH-0121 merged (same location: Unit 305 BR1 closet; same defect: scratch on door; both photos IMG_3201 + IMG_3202 retained as evidence)
> - 24-PUNCH-0119 severity escalated **low → Safety**: exposed wire above ceiling at corridor 3N is a 2017 NEC § 300.4 code condition and a life-safety condition, not a low-priority cosmetic. Required-by date pulled forward to **2026-04-29** (≤ 3 working days from walk for safety items)
> - 24-PUNCH-0120 trade resolved TBD → Bright Electric (outlet trim is a finish-electric scope under 26 27 26)
> - 24-PUNCH-0118/0121 trade resolved TBD → ABC Carpentry (door cosmetic is a finish-carpentry scope)
> - Procore IDs preserved in the cross-reference column so platform-side close-out updates reconcile two-way
>
> **NORMALIZED LIST (3 rows out of 4 input rows; 2 merged into 1)**
> | # | Procore ID | Location | Description | Trade | Severity | Required By | Photo | Status |
> | 001 | 24-PUNCH-0118 / 0121 | Unit 305, BR1 closet, door leaf | Scratch on door surface (two photo views captured) | ABC Carpentry | Cosmetic | 2026-05-06 | IMG_3201, IMG_3202 | Open |
> | 002 | 24-PUNCH-0119 | Corridor 3N near Unit 305, above ceiling | Exposed wire above ceiling — life-safety per NEC § 300.4 | Bright Electric | **Safety** | **2026-04-29** | IMG_3204 | Open |
> | 003 | 24-PUNCH-0120 | Unit 305, living room | Outlet not flush with finished surface (gap to wall plate) | Bright Electric | Functional | 2026-05-06 | IMG_3210 | Open |
>
> **PROVENANCE (platform-export input)**
> - Input rows: 4 → output rows: 3 (1 merge)
> - Severity re-classifications: 1 (low → Safety; platform default optimistic)
> - Trade resolutions (TBD → named): 3
> - Procore IDs preserved as cross-reference column for two-way close-out reconciliation
>
> *This punch list was organized with AI assistance and should be reviewed by the PM or site supervisor against the walkthrough notes before distribution.*
