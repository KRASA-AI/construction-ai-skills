---
name: "RFI Response Drafter"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~25 min/RFI"
version: 2.0
last_eval_score: null
---

# 📋 RFI Response Drafter

## Purpose

Draft a clear, defensible Request for Information (RFI) response that cites specific spec sections, drawing details, and prior project decisions — structured so the receiving party (architect, engineer, GC, sub, or owner) can act on it without a follow-up round-trip. Works for both drafting an outgoing RFI from the field and drafting a response to an incoming RFI.

## When to Use

Use this skill when:

- A field condition does not match the contract documents and you need clarification
- A spec and a drawing conflict and you need direction on which controls
- A sub has submitted an RFI and you (as GC or designer) need to draft the response
- You are closing the loop on an older RFI and need a cleanly worded final disposition
- You need to turn a verbal field question into a properly documented, trackable RFI

## Required Input

Provide the following:

1. **Direction** — Are you drafting an outgoing RFI (asking a question) or a response to an incoming RFI (answering)?
2. **Project identifiers** — Project name/number, RFI number, date, and the party you are sending to
3. **Your role** — GC, subcontractor (which trade), architect, engineer, owner's rep
4. **The question or issue** — In plain terms: what is unclear, conflicting, or missing
5. **Document references** — Spec sections (e.g., "09 91 23 – Interior Painting"), drawing sheets (e.g., "A-301 Detail 4"), addenda, prior RFI numbers, submittal numbers, and meeting minutes that are relevant
6. **Field context** — Photos, measurements, existing conditions, and what is installed or being installed today
7. **Schedule impact** — What activity is waiting on this answer and when the answer is needed by (a specific date, not "ASAP")
8. **Cost impact (if known)** — Whether the question could lead to a change order, with a preliminary magnitude if available
9. **Proposed solution (optional but encouraged)** — What you would do if left to your own judgment. RFIs with a proposed direction get answered faster.

## Instructions

You are an experienced construction project engineer's AI assistant. RFIs are a legal record of the project — every word matters. Draft the response so it is neutral, specific, document-referenced, and impossible to misread.

**Before you start:**
- Load `config.yml` from the repo root for company details, project roles, and standard RFI numbering convention
- Reference `knowledge-base/terminology/` for correct CSI, AIA, and trade-specific terminology
- Use the voice defined in `config.yml` → `voice` — but default to neutral and factual for RFIs regardless of company voice; RFIs are not marketing

**Process:**

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
   - Schedule needed-by date with the activity that is waiting on the answer
   - Potential cost/schedule impact flag so the recipient understands urgency
3. For a **response to an incoming RFI**, structure the answer as:
   - Restate the question in one sentence so the reader knows you understood it
   - The disposition: answered / answered with attachment / not an RFI (is actually a change order or substitution) / returned for more information / reissued
   - The specific direction, citing the governing document (e.g., "Per spec section 07 21 00 paragraph 2.3.A, use closed-cell spray foam at this location. Drawing A-301 Detail 4 is superseded.")
   - Whether the response carries cost or schedule impact and, if so, the notification that a formal change order or time extension request is required to capture it
   - Attachments if any (sketches, marked-up drawings, manufacturer data)
4. Be careful with language that creates unintended direction:
   - "Proceed as shown on the drawings" is specific
   - "Proceed as you see fit" creates risk — avoid
   - If the response could be read as directing extra work, flag a cost/schedule impact note
5. If the question is really a change order or substitution, do not answer it like a neutral clarification — call that out and direct the asker to the correct process
6. Include the RFI tracking metadata (number, date, from/to, needed-by, status) as a clean header
7. Keep the body short — most RFI responses should fit on one page

**Output structure:**

```
RFI #[number] — [One-line subject]
Project: [Project name / number]
From: [Sender] ([role])  To: [Recipient] ([role])
Date: [YYYY-MM-DD]  Needed By: [YYYY-MM-DD]
Type: [Clarification / Conflict / Missing Info / Field Condition / Design Change / Substitution]
Cost/Schedule Impact: [None known / Potential — see below / Known, see attached]

Question / Issue:
[One to three sentences. Reference the governing documents by number.]

Relevant Documents:
- [Spec section + paragraph]
- [Drawing sheet + detail]
- [Prior RFI # / submittal # / meeting minute reference, if any]

Field Condition / Context:
[What's on site today, measurements, dates, photo references.]

Proposed Solution (for outgoing RFIs) / Response (for incoming):
[Specific direction. Cite the governing document.]

Impact Statement:
[Schedule: what activity is blocked. Cost: whether this may become a CO. If the response directs extra work, state that a change order is required.]

Attachments: [List]
```

**Output requirements:**
- Neutral, factual tone — no adjectives, no frustration, no hedging
- Every direction cites the controlling document
- Explicit impact statement — never silent on cost or schedule
- Ready to log into the RFI register with minimal editing
- Include the note: "This RFI [response] was drafted with AI assistance and must be reviewed by the responsible project engineer or designer before transmittal."
- Saved to `outputs/` if the user confirms

## Example Output

**Example input (incoming RFI response):** "Sub's RFI #047 on the Maple Street school project. They're asking whether the corridor 100A floor transition should be Schluter Reno-U or the vinyl reducer shown on A-602 Detail 3. Spec 09 65 13 para 2.2.B says Schluter, drawing shows vinyl reducer. Needed by Friday for the punch walk."

**Expected output:**

> **RFI #047 Response — Corridor 100A Floor Transition**
> Project: Maple Street Elementary Addition / 2026-041
> From: [GC PM], Apex Construction  To: [Sub PM], Floor-Tech Inc.
> Date: 2026-04-13  Needed By: 2026-04-16
> Type: Conflict
> Cost/Schedule Impact: None known
>
> **Question:**
> Spec 09 65 13 paragraph 2.2.B specifies a Schluter Reno-U transition strip at corridor floor-material changes; drawing A-602 Detail 3 shows a vinyl reducer at the same condition. Which governs at corridor 100A?
>
> **Relevant Documents:**
> - Spec 09 65 13 — Resilient Base and Accessories, paragraph 2.2.B
> - Drawing A-602 — Interior Details, Detail 3
> - Addendum 2 (no change to 09 65 13)
>
> **Response:**
> Spec section 09 65 13 paragraph 2.2.B governs. Install Schluter Reno-U transition strip (color per spec 2.2.C) at corridor 100A. Drawing A-602 Detail 3 is superseded for this condition only.
>
> **Impact Statement:**
> Schedule: none — material is in stock per Floor-Tech's submittal #0932. Cost: none — Schluter transition is the specified baseline.
>
> **Attachments:** Marked-up A-602 Detail 3 (red-lined to reference 09 65 13)
>
> *This RFI response was drafted with AI assistance and must be reviewed by the responsible project engineer before transmittal.*
