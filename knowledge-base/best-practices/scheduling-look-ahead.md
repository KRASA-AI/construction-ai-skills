# Look-Ahead Scheduling & Last Planner Constraint Analysis — Reference

> Reference for skills that critique, generate, or audit short-interval
> look-ahead schedules (typically 2–6 weeks) for construction projects.
> Look-ahead planning is where the master schedule meets the field — the
> place where an honest constraint conversation either happens or does not.
>
> This reference is platform-neutral. It assumes a project running on a
> CPM master schedule (P6, MS Project, Phoenix, Asta, Primavera Cloud, or
> equivalent) and applies whether the team is using formal Last Planner
> System (LPS), a Lean look-ahead derived from a Pull Plan, or a traditional
> two-week look-ahead spun off the master CPM.

---

## Why Look-Ahead Discipline Matters

The master schedule says what *should* happen. The daily field plan says what *will* happen tomorrow morning. The look-ahead is the interval — usually 2–6 weeks out — where the team converts *should-do* work into *can-do* work by removing constraints. When the look-ahead is run with discipline, three things follow: weekly Plan Percent Complete (PPC) trends upward, near-critical activities are protected from float erosion, and the trades stop showing up to a work face that is not ready for them.

When the look-ahead is run as paperwork, three different things follow. Crews are released to work that has open constraints (missing material, unanswered RFI, unapproved submittal, inspection not scheduled, predecessor not complete). Trade stacking and rework absorb crew hours. Float is consumed silently — the "remaining float" number on the master keeps drifting down without anyone owning the cause. By the time the slip is visible at the master-schedule level, the cause is usually three look-ahead cycles in the past and no longer recoverable.

The discipline that prevents this is small, repeated, and unglamorous: every week, every activity in the window is examined against a fixed list of constraint categories; every constraint that is *not* clear is assigned an owner and a clear-by date; the activities whose constraints clear by Sunday night go into the next week's commitment; the activities whose constraints do not clear are not committed. PPC measures the team's reliability against its own commitments, not against the master schedule.

This reference documents the constraint taxonomy, the make-ready process (Tasks Anticipated → Tasks Made Ready → Percent Plan Complete), the reason-for-non-completion taxonomy, the float-consumption discipline, the crew-balance heuristics, and the weather / inspection scheduling rules that the look-ahead-critique skill (and any future look-ahead-generation skill) should draw on.

---

## The Last Planner System's Six Processes

The Last Planner System (Glenn Ballard / Lean Construction Institute) defines six interlocking planning processes. A look-ahead skill is operating on processes 3–5; it should be aware of where its inputs come from (1–2) and where its outputs land (5–6).

| # | Process | Horizon | Owner | Output |
|---|---|---|---|---|
| 1 | **Master Scheduling** | Project | Scheduler / PM | CPM milestones, critical path |
| 2 | **Phase Scheduling (Pull Planning)** | Phase (1–3 months) | Phase team (trades + GC) | Phase plan with handoffs and milestones |
| 3 | **Look-Ahead Planning (Make-Ready)** | 2–6 weeks | Superintendent + foremen | Constraint-cleared tasks ready for commitment |
| 4 | **Weekly Work Planning (Commitment)** | 1 week | Foremen | Committed tasks with named owners |
| 5 | **Daily Coordination** | 1 day | Foremen + crew leads | Crew assignments, sequence |
| 6 | **Learning** | Weekly + retrospective | Whole team | PPC, RNCs, root-cause |

The look-ahead window is the make-ready process. Its purpose is **not** to predict what will be built; its purpose is to **screen** the master schedule's plan against constraints and to make the work ready for next-week commitment. A task that enters the look-ahead window with open constraints either has those constraints cleared during the window or is bumped — it does not get committed with constraints still open.

---

## The Constraint Taxonomy

Every activity in the look-ahead window is screened against the same fixed list of constraint categories. The categories are durable; the specifics change activity by activity. A practitioner-level taxonomy:

### 1. Design

- Unanswered RFI affecting the activity (RFI ID, age, responsible party)
- Open ASI / SI not yet incorporated into the field set
- Coordination conflict not resolved between disciplines (BIM clash log, MEP coordination)
- Spec interpretation ambiguity for the relevant section
- Constructability question that the design team has not answered

