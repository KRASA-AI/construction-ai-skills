# Construction AI Skills

**Free, open-source AI prompts and workflows built for contractors.** Clone this repo, point your AI assistant at it, and start saving hours every week.

> Built and maintained by [KRASA AI](https://krasa.ai) — free AI tutorials and skills for every industry.
> See all industries at [krasa.ai/industries](https://krasa.ai/industries).

---

## What's Inside

This repo is a complete AI toolkit for construction. Every skill is a standalone prompt file that works with **Claude, ChatGPT, or any major AI assistant** — no coding required.

| Skill | What it does | Time saved |
|-------|-------------|------------|
| Daily Log Generator | Turn the superintendent's or foreman's raw field notes into a properly formatted daily construction report covering weather, crew and equipment on site, work performed (by location/area), materials delivered, deliveries scheduled, visitors, safety observations, delays/disruptions, quantities installed, and photos — structured to be admissible as contemporaneous project documentation if a dispute arises. | ~20 min/day |
| Punch List Organizer | Turn raw walkthrough notes — the PM's phone voice memo, the architect's marked-up set, or a stream of photo captions — into a structured punch list organized by location (floor/room) and by responsible trade, with clear item descriptions, severity, assigned party, required completion date, photo references, and a status column ready to track to close-out and substantial completion. | ~30 min/walkthrough |
| RFI Response Drafter | Draft a clear, defensible Request for Information (RFI) response that cites specific spec sections, drawing details, and prior project decisions — structured so the receiving party (architect, engineer, GC, sub, or owner) can act on it without a follow-up round-trip. | ~25 min/RFI |
| Safety Plan Builder | Generate a site-specific safety plan (SSSP) for a construction project that covers hazard identification, mitigation measures, emergency procedures, and regulatory compliance — formatted for jobsite posting and client/GC submittal. | ~45 min/plan |
| Submittal Review Summary | Summarize submittal packages and flag deviations from specs. | ~20 min/submittal |
| Value Engineering Analyzer | Review a project scope, estimate, or specification package and produce a structured list of value engineering (VE) options that reduce cost without sacrificing function, durability, or code compliance — each with an estimated savings range, trade-off notes, and owner decision points. | ~90 min/package |
| Bid Proposal Generator | Generate a persuasive, professionally structured construction bid proposal from project details, scope notes, and cost estimates — ready for client review with minimal editing. | ~45 min/proposal |
| Estimate Simplifier | Rewrite a technical construction cost estimate into clear, client-friendly language that homeowners or non-technical stakeholders can understand — reducing confusion, callbacks, and price objections. | ~15 min/estimate |
| Homeowner Update Drafter | Draft clear, plain-language project updates for homeowners and residential clients during a remodel, custom build, or occupied renovation — tuned for the situation (weekly progress, delay notification, change order preview, site access request, punch list close-out) and in the company's voice. | ~20 min/update |
| Change Order Drafter | Document scope changes with cost and schedule impact for owner approval. | ~25 min/CO |
| Contract Risk Reviewer | Analyze a construction contract (prime contract, subcontract, or purchase order) and produce a plain-language risk summary that flags problematic clauses, missing protections, and compliance gaps — so the user can negotiate or escalate before signing. | ~30 min/contract |
| Pay Application Reviewer | Review a construction pay application (AIA G702 cover sheet and G703 continuation sheet, or equivalent custom forms) and flag math errors, inconsistent percent-complete values, retainage miscalculations, missing lien waivers, stored-material documentation gaps, and contract-term conflicts — before it goes to the owner, lender, or GC for certification. | ~40 min/pay app |
| Email Drafter | Turn rough notes, bullet points, or verbal context into a professional, ready-to-send email that matches your company's voice — tailored for common construction communication scenarios. | ~10 min/use |
| Meeting Summarizer | Turn construction meeting notes — whether typed, voice-transcribed, or bullet points — into a structured summary with clear action items, decisions, and follow-ups that can be distributed to stakeholders. | ~15 min/use |
| Review Responder | Craft professional responses to online reviews — both positive and negative. | ~10 min/use |

**Total time saved per use: ~440+ minutes across all skills.**

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
