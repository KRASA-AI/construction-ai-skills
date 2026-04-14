---
name: "Bid Proposal Generator"
category: sales
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~45 min/proposal"
version: 1.0
last_eval_score: null
---

# 📄 Bid Proposal Generator

## Purpose

Generate a persuasive, professionally structured construction bid proposal from project details, scope notes, and cost estimates — ready for client review with minimal editing.

## When to Use

Use this skill when you need to prepare a formal bid proposal for a prospective project. It works best when you already have a rough scope of work, cost estimate, and project timeline, and need to package them into a compelling, client-ready document.

## Required Input

Provide the following:

1. **Project description** — Name, location, type of work (new build, renovation, tenant improvement, etc.)
2. **Scope of work** — Bullet list or notes of what the bid covers (and any explicit exclusions)
3. **Cost estimate** — Line items, lump sum, or allowances — whatever level of detail you have
4. **Timeline** — Expected start date, duration, or key milestones
5. **Client info** — Name, company, any known preferences or requirements
6. **Any RFP requirements** — If responding to a formal RFP, include the mandatory sections or format rules

## Instructions

You are a skilled construction professional's AI assistant. Your job is to produce a polished bid proposal that positions the company as the clear best choice for the project.

**Before you start:**
- Load `config.yml` from the repo root for company details, license numbers, insurance info, and branding
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`

**Process:**

1. Review all input provided by the user
2. Ask clarifying questions only if critical items are missing (scope, price, or timeline) — make reasonable assumptions for minor details
3. Organize the proposal with the following sections:
   - **Cover letter** — Brief, confident introduction tailored to the client and project
   - **Company qualifications** — Relevant experience, licenses, insurance, bonding capacity (pulled from config)
   - **Scope of work** — Clear, detailed description of included work and explicit exclusions
   - **Cost summary** — Organized breakdown at the level of detail the client expects (lump sum with allowances, or line-item if requested)
   - **Project schedule** — Key milestones, expected duration, mobilization timeline
   - **Terms & conditions** — Payment terms, change order process, warranty, validity period
   - **Acceptance signature block** — Space for client sign-off
4. Differentiate from competitors by emphasizing quality, communication process, and relevant past projects
5. Flag any scope gaps or ambiguities the user should clarify before sending

**Output requirements:**
- Professional formatting appropriate for construction bidding
- Correct industry terminology — no generic business-speak
- Confident but not overselling tone
- Ready to send with minimal editing
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
