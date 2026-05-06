# Photo-Based Hazard Identification — Reference

> Reference for skills that ingest a jobsite photo (or a small set of photos)
> and produce a structured Potential Hazard Identification Table (PHIT) — a
> ranked list of hazards visible in the image, mapped to OSHA / state-plan
> citations, with recommended controls and a triage severity. Used during
> pre-task planning, morning huddles, supervisor walks, post-incident scene
> review, and toolbox-talk preparation.
>
> This reference is platform-neutral. The same discipline applies whether the
> photo is being analyzed by a multimodal LLM (Claude / GPT / Gemini), by a
> purpose-built construction-safety vision model (Procore Safety / Autodesk
> Forma / HammerTech Intelligence / BuildPass / Field1st / Oracle Advisor for
> Safety / Turner SafeT Coach), or by a human safety professional reviewing
> the photo at the trailer. The output shape is the same; what changes is the
> reviewer-of-output discipline (see the cross-skill table at the end).

---

## Why a Reference for This

In May 2026, the largest US general contractor by revenue released its
internal AI-powered photo-hazard tool to the broader construction industry,
free of charge, timed to Construction Safety Week. The release made one
shape concrete: a worker on a phone takes a photo of a work face, the tool
returns a structured table of hazards, ranked, with controls and policy /
OSHA references, and the worker reads it back to the crew before picking up
a tool. That shape is now industry-standard the way the daily log and the
PTP are industry-standard — not because of any single vendor, but because
several vendors are converging on the same shape.

A KRASA skill that uses this shape (a photo input, a structured hazard table
out) has the same failure modes whether the underlying model is Claude,
ChatGPT, Gemini, or a dedicated safety-platform vision model: the hazards
that were not visible in the frame are still hazards (line-of-fire from a
trade out of frame; an unmonitored confined-space atmosphere; an electrical
panel behind a closed door); the hazards that the model is *over-confident*
about (every yellow vest = compliance; every guardrail = adequate; every
ladder = good) under-state real risk; and the model's citation discipline is
only as good as the prompt asks it to be. This reference exists so the
relevant skills (`safety-plan-builder.md`, `pre-task-plan-drafter.md`,
`daily-log-generator.md`, `project-qa-assistant.md`) can cite a single
practitioner-level discipline rather than re-stating it inline each time.

---

## The Photo-Based Hazard Identification Workflow

