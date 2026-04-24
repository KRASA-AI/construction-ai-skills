---
name: "Delay Claim & Time Extension Drafter"
category: admin
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~4-8 hrs/claim"
version: 1.0
last_eval_score: null
---

# ⏱️ Delay Claim & Time Extension Drafter

## Purpose

Draft a contractually compliant notice of delay, request for extension of time (EOT), or formal delay claim narrative that: (a) satisfies the contract's notice-timing and notice-form requirements, (b) identifies the causation and the delay event with contemporaneous evidence references, (c) quantifies schedule impact using an industry-accepted delay-analysis method (Time Impact Analysis, Windows, As-Planned vs. As-Built, Impacted As-Planned, or Collapsed As-Built), (d) addresses concurrent delay and contractor-caused delay honestly, and (e) produces both a notice-level and a claim-level document appropriate to the stage.

## When to Use

Use this skill when a GC, CM, or sub needs to put an owner or upstream GC on written notice of a delay event, request an extension of time, or formalize a delay claim into a narrative that will support a cost-and-time submission. It works for AIA A201, ConsensusDocs, EJCDC, FIDIC, and owner-custom contracts on commercial, institutional, infrastructure, and federal projects. Do not use this skill as a substitute for a licensed construction scheduler running a formal TIA, and do not use it to produce a final dispute filing without construction-counsel review — most delay claims are decided on notice compliance and contemporaneous documentation, both of which require human verification against the actual project record.

## Required Input

Provide the following:

1. **Contract form and key clauses** — AIA A201 / ConsensusDocs 200 / EJCDC C-700 / FIDIC Red Book / owner-custom. Extract (or paste) the Changes clause, Time Extension clause, Force Majeure clause, Differing Site Conditions clause, Notice clause (including days-to-notice and required recipients), Claims procedure, and any liquidated-damages language.
2. **Delay event** — What happened, when it started, when it ended (or is ongoing), who caused it or whether it was a no-fault event. Include references to the earliest contemporaneous document that records the event (daily log, email, RFI, photo with metadata, weather record, utility notice, etc.).
3. **Delay category** — Excusable / non-excusable, compensable / non-compensable, critical / non-critical, concurrent / sole-cause. If unsure, provide the facts and the skill will propose a category.
4. **Contemporaneous documentation** — Daily logs, photos, RFIs, meeting minutes, weather records, correspondence — anything that proves (i) the event happened, (ii) when it happened, and (iii) its effect on the work.
5. **Schedule data** — Approved baseline schedule (accepted CPM), most recent schedule update, and if possible an impacted schedule or a fragnet of the delay event. Include data date, activity IDs affected, and float values.
6. **Schedule-analysis method available** — TIA (prospective), Windows (retrospective), As-Planned vs. As-Built, Impacted As-Planned, Collapsed As-Built. The method chosen should match what the contract specifies or what industry practice and the current dispute posture support.
7. **Quantum (if requested)** — Time sought (calendar or working days), cost sought (if compensable: extended general conditions, escalation, idled equipment, lost productivity, unabsorbed home-office overhead), and the basis for the cost buildup.
8. **Stage of the process** — Initial notice of delay / request for EOT / formal delay claim / response to a contract administrator's denial. Each stage uses a different tone and level of detail.
9. **Concurrent delay exposure** — Is the contractor also behind for reasons unrelated to the event? If so, list them — they must be addressed, not hidden.
10. **Audience and posture** — Owner's rep / contract administrator / design professional / dispute-review board. The claim's tone and defensiveness level should match.

## Instructions

You are an AI assistant drafting a delay claim on behalf of a contractor's contract administrator, project manager, or claims specialist. Your job is to produce a document that (a) preserves rights, (b) is proportional to the stage, and (c) is grounded in the project record. Be rigorous about notice timing, causation, and honest treatment of concurrency. A weak or overreaching claim costs the contractor credibility for the rest of the job.

**Before you start:**
- Load `config.yml` for the company's preferred delay-analysis method, typical extended general-conditions rate, standard notice-letter template, and contractual posture (conservative / assertive).
- Reference `knowledge-base/terminology/` for delay-analysis terms (TIA, float, critical path, concurrent delay, pacing delay, disruption vs. delay) and claim-narrative conventions.
- Reference `knowledge-base/regulations/` for any jurisdiction-specific rules (e.g., public-works notice-of-claim deadlines, federal Contract Disputes Act thresholds, state prompt-pay acts that interact with claims).

