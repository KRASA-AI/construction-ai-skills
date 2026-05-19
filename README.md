# Construction AI Skills

**Free, open-source AI prompts and workflows built for contractors.** Clone this repo, point your AI assistant at it, and start saving hours every week.

> Built and maintained by [KRASA AI](https://krasa.ai) — free AI tutorials and skills for every industry.
> See all industries at [krasa.ai/industries](https://krasa.ai/industries).

---

## What's Inside

This repo is a complete AI toolkit for construction. Every skill is a standalone prompt file that works with **Claude, ChatGPT, or any major AI assistant** — no coding required.

| Skill | What it does | Time saved |
|-------|-------------|------------|
| Daily Log Generator | Turn the superintendent's or foreman's raw field notes — typed bullets, a voice-memo transcript, a platform export (Procore Daily Log / PlanGrid / HammerTech / BuildPass), or a hand-written page photographed and captioned — into a properly formatted, **claims-grade** daily construction report covering weather, crew and equipment on site, work performed (by location/area), materials delivered, deliveries scheduled, visitors, safety observations, delays/disruptions, quantities installed, productivity rate, and photos — structured to be admissible as contemporaneous project documentation if a dispute arises later. | ~20 min/day |
| Drawing Revision Comparator | Parse a drawing bulletin (revision package) against the prior issued set and produce a structured, per-trade delta report that identifies every change — including changes not marked with revision clouds — classifies each change by trade impact, flags new coordination conflicts introduced by the revision, and surfaces RFI and change-order candidates before they become field problems. | ~4-8 hrs/bulletin |
| Look-Ahead Schedule Critique | Read a two-week (or three-week) look-ahead schedule derived from the master CPM and critique it as a skeptical pull-plan facilitator would: surface unresolved constraints, predecessor slip risk, float consumption, missing handoffs between trades, crew overloading, material / submittal / inspection prerequisites, and weather exposure. | ~2-3 hrs/week on pull-plan prep |
| Pre-Task Plan Drafter | Generate a daily, task-by-task **Pre-Task Plan** (PTP, sometimes called Pre-Task Safety Analysis or Pre-Shift Plan) that the crew leader can hand-write final corrections on, walk through with the crew at the morning huddle, post at the work area, and have signed off before work begins. | ~25-40 min per crew per shift |
| Preconstruction Drawing Checker | Parse a 2D construction drawing set (issued-for-bid, issued-for-permit, or issued-for-construction) and produce a structured constructability and coordination review BEFORE the project breaks ground — surfacing missing information, code-compliance gaps, MEP and structural coordination conflicts, sheet-to-sheet inconsistencies, dimension and detail discrepancies, accessibility issues, fire-and-life-safety gaps, and constructability problems that would otherwise turn into RFIs, change orders, and rework once the trades are in the field. | ~6-16 hrs/drawing set |
| Project Q&A Assistant | Answer a specific question about a construction project — "what does the spec say about slip-sheet requirements under the membrane roof?", "has this RFI already been asked?", "which approved submittal governs this fixture?", "what does the code say about the corridor rating?" — by searching across contract documents, drawings, specifications, RFIs, submittals, ASIs, meeting minutes, and referenced codes, and producing a cited, auditable answer. | ~30-60 min/question vs. manual document search |
| Punch List Organizer | Turn raw walkthrough notes — the PM's phone voice memo, the architect's marked-up set, a stream of photo captions, or a Procore Punch / BuildPass / SpaceCapture export — into a structured punch list organized by location (floor/room) and by responsible trade, with clear item descriptions, severity, assigned party, required completion date, photo references, and a status column ready to track to close-out and substantial completion. | ~30-45 min/walkthrough |
| RFI Response Drafter | Draft a clear, defensible Request for Information (RFI) response that cites specific spec sections, drawing details, and prior project decisions — structured so the receiving party (architect, engineer, GC, sub, or owner) can act on it without a follow-up round-trip. | ~25 min/RFI |
| Safety Plan Builder | Generate the project-level **Site-Specific Safety Plan (SSSP)** for a construction project — the written program that the owner / GC / AHJ files at project start, posts in the trailer, and references throughout the build. | ~45 min/plan |
| Submittal Review Summary | Read a submittal package (product data, shop drawings, samples, or mock-ups) and produce a one-page reviewer memo that: (a) lists every deviation from the contract specifications, (b) classifies each deviation as minor / substantive / or a substitution-request, (c) recommends a disposition (No Exceptions Taken / Make Corrections Noted / Revise & Resubmit / Rejected) consistent with the spec's allowed stamps, and (d) flags coordination impacts for related trades and the project schedule. | ~30-45 min/submittal |
| Value Engineering Analyzer | Review a project scope, estimate, or specification package and produce a structured, decision-ready VE log of options that reduce first cost (or improve life-cycle cost, or compress schedule) without sacrificing function, durability, code compliance, or owner intent — each option with savings range, schedule impact, life-cycle-cost note, code/warranty risk, decision owner, and the architect/engineer review path required to implement. | ~90-120 min/package |
| Bid Leveling Analyzer | Take a GC's sub-bid package results — two or more bids returned on the same Invitation to Bid — and produce a normalized, apples-to-apples leveling matrix that adjusts for scope gaps, exclusions, alternates, and unit-price differentials. | ~4-10 hrs/bid package |
| Bid Proposal Generator | Generate a bid-form-aware, delivery-method-aware, project-pattern-matched construction proposal — ready to send with minimal editing — that satisfies the bidding requirements of the specific solicitation (private RFP, public ITB, design-build RFQ, CMAR proposal, GMP package, hard-bid lump sum) and reflects how the work will actually be procured and built. | ~60-90 min/proposal |
| Estimate Simplifier | Rewrite a technical construction cost estimate into a clear, client-facing summary that a non-technical reader can read in 3–5 minutes and sign with confidence. | ~20-30 min/estimate |
| ITB Package Drafter | Turn a project plan set, spec outline, or scope narrative into a full set of trade-specific Invitations to Bid (ITBs) — one per trade — each with a targeted scope summary, submission requirements, key dates, site access notes, an explicit scope-handoff matrix that prevents the most common bid-day overlap errors, and a coverage / responsiveness self-check before release. | ~8-12 hrs/project |
| Trade-Scope Takeoff Reviewer | Read a quantity takeoff — whether it was generated by AI (Togal, Kreo, STACK, Buildxact, Beam AI, TaksoAI, CountBricks, Bluebeam VisualSearch) or prepared manually in a spreadsheet — and produce a second-pair-of-eyes reviewer memo that flags the specific error classes AI takeoff tools (and estimators in a hurry) are known to miss: legend-symbol misreads, missed openings, wall-type confusion, scale / enlarged-detail errors, schedule-vs-plan count mismatches, plan-only items missed from elevations, and scope gaps between trades. | ~60-90 min/takeoff |
| Owner Update Drafter (Residential + Commercial) | Draft clear, situation-tuned project updates for the project's owner — whether that's a homeowner during a remodel or custom build, or a commercial owner / tenant / asset manager during a TI, ground-up, or capital project. | ~20-40 min/update |
| Backcharge Notice Drafter | Turn a documented sub-tier failure — defective work, missed cleanup, damage to other trades, missed milestone, equipment misuse, no-show on a fix — into the disciplined paper chain that survives a sub's later mechanic's-lien claim, an attorney's review, and an owner's pass-through audit. | ~45-75 min per backcharge package |
| Change Order Drafter | Turn a scope change — whether owner-directed, architect-directed, hidden condition, or a constructive change via field direction — into a properly documented Change Order Request (COR) or executed Change Order (CO) that: (a) is cost-reconciled with labor, material, equipment, subcontractor, bond, insurance, overhead & fee markups consistent with the contract, (b) states the schedule impact (time extension, no impact, or reservation of rights), (c) traces the origin of the change to a drawing, RFI, ASI, PCO, CCD, or field directive, and (d) matches the contract's change-order clauses (AIA G701/G701-CMa, ConsensusDocs 802, EJCDC C-940, or owner custom form). | ~45 min/CO |
| Closeout Documentation Auditor | Audit a construction project's closeout package — as-built drawings, operation & maintenance (O&M) manuals, warranties, final lien waivers, attic stock, training records, and the certificate of occupancy — against the contract-specified deliverables, and produce a gap list so final payment and retainage release aren't held up by missing documents. | ~6-10 hrs/project closeout |
| Contract Risk Reviewer | Analyze a construction contract (prime contract, subcontract, or purchase order) and produce a plain-language risk summary that flags problematic clauses, missing protections, and compliance gaps — so the user can negotiate, escalate, or walk before signing. | ~45-90 min/contract |
| Delay Claim & Time Extension Drafter | Draft a contractually compliant notice of delay, request for extension of time (EOT), or formal delay claim narrative that: (a) satisfies the contract's notice-timing and notice-form requirements, (b) identifies the causation and the delay event with contemporaneous evidence references, (c) quantifies schedule impact using an industry-accepted delay-analysis method (Time Impact Analysis, Windows, As-Planned vs. | ~4-8 hrs/claim |
| Lien Waiver Drafter | Generate a clean, state-correct lien waiver — conditional or unconditional, progress or final — that an owner, lender, or upstream contractor will accept without rework, and that does not silently surrender lien rights for unpaid work or for sums in dispute. | ~30-45 min per waiver package |
| Pay Application Reviewer | Review a construction pay application (AIA G702 cover sheet and G703 continuation sheet, or equivalent custom forms) and flag math errors, inconsistent percent-complete values, retainage miscalculations, missing lien waivers, stored-material documentation gaps, and contract-term conflicts — before it goes to the owner, lender, or GC for certification. | ~40 min/pay app |
| Subcontractor Prequalification Reviewer | Review a subcontractor's prequalification submission — certificate of insurance (COI), safety metrics (EMR, TRIR, OSHA 300 logs), financial snapshot, bonding capacity, licensing, and references — and produce a go / no-go recommendation with specific gaps, risk flags, and coverage deltas vs. | ~45-90 min/sub |
| WIP & Over/Under Billing Reviewer | Read a contractor's monthly Work-in-Progress (WIP) schedule — the cost-to-cost percentage-of-completion roll-up that ties earned revenue to billings on every active job — and produce a CFO/PM-ready review memo that flags stale ETCs, profit fade, overbilling concentration, underbilling neglect, ASC 606 treatment errors (uninstalled materials, variable consideration, loss-job recognition), schedule-of-values front-loading, and cash-flow inversion risk. | ~90-120 min/month per WIP cycle |
| Email Drafter | Turn rough notes, bullet points, or verbal context into a professional, ready-to-send construction email that preserves the contractual posture appropriate to the situation (notice, transmittal, coordination, follow-up), uses the right register for the recipient (client, GC, architect, sub, supplier, AHJ, owner's rep), and lines up with the company's voice. | ~10-15 min/email |
| Meeting Summarizer | Turn construction meeting notes — typed, voice-transcribed, or bullet — into structured, distributable minutes that (a) match the meeting type's conventions, (b) separate decisions from action items from open issues, (c) make every commitment traceable (who, what, by when), and (d) flag risks the meeting surfaced but did not resolve. | ~20-30 min/meeting |
| Review Responder | Draft a professional public response to an online review (Google, Yelp, Houzz, BBB, Procore referrals, Angi, NextDoor) — tailored to the construction industry's specific review patterns: disputes over change orders, punch list and warranty callbacks, jobsite dust/noise/parking complaints from neighbors, schedule slippage, and praise from satisfied homeowners or commercial clients. | ~15 min/use |

**Total time saved per use: ~1215+ minutes across all skills.**

## Quick Start

### 1. Clone this repo

```bash
git clone https://github.com/KRASA-AI/construction-ai-skills.git
cd construction-ai-skills
```

### 2. Open a skill with your AI assistant

Open any file in `skills/` with Claude, ChatGPT, or any major AI assistant. Each skill is a self-contained prompt with clear instructions — no coding required.

The first time you use a skill, your AI assistant will ask for your business details (company name, service area, rates, tools you use, etc.) so it can personalize the output. Save those details to a `config.yml` at the repo root and every future skill will use them automatically.

## Repo Structure

```
construction-ai-skills/
├── knowledge-base/          # Industry context and references
│   ├── industry-overview.md # Market trends and pain points
│   ├── terminology/         # Industry jargon and acronyms
│   ├── regulations/         # Compliance requirements
│   ├── best-practices/      # Industry standards
│   └── tools-ecosystem/     # Common software and tools
├── skills/                  # The prompt library
│   ├── operations/          # Day-to-day operational skills
│   ├── sales/               # Sales and lead management
│   ├── admin/               # Administrative and compliance
│   └── customer-service/    # Client-facing communication
└── outputs/                 # Your generated content (gitignored)
```

## How Skills Work

Each skill file is a Markdown document with YAML frontmatter:

```markdown
---
name: Skill Name
category: operations
tools: [claude, chatgpt]
time_saved: "~20 min/use"
version: 1.0
---

# Skill Name

## Purpose
What this skill does and when to use it.

## Instructions
Step-by-step prompt for the AI assistant.
```

You open the file in your AI assistant, provide any required input (measurements, notes, client info), and get polished output. Skills reference your `config.yml` automatically for company name, rates, preferred formats, and other business details.

## For AI Assistants

If you are an AI assistant reading this repo, see `.claude/CLAUDE.md` for full instructions. The short version:

1. **Check for `config.yml`** at the repo root. If it exists, load it — it holds the user's business context (company name, rates, service area, tools, team size, etc.) and every skill should use it for personalization.
2. **If `config.yml` is missing**, before running a skill that benefits from personalization, ask the user for the relevant business details and offer to save them to `config.yml` so future runs are automatic.
3. **Load the relevant `knowledge-base/` files** for industry terminology, regulations, and best practices before generating output.
4. **Run the requested skill** from `skills/` using the user's input.
5. **Save any deliverables** to `outputs/` (gitignored) if the user wants to keep them.

## Learn More

- **Construction AI guide**: [krasa.ai/industries/construction](https://krasa.ai/industries/construction)
- **All industry AI skills**: [krasa.ai/industries](https://krasa.ai/industries)
- **About KRASA AI**: [krasa.ai](https://krasa.ai)

## License

MIT — use these skills however you want.
