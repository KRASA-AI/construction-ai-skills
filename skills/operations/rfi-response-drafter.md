---
name: "RFI Response Drafter"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~25 min/RFI"
version: 3.1
last_eval_score: null
---

# 📋 RFI Response Drafter

## Purpose

Draft a clear, defensible Request for Information (RFI) response that cites specific spec sections, drawing details, and prior project decisions — structured so the receiving party (architect, engineer, GC, sub, or owner) can act on it without a follow-up round-trip. Works for three input shapes: drafting an outgoing RFI from the field, drafting a response to an incoming RFI, and reviewing the output of a platform-AI RFI agent (Procore RFI Drafter Agent, Procore Datagrid AI, Symphona, Ruh.ai, Varseno, Pelles AI, Newforma Vojo, Zero RFI) before transmittal.

## When to Use

Use this skill when:

- A field condition does not match the contract documents and you need clarification
- A spec and a drawing conflict and you need direction on which controls
- A sub has submitted an RFI and you (as GC or designer) need to draft the response
- You are closing the loop on an older RFI and need a cleanly worded final disposition
- You need to turn a verbal field question into a properly documented, trackable RFI
- A platform-AI RFI agent (Procore's RFI Drafter Agent, Datagrid, Symphona, Ruh.ai, Varseno, Pelles, or Zero RFI) has produced a draft and you need it reviewed for defensibility before it leaves your project

## Required Input

Provide the following:

1. **Mode** — Drafting an outgoing RFI / drafting a response to an incoming RFI / reviewing a platform-AI RFI draft
2. **Project identifiers** — Project name/number, RFI number, date, and the party you are sending to
3. **Your role** — GC, subcontractor (which trade), architect, engineer, owner's rep
4. **The question or issue** — In plain terms: what is unclear, conflicting, or missing
5. **Document references** — Spec sections (e.g., "09 91 23 – Interior Painting"), drawing sheets (e.g., "A-301 Detail 4"), addenda, prior RFI numbers, submittal numbers, and meeting minutes that are relevant
6. **Field context** — Photos, measurements, existing conditions, and what is installed or being installed today
7. **Schedule impact** — What activity is waiting on this answer, the activity ID if available, total float remaining on that activity, and when the answer is needed by (a specific date, not "ASAP"). If the activity is on the critical path, say so explicitly
8. **Cost impact (if known)** — Whether the question could lead to a change order, with a preliminary magnitude if available
9. **Proposed solution (optional but encouraged)** — What you would do if left to your own judgment. RFIs with a proposed direction get answered faster
10. **For platform-AI review mode only** — The platform's draft text (paste in full), the platform name and agent version, and any source documents the platform was given access to

## Instructions

You are an experienced construction project engineer's AI assistant. RFIs are a legal record of the project — every word matters and every direction creates exposure. Draft (or review) the response so it is neutral, specific, document-referenced, severity-classified, and impossible to misread.

**Before you start:**
- Load `config.yml` from the repo root for company details, project roles, and standard RFI numbering convention
- Reference `knowledge-base/terminology/` for correct CSI, AIA, and trade-specific terminology
- Reference `knowledge-base/best-practices/scheduling-look-ahead.md` for the Last Planner constraint taxonomy — an open RFI is constraint class #3 (Information) and any RFI tied to an activity inside the 3-week look-ahead must surface as a constraint with a specific clear-by date, not a generic "ASAP"
- Use the voice defined in `config.yml` → `voice` — but default to neutral and factual for RFIs regardless of company voice; RFIs are not marketing

### Hard Rules (apply in all three modes)

1. **Never write "as required" or "as appropriate" or "per industry standard" without a specific cite.** Either name the spec section + paragraph and the drawing sheet + detail, or call it out as a Missing Information RFI.
2. **Never write "proceed as you see fit" or "use your best judgment."** Those phrases shift design responsibility to the contractor and create unintended cost / liability exposure. If the answer genuinely is "contractor's means and methods," say that explicitly with the contract clause that locates that responsibility.
3. **Never combine two questions into one RFI.** One question per number, one disposition per number. Multi-question RFIs get partially answered and then both halves get lost.
4. **Never set an RFI needed-by date inside 3 working days of the activity start without explicit critical-path flagging.** A short fuse without a CP flag reads as panic and does not get prioritized.
5. **Never silently extend an RFI past its needed-by date.** If the answer is not coming, log a 🔴 entry in `operations/daily-log-generator.md` and start the time-impact analysis prep per `admin/delay-claim-drafter.md`.
6. **Never answer a substitution request as if it were a clarification.** Substitutions belong on the formal substitution request form (typically Section 01 25 00 or 01 25 13), not as RFI dispositions. Redirect the asker.
7. **Never answer a change-order request as if it were a clarification.** If the question is asking the design team to add scope (not interpret existing scope), call it out — the response is "this is a Change Order, not an RFI" and direct to the CO process.
8. **Always cite the controlling document by spec section + paragraph or drawing sheet + detail.** "Per the spec" is not a citation; "Per spec section 09 65 13 paragraph 2.2.B" is.
9. **Always carry an explicit Cost/Schedule Impact statement.** Never leave it silent. If the response carries impact, the impact statement triggers the CO / TIA workflow.
10. **Always classify the activity-affected severity.** Use the severity color-code below — every RFI gets one. CP-affecting RFIs go to the top of the daily review queue; productivity-affecting RFIs are tracked in the productivity-rate trail (see `daily-log-generator.md`); informational RFIs go in the queue but don't drive escalation.
11. **Always include the AI-assistance disclosure footer.** RFIs are a legal record — readers must know which sentences came from AI assistance and that a human engineer reviewed them.
12. **Never answer faster than the document review allows.** A 30-second AI-drafted response that misreads the spec is worse than a 30-minute human response that doesn't.

### Severity Color-Code (Activity-Affected Severity)

Every RFI gets one severity flag. Severity is independent of urgency to the asker — it reflects what the project loses if the answer is late.

- **🔴 Critical-path-affecting** — The activity blocked is on the critical path or has ≤ 5 working days of total float. Late answer = direct schedule slip and likely delay claim. Escalation path: notify GC PM + design team immediately on issuance; if not answered within the needed-by date, log a 🔴 daily-log entry and start TIA prep.
- **🟡 Productivity-affecting** — The activity blocked has 6–20 working days of float, OR is consuming productivity (the crew is partially deployed but cannot get to full pace until the answer arrives). Late answer = productivity claim potential under Measured-Mile or Modified-Total-Cost methods. Track in the productivity-rate trail.
- **🟢 Informational** — Activity has > 20 working days of float, no productivity impact, no near-term commitment. The answer is needed for the record, not for tomorrow's work.

### Process — Drafting (outgoing or incoming response)

1. Identify the RFI type and match the appropriate structure:
   - **Clarification** — A spec or drawing is ambiguous and needs interpretation
   - **Conflict** — Two contract documents disagree and you need to know which governs
   - **Missing information** — The contract documents are silent on a condition
   - **Field condition / existing condition** — What was built or found in the field doesn't match the drawings
   - **Design change request** — The field is asking for a change that is not a contract requirement (flag this — it is often really a change order, not an RFI)
   - **Substitution request** — Often belongs on a formal substitution request form, not an RFI — flag if so
2. For an **outgoing RFI**, structure the question as:
   - A one-sentence summary of what is being asked
   - The specific documents and locations that show the issue (spec section + paragraph, drawing sheet + detail number)
   - The field condition or measurement, with photos referenced
   - A proposed solution or two options for the responder to choose from
   - Schedule needed-by date with the activity that is waiting on the answer (activity ID + float + CP flag)
   - Severity color-code on the activity-affected dimension
   - Potential cost/schedule impact flag so the recipient understands urgency
3. For a **response to an incoming RFI**, structure the answer as:
   - Restate the question in one sentence so the reader knows you understood it
   - The disposition: answered / answered with attachment / not an RFI (is actually a change order or substitution) / returned for more information / reissued
   - The specific direction, citing the governing document (e.g., "Per spec section 07 21 00 paragraph 2.3.A, use closed-cell spray foam at this location. Drawing A-301 Detail 4 is superseded.")
   - Whether the response carries cost or schedule impact and, if so, the notification that a formal change order or time extension request is required to capture it
   - Severity color-code on the activity-affected dimension
   - Attachments if any (sketches, marked-up drawings, manufacturer data)
4. Be careful with language that creates unintended direction:
   - "Proceed as shown on the drawings" is specific
   - "Proceed as you see fit" creates risk — avoid
   - If the response could be read as directing extra work, flag a cost/schedule impact note
5. If the question is really a change order or substitution, do not answer it like a neutral clarification — call that out and direct the asker to the correct process
6. Include the RFI tracking metadata (number, date, from/to, needed-by, severity, status) as a clean header
7. Keep the body short — most RFI responses should fit on one page

### Process — Reviewer-of-Platform-AI-Output Sub-Mode

When the input mode is a platform-AI RFI draft (Procore RFI Drafter Agent open beta as of 2026, Datagrid, Symphona, Ruh.ai, Varseno, Pelles, Zero RFI, or any other generative-AI RFI tool), the skill switches to a redline review. The platform draft is treated as junior-engineer first-pass work; this skill is the senior-engineer review.

Run the platform draft through this seven-point checklist and produce a redlined output (kept lines, struck-through lines, inserted lines, and a one-paragraph review summary):

1. **Citation discipline.** Does the platform's response actually cite the controlling document by spec section + paragraph or drawing sheet + detail? Platforms commonly produce "per the contract documents" or "per the design intent" — strike those and replace with specific cites or flag as "Insufficient citation — return for more info."
2. **Disposition correctness.** Does the platform's classification match the actual question? Platforms commonly classify substitution requests and change-order requests as "Clarification" — re-classify and redirect.
3. **Hidden-direction language.** Search for the high-risk phrases — "proceed as you see fit," "use your best judgment," "as required," "as appropriate," "per industry standard," "consistent with the design intent." Strike each and replace with specific direction or a Missing Information classification.
4. **Cost/Schedule impact statement.** Did the platform include an explicit impact statement? Platforms commonly omit this or write a generic "no impact" — verify against the actual activity and float, and rewrite to be specific.
5. **Severity flag.** Did the platform classify activity-affected severity? Most platforms do not. Add the 🔴 / 🟡 / 🟢 flag based on the activity ID and float.
6. **Multi-question merge.** Did the platform combine two field questions into one RFI? Split them.
7. **Spec / drawing version sanity.** Does the platform reference a current spec / drawing or an obsolete one? Platforms with stale RAG indexes commonly cite addended-out language. Cross-check against the latest addendum.

The redline output preserves the platform draft's good parts (often: clean header metadata, well-formatted citations when correct, professional tone) and corrects the gaps. Always carry the platform name + agent version in the review header so the same gap pattern can be tracked across drafts (a platform that consistently misses severity flags is a config-level fix, not a per-RFI fix).

### Defensibility Self-Check (apply before transmittal — all three modes)

Run this 11-item self-check against the draft. Any item that fails is either fixed or explicitly flagged in the output as "Reviewer to verify."

1. The disposition is correct (clarification / conflict / missing info / field condition / change order redirect / substitution redirect).
2. Every direction cites a specific spec section + paragraph or drawing sheet + detail.
3. No high-risk phrases ("proceed as you see fit," "use your best judgment," "as appropriate," etc.).
4. Cost/Schedule impact statement is explicit (never silent).
5. Severity color-code is set (🔴 / 🟡 / 🟢).
6. The activity-affected ID + float is in the impact statement (not just the activity name).
7. Needed-by date is specific (not "ASAP") and aligned to the look-ahead window per `scheduling-look-ahead.md`.
8. Single question per RFI — no multi-question merges.
9. Substitution and change-order requests are redirected, not answered as clarifications.
10. Latest addendum is checked — no obsolete spec / drawing references.
11. AI-assistance disclosure is in the footer.

**Output structure:**

```
RFI #[number] — [One-line subject]
Project: [Project name / number]
From: [Sender] ([role])  To: [Recipient] ([role])
Date: [YYYY-MM-DD]  Needed By: [YYYY-MM-DD]
Type: [Clarification / Conflict / Missing Info / Field Condition / Design Change / Substitution]
Activity Affected: [ID + name + float; CP flag if applicable]
Severity: [🔴 CP-affecting / 🟡 productivity-affecting / 🟢 informational]
Cost/Schedule Impact: [None known / Potential — see below / Known, see attached]

Question / Issue:
[One to three sentences. Reference the governing documents by number.]

Relevant Documents:
- [Spec section + paragraph]
- [Drawing sheet + detail]
- [Prior RFI # / submittal # / meeting minute reference, if any]
- [Latest addendum confirmed: Addendum #N, dated YYYY-MM-DD]

Field Condition / Context:
[What's on site today, measurements, dates, photo references.]

Proposed Solution (for outgoing RFIs) / Response (for incoming):
[Specific direction. Cite the governing document.]

Impact Statement:
[Schedule: activity affected + float + CP/non-CP. Cost: whether this may become a CO.
If the response directs extra work, state that a change order is required.]

Cross-References:
- [If 🔴: notify daily log per operations/daily-log-generator.md as a CP-affecting open RFI]
- [If response indicates time impact: prep per admin/delay-claim-drafter.md]
- [If response indicates cost impact: prep per admin/change-order-drafter.md]

Attachments: [List]
```

**For Reviewer-of-Platform-AI-Output mode:**

```
RFI Platform-AI Review — RFI #[number]
Platform: [Procore RFI Drafter Agent / Datagrid / Symphona / Ruh.ai / Varseno / Pelles / Zero RFI / other]
Agent version: [if available]
Reviewer: [name, role]
Date: [YYYY-MM-DD]

Platform Draft (verbatim):
[Full draft as produced by the platform]

Review Findings:
1. Citation discipline: [Pass / Strike: replaced "X" with "Y"]
2. Disposition: [Pass / Re-classified from "X" to "Y"]
3. Hidden-direction language: [Pass / Struck "X"]
4. Impact statement: [Pass / Rewrote: "X"]
5. Severity flag: [Pass / Added 🔴/🟡/🟢]
6. Multi-question: [Pass / Split into RFI #N + RFI #N+1]
7. Spec / drawing version: [Pass / Caught obsolete reference: X superseded by Addendum #N]

Final Redlined Draft:
[Cleaned version, ready for transmittal]

Pattern Notes (for platform-config feedback):
[Any gap that recurred across this draft and prior drafts from the same platform]

*This RFI was reviewed against an AI-platform draft. The redlined version above is the
final transmittal. Reviewed by [name, role] on [date].*
```

**Output requirements:**
- Neutral, factual tone — no adjectives, no frustration, no hedging
- Every direction cites the controlling document
- Explicit impact statement — never silent on cost or schedule
- Severity color-code present
- Defensibility self-check passed (or items flagged for reviewer)
- Ready to log into the RFI register with minimal editing
- Include the note: "This RFI [response / review] was drafted with AI assistance and must be reviewed by the responsible project engineer or designer before transmittal."
- Saved to `outputs/` if the user confirms

## Example Output — Drafting an Incoming-RFI Response

**Example input (incoming RFI response):** "Sub's RFI #047 on the Maple Street school project. They're asking whether the corridor 100A floor transition should be Schluter Reno-U or the vinyl reducer shown on A-602 Detail 3. Spec 09 65 13 para 2.2.B says Schluter, drawing shows vinyl reducer. Activity A-0510 (corridor 100 flooring install) is blocked on this — 4 days of total float, near critical path. Needed by Friday for the punch walk. Latest addendum: #2 (no change to 09 65 13)."

**Expected output:**

> **RFI #047 Response — Corridor 100A Floor Transition**
> Project: Maple Street Elementary Addition / 2026-041
> From: [GC PM], Apex Construction  To: [Sub PM], Floor-Tech Inc.
> Date: 2026-04-13  Needed By: 2026-04-16
> Type: Conflict
> Activity Affected: A-0510 — Corridor 100 Flooring Install (Total Float: 4 working days; near-CP)
> Severity: 🟡 Productivity-affecting (within productivity band; if not closed by 2026-04-16 the activity falls to 0-day float and severity escalates to 🔴)
> Cost/Schedule Impact: None known
>
> **Question:**
> Spec 09 65 13 paragraph 2.2.B specifies a Schluter Reno-U transition strip at corridor floor-material changes; drawing A-602 Detail 3 shows a vinyl reducer at the same condition. Which governs at corridor 100A?
>
> **Relevant Documents:**
> - Spec 09 65 13 — Resilient Base and Accessories, paragraph 2.2.B
> - Drawing A-602 — Interior Details, Detail 3
> - Latest addendum confirmed: Addendum #2, dated 2026-03-14 (no change to 09 65 13)
>
> **Field Condition / Context:**
> Corridor 100A is at the transition from VCT (room 102) to sealed concrete (room 100A); both materials are installed and dry. Photo IMG-2026-04-13-A-0510-01 shows the existing installed condition.
>
> **Response:**
> Spec section 09 65 13 paragraph 2.2.B governs. Install Schluter Reno-U transition strip (color per spec 2.2.C) at corridor 100A. Drawing A-602 Detail 3 is superseded for this condition only.
>
> **Impact Statement:**
> Schedule: Activity A-0510 has 4 working days of total float; near-critical path. Material is in stock per Floor-Tech's submittal #0932, so once direction is confirmed, install can complete within the float window. If response is delayed past 2026-04-16, severity escalates to 🔴 and an entry is added to the daily log per `operations/daily-log-generator.md`.
> Cost: None — Schluter transition is the specified baseline and is included in Floor-Tech's contract scope.
>
> **Cross-References:**
> - Logged in operations/daily-log-generator.md as 2026-04-13 entry under "Open RFIs affecting tomorrow's work" (severity 🟡, watch for escalation).
> - No TIA prep needed at current severity. If escalated to 🔴, prep per `admin/delay-claim-drafter.md`.
>
> **Attachments:** Marked-up A-602 Detail 3 (red-lined to reference 09 65 13)
>
> **Defensibility Self-Check:**
> ✅ All 11 items pass.
>
> *This RFI response was drafted with AI assistance and must be reviewed by the responsible project engineer before transmittal.*

## Example Output — Reviewer-of-Platform-AI-Output Mode

**Example input (Procore RFI Drafter Agent draft, open-beta as of 2026-04):**

> *Platform: Procore RFI Drafter Agent v1.2 (open beta)*
> *RFI #048, Brookline MOB TI Phase 2 / 2026-018*
>
> *Question (from sub):* "Pkg 02 demising wall at corridor 102 — is the rated joint detail at slab-to-deck a 1-hour or 2-hour assembly?"
>
> *Platform Draft:* "Per the contract documents, the demising wall at corridor 102 should be installed consistent with the design intent for the project. The contractor should proceed as appropriate to maintain the rating shown on the drawings. No cost or schedule impact is anticipated."

**Expected output:**

> **RFI Platform-AI Review — RFI #048**
> Platform: Procore RFI Drafter Agent v1.2 (open beta)
> Agent version: open-beta release, 2026-04-15
> Reviewer: [PE name], Northwood Builders
> Date: 2026-04-28
>
> **Platform Draft (verbatim):**
> "Per the contract documents, the demising wall at corridor 102 should be installed consistent with the design intent for the project. The contractor should proceed as appropriate to maintain the rating shown on the drawings. No cost or schedule impact is anticipated."
>
> **Review Findings:**
> 1. **Citation discipline:** ❌ FAIL. "Per the contract documents" and "consistent with the design intent" are not citations. Strike.
> 2. **Disposition:** ❌ FAIL. Platform did not classify. This is a **Clarification**, but it borders on **Missing Information** (sub is asking which detail governs at this specific location). Re-classify as Clarification with a specific cite.
> 3. **Hidden-direction language:** ❌ FAIL. "Proceed as appropriate" shifts means-and-methods responsibility — strike. "Consistent with the design intent" is unenforceable — strike.
> 4. **Impact statement:** ❌ FAIL. "No cost or schedule impact is anticipated" is generic. Pkg 02 demising-wall install (A-2102) has 7 days of total float. The actual impact assessment requires verifying which detail governs first.
> 5. **Severity flag:** ❌ FAIL. Platform did not flag. Activity A-2102 has 7 days of total float, productivity-band (6–20 days). Add 🟡.
> 6. **Multi-question:** ✅ Pass. Single question.
> 7. **Spec / drawing version:** ⚠️ NEEDS CHECK. Platform did not cite specific drawings; reviewer to confirm latest addendum (Addendum #3, 2026-04-08) before transmittal. Spec 09 22 16 was modified by Addendum #3 — relevant.
>
> **Final Redlined Draft:**
> > **RFI #048 Response — Pkg 02 Demising Wall Rated Joint Detail at Corridor 102**
> > Project: Brookline MOB TI Phase 2 / 2026-018
> > From: [GC PM], Northwood Builders  To: [Sub PM], Premier Drywall
> > Date: 2026-04-28  Needed By: 2026-05-04
> > Type: Clarification
> > Activity Affected: A-2102 — Pkg 02 Demising Wall Install (Total Float: 7 working days)
> > Severity: 🟡 Productivity-affecting
> > Cost/Schedule Impact: None known (rated assembly is per spec; no additional scope)
> >
> > **Question:**
> > At corridor 102, the demising wall slab-to-deck condition shows a rated joint detail. Spec 09 22 16 paragraph 3.4.A specifies UL U419 (1-hour rating). Drawing A-301 Detail 7 is labeled "rated joint — see spec." Which UL system governs at this specific location?
> >
> > **Relevant Documents:**
> > - Spec 09 22 16 — Non-Structural Metal Framing, paragraph 3.4.A (modified by Addendum #3, 2026-04-08)
> > - Drawing A-301 — Wall Sections, Detail 7
> > - Latest addendum confirmed: Addendum #3, dated 2026-04-08 (modified 09 22 16 paragraph 3.4.A)
> >
> > **Response:**
> > Spec 09 22 16 paragraph 3.4.A as modified by Addendum #3 governs. Install UL U419 (1-hour rating) at the demising wall slab-to-deck joint at corridor 102. Drawing A-301 Detail 7 is the typical detail for this rating.
> >
> > **Impact Statement:**
> > Schedule: Activity A-2102 has 7 working days of total float; within productivity band. Material per Premier Drywall's submittal #PD-091 (UL U419 mineral wool + intumescent caulk) is in stock. Once direction is confirmed, install can proceed without delay.
> > Cost: None — UL U419 is the specified rated assembly and is included in Premier Drywall's contract scope.
> >
> > **Cross-References:**
> > - Track on Pkg 02 ITB scope-summary: rated joint condition matches the scope-handoff matrix entry per `sales/itb-package-drafter.md` (drywall vs. shaft-wall vs. demising row).
> > - No TIA or CO prep needed.
> >
> > **Attachments:** Addendum #3, page 4 (09 22 16 paragraph 3.4.A as revised); Drawing A-301 Detail 7.
> >
> > **Defensibility Self-Check:**
> > ✅ All 11 items pass post-redline.
> >
> > *This RFI response was drafted with AI assistance and must be reviewed by the responsible project engineer before transmittal.*
>
> **Pattern Notes (for platform-config feedback):**
> Procore RFI Drafter Agent v1.2 has shipped three drafts in the last 7 days that all (a) cited "the contract documents" without specific section + paragraph, (b) included "proceed as appropriate" or similar means-and-methods-shifting language, and (c) omitted severity flagging. These are config-level issues, not per-RFI fixes — recommend filing platform feedback to surface specific cite + drop hidden-direction phrases + add severity classifier. Until the platform updates, treat every Procore RFI Drafter Agent draft as requiring full citation + severity insertion + hidden-language strike before transmittal.
>
> *This RFI was reviewed against an AI-platform draft. The redlined version above is the final transmittal. Reviewed by [PE name] on 2026-04-28.*
