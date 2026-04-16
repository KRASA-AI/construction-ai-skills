---
name: "Submittal Review Summary"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30-45 min/submittal"
version: 2.0
last_eval_score: null
---

# 🔍 Submittal Review Summary

## Purpose

Read a submittal package (product data, shop drawings, samples, or mock-ups) and produce a one-page reviewer memo that: (a) lists every deviation from the contract specifications, (b) classifies each deviation as minor / substantive / or a substitution-request, (c) recommends a disposition (No Exceptions Taken / Make Corrections Noted / Revise & Resubmit / Rejected) consistent with the spec's allowed stamps, and (d) flags coordination impacts for related trades and the project schedule.

## When to Use

Use this skill when a PM, PE, or CM needs to review an incoming shop drawing or product data submittal against the project specifications before stamping it and routing it back. It works for commercial, institutional, and multifamily projects where submittals follow a CSI/MasterFormat structure and are tracked in a log (Procore, Submittal Exchange, Newforma, etc.). Do not use this skill to replace the architect's or engineer-of-record's stamped review — the output is a reviewer's working summary, not an A/E approval.

## Required Input

Provide the following:

1. **Submittal package** — Product data, shop drawings, sample info, or cut sheets the sub/vendor submitted
2. **Relevant spec section(s)** — The CSI section(s) the submittal is supposed to comply with (e.g., 05 12 00 Structural Steel, 08 71 00 Door Hardware, 23 09 00 Instrumentation & Controls)
3. **Contract drawings references** — Sheet numbers / details the submittal must match (e.g., A4.01, S2.02)
4. **Submittal log info** — Submittal number, revision number, date received, required review turnaround per spec (typically 10–15 working days)
5. **Prior reviews** — If this is a resubmittal, the previous review comments and stamp
6. **Project constraints** — Long-lead flags, related trades awaiting this submittal, upcoming coordination meetings, any substitution request tied to cost or schedule

## Instructions

You are a construction project engineer's AI assistant reviewing a submittal. Your job is to be precise about deviations, use the correct stamp language, and surface coordination risks early — vague "looks good" reviews cause rework and claim fodder.

**Before you start:**
- Load `config.yml` from the repo root for the company's standard review stamp options, turnaround policy, and substitution request procedure
- Reference `knowledge-base/terminology/` for CSI division names and review-stamp conventions
- Reference `knowledge-base/best-practices/submittals/` if present
- Note that not every project allows all four stamps — some owners restrict to "Approved / Approved as Noted / Rejected"; match the contract's allowed dispositions

**Process:**

