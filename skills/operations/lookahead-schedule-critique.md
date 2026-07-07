---
name: "Look-Ahead Schedule Critique"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2-3 hrs/week on pull-plan prep"
version: 1.1
last_eval_score: 9.1
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
- Load `config.yml` for: (a) the company's crew-size standards by trade (typical foreman:journeyman:apprentice ratios; daily production rates for the trades the GC self-performs or routinely runs); (b) the company's PPC target (typical: 80% for traditional teams, 85% for mature LPS teams); (c) preferred trade sequencing patterns; (d) the company's near-critical-float threshold (typical: ≤ 5 working days = near-critical); (e) the company's scheduling-platform choice (P6 / MS Project / Phoenix / Asta / Touchplan / vPlanner — see Reviewer-of-Platform-AI sub-mode below); and (f) typical lead-time conventions by AHJ for inspections (e.g., 24-hr / 48-hr / 72-hr).
- Reference `knowledge-base/best-practices/scheduling-look-ahead.md` for the full 11-category constraint taxonomy, Last Planner System make-ready / commit / measure cycle, PPC + RNC discipline, float-consumption rules, and crew-balance heuristics.
- Reference `knowledge-base/terminology/` for correct use of Last Planner terms (constraints, commitments, backlog, PPC, RNC, make-ready, Tasks Anticipated → Tasks Made Ready) and CPM terms (float, lag, lead, predecessor, successor, near-critical, longest path).
- Note the project-specific order of precedence for conflicting constraints (safety > code > contract > preference).

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

## Reviewer-of-Platform-AI-Output Sub-Mode

