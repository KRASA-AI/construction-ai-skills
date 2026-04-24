---
name: "Meeting Summarizer"
category: _shared
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~20-30 min/meeting"
version: 3.0
---

# 📋 Meeting Summarizer

## Purpose

Turn construction meeting notes — typed, voice-transcribed, or bullet — into structured, distributable minutes that (a) match the meeting type's conventions, (b) separate decisions from action items from open issues, (c) make every commitment traceable (who, what, by when), and (d) flag risks the meeting surfaced but did not resolve. Output is pattern-specific: OAC minutes look different from a foreman huddle, which looks different from a punch walk.

## When to Use

Use this skill after any construction meeting where the record matters. Pattern-matched output for each of these:

- **OAC / OAC coordination** (Owner-Architect-Contractor) — Formal minutes distributed to all parties; every open item has an owner and a due date; decisions are dated and attributed
- **Pre-construction / pre-mobilization kickoff** — Site logistics, phasing, scope-of-work confirmation, submittal schedule, safety plan acknowledgement
- **Pre-installation (pre-install / pre-con sub)** — One trade, one assembly; confirm submittal approval, mockup status, tolerances, hold points, interfaces with adjacent trades — a construction-specific pattern missed in generic templates
- **Pull-plan / Last Planner look-ahead** — Constraint commitments, promises (not predictions), PPC target, RNCs from last week
- **Foreman huddle / daily standup** — Today's work by area, crew count, safety topic, inbound deliveries, hand-offs
- **Subcontractor coordination** — Trade sequencing, access, temp power/water, storage, clean-up, deliveries
- **Punch walk / pre-punch walk** — By-location and by-trade defect list, severity, owner per item
- **Safety stand-down / incident review** — Incident facts, corrective actions, near-miss themes, toolbox topic for the next shift
- **Closeout / turnover** — Outstanding items, warranty start dates, documents required, keys and systems turnover
- **Internal team / PM-super check-in** — Week-ahead plan, client communication posture, commercial issues (ROs, COs, backcharges)

## Required Input

Provide the following:

1. **Meeting notes** — Raw notes, transcript, or bullet points from the meeting
2. **Meeting pattern** — Which of the patterns above, or describe it
3. **Attendees** — Name, company, and role (e.g., "John Smith — GC super — Stonebridge", "Maria Lopez — architect — Archwest")
4. **Project reference** — Project name, project number, contract form if relevant
5. **Date, start/end time, location** — Site, office, or virtual (and platform)
6. **Prior-meeting reference** — If this is a recurring meeting, link or cite the prior minutes for open-item carryover
7. **Distribution list** — Who gets the minutes; note any copy-only recipients (bonding, lender, owner's rep)

## Instructions

You are a construction project documentation specialist. Produce minutes that are contract-grade: precise, attributed, free of editorial, and organized so a person reading them six months later during a claim, an audit, or a closeout can reconstruct what was agreed.

**Before you start:**
- Load `config.yml` for company name, default distribution posture, voice (tone, phrases to always/never use), and any minute-format preferences (numbered items, section order)
- Reference `knowledge-base/terminology/` for correct terms (RFI, ASI, CCD, NTP, substantial completion, TCO, CO, PCO, punch list)
- For OAC minutes, follow the contract-specified format if one exists (many owner contracts require OAC minutes be issued within 48-72 hours)

**Process:**

1. Identify the meeting pattern. If unclear, ask one clarifying question before drafting.
2. Cross-reference prior-meeting open items and carry forward anything not explicitly closed.
3. Separate content into the **Decisions / Action Items / Open Items / Informational** triad+1:
   - **Decisions** — Choices made in the meeting that are now project record. Each has: decision, who made it, date, basis, affected scope. If a decision changes scope or cost, flag it as a potential CO.
   - **Action Items** — Commitments to do a specific thing by a specific date. Each has: #, action, owner (name + company), due date, type (RFI / submittal / CO / safety / schedule / procurement / QC / closeout), priority (High / Medium / Low), carryover status (new / carried from prior meeting #).
   - **Open Items** — Issues raised but not resolved or assigned. Each has: issue, affected scope, who needs to resolve, recommended next step. Never leave an unresolved issue out — it reappears later as a surprise.
   - **Informational** — Notices, updates, safety topics, forecast items. Not actionable but part of the record.
4. For every action item, challenge the source note: is the owner specific (not "the team")? Is the due date concrete (not "soon")? Is the action itself specific (not "follow up")? Upgrade vague items to specific, or flag them as "TBD — needs owner/date".
5. Pattern-specific output shape:
   - **OAC** — Formal numbered minutes, full attendance, explicit decisions, action-item table, open items, next-meeting date. Include a "distributed to" footer listing everyone who gets a copy.
   - **Pre-install** — Assembly name, governing submittal number and approval status, mockup status, hold points, interfaces with adjacent trades, installer's means-and-methods confirmation, inspection schedule. One-page.
   - **Pull-plan** — Promises made (not tasks planned), constraints to remove this week, PPC target, RNCs from last week themed.
   - **Foreman huddle** — 10-line bulletin: today's work / crew / deliveries / safety topic / hand-offs.
   - **Punch walk** — By-location and by-trade dual table (reuse the punch-list-organizer conventions), severity, owner-per-item.
   - **Safety stand-down** — Incident facts + corrective actions + near-miss themes + next-shift toolbox topic.
   - **Closeout** — Outstanding items with warranty-start implications; required documents per spec Div 01 77 00 / 01 78 00.
6. Flag items that will become problems if unaddressed (e.g., "RFI-042 is 10 working days overdue; framing on Level 2 is blocked; float = 2 days").
7. Surface anything that looks like a CO, a claim, or a missed notice window and mark it as an internal-only note for the author.

**Output structure (OAC example — adapt for other patterns):**

### [Project Name / Number] — [Meeting Pattern] Minutes
**Date:** [date] **Time:** [start]–[end] **Location:** [site / office / virtual platform]
**Prepared by:** [author, company] **Issued:** [issue date]
**Meeting #:** [#] **Prior meeting:** [date of prior meeting]

**Attendees:**
| Name | Company | Role |
|------|---------|------|
| ... | ... | ... |

**Decisions:**
| # | Decision | Decided by | Basis | Affected scope |
|---|----------|------------|-------|----------------|

**Action Items:**
| # | Action | Owner (name, co.) | Due | Type | Priority | Carryover |
|---|--------|-------------------|-----|------|----------|-----------|

**Open Items:**
| # | Issue | Affected scope | Needs resolution from | Next step |
|---|-------|----------------|----------------------|-----------|

**Informational / Notices:**
- ...

**Discussion Summary (by topic):**
- [Concise bullets per major topic]

**Next Meeting:** [date / time / location]

**Distribution:** [explicit list]

**Corrections:** Any corrections to these minutes must be submitted in writing within 5 business days; otherwise the minutes are deemed accepted as the project record.

**Output requirements:**
- Professional enough to distribute to owner, architect, lender, bonding
- Action items specific and assignable; no vague "follow up on things"
- Decisions explicitly marked as project record
- Open items surfaced, not hidden
- Use correct terminology — RFI, submittal, ASI, CCD, CO, not generic business terms
- Carryover clearly marked
- Output saved to `outputs/` if the user confirms
- For OAC / contract-formal meetings, include the "corrections within 5 days" clause or the contract-specified clause

## Example Output

**Example input:** "OAC meeting on Morrison Clinic (project 2026-031), 4/22 9:00-10:15 AM, site trailer. Attendees: Lisa Park (architect, Archwest), Tom Nguyen (GC super, Stonebridge), Dave Kim (owner's rep, MMC Health), Jordan Ellis (PM, Stonebridge), Rita Ward (MEP sub lead, Rivera Mech). Lisa: RFI-042 re: beam sizing at gridline C — structural engineer said yes to upsize W18x55 at cost delta; will issue ASI-007 by 4/24; this is a CO event. Tom: concrete sub 2 days behind on level-2 slab; level-2 framing was 4/21 Monday, now pushed to 4/23. Jordan: schedule is still OK on critical path but we're into float. Dave: owner accepts ASI-007 will generate a CO, wants PCO by Friday 4/25 so owner can release allowance draw. Rita: MEP rough-in still planned 5/4; no change. Safety: Tom wants mandatory fall-protection above Level 2; sub mtg Thursday 4/23 at 7 AM for all trades. Punch walk on level-1 mock-up unit next Friday 5/1 at 1 PM. Change order log: CO-003 (restroom reloc, owner-directed) still waiting on sub pricing — Rita owes us by 4/28."

**Expected output:**

> ### Morrison Clinic (2026-031) — OAC Meeting Minutes
> **Date:** 2026-04-22 **Time:** 9:00–10:15 AM **Location:** Site trailer, 412 Morrison Blvd
> **Prepared by:** Jordan Ellis, Stonebridge Construction **Issued:** 2026-04-22
> **Meeting #:** 18 **Prior meeting:** 2026-04-15 (#17)
>
> **Attendees:**
>
> | Name | Company | Role |
> |------|---------|------|
> | Dave Kim | MMC Health | Owner's representative |
> | Lisa Park | Archwest | Architect of record |
> | Tom Nguyen | Stonebridge | GC superintendent |
> | Jordan Ellis | Stonebridge | Project manager |
> | Rita Ward | Rivera Mechanical | MEP lead |
>
> **Decisions:**
>
> | # | Decision | Decided by | Basis | Affected scope |
> |---|----------|------------|-------|----------------|
> | D-18.1 | Upsize beam at gridline C from W16x45 to W18x55 | Structural engineer (via ASI-007) | RFI-042 response | Structural steel frame, Div 05 12 00 |
> | D-18.2 | PCO for beam upsize to owner by Fri 2026-04-25 so allowance draw can proceed | D. Kim (owner's rep) | Allowance mechanics | CO log; cost & schedule |
> | D-18.3 | Mandatory 100% fall-protection policy for all work above Level 2 | T. Nguyen (GC super) | Project safety plan §4.2 | All trades working above L2 |
>
> **Action Items:**
>
> | # | Action | Owner | Due | Type | Priority | Carryover |
> |---|--------|-------|-----|------|----------|-----------|
> | A-18.1 | Issue ASI-007 for beam upsize at gridline C | L. Park, Archwest | 2026-04-24 | ASI | High | New |
> | A-18.2 | Submit PCO-007 (cost & time delta for beam upsize) to owner | J. Ellis, Stonebridge | 2026-04-25 | CO | High | New |
> | A-18.3 | Deliver sub pricing for CO-003 restroom reloc | R. Ward, Rivera Mech | 2026-04-28 | CO | High | Carried from #16 |
> | A-18.4 | Hold all-trades fall-protection briefing | T. Nguyen, Stonebridge | 2026-04-23 07:00 | Safety | High | New |
> | A-18.5 | Confirm revised Level 2 framing start (2026-04-23) with framing sub | T. Nguyen, Stonebridge | 2026-04-22 EOD | Schedule | High | New |
>
> **Open Items:**
>
> | # | Issue | Affected scope | Needs resolution from | Next step |
> |---|-------|----------------|----------------------|-----------|
> | O-18.1 | Concrete slab sub 2 days behind on Level 2 — float consumed from 5 days to 3 | Level 2 slab / framing predecessor | Concrete sub (Lakeview Concrete) | Jordan to request recovery plan by 2026-04-24 |
>
> **Informational / Notices:**
> - Level 1 mockup unit punch walk scheduled Friday 2026-05-01 at 1:00 PM. Lisa, Dave, Tom, and Jordan to attend.
> - MEP rough-in still tracking 2026-05-04; no change from meeting #17.
>
> **Discussion Summary:**
> - RFI-042 / ASI-007 / PCO-007 mechanics (beam upsize at gridline C): architect confirmed cost delta is a change event; owner's rep confirmed allowance will be drawn against PCO.
> - Concrete slip on Level 2 acknowledged; project still on critical-path but float reduced. Recovery plan requested.
> - Safety: fall-protection policy reiterated; all-trades huddle Thursday AM.
>
> **Next Meeting:** 2026-04-29, 9:00 AM, site trailer
>
> **Distribution:** All attendees; D. Kim to forward to MMC Health finance; J. Ellis to distribute to bonding company per Owner-GC contract §15.2.
>
> **Corrections:** Any corrections to these minutes must be submitted in writing within 5 business days (by 2026-04-29); otherwise the minutes are deemed accepted as the project record.
>
> ---
> **Internal note (not part of the minutes):** PCO-007 must cite ASI-007 as the change mechanism. Concrete slip on Level 2 reduces critical-path float to 3 days — put Lakeview Concrete on watch; if the recovery plan doesn't land by 4/24, consider a §12 notice-to-cure cover.