### 2. Materials

- Material on site? If not, confirmed delivery date with carrier? Released for delivery from supplier?
- For long-lead items (switchgear, custom millwork, AHUs, generators): tracked separately on the long-lead log; ship date confirmed or at risk?
- Owner-furnished items (OFCI / OFOI): in custody and accepted, or still with the owner / vendor?
- Just-in-time deliveries: laydown space allocated, unloading equipment scheduled, receiving crew allocated?

### 3. Submittals

- All submittals required for the activity at status "Approved" or "Approved as Noted" before install?
- Substitution requests still pending? (A pending substitution is an open constraint, not just a paperwork item.)
- Color / finish samples approved by the owner / architect for the relevant scope?
- Manufacturer's installation instructions in the field foreman's hands (specifically — not just on the file server)?

### 4. Inspections & Hold Points

- Required inspection scheduled with the AHJ / CxA / SOI / IOR with adequate lead time (usually 24–48 hr in most jurisdictions)?
- Owner-required inspections (envelope mock-up, mock-up sign-off, owner-witness pour) coordinated and confirmed?
- Hold points in the spec that block the next activity (concrete pre-pour, MEP rough close-in, fire-rated joint pre-cover) covered by a confirmed inspection slot?

### 5. Permits & Approvals

- Building permit current and not in renewal limbo?
- Trade permits required for the activity (electrical, plumbing, mechanical, fire, hot-work, demo, dewatering, street use, after-hours, crane swing) in hand?
- Special permits (utility shutoff, crane closure, road closure, energization) applied for and granted with the right window?
- Environmental approvals (storm-water, dust control, noise variance, hazmat) current and matched to the activity scope?

### 6. Predecessors

- Every predecessor either complete or in a status that allows the activity to start as planned?
- For in-progress predecessors: remaining duration realistic vs. observed crew output (the skill should compute the implied daily production rate and compare to as-planned)?
- Soft-logic predecessors (those that are sequencing preferences, not technical requirements) flagged so they can be challenged in the pull-plan?

### 7. Crew & Resources

- Trade headcount available on the planned days, in the planned skill mix?
- Foreman / lead allocated and not split between projects?
- Equipment in place and in working order (lifts, scaffolding, tower-crane time, generators, pumps, power, water, light, heat for cold-weather concrete)?
- Conflicting demands from other trades on the same shared resource (one mast climber, one tower crane, one personnel hoist)?

### 8. Site Conditions & Access