Many GCs in 2026 have adopted Last-Planner-platform and CPM-platform AI assistants that generate look-ahead summaries and constraint flags automatically: **Touchplan AI** (constraint-clearance prompts + auto-flagging of un-cleared make-ready tasks), **vPlanner AI** (LPS commitment-reliability scoring + RNC trend reading), **Phoenix Project Manager AI** (CPM-derived look-ahead with critical-path delta detection), **P6 Cloud AI Add-On** (auto-narrative from schedule update + Monte Carlo risk), **BIM Track Look-Ahead** (clash-driven constraint surfacing), and **Procore Schedule AI** (Procore Schedule Module's AI insights for activity slip prediction). These platforms produce a draft look-ahead critique; the superintendent or PM is then the reviewer-of-AI-output. This sub-mode produces a redline of the platform's draft before it goes into Monday's pull-plan briefing.

When the input is a platform-AI look-ahead draft (not raw schedule + constraint log), apply this six-point redline check:

1. **Constraint-completeness check.** Platforms typically surface 4–6 of the 11 constraint categories (per `knowledge-base/best-practices/scheduling-look-ahead.md`) — usually materials, submittals, RFIs, predecessors, sometimes weather. They miss owner / tenant / operations coordination (Cat 11), site conditions & access (Cat 8, especially the locked-behind-another-trade case), permits-to-work (Cat 10 high-risk activities), and inspections-and-hold-points lead-time (Cat 4). Re-run the activity list against the full 11-category taxonomy and add the missing categories.
2. **In-progress-activity production-rate sanity check.** Platforms read remaining duration straight from the as-planned schedule. They do not compute the implied daily production rate from observed % complete and compare to the as-planned rate. Re-compute: implied remaining production rate vs. as-planned production rate; if implied is >115% of as-planned, the activity is at-risk of slipping into the look-ahead window.
3. **Near-critical activity identification.** Platforms flag the critical path (float = 0) but typically miss the near-critical band (float ≤ 5 working days per config.yml). One day of slip on a near-critical activity consumes the rest of its float silently. Re-run the float analysis at the config-driven threshold and add near-critical activities to the at-risk list.
4. **Trade-stacking and crew-balance reading.** Platforms read activity-level resource allocation but do not read trade-stacking (two trades in the same work face on the same day) or crew-split (one foreman across non-adjacent work faces with travel time). Re-read the daily-by-trade-by-area matrix and flag stacking + split.
5. **Soft-logic-vs-hard-logic predecessor reading.** Platforms treat all predecessors as hard. Many are soft (sequencing preferences, not technical requirements). Re-classify predecessors and flag soft predecessors that could be challenged in the pull-plan to recover float.
6. **PPC / RNC trend reading.** Platforms produce a PPC number for the most recent week but typically do not surface the RNC root-cause trend. Re-read the last 4 weeks of RNCs and group by root-cause category (un-cleared constraint / late predecessor / crew under-staffed / scope-change-mid-week / weather / safety stand-down). The dominant RNC category is the biggest leverage point for next week's pull-plan ask.

Sub-mode output: (a) platform's draft look-ahead summary (preserved verbatim), (b) six-point redline, (c) final pull-plan briefing that may agree or disagree with the platform, (d) provenance footer noting which platform produced the draft, what the redline changed, and the recommended PPC target.

## Example Output

**Example input scenario:** Brookline MOB TI Phase 2 (GC = Stonebridge Construction, 32,000 SF medical-office build-out, $4.2M total contract). Look-ahead horizon: Monday 2026-06-01 through Friday 2026-06-12 (10 working days, weeks 18 and 19 of construction). Master schedule: P6, data date 2026-05-22, current Substantial Completion 2026-10-12 (8 WD slip already absorbed in SU-12 per the Differing Site Condition utility-tap RFCA — see `admin/delay-claim-drafter.md` worked example). Active scope in window: MEP rough-in (Pkg 06 Acme Mechanical + Pkg 07 Bright Electric), in-wall blocking (Pkg 04 ABC Carpentry), framing close-out (Pkg 02 Premier Drywall — pending the subcontract review in `admin/contract-risk-reviewer.md`), and ICRA-zone monitoring throughout. Last 4 weeks PPC: 79% / 81% / 74% / 77% (rolling avg 78%, below the GC's 85% LPS target per config.yml).

**Expected output:**

> # LOOK-AHEAD PULL-PLAN BRIEFING
>
> **Project:** 2026-031 Brookline MOB TI Phase 2 (Brookline Health Partners)
> **Window:** 2026-06-01 (Mon) — 2026-06-12 (Fri), 10 working days
> **Prepared for:** Pull-plan meeting, Monday 2026-06-01 at 6:30 AM site trailer
> **Prepared by:** Site Super (AI-assisted), Stonebridge Construction
> **Prepared date:** 2026-05-26 (data date 2026-05-22)
>
> ## TOP 5 CONCERNS (Priority Order)
>
> **1. 🔴 SAFETY / NEAR-CRITICAL — Activity A-1142 MEP rough-in above ICRA Zone 2 corridor, Tue 2026-06-02 to Thu 2026-06-04.** Above-ceiling MEP rough by Acme Mechanical (Pkg 06) plus Bright Electric (Pkg 07) is scheduled in occupied-healthcare-adjacent corridor with daytime patient access. **Action:** Confirm ICRA Class III precautions in place (anteroom + HEPA-filtered negative pressure + daily wet-vacuuming) by 6:00 AM Monday; confirm both subs have ICRA-trained crew on site (Acme's program addendum was the pre-NTP condition per `admin/subcontractor-prequal-reviewer.md` — verify acceptance). **Owner:** Site Super + Stonebridge Safety Director. **Float:** 3 WD (near-critical per config.yml threshold ≤ 5). **PPC commitment required from both subs by Mon AM.**
>
> **2. 🔴 NEAR-CRITICAL — Activity A-1158 Plumbing rough-in Zone 3 (Acme Mechanical), Wed 2026-06-03 to Fri 2026-06-05.** **Predecessor A-1155 In-wall blocking Zone 3 (ABC Carpentry)** is in-progress at 60% complete with as-planned 5 WD remaining. **Implied daily production rate computed from last 5 WD of carpenter output: 14 LF/day vs. as-planned 18 LF/day (78% of plan).** At observed rate, blocking finishes 2026-06-04 not 2026-06-02 — **2 WD slip — which collapses A-1158's plumbing rough-in into a hard-stacked start.** **Action:** add second carpenter pair to ABC Carpentry crew Mon AM, or accept 2 WD slip on A-1158 (which would push A-1158 to zero float). **Owner:** ABC Carpentry GF + Site Super by 7:00 AM Mon. **External dependency:** none — this is a controllable commitment.
>
> **3. 🟠 EXTERNAL DEPENDENCY — Activity A-1163 Above-ceiling MEP inspection (Brookline Building Dept), required 2026-06-09 (Tue, WD 7 of window).** Inspection request must be submitted to Brookline BD by **Mon 2026-06-01 1:00 PM** for the 48-hr lead-time + buffer; AHJ has been running 1 WD over on inspection scheduling for the last 3 weeks. **Action:** PM to submit inspection request by 12:00 noon Mon (1 hr buffer); contingency: confirm BD will accept a 2026-06-10 alternate date if first slot drops. **Owner:** PM (external dependency).
>
> **4. 🟠 RESOURCE — Trade stacking at Zone 4 close-in, Thu 2026-06-04 to Fri 2026-06-05.** Acme Mechanical (HVAC rough completion), Bright Electric (lighting rough), and Premier Drywall (framing close-out) are all scheduled in Zone 4 corridor 4N on the same two days. Work face is 320 LF of corridor — adequate for two trades but not three. **Action:** sequence-split — recommend Premier Drywall slides framing close-out to Fri PM / Mon AM after MEP rough is closed in; Acme Mechanical finishes Thu noon, Bright Electric finishes Fri AM. **Owner:** Site Super to negotiate at pull-plan; one of three trades will need to commit to off-cycle.
>
> **5. 🟡 WEATHER — Activity A-1177 Membrane roofing patch at AHU curb, Tue 2026-06-09 to Wed 2026-06-10.** NOAA 7-day forecast (pulled 2026-05-26): 50% rain probability Tue afternoon and Wed AM. Membrane roofing requires < 10% precip and surface dry-time. **Action:** identify 2026-06-11 (Thu) as contingency day; have roofer (Apex Roofing) pre-positioned with materials by Mon to allow either-day start. **Owner:** Apex Roofing foreman + Site Super.
>
> ## CONSTRAINT-READINESS TABLE (All Activities in Window)
>
> Constraint codes: M = materials, S = submittals, R = RFIs, I = inspections, Pe = permits, Pr = predecessors, C = crew, Site = site conditions, W = weather, Sf = safety, O = owner/tenant
>
> | Activity ID | Description | Trade | Days in Window | M | S | R | I | Pe | Pr | C | Site | W | Sf | O | Status |
> |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
> | A-1140 | In-wall blocking Zone 2 cont. | ABC Carpentry | Mon-Tue | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | **GO** |
> | A-1142 | MEP rough above ICRA Z2 | Acme + Bright | Tue-Thu | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟡 | 🟢 | n/a | **🔴** | **🔴** | **HOLD** until ICRA confirmation Mon AM |
> | A-1155 | In-wall blocking Zone 3 | ABC Carpentry | Mon-Wed | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | **🟠** | 🟢 | n/a | 🟢 | 🟢 | **AT-RISK** — 14 LF/day vs. 18 LF/day planned |
> | A-1158 | Plumbing rough Zone 3 | Acme Mech | Wed-Fri | 🟢 | 🟢 | 🟢 | n/a | 🟢 | **🟠** | 🟢 | 🟢 | n/a | 🟢 | 🟢 | **AT-RISK** — depends on A-1155 |
> | A-1162 | Above-ceiling sign-off prep | Field Engr | Mon-Fri | n/a | n/a | n/a | n/a | n/a | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | **GO** |
> | A-1163 | Above-ceiling inspection | BD | Tue 6/9 | n/a | n/a | n/a | **🟠** | 🟢 | 🟢 | n/a | n/a | n/a | n/a | 🟢 | **HOLD** until request submitted Mon noon |
> | A-1170 | Framing close-out Zone 4 | Premier DW | Thu-Fri | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟡 | **🟠** | n/a | 🟢 | 🟢 | **AT-RISK** — Zone 4 stacking |
> | A-1171 | Lighting rough Zone 4 | Bright Elec | Thu-Fri | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟢 | **🟠** | n/a | 🟢 | 🟢 | **AT-RISK** — Zone 4 stacking |
> | A-1172 | HVAC rough completion Z4 | Acme Mech | Thu | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟢 | **🟠** | n/a | 🟢 | 🟢 | **AT-RISK** — Zone 4 stacking |
> | A-1177 | Membrane roof patch AHU | Apex Roof | Tue-Wed | 🟢 | 🟢 | 🟢 | n/a | 🟢 | 🟢 | 🟢 | 🟢 | **🟡** | 🟡 | 🟢 | **WEATHER-WATCH** |
>
> ## CREW / HANDOFF CONFLICT LIST
>
> 1. **Zone 4 trade stacking** Thu-Fri (3 trades, 2-trade work face) — see Concern #4. **Soft-logic predecessor:** A-1172 HVAC rough → A-1170 framing close-out is treated as a hard predecessor in the schedule but is actually a sequencing preference (drywall can be closed up the day after MEP rough is closed in, doesn't need same-day handoff). **Challenge in pull-plan:** can A-1170 slip to Fri PM start without affecting the next week?
> 2. **ABC Carpentry crew split** Tue-Wed (carpenter pair on Zone 2 finish-up A-1140 + Zone 3 start A-1155 with ~250 ft of travel between zones) — recommend committing both pair to Zone 3 by Tue noon; Zone 2 finish-up has 2 WD float and can wait.
> 3. **Acme Mechanical handoff to Bright Electric** for above-ceiling MEP rough (A-1142) — implicit in look-ahead but not committed. **Question for pull-plan:** confirm Wed PM hard handoff at Zone 2 corridor (Acme done by 2 PM, Bright starts 2 PM) — both foremen present.
>
> ## QUESTIONS TO RAISE IN MONDAY'S PULL-PLAN
>
> 1. **ABC Carpentry GF (Mike R.):** can you commit a 2nd carpenter pair to Zone 3 Mon AM through Wed to recover the 14-LF/day production rate? If not, who slips — A-1155 or A-1158?
> 2. **Acme Mechanical PM (Linda K.):** ICRA program addendum acceptance — confirmed by Stonebridge Safety Director on date X? If not, A-1142 holds.
> 3. **Premier Drywall PM (Tomás G.):** can A-1170 framing close-out shift Thu→Fri PM start to de-stack Zone 4? Impact on Mon 6/15 next-week work?
> 4. **PM (Sarah J.):** above-ceiling inspection request submitted by noon Mon? BD contingency confirmed?
> 5. **Apex Roofing foreman (Pete L.):** materials pre-positioned by Mon for either-day Tue-or-Thu start on the AHU curb membrane patch?
> 6. **All foremen:** Zone 4 handoff sequence Thu-Fri — confirmed?
> 7. **All foremen:** last week's RNC root cause — un-cleared constraint dominant (3 of 4 RNCs on PPC week of 5/18 = un-cleared above-ceiling inspection request). **What changes Mon to break the pattern?**
>
> ## RECOMMENDED PPC TARGET FOR WEEK OF 2026-06-01
>
> **78%** (rolling 4-week average held; not raising the target until the un-cleared-constraint RNC pattern is broken; configurable-target 85% remains the aspiration). Re-evaluate after week-of 6/8 if the inspection-request-submission discipline holds.
>
> ## DISCLAIMER
>
> This is an AI-assisted look-ahead critique, not a replacement for the project scheduler's CPM update, a licensed scheduler's Time Impact Analysis, or a field-walked constraint log. The superintendent or PM should spot-check every activity-ID-tagged flag against the field-walk reality before relying on this briefing for the pull-plan commitment. Production-rate calculations are based on the reported % complete in the schedule; if % complete is over- or under-reported, the implied rate is wrong.

## Example Output — Reviewer-of-Platform-AI-Output Sub-Mode (Touchplan AI)

**Example input scenario:** The GC's Last Planner platform (Touchplan AI) has produced a draft look-ahead for the same Brookline MOB TI Phase 2 window. The Touchplan AI draft reads:

> **Touchplan AI Look-Ahead, week of 2026-06-01:**
> 10 activities in window. PPC last week 77%. Constraints flagged: 2 (material delivery for A-1140 blocking confirmed Mon AM; submittal A-1158 plumbing rough fixtures approved). At-risk activities: none flagged. Critical path: A-1170 framing close-out → A-1175 ceiling grid → A-1182 ACT install (downstream). Recommendation: Proceed as planned. PPC target 80%.

The Site Super is the reviewer-of-AI-output.

**Expected output:**

> # PLATFORM AI LOOK-AHEAD — REDLINE
>
> **Platform:** Touchplan AI, AI version per 2026-Q2 release
> **Project:** Brookline MOB TI Phase 2, window 2026-06-01 to 2026-06-12
> **Reviewed by:** Site Super (AI-assisted), Stonebridge Construction
> **Review date:** 2026-05-26
>
> ## PLATFORM AI DRAFT (PRESERVED VERBATIM)
>
> *Touchplan AI Look-Ahead, week of 2026-06-01: 10 activities in window. PPC last week 77%. Constraints flagged: 2 (material delivery for A-1140 blocking confirmed Mon AM; submittal A-1158 plumbing rough fixtures approved). At-risk activities: none flagged. Critical path: A-1170 → A-1175 → A-1182. Recommendation: Proceed as planned. PPC target 80%.*
>
> ## SIX-POINT REDLINE
>
> **1. Constraint-Completeness Check — ❌ FAILS.** Touchplan AI flagged 2 of 11 categories (materials + submittals). Re-running the full taxonomy adds: **inspections-and-hold-points (A-1163 above-ceiling inspection request not submitted)**, **safety / permits-to-work (A-1142 above ICRA Zone 2 — ICRA Class III precautions and ICRA-trained crew not confirmed)**, **owner / tenant / operations coordination (A-1142 occupied-healthcare-adjacent corridor daytime patient access)**, **site conditions & access (Zone 4 three-trade stacking Thu-Fri)**, and **weather (A-1177 membrane roof patch 50% rain probability Tue PM / Wed AM)**. Net 5 categories missed — that's 5 missed pre-constraints, not "proceed as planned."
>
> **2. In-Progress Production-Rate Sanity Check — ❌ FAILS.** Touchplan reads as-planned remaining duration on A-1155 in-wall blocking Zone 3 as 5 WD (consistent with the 60% complete + as-planned 18 LF/day). Re-computed: last 5 WD of ABC Carpentry actual output averages 14 LF/day = 78% of as-planned rate. **Implied finish 2026-06-04, not 2026-06-02.** A-1158 plumbing rough (which depends on A-1155 finish) is now **at-risk of a 2 WD slip** — Touchplan flagged neither. Promote A-1155 to 🟠 and A-1158 to 🟠.
>
> **3. Near-Critical Identification — ❌ FAILS.** Touchplan flagged only the critical path (A-1170 / A-1175 / A-1182). Re-run at config-driven ≤ 5 WD float threshold: **A-1142 MEP above ICRA Z2 (float = 3 WD)** is near-critical and unflagged. Add to at-risk.
>
> **4. Trade-Stacking & Crew-Balance Reading — ❌ FAILS.** Touchplan does not surface Zone 4 three-trade stacking (Acme + Bright + Premier all in 320 LF corridor Thu-Fri) — would require activity-by-area-by-day matrix that the platform does not generate. Add as Concern #4.
>
> **5. Soft-Logic-vs-Hard-Logic Predecessor Reading — ❌ FAILS.** Touchplan treats A-1172 HVAC rough → A-1170 framing close-out as hard. **It is soft** — drywall close-up can occur the day after MEP rough, not same-day. Re-classifying this predecessor opens float-recovery option in the pull-plan ask. (Same point as Concern #4 in the pull-plan briefing.)
>
> **6. PPC / RNC Trend Reading — ❌ FAILS.** Touchplan reports last-week PPC 77% with no RNC root-cause breakdown. Re-read of last 4 weeks of RNCs: **3 of 4 RNCs in PPC week of 5/18 = un-cleared above-ceiling inspection request** — dominant root cause. The PPC target should not raise to 80% until that root cause is broken. **Recommended PPC target: 78% (hold current), not 80% (raise) — pull-plan ask is to break the un-cleared-inspection-request pattern, then raise.**
>
> ## FINAL SITE-SUPER-ACCEPTED RECOMMENDATION
>
> **Do NOT "proceed as planned."** Hold A-1142 until ICRA confirmation Mon AM; commit ABC Carpentry +1 pair to Zone 3 Mon AM (or accept 2 WD A-1158 slip); submit inspection request by noon Mon; de-stack Zone 4 via pull-plan ask; pre-position roofing materials for either-day membrane patch. **PPC target 78%, not 80%.** Five concerns to raise in Monday's pull-plan, prioritized above.
>
> ## PROVENANCE
>
> - **Platform:** Touchplan AI, AI version per 2026-Q2 release
> - **Platform recommendation:** Proceed as planned, PPC target 80%
> - **Redline changes:** All 6 dimensions flagged adjustments. 5 constraint categories added (inspection, safety, owner, site, weather). 2 activities promoted to at-risk (A-1155, A-1158). 1 near-critical activity surfaced (A-1142). 1 soft-predecessor reclassified (A-1172 → A-1170). PPC target held at 78% (not raised to 80%).
> - **Final super recommendation:** Five-concern pull-plan briefing with explicit ask for each; PPC target 78% pending un-cleared-inspection-request RNC pattern break.
> - **Disclaimer:** This redline is AI-assisted; pull-plan commitment requires the foremen's actual commitments, not the platform's or the AI's inference.
