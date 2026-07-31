# Federal Prevailing-Wage (Davis-Bacon) AI Guardrails — Reference

> Reference for skills that draft narrative content on federally funded or
> Davis-Bacon-covered projects (change orders, contract risk reviews, delay
> claims, closeout documentation, lien waivers). Certified payrolls and
> wage-determination decisions are legal disclosures made to a federal
> officer; liability for them is personal to the signer.
>
> This document is not legal advice. Wage-classification disputes and
> certified-payroll discrepancies should be reviewed by counsel or a
> compliance officer familiar with Davis-Bacon and Related Acts (DBRA).

---

## Why This Guardrail Exists

Construction AI drafting tools are now common enough on federal and
prevailing-wage work that the boundary between "AI drafts the narrative"
and "AI touches the wage determination" needs to be explicit, not assumed.
The risk is asymmetric: a narrative error (an awkward change-order
sentence, a slightly-off RFI tone) gets caught at review and re-drafted at
no cost. A wage-classification error or a certified-payroll number that
was auto-populated and not independently verified becomes a federal
compliance finding, a potential False Claims Act exposure, and a personal
liability question for whoever signed the WH-347 — long after the AI
draft that produced it is forgotten.

## The Guardrail

**Narrative generation — AI-assisted drafting is appropriate for:**
- Change-order cover narratives and justifications
- RFI language and submittal review comments
- Contract risk-review flags and counter-proposal letters
- Delay-claim narrative and timeline construction
- Closeout documentation narrative

**Wage and classification decisions — AI should never generate or
auto-populate, only flag for human decision:**
- Certified payroll figures (WH-347) — hours, rates, and classifications
- Wage-determination lookups or classification calls (which DBRA wage
  determination applies, which labor classification a given task falls
  under)
- Fringe-benefit credit calculations
- Apprentice-ratio compliance determinations

## Applying This in a Skill

Any skill that drafts narrative content for a project flagged as
federal / Davis-Bacon-covered (a config or input field naming the project
as federally funded, DBRA-covered, or subject to a state "little
Davis-Bacon" act) should:

1. Draft the narrative content normally — cover letters, justifications,
   RFI text, submittal comments — this is the safe, appropriate use.
2. If the narrative would otherwise need to state a wage rate, a labor
   classification, a certified-payroll number, or an apprentice ratio,
   stop and insert a flag instead of a number: `[WAGE/CLASSIFICATION
   DETERMINATION REQUIRED — route to compliance officer / payroll admin;
   do not auto-populate]`.
3. Never infer a labor classification from a job title or scope
   description and state it as fact — classification is a compliance
   determination, not a narrative-writing task.
4. Keep a version history of any AI-assisted document used on federal
   work, in case a compliance auditor asks how the document was produced.
5. Honesty in any statement made to a federal officer is a legal
   requirement — labeling a document "AI-assisted" is not required by
   prevailing-wage rules, but the underlying content must be accurate and
   human-verified before submission.

## Skills This Applies To

`admin/change-order-drafter.md`, `admin/contract-risk-reviewer.md`,
`admin/delay-claim-drafter.md`, `admin/closeout-documentation-auditor.md`,
`admin/lien-waiver-drafter.md`, and `sales/bid-proposal-generator.md` /
`sales/itb-package-drafter.md` when the project is federally funded or
otherwise DBRA-covered. Each skill's own instructions govern its specific
workflow; this reference is the shared guardrail they point to rather
than each re-deriving it independently.
