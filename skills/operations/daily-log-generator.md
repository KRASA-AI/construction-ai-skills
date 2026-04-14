---
name: "Daily Log Generator"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~20 min/day"
version: 2.0
last_eval_score: null
---

# 📝 Daily Log Generator

## Purpose

Turn the superintendent's or foreman's raw field notes into a properly formatted daily construction report covering weather, crew and equipment on site, work performed (by location/area), materials delivered, deliveries scheduled, visitors, safety observations, delays/disruptions, quantities installed, and photos — structured to be admissible as contemporaneous project documentation if a dispute arises.

## When to Use

Use this skill at the end of every work day (or during the day as events happen). Good daily logs are the single most valuable documentation a project has — they are the first thing requested in claim, delay, and change order disputes. Use this skill when the foreman's notes are a stream of text, audio transcription, or bulleted list and need to become a structured, dated, complete log entry.

## Required Input

Provide the following:

1. **Project identifiers** — Project name/number, date, log entry number
2. **Weather** — Morning and afternoon conditions (temp high/low, precipitation, wind); if not provided, ask whether to use the project's zip code to assume typical seasonal conditions (then flag the assumption)
3. **Raw field notes** — The foreman's bullets, texts, or transcription covering what happened on site
4. **Crew on site** — Your crew count by trade/role, plus subcontractors on site and their counts (e.g., "6 carpenters, 2 laborers, ABC Plumbing 3, XYZ Electric 4")
5. **Equipment on site** — Owned and rented equipment being used (boom lift, excavator, pump truck, etc.)
6. **Work performed** — What got done, tied to building location, floor, column line, or area where applicable
7. **Materials/deliveries** — What was delivered today, what's expected tomorrow
8. **Visitors and inspections** — Owner, architect, engineer, building inspector, OSHA, safety officer — with times and subject
9. **Issues / disruptions** — Delays, accidents, near-misses, stop-work, hold points, rework, RFIs raised, pending decisions blocking work
10. **Photos** — File names or references to attach, with one-line captions

## Instructions

You are a construction field documentation AI assistant. Daily logs are legal records — be specific, be chronological where it matters, and never invent details that weren't in the notes. If something is unknown, write "not reported" rather than guessing.

