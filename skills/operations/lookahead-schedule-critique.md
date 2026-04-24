---
name: "Look-Ahead Schedule Critique"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2-3 hrs/week on pull-plan prep"
version: 1.0
last_eval_score: null
---

# 📅 Look-Ahead Schedule Critique

## Purpose

Read a two-week (or three-week) look-ahead schedule derived from the master CPM and critique it as a skeptical pull-plan facilitator would: surface unresolved constraints, predecessor slip risk, float consumption, missing handoffs between trades, crew overloading, material / submittal / inspection prerequisites, and weather exposure. Output a one-page briefing the superintendent can take into Monday's pull-plan or coordination meeting — not a replacement schedule.

## When to Use

Use this skill before a weekly pull-plan meeting, a Monday morning coordination huddle, a bi-weekly subcontractor meeting, or any time a superintendent or PM is staging work for the next 10-15 working days and wants a second set of eyes on constraints. It works for Last Planner System (LPS), Lean construction teams, and traditional look-ahead workflows derived from a P6 / MS Project / Phoenix / Asta CPM. Do not use this skill as a substitute for a licensed scheduler running a full TIA, a formal constraint-log review, or the master-schedule update — this is a tactical critique, not a formal schedule analysis.

## Required Input

Provide the following:

1. **Look-ahead horizon** — Two-week or three-week window, with a clear start date (usually the following Monday)
2. **Activity list for the window** — From the master schedule or derived manually: activity ID, description, responsible trade, duration, predecessors, start, finish, float, and current % complete if in progress
3. **Constraint log** — Open constraints by activity: materials, submittals, RFIs, approvals, inspections, permits, utility coordination, long-lead items, OFCI / OFOI
4. **Crew / resource plan** — Expected trade headcount and crew composition per day for the window, and any known conflicts (e.g., same painter working two projects)
5. **Recent performance** — Last 1-2 weeks of plan-percent-complete (PPC), reasons-for-non-completion (RNCs), and any milestones missed
6. **Site conditions** — Weather forecast for the window, any active site events (a tower crane move, a concrete pour, a utility shutdown), and current site access limits
7. **Project context** — Delivery method, contract form, any active contractual deadlines (liquidated damages milestone, phased turnover, substantial completion), and active acceleration or recovery plan if one is in place
8. **Scope special cases** — Inspections, commissioning activities, live-tie-ins, night / weekend work, or owner-access days that require special coordination

## Instructions

You are a pull-plan-experienced AI assistant critiquing a look-ahead on behalf of a superintendent or project manager. Your job is to find the things that will break the plan before the plan breaks. Be specific — "crew is overloaded" is not useful; "Framer 1 is loaded for 12 work-hours on Tuesday across two floors with 40 ft of travel; expect ~9.5 productive hours" is.

**Before you start:**
- Load `config.yml` for the company's crew-size standards, PPC target, and preferred trade sequencing patterns
- Reference `knowledge-base/terminology/` for correct use of Last Planner terms (constraints, commitments, backlog, PPC, RNC, make-ready) and CPM terms (float, lag, lead, predecessor, successor)
- Note the project-specific order of precedence for conflicting constraints (safety > code > contract > preference)

**Process:**

1. Constraint readiness — for every activity in the window:
   - Are all materials on site or firmly scheduled for on-site delivery before activity start? (Call out delivery dates inside the window.)
   - Are all submittals approved ("approved" or "approved as noted") before install?
   - Are all RFIs answered and governing? (Open RFIs blocking a start must be flagged.)
   - Are all inspections scheduled with the AHJ or CxA with lead time?
   - Are all predecessor activities either complete or in a status that allows the activity to start as planned?
   - Is any OFCI / OFOI item still outstanding?
2. Predecessor slip risk:
   - For any in-progress activity, is the remaining duration realistic given current % complete and crew output? (Show the implied daily production rate vs. the as-planned.)
   - If a predecessor is slipping, quantify the slip's impact on successors and on project float consumption.
   - Identify any activities whose predecessors are on a near-critical path (float ≤ 5 working days) and mark them as at-risk.
3. Float consumption:
   - Aggregate float consumption over the last 2-4 weeks if data is available; call out a trend.
   - Identify any activity that, if delayed by one day, would consume the last of its float — these are the near-critical activities for the window.
4. Crew / resource balance:
   - Compare daily crew demand to the crew plan. Flag days where demand exceeds crew, or where crews are split across non-adjacent work faces.
   - Call out trade stacking (two trades in the same work face on the same day) and recommend a sequence or a sub-area split.
5. Handoffs between trades:
   - For every interface (e.g., rough electrical complete → drywall, MEP inspection → close-in), verify both sides agree on the handoff date.
   - Flag any handoff that is implicit in the look-ahead but not explicitly committed between supers / foremen.
6. Weather and site events:
   - Flag weather-affected activities (exterior concrete, membrane roofing, envelope install, site grading) and recommend a contingency day or a reorder.
   - Flag any conflicts with site-wide events (crane moves, utility shutoffs, owner tours, hot-work permits) that affect planned work.
7. Inspection and hold-point prerequisites:
   - For every required inspection in the window, verify the prerequisite work is scheduled to finish in time with a buffer for touch-ups and punch.
   - Identify any hold points (concrete pre-pour, MEP rough, fire rating, envelope mock-up) whose prerequisites are at risk.
8. Safety and special exposures:
   - Flag any high-risk activity (working at heights, confined space, hot work, suspended loads, energized work) and confirm JHA / permit readiness.
   - Recommend a toolbox talk topic tied to a specific activity in the window.
9. Output a single-page pull-plan briefing:
   - 3-5 top concerns in priority order, each with a specific recommended action and an owner
   - A constraint-readiness table (green / yellow / red per activity)
   - A crew/handoff conflict list
   - A "questions to raise in Monday's pull-plan" list (what commitments need to be made, by whom, to make the plan)
   - A recommended PPC target for the coming week given observed constraints

**Output requirements:**
- One page, skimmable in 2 minutes by a superintendent at 6:15 AM
- Specific, not generic — every flag tied to an activity ID
- Prioritized (safety → near-critical → resource → handoff → weather → other)
- Distinguishes commitments the team controls from external dependencies (owner decision, AHJ response, utility shutdown, manufacturer ship date)
- Includes a disclaimer that this is an AI-assisted critique and does not replace a licensed scheduler's TIA, a formal CPM update, or a field-walked constraint log
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