- Work face physically ready and accessible? (Often the most-missed category — the materials are on site, the submittal is approved, the crew is staffed, but the work area is locked behind another trade's incomplete work or a temporary protection that has not been removed.)
- Access route clear (laydown, hoist time, vertical transport, freight elevator slot)?
- Adjacent activity not creating a conflicting hazard exposure (overhead work above, hot work alongside, energization nearby)?
- Site logistics (parking, deliveries, dust / noise / vibration controls) compatible with the activity?

### 9. Weather

- Activity weather-sensitive (exterior concrete pour, membrane roofing, envelope install, exterior paint, site grading, exterior hardscape)?
- Forecast for the window read against the activity's weather thresholds (wind for crane, rain for concrete, temperature for masonry, humidity for paint and coatings, sun-load for sealants)?
- Contingency day or alternate sequence identified?

### 10. Safety & Permits-to-Work

- High-risk activity (working at heights, confined space, hot work, suspended loads, energized work, trenching, demolition, lift over occupied space) has the JHA / PTP / permit-to-work prepared?
- Stand-by personnel (fire watch, attendant, qualified rescuer) committed?
- Pre-task plan complete and signed by the crew before tools come out (see `operations/pre-task-plan-drafter.md`)?

### 11. Owner / Tenant / Operations Coordination (Occupied / Operating Sites)

- Owner-required after-hours window confirmed?
- Tenant-coordination notice sent within the lease-required notice window?
- Operating-utility shutdown coordinated with facility operations (hospitals, data centers, manufacturing, retail) with a written switching plan?
- Owner-access day not conflicting with the activity's noise / dust / access profile?

A constraint that is in the **wrong category** or **missing from the taxonomy** is the most common cause of a look-ahead miss. The taxonomy is fixed; the activity-specific entries change every week. Skills that critique a look-ahead should screen every activity against every category — not because every category will be relevant to every activity, but because the practitioner discipline of "yes this constraint is N/A" is materially different from "I forgot to check this category."

---

## Tasks Anticipated → Tasks Made Ready → Percent Plan Complete

The Last Planner System's three measurement signals form a learning loop:

```
Master Schedule → Look-Ahead Window → Weekly Work Plan → Daily Coordination
                  (Tasks Anticipated)  (Tasks Made Ready)  (Tasks Completed)
                          │                    │                   │
                          │                    │                   │
                          └─── TMR / TA ───────┴── PPC = TC / TMR ─┘
                              "Make-Ready Rate"  "Plan Reliability"
```

### Tasks Anticipated (TA)

The number of tasks the look-ahead window placed in the immediate (next-week) commit zone. This is what the team *intends* to commit if constraints clear.

### Tasks Made Ready (TMR)

The number of those Anticipated tasks whose constraints actually cleared in time for next-week commitment. The ratio **TMR / TA** is the **make-ready rate** — how good the team is at clearing constraints during the look-ahead. A make-ready rate below ~80% on a stable project is a constraint-clearing process problem (usually: late RFI responses, late submittal returns, owner decisions held for monthly OAC instead of weekly).

### Tasks Committed (TC)

The number of TMR tasks that were actually committed to in the weekly work plan. (Some tasks made ready are deferred for sequencing reasons; not every TMR is committed.)

### Plan Percent Complete (PPC)

```
                    Tasks Completed at 100% as committed
PPC  =  ─────────────────────────────────────────────────────────────
                       Tasks Committed in the Weekly Work Plan
```

A task is counted as complete only if it was finished **on time, in the planned location, by the committed crew, to the agreed quality.** A task that is 95% complete is **not** counted. A task that is complete but late is **not** counted. A task that is complete on time but at a different location than committed is **not** counted.

PPC is binary by design. The point is reliability of commitments, not progress against the master.

### PPC Bands

| PPC | Reading |
|---|---|
| < 50% | The plan is fiction. The look-ahead is not screening constraints; the WWP is overcommitting. Reset the discipline. |
| 50–65% | Lower bound of "trying." Common on first-time-LPS projects in the first 4–8 weeks of adoption. Improvement should be visible week over week. |
| 65–80% | The plan is real but not reliable. Most projects live here. Targeted improvement on the top 2–3 RNC categories typically lifts 5–10 points per quarter. |
| 80–90% | The plan is reliable. The team can pull from backlog when work clears early. Constraints are clearing during the look-ahead, not during commitment week. |
| > 90% | The plan is reliable and the team is leaving capacity unused. Either pull more aggressively from backlog, or flag that the plan is being padded. Sustained > 95% for 4+ weeks usually means the WWP is protecting the PPC number. |

### Make-Ready Rate (TMR / TA) Bands

| TMR / TA | Reading |
|---|---|
| < 70% | Constraint-clearing process is broken. Look at RFI cycle time, submittal cycle time, and the look-ahead horizon (often too short). |
| 70–85% | Typical on most projects. Targeted improvement on the slowest-clearing constraint category usually drives the most lift. |
| > 85% | The constraint-clearing process is healthy. Focus moves to commitment discipline (PPC) and learning (RNC trends). |

A look-ahead-critique skill that does not surface TMR/TA and PPC trends — when the data is provided — is missing the most diagnostic signals on a Lean project.

---

## Reasons for Non-Completion (RNC) Taxonomy

When a committed task does not complete, the foreman records a Reason for Non-Completion. The taxonomy is small enough to be remembered and large enough to discriminate. A practitioner-level RNC list:

1. **Prerequisite not complete** — predecessor activity slipped (most common; root-cause should be traced one level deeper)
2. **Material not available** — not on site, late delivery, wrong material delivered, damaged in transit
3. **Information not available** — open RFI, unapproved submittal, conflicting drawings, incomplete BIM coordination
4. **Crew not available** — labor short, foreman pulled, crew on different project, attendance
5. **Equipment not available** — lift down, crane unavailable, generator failure, hoist queue
6. **Site conditions** — work face not accessible, adjacent trade incomplete, temporary protection in place, owner access required
7. **Weather** — outside the activity's threshold; correctly forecast or surprise
8. **Inspection / authority** — inspector did not show, AHJ punched the work, CxA failed the test
9. **Owner / tenant / operations** — owner decision pending, tenant access denied, operations shutdown deferred
10. **Estimating / planning error** — task size mis-estimated, sequence wrong, crew sized for different scope
11. **Safety** — unsafe condition halted the work, near-miss triggered a stand-down, missing permit
12. **Other** — the catch-all; aggressive use of "Other" usually means the taxonomy is missing a category for the project

The **distribution** of RNCs over a 4–8 week trailing window is more diagnostic than any single PPC number. A team with PPC = 72% running 60% on RNC #1 (prerequisite not complete) has a different problem than a team with PPC = 72% running 50% on RNC #3 (information not available). The first is a sequencing / commitment problem; the second is an information-flow problem.

A look-ahead critique skill should call out the **top 1–2 RNC categories from the trailing window** and tie a specific recommendation to the activities in the upcoming window that are most exposed to the same category.

---

## Float Consumption Discipline

Float — the number of working days an activity can slip without delaying the project completion or the next milestone — is a finite project resource. The discipline of look-ahead is to spend it deliberately.

### Float Bands (Working Days)

| Total Float | Status | Look-Ahead Treatment |
|---|---|---|
| Negative | **Project late.** Recovery plan required. | Flag every activity; recovery sequence is the look-ahead. |
| 0–5 | **Near-critical.** | Flag explicitly; review constraint-readiness before every commitment. |
| 6–10 | **Limited float.** | Monitor float consumption rate; flag if consuming > 1 day per week. |
| 11–20 | **Buffered.** | Standard look-ahead screening. |
| > 20 | **Floater.** | Standard look-ahead screening; watch for soft-logic ties that may be obscuring criticality. |

### Float Consumption Rate

Track over a trailing 4-week window the change in **total float for each activity**. A float-consumption rate of more than ~1 day per calendar week on a non-critical activity is the early warning that a near-critical activity is forming. The look-ahead-critique skill should flag activities whose float has dropped by ≥ 5 working days in the trailing 4 weeks, even if the current float is still positive.

### Soft Logic vs. Hard Logic

A predecessor relationship is **hard** when one activity *cannot* start until another completes for technical reasons (you cannot frame walls before slab cure; you cannot install drywall before MEP rough close-in). It is **soft** when the relationship is a sequencing preference (we want to finish floor 3 before starting floor 4, because we have one mast climber).

Soft-logic ties often get hard-coded into CPM software and then drive critical-path calls that are not technically real. A pull-plan facilitator's job — and a look-ahead critique skill's job — is to surface soft-logic ties on near-critical activities and ask whether they can be broken (with a second crew, a different sequence, an additional resource) to recover float.

### Path-of-Construction Sanity Check

For any near-critical chain in the look-ahead window, walk the **physical path of construction**:

1. Where is the work?
2. What is above it, below it, alongside it?
3. Who is working in the same space on the same day?
4. What temporary protection or condition is required for the work?
5. Who removes the temporary protection, and when?

A near-critical activity whose physical path-of-construction is not clear in 30 seconds of conversation is the activity most likely to slip. The look-ahead is the venue to surface that.

---

## Crew Balance & Productivity Heuristics

### Daily Crew-Hour Budget

For each crew on each day, compare the **demanded crew-hours** (from the look-ahead) to the **available crew-hours** (from the resource plan). Available crew-hours are not headcount × shift length. They are headcount × productive hours per shift, where productive hours per shift on most US commercial projects ranges 5.5–7.0 against an 8-hour day, after accounting for huddle, travel within the project, breaks, end-of-shift cleanup, and unproductive-but-necessary time (waiting on lift, waiting on inspection, waiting on adjacent trade).

A daily demand exceeding ~110% of available is overcommitted; the work either spills to the next day, gets done at lower quality, or pulls labor from a different planned task.

### Travel & Setup Tax

When a crew is split between non-adjacent work faces — different floors, different buildings, different ends of a long site — the travel-and-setup tax compounds. A practitioner-level rule of thumb: a crew split across two non-adjacent faces loses 0.5–1.0 productive hours per worker per day to travel, transitions, and tool-pack movement. Split across three faces loses 1.5–2.0 hours per worker per day. The look-ahead should consolidate work faces where possible, and where it cannot, the demand-vs-available calculation should reflect the tax.

### Trade Stacking

Two crews working in the same physical work face on the same day is **stacking**. Some stacking is unavoidable (MEP rough on the same floor; ceiling and above-ceiling work in coordinated bands). Most stacking that shows up in a look-ahead is avoidable — it is the residue of a master schedule that did not separate trades by time or by sub-area. The look-ahead-critique skill should flag every stack and recommend either a sub-area split (one crew north, one south) or a time split (one crew morning, one afternoon).

### First-Run Studies & Productivity Benchmarks

For repeating activities (decking square footage per day, drywall hung per day per worker, MEP rough per fixture per day, brick laid per day per mason), the team should track actual production rates and use them — not estimating-stage benchmarks — to size crew-hours in the look-ahead. A first-run study is the formal way to capture this on a new repeating scope; a reasonable substitute is the foreman's tracked production from the last week of the same activity.

The look-ahead-critique skill, when given recent production data, should compute the implied daily production rate for any in-progress activity and compare it to the as-planned rate. A rate at 70% of as-planned is a flag; a rate below 60% is a near-certainty of slip.

---

## Weather Scheduling

Weather is the constraint category most often handled by reaction. The look-ahead window is the place to handle it by anticipation.

### Weather-Sensitive Activities (Common)

| Activity | Threshold (Typical) |
|---|---|
| Exterior concrete pour | Air temp 40–90 °F; no rain in 4 hr post-pour; wind ≤ 25 mph for finishing; hot-weather and cold-weather concreting ACI 305 / 306 protections required outside the band |
| Membrane roofing (single-ply) | Surface temp ≥ 40 °F (per manufacturer); dry surface; wind ≤ 25 mph |
| Built-up / mod-bit roofing | Air temp ≥ 50 °F; dry deck; calm conditions |
| Masonry | Air temp ≥ 40 °F unless cold-weather protections (ACI 530.1 / TMS 602); humidity ≤ 90% |
| Exterior paint / coatings | Per manufacturer; usually 50–95 °F, surface dry, RH ≤ 85%, surface temp ≥ 5 °F above dew point |
| Sealants / weatherproofing | Per manufacturer; usually 40–100 °F; surface dry |
| Crane lift | Wind per manufacturer chart (often gust limit 20 mph for routine, 35 mph for heavy lift) |
| Tower-crane swing | Per manufacturer chart and local code; gust limits typically 35–45 mph |
| Site grading / earthwork | Soil moisture content within specified band; not on consecutive rain days for cohesive soils |
| Exterior welding / hot work | Wind ≤ 5 mph for shielded processes; relative-humidity-driven dew control; permit-to-work |
| Caulk / fire-stopping at exterior | Surface temp ≥ 5 °F above dew point; substrate dry |
| Exterior glazing | Wind ≤ 25–30 mph; sealant-cure temp threshold per manufacturer |

### Look-Ahead Weather Read

For each weather-sensitive activity in the window, the look-ahead-critique skill should:

1. Read the forecast for the planned day(s)
2. Compare to the activity's threshold
3. Flag activities that are below threshold or marginal
4. Suggest a swap with a non-weather-sensitive backlog activity for the same crew, *if backlog exists*
5. If no backlog swap is available, flag the float consumption that would result from a slip

A common look-ahead miss: the activity is technically weather-feasible (e.g., concrete pour at 42 °F) but the **crew sequence around it** is not (the finishing crew is unavailable on Saturday for the cold-weather follow-on protection). The look-ahead has to read both.

---

## Inspection Scheduling

### Lead-Time Discipline

Most AHJs and CxAs require 24–48 hours of notice for an inspection. A few jurisdictions and many high-rise / hospital / data-center projects require longer (48–72 hours, or a fixed inspection window per week). The look-ahead should schedule the inspection request **before** the prerequisite work is sequenced to complete, not after.

Hold-point inspections (concrete pre-pour, MEP rough close-in, fire-stop pre-cover, envelope mock-up sign-off, structural welding NDE, tank pressure test, balancing report sign-off) block the next activity. A missed hold-point inspection becomes a **two-day** slip in most jurisdictions — one day to re-schedule, one day to actually inspect. The look-ahead window should treat hold points as named activities with their own predecessor relationships, not as paperwork.

### Inspector Availability

On busy AHJ rosters (urban municipalities, certain state programs, inspector shortages in high-growth markets), inspector availability is a real constraint. The look-ahead should track a running inspection schedule with the AHJ contact and treat any rejection or no-show as a constraint-clearing failure on the relevant activity.

### CxA / Owner-Witness Coordination

Commissioning agent (CxA) inspections, owner-witness pours, and tenant-witness sign-offs require coordination on a multi-party calendar. The look-ahead should escalate any CxA / owner-witness item that is not confirmed by the start of the look-ahead window — these never clear faster late.

---

## Hard Rules (Look-Ahead Discipline)

These are the discipline rules the look-ahead-critique skill enforces in every output. They are not preferences; they are the rules a skeptical pull-plan facilitator applies in the room.

1. **No commitment without constraint clear.** A task with any open constraint at end-of-day Sunday is not committed for the next week. (Move to backlog or push to a later week.)
2. **No silent floats.** Float consumption is announced. An activity moving from 8 days of float to 3 days of float in a week is reported, not absorbed.
3. **No stacking without a plan.** Trade stacks are either coordinated (named owners, time bands, sequence) or reorganized.
4. **No "we'll figure it out."** A handoff between trades that is "implicit" is not a handoff — it is a future RNC. Every interface gets a date and an owner.
5. **No paper inspection scheduling.** An inspection that is "scheduled" without a confirmation from the AHJ is open. Treat it as a constraint.
6. **No PPC inflation.** A task at 95% does not count. A task complete late does not count. A task complete in a different location does not count. The number means what the LPS says it means.
7. **No master-schedule overrides.** The look-ahead does not change the master schedule's logic; it screens the master against constraints. Logic changes — soft-to-hard, sequence revisions, scope re-allocation — go through the formal CPM update.
8. **No JHA / PTP retro-fit.** A high-risk activity in the window without a pre-task plan in hand by the morning huddle is not committed. (See `operations/pre-task-plan-drafter.md`.)
9. **No silent weather rolls.** A weather-sensitive activity that slipped from one day to another *because of weather* is recorded with the actual weather data, not "weather TBD."
10. **No "the AI said it was ready."** Constraint-readiness calls are made by named people (foreman, super, PM, scheduler), not by an AI assistant. The AI surfaces; the people decide.

---

## Severity Triage for Look-Ahead Flags

When a look-ahead-critique skill produces a one-page briefing, it should color-code its flags so the superintendent can read it in 90 seconds at 6:15 AM:

- 🔴 **Red — must clear before commitment.** Open constraint with no path-to-clear by Sunday; or near-critical activity (float ≤ 5 working days) with any open constraint; or safety / permit / inspection blocker.
- 🟡 **Yellow — at-risk, owner assigned, clear-by date this week.** Constraint has a path-to-clear but is not yet cleared.
- 🟢 **Green — cleared.** Constraint resolved, activity ready for commitment.

Order in the briefing: 🔴 first, 🟡 second, 🟢 only as confirmation that the constraint-readiness table is current.

---

## Recovery Plans (When the Window Is Already Late)

When the master schedule is already showing negative float on the critical path, the look-ahead's job changes from screening to recovery. The discipline shifts to:

1. **Concurrent vs. sequential.** What activities currently sequenced sequentially can be run concurrently with added crew, sub-area split, or extended hours?
2. **Crew-size up.** Where is the duration crew-limited (more workers shorten the duration) vs. work-face-limited (more workers do not help)?
3. **Shift extension.** Is there an extended-shift or weekend-shift option that the contract allows and the crew can sustain (typically 2–4 weeks before productivity collapses on sustained 6×10s)?
4. **Re-sequencing.** Are there soft-logic ties on the critical path that can be broken to recover float?
5. **Scope deferral.** Can any non-critical scope be deferred past substantial completion (TCO scope, punch-list scope, finish-out scope) to take it off the critical path?
6. **Notification.** Has the schedule slip been formally notified per the contract notice clause? (Most contracts have a 7 / 14 / 21-day notice window for delays affecting the critical path; missing the notice is a different problem than missing the schedule.)

A recovery-mode look-ahead is a different document than a normal look-ahead. The skill should detect the negative-float condition on input and switch modes.

---

## Cross-Skill Coordination

This reference is consumed by, and informs, the following skills:

| Skill | How it draws on this reference |
|---|---|
| `operations/lookahead-schedule-critique.md` | The constraint taxonomy, RNC categories, PPC bands, float discipline, weather-threshold table, and severity triage are the core engine of the critique |
| `operations/daily-log-generator.md` | The RNC taxonomy is the same one used in the daily-log delay/disruption section; the float-consumption flag in the daily log uses these bands |
| `operations/rfi-response-drafter.md` | Open RFIs are constraint-category #1 (Design); the RFI cycle-time standard from this reference (typical 5 working days) sets the urgency on look-ahead-blocking RFIs |
| `operations/submittal-review-summary.md` | Open submittals are constraint-category #3; the make-ready rate is sensitive to submittal cycle time |
| `operations/pre-task-plan-drafter.md` | Constraint-category #10 (Safety) is the bridge — a high-risk activity does not commit without a PTP in hand |
| `operations/punch-list-organizer.md` | RNC #6 (Site Conditions) often surfaces as punch-list items being worked in adjacent activities; coordination with the punch-list helps clear category #8 (Site Conditions & Access) |
| `admin/delay-claim-drafter.md` | Float consumption, RNC documentation, and trailing-window PPC trends are the contemporaneous evidence base for any delay claim |
| `admin/wip-billing-reviewer.md` | A look-ahead trending into negative float on the critical path is a signal that the next WIP cycle should expect productivity adjustments and possible cost-to-complete revisions |
| `admin/contract-risk-reviewer.md` | The contract notice clause for delays interacts with the recovery-plan workflow; the reviewer reads the notice clause; the look-ahead surfaces when it triggers |

---

## What This Reference Does Not Cover

This reference is intentionally scoped to **look-ahead window** discipline. It does not cover:

- **Master CPM scheduling and TIA methodology** — that is a licensed scheduler's domain. The reference assumes a master CPM exists and is being updated separately.
- **Earned-value methodology** — covered indirectly via the WIP-reporting and delay-claim references; not the focus here.
- **Specific scheduling-software workflow** — P6, MS Project, Phoenix, and Asta differ in their data models. This reference is platform-neutral.
- **Resource-leveling algorithms** — handled by scheduling software; the reference assumes the resource plan is an input.
- **Pull-planning facilitation technique** — covered in LPS / LCI training and is a meeting-facilitation skill, not a look-ahead-document skill. The reference assumes a phase pull-plan exists upstream.

Where the look-ahead surfaces a finding that requires master-schedule logic changes, formal TIA, or a recovery acceleration plan — the look-ahead-critique skill should flag the finding and recommend the appropriate downstream artifact. It does not produce them.

---

## Sources & Further Reading

- Glenn Ballard. *The Last Planner System of Production Control* (PhD thesis and subsequent practice guides via Lean Construction Institute).
- Lean Construction Institute. LPS practice guides on Make-Ready, PPC, and RNCs.
- ACI 305R / 306R for hot-weather and cold-weather concreting thresholds.
- TMS 602 / ACI 530.1 for cold-weather masonry.
- AGC of America and ENR practitioner literature on schedule recovery.
- Yoonhwa Jung & Mani Golparvar-Fard, *ExpertPlanner: A Mixture-of-Experts Transformer Language Model for Decomposing Construction Look-ahead Plan Tasks from Long-term Master Schedules* (2026) — academic validation that look-ahead generation from master-schedule activities is a learnable task with measurable outputs (BLEU@4 71.2; average score 82.4 on a 4-master-schedule / 30-look-ahead-plan / ~3,400-task corpus). Useful as a reference for AI-generated look-ahead candidates that the critique skill might validate against.

This reference does not reproduce or paraphrase any of the above. It documents the practitioner-level discipline that the look-ahead-critique skill consumes.