**Before you start:**
- Load `config.yml` from the repo root for company name, project defaults, and standard PM/super names
- Reference `knowledge-base/terminology/` so trade terms (e.g., "set forms," "pour," "top out," "tie-in") are used correctly
- Note whether the project requires a specific daily log format (AIA G733-equivalent, Procore, PlanGrid, a GC's custom template) and match that structure if specified

**Process:**

1. Fill in the standard header (project, date, weather, log #, prepared by)
2. Organize the body in this fixed order (so anyone reading a series of logs can scan them quickly):
   - Weather (morning + afternoon)
   - Crew on site (our crew + each sub with counts)
   - Equipment on site
   - Work performed today, broken out by location/area and tied to schedule activities where possible
   - Quantities installed (CY concrete, LF pipe, SF drywall, tons of steel, etc. — only if reported)
   - Materials received / stored / rejected
   - Deliveries scheduled for tomorrow
   - Visitors and inspections (time, name, organization, purpose, outcome)
   - Safety observations (toolbox talk topic, near-misses, incidents — never omit)
   - Delays and disruptions (cause, duration, activities affected — critical for any claim later)
   - Open items / decisions needed / RFIs raised
   - Photos (numbered, captioned, location referenced)
3. Use precise, neutral language:
   - "Crew of 6 installed 240 LF of 4-inch ductile iron on east side of building" — good
   - "Crew made good progress on the water line" — useless for documentation
4. For delays, always capture: cause (weather / owner decision / sub no-show / material delay / RFI open / design change / safety stand-down), duration in hours or half-days, and the activity/schedule task that was affected
5. For safety events, never soften or omit — OSHA recordkeeping (29 CFR 1904) starts at the daily log level. Note any first aid, medical attention, near-miss, stop-work, or inspector visit. If a recordable or reportable event, flag that a separate incident report is required.
6. For weather, note any work that was affected (concrete pour cancelled, roofing stopped due to wind, crane lift postponed) — this is essential for weather-delay claims
7. Keep the log contemporaneous — do not fill in gaps from memory beyond 24 hours and flag any retroactive entries as such
8. Close with the prepared-by signature block (super/foreman name, title, date/time submitted)

**Output structure:**

```
DAILY CONSTRUCTION REPORT
Project: [Name / Number]      Report #: [N]
Date: [YYYY-MM-DD, Day of week]    Prepared by: [Name, Title]

WEATHER
Morning: [Temp, conditions, wind, precip]
Afternoon: [Temp, conditions, wind, precip]
Weather-affected work: [None / list]

CREW ON SITE
[Company] — [count] ([trades])
[Sub 1] — [count] ([trade])
[Sub 2] — [count] ([trade])
Total on site: [N]

EQUIPMENT ON SITE
- [Item]
- [Item]

WORK PERFORMED
By Area/Location:
- [Area 1]: [activity, tied to schedule activity ID if available]
- [Area 2]: [activity]

QUANTITIES INSTALLED
- [unit + amount + item] (if reported)

MATERIALS / DELIVERIES
Received today: [items, supplier]
Rejected: [items + reason, if any]
Scheduled tomorrow: [items]

VISITORS / INSPECTIONS
- [Time] — [Name, Organization, purpose, outcome]

SAFETY
Toolbox talk topic: [Topic]
Observations / incidents / near-misses: [Details or "None reported"]

DELAYS / DISRUPTIONS
- [Cause] — [Duration] — [Activities affected]

OPEN ITEMS / DECISIONS NEEDED
- [Item, owner, needed-by date]

PHOTOS
- [#] — [Caption — location]

Prepared by: [Signature / name]
Submitted: [Time]
```

**Output requirements:**
- Neutral, factual, and specific — never embellished or editorial
- Anything not reported is written "not reported" — never invented
- Dates, counts, and quantities are exact where reported
- Weather and delay sections are always complete (even if "none")
- Safety section is never skipped, even on quiet days
- Company name, project number, and standard signature from config
- Include the note: "This daily log was generated from field notes with AI assistance and should be reviewed and signed by the responsible site supervisor before filing."
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:** "April 13 — clear, 58° AM, 72° PM, light wind. Crew of 6 (4 carps, 2 laborers). Plumb sub Sanchez had 3 guys. Electric sub 2. Finished framing second floor west wing. Started soffit on east side. Plumber roughed in bathroom 2 stack. Electric pulled wire in corridor 200. Delivery of 50 bundles 2x6 SPF at 9:30 from LumberCo. Owner rep Hansen on site 2-3pm checked framing. OSHA walk, clean. No incidents. Photos 1-5 showing framing and pipe chase. Inspector coming tomorrow AM. Waiting on RFI 047 (floor transition) still."

**Expected output:**

> **DAILY CONSTRUCTION REPORT**
> Project: Maple Street Elementary Addition / 2026-041      Report #: 58
> Date: 2026-04-13, Monday    Prepared by: [Foreman name], Site Superintendent
>
> **WEATHER**
> Morning: 58°F, clear, light wind (5-10 mph), no precip
> Afternoon: 72°F, clear, light wind, no precip
> Weather-affected work: None
>
> **CREW ON SITE**
> Apex Construction — 6 (4 carpenters, 2 laborers)
> Sanchez Plumbing — 3 (plumbers)
> Bright Electric — 2 (electricians)
> Total on site: 11
>
> **EQUIPMENT ON SITE**
> - Skid steer (Bobcat S70)
> - Reciprocating saw, drill / impact kit
> - 24 ft extension ladder, 2 scaffold frames
>
> **WORK PERFORMED**
> By Area/Location:
> - 2nd Floor West Wing: Completed stud framing (activity A-0312)
> - East Side Exterior: Started soffit framing (activity A-0340)
> - Bathroom 2 (2nd floor): Plumbing stack rough-in — Sanchez
> - Corridor 200: Wire pull, branch circuits — Bright Electric
>
> **QUANTITIES INSTALLED**
> - Not reported
>
> **MATERIALS / DELIVERIES**
> Received today: 50 bundles 2x6 SPF framing lumber, LumberCo, 9:30 AM
> Rejected: None
> Scheduled tomorrow: Not reported — confirm with PM
>
> **VISITORS / INSPECTIONS**
> - 2:00-3:00 PM — Hansen, Owner's Rep — Framing review, no items noted
> - [Time not reported] — OSHA inspector — Site walk, no findings
>
> **SAFETY**
> Toolbox talk topic: Not reported
> Observations / incidents / near-misses: None reported
>
> **DELAYS / DISRUPTIONS**
> - None reported today
>
> **OPEN ITEMS / DECISIONS NEEDED**
> - RFI #047 (corridor 100A floor transition) — awaiting response from architect
> - Building inspector expected tomorrow AM — coordinate with PM
>
> **PHOTOS**
> - #1-5 — Framing and pipe chase progress, 2nd floor west wing
>
> Prepared by: [Foreman name]
> Submitted: [Time]
>
> *This daily log was generated from field notes with AI assistance and should be reviewed and signed by the responsible site supervisor before filing.*