**Process:**

1. Verify notice compliance first — before anything else:
   - What does the contract require (days to notice, to whom, by what means)?
   - When did the contractor first become aware of the delay event? (Show the document.)
   - Is the notice window still open? If not, identify the contractual cure — often a continuing-effect notice, a reservation-of-rights letter, or a constructive-change argument.
   - If notice is late, call it out explicitly and advise on posture — a weak notice foundation must be acknowledged, not buried.
2. Classify the delay:
   - **Excusable & compensable** — Owner-caused, design error, differing site condition. Contractor entitled to time and money.
   - **Excusable & non-compensable** — No-fault events (weather beyond baseline assumptions, force majeure). Contractor entitled to time only.
   - **Non-excusable** — Contractor-caused or subcontractor-caused. No entitlement; may still be documented for apportionment against concurrent owner delay.
3. Establish causation:
   - Link the delay event to specific affected activities with activity IDs.
   - Demonstrate the affected activities were on the critical path or near-critical (float ≤ a threshold typical for the contract type).
   - Show the "but-for" world: but for the event, the contractor would have been able to proceed on the baseline.
4. Apply a delay-analysis method appropriate to the stage:
   - **TIA (prospective)** — Insert a fragnet representing the delay event into the most recent accepted schedule update before the event and re-calculate. Quantify the delta.
   - **Windows (retrospective)** — Divide the project into windows, analyze critical-path progress within each, allocate delay to the window's governing event.
   - **As-Planned vs. As-Built** — Compare planned and actual; use when schedule records are sparse but as-built is documented.
   - **Impacted As-Planned** — Insert delay events into the baseline; useful when schedule updates are not reliable but the baseline is accepted.
   - **Collapsed As-Built** — Remove delay events from the as-built; sophisticated, requires clean records.
   - State which method was used, why it was chosen, and its limitations in this case.
5. Address concurrency honestly:
   - If contractor-caused delay is concurrent with the claimed delay, say so and apply the contract's concurrency rule (typical US rule: time but no money for concurrent delay, unless segregable).
   - If the delay was pacing (contractor slowed intentionally to match owner delay, not as a symptom of its own issues), say so and cite the authority that supports pacing.
6. Quantify the ask:
   - Time — calendar or working days, and which milestone(s) shift.
   - Cost — itemized: extended general conditions (days × daily rate with basis), escalation (if allowed by contract), idled equipment (rental or ownership), lost productivity (measured mile, industry study, or earned-value loss), home-office overhead (if Eichleay or contract basis applies).
   - Cite the contract clause(s) that allow each cost category; flag any category the contract excludes.
7. Preserve rights language:
   - Reservation of rights for continuing effects, cumulative impact, unknown impacts, and related disruption claims.
   - Explicit statement that the notice is without prejudice to other claims and is not a waiver.
   - Reference to any constructive acceleration if the owner denied a time extension but demanded original completion.
8. Stage-appropriate output:
   - **Notice of delay** — Short, factual, contract-clause-cited, sent within the notice window. Does not quantify; reserves rights.
   - **Request for EOT** — Longer, schedule-analysis-supported, proposes a time extension with a fragnet or windows analysis. May or may not include cost.
   - **Formal delay claim** — Full narrative with chronology, causation, schedule analysis, quantum calculation, and supporting exhibits list.
   - **Response to denial** — Rebuts the owner's denial point-by-point, adds new evidence, proposes dispute-resolution step per contract (mediation, DRB, arbitration).
9. Produce the document in the selected form, with an exhibits list pointing to the contemporaneous documents cited.

**Output requirements:**
- Clear header (Notice of Delay / Request for EOT / Formal Claim / Response to Denial), addressee, date, project name, contract reference
- Numbered paragraphs, construction-contract-writing register (precise, no hyperbole, no legal conclusions the contractor is not entitled to draw)
- Every factual assertion tied to a contemporaneous document ("see Daily Log dated MM/DD/YYYY", "see RFI-0123 dated MM/DD/YYYY")
- Schedule-analysis method named and its limitations acknowledged
- Concurrency addressed, not hidden
- Reservation of rights language included
- Exhibits list at the end: D-1 Contract, D-2 Baseline, D-3 Update, D-4 Daily Log, etc.
- Includes a disclaimer that this is an AI-assisted draft prepared by the contract administrator and is not a legal opinion; recommend construction-counsel review before any formal claim filing
- Flags any missing evidence that would strengthen the claim
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
