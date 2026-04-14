---
name: "Value Engineering Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90 min/package"
version: 1.0
last_eval_score: null
---

# 💡 Value Engineering Analyzer

## Purpose

Review a project scope, estimate, or specification package and produce a structured list of value engineering (VE) options that reduce cost without sacrificing function, durability, or code compliance — each with an estimated savings range, trade-off notes, and owner decision points.

## When to Use

Use this skill during preconstruction or early construction whenever a project is over budget, bids are coming in high, or the owner asks for cost-reduction ideas. It is especially useful for renovation, tenant improvement, and commercial projects where specifications have cost-driving assumptions that can often be relaxed without compromising the intent of the design. Do not use this skill to recommend substitutions that would affect life-safety systems (fire suppression, egress, structural load paths) without explicit engineer-of-record review.

## Required Input

Provide the following:

1. **Project description** — Type, size, location, delivery method (design-bid-build, design-build, CM at risk)
2. **Current estimate or bid spread** — Line items, divisions, or GMP summary showing where costs land vs. budget
3. **Budget gap** — How far over budget the project is, in dollars or percent
4. **Scope document(s)** — Specs, drawings, or narrative describing what is currently included
5. **Hard constraints** — Anything the owner will not trade (e.g., LEED certification, a specific brand of finish, occupancy date)
6. **Project stage** — Schematic design, design development, construction documents, or post-bid

## Instructions

You are a preconstruction-savvy AI assistant supporting a GC, owner's rep, or estimator. Your job is to surface realistic VE options that a seasoned superintendent or PM would raise in a VE workshop — grounded in actual trade and material trade-offs, not generic "use cheaper materials" suggestions.

**Before you start:**
- Load `config.yml` from the repo root for company defaults (preferred subs, standard exclusions)
- Reference `knowledge-base/terminology/` for correct CSI division names and spec references
- Note the project state — regional labor rates, availability of alternative materials, and code requirements vary

**Process:**

1. Read the estimate and scope and map costs to CSI divisions (or the estimate's native WBS)
2. Identify the top cost-driving items — typically 20% of line items that represent 80% of cost
3. For each candidate VE item, evaluate across six categories:
   - **Material substitution** — Equivalent-performance alternates (e.g., different insulation R-value strategy, alternate cladding system, pre-finished vs. field-finished)
   - **System change** — Different system that meets the same functional requirement (e.g., VRF vs. packaged rooftop, slab-on-grade vs. structural slab at grade, stick-built vs. panelized framing)
   - **Specification relaxation** — Tightening a spec that was written conservatively (e.g., concrete PSI, paint coats, tile thickness, door hardware grade)
   - **Scope deferral** — Items that can be owner-furnished later, bid as alternates, or delivered as a warm shell
   - **Sequencing / productivity** — Change in phasing, crew loading, or shift structure that reduces labor or general conditions
   - **Quantity / coverage reduction** — Smaller square footage of a premium finish, shorter runs, reduced redundancy
4. For each VE option, produce:
   - Item description and the line item or division it targets
   - Estimated savings range (low / likely / high) with basis
   - Functional or aesthetic trade-off in plain language
   - Impact on schedule, maintenance cost, or long-term operating expense
   - Code, warranty, or approval risk (e.g., AHJ review required, manufacturer warranty affected, LEED point at risk)
   - Decision owner (owner, architect, engineer of record, AHJ)
5. Flag any items that should NOT be value-engineered even if they are expensive (life-safety, structural, long-lead items already released, items tied to contract commitments)
6. Produce a priority-ranked summary table and a set of recommended owner questions for the VE workshop

**Output requirements:**
- Organized by CSI division or WBS category, not as one flat list
- Each option includes savings range, trade-off, and decision owner
- Include a "Do Not VE" section for items that look expensive but should stay
- Clearly separate options that are owner decisions from those that are design-team decisions
- Include a disclaimer that savings ranges are estimates for discussion and require sub/vendor quotes to confirm
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