The end-to-end workflow has six steps. A skill drafting or reviewing the
output should know which of these steps are happening *outside* the prompt
(the human's responsibility) and which are happening *inside* (the model's
responsibility — and therefore the prompt's).

| # | Step | Who owns it | What gets produced |
|---|---|---|---|
| 1 | **Photo capture** | Crew leader / superintendent / safety officer in the field | One or more photos of the work face, framed to show the hazards in context |
| 2 | **Frame quality check** | Capturing person | A confirmation that the photo shows the work face (not just a worker's back), at adequate resolution, with adequate lighting |
| 3 | **Hazard identification** | Model / AI / reviewing safety pro | Structured PHIT — hazards, OSHA citations, controls, PPE, severity |
| 4 | **Out-of-frame supplementation** | The capturing person, prompted by the model | Hazards present at the work face that the photo does not show (overhead trades; energized panels behind closed covers; confined-space atmosphere; tomorrow's weather) |
| 5 | **Triage and disposition** | Crew leader / competent person | Each hazard is dispositioned: *control already in place* / *control to apply now* / *stop work and reset* |
| 6 | **PTP / toolbox-talk integration** | Crew leader | The day's PTP or the week's toolbox talk references the PHIT and any open dispositions |

The skill is operating on step 3, with explicit prompts that *require* the
human to provide step 4 inputs. A skill that produces a PHIT *without*
asking what is out of frame is producing a half-PHIT.

---

## Photo Quality Requirements

The PHIT is only as good as the photo. The skill should reject a photo (and
say so plainly) when any of the following are true. These are reject
conditions, not advisory ones — the right output for a bad photo is "I
cannot run a PHIT on this image; please retake with [specific fix]," not a
PHIT with three hazards and an apology.

- **Resolution too low.** Lower than ~1024 px on the long side, or compressed
  past the point where guardrail tops, scaffold planking, harness D-rings,
  PPE markings, and OSHA-required tags are legible.
- **Subject not the work face.** The photo shows a worker's back, the inside
  of the trailer, the parking lot, the safety stand-down posters, etc. The
  PHIT is for the *work face* — the location where the next eight hours of
  work will happen. A face shot of a worker with no work context is not a
  PHIT-able input.
- **Critical hazard occluded.** The lower half of the trench is out of
  frame; the crane boom is cut off above the lift radius; the working
  surface of the scaffold is not visible; the energized panel face is
  blocked by a body. If the hazard the worker came to ask about is not
  visible, the PHIT cannot identify it.
- **Light too low or too uneven.** Backlit silhouettes; flash hot-spots that
  blow out the working surface; shadowed near-side that hides the trench
  wall or the floor opening. The PHIT misses the most when the light is
  wrong, because the missed hazard is exactly where the eye cannot see.
- **Image staged.** Pre-toolbox-talk poses, bid-photo glamour shots, hard-hat
  group photos. The PHIT is for honest field conditions, not for marketing.

When the photo passes, the skill proceeds. When it does not, the skill
returns a single-line reject with the specific fix and stops there.

---

## The Potential Hazard Identification Table (PHIT)

The PHIT is the structured output. It has nine columns and a one-line header.
Every row is one hazard. A photo with no visible hazard returns a PHIT with
zero rows and a single line of explanation — a zero-row PHIT is a legitimate
output, not a failure.

| Column | What it holds | Example |
|---|---|---|
| **#** | Row number | 1 |
| **Hazard** | Specific, location-anchored description | "Unprotected leading edge at floor opening, north wall of L4, ~5 ft × 8 ft, no guardrail or cover" |
| **OSHA / Standard** | The applicable citation, verified, not invented | "29 CFR 1926.501(b)(4) — Holes" |
| **Severity** | 🔴 stop-work / 🟡 control-now / 🟢 monitor | 🔴 |
| **Engineering control** | The physical control that removes or reduces the hazard | "Install standard guardrail (top rail 42 in ± 3 in; midrail; toeboard) or rated cover with secured edges" |
| **Administrative control** | The procedural control | "No work within 6 ft of the opening until guardrail or cover is in place; competent-person daily inspection logged" |
| **PPE beyond baseline** | Task-specific PPE | "Personal fall-arrest system tied to the column-line E certified anchor while installing guardrail" |
| **Disposition** | Already in place / apply now / stop-work | "Stop work; install guardrail before work resumes" |
| **Out-of-frame ask** | What the model needs the human to confirm | "Confirm whether opening is on a permit-required confined-space level; confirm whether overhead trade is scheduled today" |

Two notes on the PHIT format. First, **severity comes before controls** in
the column order on purpose — the eye should land on 🔴 first so the most
dangerous hazard is read first when the crew leader walks the table. Second,
the **out-of-frame ask** column is what makes the PHIT honest: every row
has at least one out-of-frame question the model is *asking the human*, not
answering. A PHIT with no out-of-frame asks is a PHIT that thinks it can see
through walls.

---

## Severity Triage (🔴 / 🟡 / 🟢)

The triage is calibrated to the same three-band shape used by
`rfi-response-drafter.md` (CP-affecting / productivity-affecting /
informational), `daily-log-generator.md` (delay/disruption severity), and
`safety-plan-builder.md` (incident severity). The semantic per skill is
different but the visual is consistent across the repo so the same eye scan
works.

- **🔴 Stop-work.** A reasonable competent person walking the photo would
  not let the next hour of work happen at this work face without a control
  applied first. Examples: unprotected leading edge with crew working within
  the fall-distance; trench >5 ft with no protective system and a worker in
  it; energized panel open with bare conductors and an unqualified worker
  within reach; lift radius pinned by an obstacle the operator cannot see;
  combustible material under hot work with no fire watch.
- **🟡 Control-now.** The hazard is real and the control is missing or
  incomplete, but a brief pause to apply the control returns the work face
  to acceptable. Examples: guardrail top rail below 39 in; scaffold
  planking gapped; ladder set at a slope outside 4:1 ± 5°; missing toeboard
  on a multi-level scaffold; a fire extinguisher within reach but expired;
  PPE on but not adjusted (chinstrap unbuckled, harness leg-strap
  unhooked); housekeeping debris in the egress path.
- **🟢 Monitor.** The hazard is below the threshold for an active control
  but is worth flagging: the control in place is correct but is one
  condition-change from being inadequate (wind picking up, an adjacent
  trade arriving, light fading). The crew leader watches this and re-runs
  the PHIT if the condition changes.

A PHIT with all 🟢 rows is suspicious and the skill should say so — most
work faces have at least one 🟡, and a clean-photo PHIT often misses a
real-hazard 🔴 because the eye stopped scanning.

---

## OSHA / Standard Citation Discipline

The PHIT's value collapses if its citations are wrong. The skill has four
hard rules on citations:

1. **Never invent a citation.** If the model is not confident in the
   subpart-and-paragraph, the right answer is the subpart only ("29 CFR
   1926 Subpart M") with a note that the specific paragraph requires a
   verified-citation pass. A made-up citation looks correct and is the
   most damaging failure mode of the skill.
2. **State-plan additions matter.** Federal OSHA is the floor. CA Title 8
   has heat-illness, indoor-heat, and respirable-silica rules tighter than
   federal; WA has its own fall-protection threshold (10 ft for residential
   construction in some classes); OR has its own respirable-silica
   construction rule. If the project state is a state-plan state and the
   hazard is one the state-plan covers more strictly, cite the state
   standard, not the federal floor.
3. **Cite the regulating standard, not the consensus standard, unless the
   consensus standard is incorporated by reference.** ANSI A14.7 ladder
   guidance is useful; the binding citation is 29 CFR 1926.1053. ANSI Z359
   fall-protection guidance is useful; the binding citation is 29 CFR 1926
   Subpart M. NFPA 51B governs hot work because OSHA references it; cite
   both.
4. **Never cite a citation the photo does not support.** If the photo shows
   a guardrail issue, do not cite 1926.501(b)(13) (residential
   construction) for a commercial project. The PHIT's citations have to
   match what is in the frame.

A "competent-person quick-reference" map of the OSHA 1926 subparts most
commonly cited from PHITs:

| Subpart | Title | Common PHIT hazards |
|---|---|---|
| C | General Safety & Health | Housekeeping, illumination, PPE general |
| D | Occupational Health & Environmental Controls | Sanitation, hearing, respiratory |
| E | PPE | Head, eye, hearing, foot, hand |
| F | Fire Protection & Prevention | Extinguishers, hot work, flammable storage |
| G | Signs, Signals, Barricades | Traffic, public protection, MUTCD |
| K | Electrical | Live circuits, GFCI, temp power, panels open |
| L | Scaffolds | Frame / system / rolling tower / aerial lift |
| M | Fall Protection | Edges, holes, roofs, leading edge, anchors |
| N | Cranes & Derricks | Old ref — see CC for current |
| O | Motor Vehicles, Mech. Equip., Marine | Equipment, swing radius, line of fire |
| P | Excavations | Trenches, protective systems, soil class, egress |
| Q | Concrete & Masonry | Forms, shoring, post-tensioned, masonry |
| R | Steel Erection | Multi-employer steel, decking, perimeter cables |
| S | Underground Construction | Tunnels, shafts |
| V | Power Transmission & Distribution | Min approach distance, qualified workers |
| X | Stairways & Ladders | Ladder type, rail, footing, slope |
| AA | Confined Spaces in Construction | PRCS, atmospheric, rescue, attendant |
| CC | Cranes & Derricks in Construction | Current crane standard, signal, qualifications |
| § 1926.62 | Lead | Lead-bearing surfaces, exposure, hygiene |
| § 1926.95–106 | PPE detail | Specific PPE selection |
| § 1926.1101 | Asbestos | Class I-IV, containment |
| § 1926.1153 | Respirable Crystalline Silica | Table 1 method or alternate |
| 29 CFR 1904 | Recording & Reporting | OSHA 300 / 300A / 301 trigger |

This table is intentionally not a citation index — it is a starting point
for the correct subpart so the verified-citation pass can find the right
paragraph.

---

## Out-of-Frame Asks (the Anti-Hallucination Discipline)

A photo shows what is in the frame. The model's worst failure mode is
filling in confident answers about what is *not* in the frame. The PHIT
includes an explicit "out-of-frame ask" column for this reason. Common
asks the model should *always* surface:

- **Adjacent / overhead trade.** The photo shows the work face. Is anything
  scheduled overhead today (steel erection, façade, concrete pump, crane
  pick)? Is anything scheduled on the same level adjacent (welding, paint,
  demolition)?
- **Energy state.** The photo shows a panel face. Is the panel locked out?
  Has zero-energy verification been done in the last hour? Who applied the
  lock?
- **Permit state.** The photo shows hot work, confined-space entry,
  energized work, a lift, or excavation. Is the permit issued? Is the fire
  watch posted? Is the attendant in place?
- **Atmospheric state (for confined-space photos).** What was the last
  reading (O₂, LEL, CO, H₂S)? What time was it taken? Is the meter
  bump-tested?
- **Weather change for the next four hours.** Wind forecast, lightning
  forecast, precipitation forecast, temperature trend. The PHIT was honest
  for the moment of capture; what is the trend?
- **Crew composition.** Who is the competent person on shift for the
  applicable standard (excavation, scaffolding, fall protection, confined
  space, demolition)? Is any apprentice / first-day worker on the crew?
- **Recent near-miss / incident.** Has anything happened on this work face
  in the last 14 days that should be mentioned in the PTP?

Every PHIT has at least one out-of-frame ask. A PHIT without one is a PHIT
that has hallucinated a complete picture from a partial frame.

---

## Common False-Positive Patterns (Over-Calling Compliance)

The model can over-call compliance based on visual cues that look like
controls but are not. The skill should be primed against these specifically:

- **Yellow-vest = compliant.** A high-vis vest is one PPE element; it is
  not the whole PPE picture. Hard-hat condition, eye-pro, hearing-pro,
  task-specific PPE (arc-rated, fire-rated, fall-arrest, cut-resistant
  glove) all matter.
- **Guardrail visible = adequate.** The guardrail might be at the wrong
  height (top rail 42 in ± 3 in; midrail at 21 in), missing toeboard,
  ungated at the access point, or installed past the leading edge. The
  PHIT calls out *what about the guardrail* satisfies the standard.
- **Harness on = tied off.** The lanyard has to be attached to a certified
  anchor *and* the snap-hook has to be locked. A harness with a dangling
  lanyard is not fall-arrest.
- **Caution tape = barricade.** Caution tape marks a hazard; it does not
  arrest a worker. For an actual edge, a top-rail / midrail / toeboard
  guardrail is the control.
- **Fire extinguisher present = hot-work compliant.** Extinguisher type
  (A / B / C / D / K), size, inspection date, and the fire-watch's
  attention all matter.
- **Cones = traffic control.** Cones are a flag, not a barrier. MUTCD
  Part 6 controls govern actual public traffic.

A model that returns "all controls in place" on a hot-work photo because it
sees an extinguisher is failing the discipline. The PHIT names *which*
control is in place and *why* it is adequate.

---

## Common False-Negative Patterns (Missing Real Hazards)

The flip side. The model misses hazards that a competent person reading the
same photo would catch on the second glance:

- **Line-of-fire.** A worker is positioned where a falling object,
  swinging load, recoiling chain, or rolling pipe would strike them.
  Often visible in the frame and easy for the model to under-call.
- **Pinch points.** Between equipment and structure, between two pieces
  of equipment, between material being handled and the body.
- **Slip / trip on the egress path.** The egress path matters more than
  the work face; an injured worker getting *out* of the work area is the
  failure mode.
- **Energized panel cover removed.** The cover is not in the frame; the
  open face is. The PHIT should ask *where is the cover* and *who removed
  it*.
- **Tag missing from scaffold / aerial / crane.** A scaffold without a
  legible tag is a stop-work; a missing tag is a missed hazard.
- **Combustibles within hot-work radius.** 35 ft per NFPA 51B (or the
  permit's specific radius). Cardboard, plastic, sawdust, aerosol cans
  inside that radius is a 🔴 every time.
- **Crew on a leading-edge with no anchor visible.** The harness is on
  but the anchor is not in frame — that is a 🔴 *out-of-frame ask*, not a
  green light.

The PHIT's value is in catching these, not in re-confirming the obvious.

---

## Multi-Photo PHIT (Series, Walks, Stand-Downs)

When several photos are submitted together (a supervisor walk, a stand-down
walkthrough, a pre-pour readiness review), the PHIT is run once per photo
and a roll-up summary is added at the top. The roll-up has three lines:

- **Total rows:** by severity (🔴 *n* / 🟡 *n* / 🟢 *n*)
- **Recurring hazards:** any hazard appearing in ≥2 photos (pattern signal)
- **Walk disposition:** stop-work / control-now-and-resume / monitor

A recurring 🟡 across several photos is often a 🔴 in disguise — the same
control gap is repeated, which usually means a competent-person walk is
needed at the project level, not just at the work-face level.

---

## Integration with PTP and Toolbox Talk

The PHIT does not replace the PTP. It feeds it. The cleanest workflow:

1. **Morning, before huddle.** Crew leader takes one to three photos of
   the day's work face. Runs the PHIT.
2. **Huddle.** PHIT is read at the huddle. Each 🔴 is dispositioned before
   work starts. Each 🟡 has a control-apply-then-resume plan. Each 🟢 has a
   monitor-trigger.
3. **PTP issuance.** The PTP (output of `pre-task-plan-drafter.md`)
   incorporates the open dispositions from the PHIT. The PTP carries the
   "near-miss / corrective-action callout" — the PHIT carries the
   *current-condition* callout.
4. **Toolbox-talk feedback.** The most-recurring 🟡 hazard from the prior
   week's PHITs becomes the next week's toolbox-talk topic (sub-mode in
   `safety-plan-builder.md`).
5. **Post-incident scene.** After any near-miss or recordable, the scene
   PHIT is run as part of the investigation packet — the photo is timed,
   geotagged, and attached to the OSHA 301 / company incident report.

When the workflow runs, the PHIT becomes an honest input to the day's
safety conversation. When it does not, the PHIT becomes a paperwork artifact
that no one reads. The discipline is in the workflow, not in the table.

---

## Ten Hard Rules

1. **No PHIT on a bad photo.** Reject and ask for the retake.
2. **Every row has a verified OSHA / standard citation, or it doesn't ship.**
3. **Severity drives the eye.** 🔴 first, 🟡 next, 🟢 last.
4. **Every PHIT has at least one out-of-frame ask.**
5. **No "control in place" without naming *which* control.**
6. **No invented citations.** Subpart-only is better than a wrong paragraph.
7. **State-plan rules supersede federal where stricter.**
8. **A PHIT with all 🟢 rows on a real work face is suspect.** Re-scan.
9. **Recurring 🟡 across a multi-photo walk is a 🔴 in disguise.**
10. **The AI surfaces, the people decide.** The competent person on shift
    is the one who closes the disposition.

---

## Defensibility Self-Check (Skill-Side)

Any skill producing or reviewing a PHIT runs the same self-check before
returning the table:

- [ ] Photo passed the quality check (resolution, subject, occlusion,
      lighting, not staged)
- [ ] Every row has a hazard, citation, severity, engineering control,
      administrative control, PPE, disposition, and out-of-frame ask
- [ ] Citations verified against the actual standard (no inventions; no
      wrong paragraphs)
- [ ] State-plan rules applied if project state is a state-plan state and
      the hazard is one the state-plan covers more strictly
- [ ] Severity calibrated (🔴 reserved for stop-work; 🟡 for control-now;
      🟢 for monitor)
- [ ] At least one out-of-frame ask per row
- [ ] No false-positive compliance call (yellow-vest = compliant; rail
      visible = adequate; harness on = tied off; etc.)
- [ ] No false-negative pattern unchecked (line-of-fire; pinch; egress
      slip; cover off; combustibles in hot-work radius)
- [ ] Roll-up summary present if multi-photo
- [ ] PTP / toolbox-talk integration noted where relevant

A "no" on any line is a hold; the PHIT does not ship until the box is
checked or the gap is flagged in the output.

---

## What This Reference Does *Not* Cover

- **Computer-vision model training.** The discipline above applies to the
  prompt-and-output side. The model side (training data, label schema,
  IoU / mAP metrics, edge-vs-cloud inference) is platform engineering.
- **Real-time CCTV / drone / wearable feeds.** Continuous-monitoring
  systems (Smartvid.io / OpenSpace Capture / Doxel / Track3D) operate on a
  different shape (alerts, not tables). The PHIT shape is for a
  point-in-time photo, not a stream.
- **Incident root-cause analysis.** A scene PHIT is an *input* to the
  investigation; the 5-Why / fishbone / TapRooT analysis is downstream.
- **Insurance / claims documentation.** The PHIT is operational; the
  carrier-required claim photo is a separate, higher-burden artifact
  (chain-of-custody, multiple angles, scale reference).
- **Specific vendor implementations.** Procore Safety, Autodesk Forma,
  HammerTech Intelligence, BuildPass, Field1st, Oracle Advisor for Safety,
  Turner SafeT Coach, and any other tool ships in this space all have
  their own UI, prompt patterns, and model behavior. The PHIT shape above
  is the platform-neutral target a *reviewer-of-platform-AI-output*
  sub-mode can validate against. Cite the vendor when reviewing the
  vendor's output.

---

## Cross-Skill Coordination

The PHIT discipline is referenced by the following skills:

| Skill | How it uses the reference |
|---|---|
| `operations/safety-plan-builder.md` | Toolbox-talk sub-mode pulls recurring 🟡 hazards from prior-week PHITs; SSSP cross-references the daily PHIT cadence as the implementation discipline |
| `operations/pre-task-plan-drafter.md` | PTP incorporates open PHIT dispositions; the day's stop-work triggers are calibrated to the morning PHIT's 🔴 / 🟡 rows |
| `operations/daily-log-generator.md` | The day's PHIT roll-up (severity counts) lands in the safety section of the daily log; recurring patterns get flagged as a multi-day signal |
| `operations/project-qa-assistant.md` | Reviewer-mode for a contractor or sub asking "what hazards did the platform miss in this photo" runs the PHIT discipline as the platform-neutral validator |
| `admin/closeout-documentation-auditor.md` | Project-closeout safety packet includes the recurring-hazard pattern from the project's PHIT history |
| `_shared/meeting-summarizer.md` | OAC / safety-stand-down minutes reference the week's PHIT roll-up where relevant |

---

## Sources

- OSHA 29 CFR 1926 (Construction) and 29 CFR 1904 (Recording & Reporting),
  cited by subpart and section above; the PHIT cites these as the binding
  standards for the hazards visible in any given photo.
- OSHA-approved state plans (CA Title 8, WA L&I, OR OSHA, MI MIOSHA, KY
  KOSH, NC OSHA, MD MOSH, VA VOSH, IN IOSHA, IA OSHA, NM OHSB, AZ ADOSH,
  NV OSHA, NJ public sector, NY public sector, AK AKOSH, WY OSHA, HI HIOSH,
  MN MNOSHA, SC OSHA, TN TOSHA, UT UOSH, VT VOSHA, PR OSHO) — referenced
  for the state-plan-additions discipline.
- NFPA 51B (Hot Work) and NFPA 70E (Electrical Safety in the Workplace) —
  consensus standards incorporated into OSHA enforcement for the relevant
  hazards.
- ANSI A10 / A14 / Z359 series — referenced as practitioner guidance,
  cited only when the federal or state standard incorporates them.
- MUTCD Part 6 — referenced for traffic-control PHIT rows that touch
  public-way work.
- AGC and ENR practitioner literature on safety-week stand-downs and on
  multi-photo walk-down reviews — consulted for the multi-photo roll-up
  shape; not reproduced.
- Construction Safety Week 2026 (May 4–8, "All In Together: Recognize.
  Respond. Respect.") — context for the industry release of free
  photo-hazard tooling that catalyzed this reference's creation.

This reference cites the standards above as the binding sources and the
practitioner literature as background; no copyrighted material is
reproduced.