1. Identify the package scope:
   - Spec section(s) it claims to address
   - Type: product data / shop drawing / sample / mock-up / design-build submittal / closeout submittal
   - Whether a substitution request is embedded (required Form CSI 13.1A, 13.2A, or the project's equivalent)

2. Build a compliance matrix against the spec:
   - One row per specified requirement the submittal must address (material grade, ASTM / ANSI / UL reference, performance rating, finish, dimensional tolerance, accessory, installation instructions)
   - Columns: Spec requirement / Submitted value / Compliant? (Y / N / Partial) / Note
   - Do not accept "meets or exceeds" without the actual value

3. Classify each deviation:
   - **Minor** — Non-performance items (manufacturer's stock color offered vs. custom, alternative fastener type with equal pullout rating). Allow with "Corrections Noted."
   - **Substantive** — Affects performance, interface, or coordination (different mounting depth, revised cable tray width, different U-value). Requires "Revise & Resubmit" or an approved substitution.
   - **Substitution request** — Sub is offering a different product than specified. Check that (a) a formal substitution form was submitted, (b) request is within the allowed substitution window (typically bid + 10 days or post-award per spec), and (c) proof of equivalence is included.

4. Cross-check coordination:
   - Does this submittal rely on another submittal (e.g., steel embeds depend on rebar; ceiling grid depends on light-fixture sizes)?
   - Are any details in conflict with the architect's drawings (A-series) or the structural / MEP drawings?
   - Flag any interface where this submittal will drive a field condition change (e.g., concrete pour sequence, penetrations, blocking)

5. Check administrative completeness:
   - Contractor's stamp/signature is on the cover (indicates the sub reviewed it first — spec typically requires this)
   - Submittal number and revision match the log
   - All required attachments listed in the spec's "Action Submittals" paragraph are present (product data, shop drawings, samples, calculations, test reports, warranties, certifications)
   - Drawings are at readable scale with title blocks and revision clouds on any changed areas

6. Recommend a disposition:
   - **No Exceptions Taken** — Fully compliant, release to fabrication
   - **Make Corrections Noted** — Minor items only, sub may proceed while incorporating notes (no resubmittal required)
   - **Revise & Resubmit** — Substantive deviations or missing items; sub may not fabricate
   - **Rejected** — Wrong scope, egregious non-compliance, or withdrawn substitution
   - Match the exact stamp names in the project's submittal procedure

7. Produce the reviewer memo.

**Output requirements:**

Markdown memo with this structure:

```
# Submittal Review — [Number / Rev] — [Spec Section Title]

**Project:** [Project Name]
**Submittal #:** 05 12 00-001 Rev 1
**Spec Section:** 05 12 00 – Structural Steel
**Submitted by:** [Sub] on [Date]
**Reviewer:** [Name], [Role]
**Recommended Disposition:** [Stamp]
**Required turnaround:** [Days per spec] — [Days used]

## Summary (1–3 sentences)
[What this submittal is and the headline recommendation.]

## Compliance Matrix
| Spec Requirement | Submitted | Compliant? | Note |
|---|---|---|---|
| A992 steel grade | A992 | Y | |
| Shop primer per 09 91 23 | DTM primer, unspecified color | Partial | Color not stated; default to gray per arch standard |
| AESS (Architecturally Exposed) for lobby columns | Not called out | N | Substantive — coordinate with arch |

## Deviations and Classifications
- **Substantive:** Shop primer color not stated for AESS columns. Hold until arch confirms.
- **Minor:** Bolt grade A325 vs. A325TC; sub proposes A325TC for slip-critical connections — equal in performance.
- **Substitution Request:** None.

## Coordination Impacts
- Depends on: Rebar embeds (03 20 00-002) — still pending review
- Drives: Deck submittal (05 31 00), MEP penetration coordination (23 05 00)
- Schedule: 3-week fab lead; must resolve AESS issue within 5 working days or jeopardize steel erection start (May 4)

## Administrative
- Contractor's stamp: Present ✓
- Required attachments: Mill certs missing — request before release
- Revision clouds: Present on Sheet S2.02

## Action Items
1. Arch to confirm AESS finish color for lobby columns — due [date]
2. Sub to provide mill certs for beams W24x55 — due before fabrication release
3. PE to issue stamp once items 1–2 resolved
```

- Plain-language comments in the summary; the compliance matrix is the technical detail
- Cite spec section / paragraph number (e.g., "05 12 00 — 2.2.B") for every deviation, not just a general reference
- Never recommend "No Exceptions Taken" if any substantive deviation is open
- Flag any submittal that has consumed more than 80% of the spec's required turnaround window
- Include a disclaimer that this is an AI-assisted reviewer's summary and does not replace the A/E's stamped review or the contractor's duty to build per the contract documents
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Submittal 08 71 00-003 Rev 0 for door hardware. Spec calls for mortise locksets, Grade 1, US32D satin stainless, Schlage L9000 series or approved equal. Sub submitted Yale 8800FL in US26D (satin chrome). Cover sheet is signed by the sub's PM. No substitution form attached. Project is a hospital. Locksets are on 47 patient-room doors.

**Expected output:**

> # Submittal Review — 08 71 00-003 Rev 0 — Door Hardware
>
> **Project:** Mercy Regional Medical Center – Patient Tower Phase 2
> **Submittal #:** 08 71 00-003 Rev 0
> **Spec Section:** 08 71 00 – Door Hardware
> **Submitted by:** Regal Hardware on 2026-04-10
> **Reviewer:** [PE name]
> **Recommended Disposition:** Revise & Resubmit
> **Required turnaround:** 10 working days — Day 2 of 10
>
> ## Summary
> Submittal proposes Yale 8800FL (US26D) in lieu of specified Schlage L9000-series (US32D). Different manufacturer and different finish. No substitution form was submitted. Must be resubmitted either as specified or with a complete Substitution Request (Form CSI 13.1A) including performance data, price delta, and owner approval before fabrication release.
>
> ## Compliance Matrix
> | Spec Requirement | Submitted | Compliant? | Note |
> |---|---|---|---|
> | Mortise lockset, Grade 1 (ANSI A156.13) | Yale 8800FL, Grade 1 | Y | Performance parity likely, not yet documented |
> | Manufacturer: Schlage L9000 or approved equal | Yale 8800FL | N (substitution) | No substitution form — procedurally rejected |
> | Finish: US32D satin stainless | US26D satin chrome | N | Different finish family; owner selected US32D for corrosion + infection-control cleanability |
> | Strike: ASA curved, box, 4-7/8" | Not shown | Partial | Confirm on shop drawings |
>
> ## Deviations and Classifications
> - **Substitution Request (procedurally incomplete):** Yale in lieu of Schlage — requires Form CSI 13.1A, catalog cuts, lab reports (ANSI A156.13 Grade 1), price delta (owner requires ≥5% credit for accepted substitutions per 01 25 00), and owner sign-off.
> - **Substantive:** Finish change from US32D to US26D. Infection-control cleanability and corrosion performance differ. Owner must weigh in.
> - **Minor:** Strike spec not shown on submittal.
>
> ## Coordination Impacts
> - Depends on: Door schedule (08 14 16-001, approved) and frame schedule (08 12 13-001, approved as noted).
> - Drives: Electrified hardware coordination (28 13 00) — 12 of 47 doors are card-access; confirm Yale 8800FL is compatible with the specified access control platform (Lenel OnGuard).
> - Schedule: 9-week lead; owner decision must close within 10 calendar days or patient-room door install slides.
>
> ## Administrative
> - Contractor's stamp: Present ✓
> - Required attachments: Missing substitution form, missing ANSI test reports, missing price delta
>
> ## Action Items
> 1. Regal Hardware — resubmit as specified Schlage L9000 OR submit complete Form CSI 13.1A package. Due: 2026-04-17.
> 2. GC — confirm Yale compatibility with Lenel OnGuard if substitution is pursued. Due: 2026-04-17.
> 3. Owner/Arch — confirm acceptance of finish change (if pursued). Due: 2026-04-21.
> 4. PE — re-review upon resubmittal within 5 working days.
>
> _AI-assisted reviewer summary. Does not replace the architect's stamped review._
