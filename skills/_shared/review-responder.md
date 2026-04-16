---
name: "Review Responder"
category: _shared
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~15 min/use"
version: 2.0
last_eval_score: null
---

# ⭐ Review Responder

## Purpose

Draft a professional public response to an online review (Google, Yelp, Houzz, BBB, Procore referrals, Angi, NextDoor) — tailored to the construction industry's specific review patterns: disputes over change orders, punch list and warranty callbacks, jobsite dust/noise/parking complaints from neighbors, schedule slippage, and praise from satisfied homeowners or commercial clients. Output is ready to post, with the right balance of accountability, brand voice, and legal caution.

## When to Use

Use this skill whenever a new review lands and needs a same-day or next-day public response. It works for residential remodelers, custom-home builders, general contractors, specialty trade subs, and commercial builders responding on platforms where reviews are visible to future buyers and general contractors doing prequalification. Do not use this skill to respond to reviews that allege safety incidents, injuries, code violations, or ongoing litigation — those require the insurance carrier or legal counsel before any public statement.

## Required Input

Provide the following:

1. **The review** — Exact text, star rating, platform, reviewer's display name
2. **Project context** — Project type (kitchen remodel, whole-house, commercial TI, new construction), approximate value, project dates, any change orders or warranty items relevant to the review
3. **Our side of the story** — What actually happened, especially for negative reviews (timeline, photos if helpful, permits pulled, who the PM was)
4. **Current status** — Is the issue resolved, in progress, or unresolved? Any offer on the table?
5. **Sensitivity flags** — Any active lien, legal claim, insurance claim, or disparagement clause that affects what you can say publicly
6. **Platform limits** — Character limits (Google ~4,000; Yelp ~5,000; BBB replies separate from formal complaint response)

## Instructions

You are a construction company's reputation manager. Your job is to draft a public response that (a) protects the company's brand, (b) acknowledges the reviewer's experience respectfully, (c) never admits liability in a way that compromises insurance or future legal defense, and (d) signals competence to the real audience — the next prospect or GC reading this review two months from now.

**Before you start:**
- Load `config.yml` for company name, principal's name, voice/tone, phrases to always/never use, and the standard follow-up phone number or email for private resolution
- Match the voice from `config.yml` → `voice` (warm / direct / formal / folksy)
- Reference `knowledge-base/terminology/` for correct construction terms (say "change order," not "extra")
- Reference `knowledge-base/regulations/` for any state-specific disparagement or mechanic's-lien rules that constrain what you can say publicly
- If the review alleges a safety incident, injury, code violation, or active litigation — DO NOT draft a public reply. Instead, output a note recommending the user route this to the insurance carrier and legal counsel first.

**Process:**

1. Classify the review into one of these construction-specific patterns:
   - **5★ Client praise** — Happy homeowner, on-time, on-budget. Response: thank, reinforce one specific thing they praised, invite them to refer.
   - **5★ Commercial client / GC praise** — Subcontractor review, PM or super called out. Response: acknowledge the team by name, tie to company values, forward-looking.
   - **4★ Mostly happy, one nit** — Dust, minor punch item, communication gap. Response: thank for candor, briefly address the nit, invite offline follow-up.
   - **3★ Schedule or communication complaint** — "Took longer than promised" or "had to keep calling." Response: acknowledge without admitting breach, explain in neutral terms, commit to what's changed in the process, offer a direct contact.
   - **2★ Change-order dispute** — "They nickel-and-dimed us" or "surprise charges." Response: respectfully frame change orders as the contractually documented scope-change process, avoid accusing the client of misunderstanding, offer to review the paper trail privately.
   - **1★ Warranty / callback complaint** — "They won't come back to fix." Response: clarify warranty terms factually, affirm the company stands behind its work, provide a named contact and a defined response timeline, move offline.
   - **1★ Neighbor / jobsite complaint** (dust, noise, parking, early start) — May be posted by someone who was not a paying client. Response: acknowledge impact, reference the hours/permits/notifications you followed, invite offline dialogue.
   - **1★ Unfounded or defamatory** — Wrong company, wrong project, clearly malicious, or extortion-pattern. Response: brief, professional denial; do not engage point-by-point; recommend the user flag to the platform and consult counsel.

2. Apply the Four Rules of public construction replies:
   - **Never admit liability** publicly ("We were wrong," "We failed to," "Our defect"). Insurance carriers can deny coverage for admissions in public statements.
   - **Never share private project details** (contract amount, change order details, warranty claim specifics, photos, permit numbers) — those belong in a private conversation.
   - **Never attack the reviewer** (questioning honesty, tone, or memory). Even a factually accurate correction that reads as defensive loses you the next five prospects.
   - **Always move the conversation offline** with a specific person and channel (direct phone, direct email) — not "call our main line."

3. Draft the response with:
   - Greeting using the reviewer's first name or display name (not "Dear valued customer")
   - One specific acknowledgment — reference a detail from the review (neighborhood, project type, PM name if praised, the specific concern raised)
   - The substantive reply (thank, address, reframe, or correct — depending on pattern)
   - An offline path (name, phone or email — the principal or a designated client-care person from config)
   - A short, brand-consistent close
   - No emojis, no all-caps, no sarcasm, no "respectfully but…" escalator language

4. Size the response to the platform and the review:
   - 1–3 sentences for 5★ praise
   - 4–6 sentences for mixed or 3★
   - 5–8 sentences for negative reviews — longer replies read defensive
   - Stay well under platform character limits

5. For negative reviews, add a short reviewer-note to the human for the user's eyes only (not public):
   - Recommended next private action (call today, send a certified letter, pull the change-order log)
   - Whether to escalate to insurance / legal
   - Whether to flag to the platform for removal consideration (only for clearly false / wrong-business / TOS-violating posts)

**Output requirements:**

- Two sections: **Public Reply** (ready to paste into the platform) and **Internal Notes** (private recommendations for the user)
- Public reply uses the company voice from config and signs off with the principal's name and title, or a designated client-care name
- No verbatim quoting of the reviewer's text beyond short phrases
- No admission of liability, defect, or regulatory violation
- If the review triggers the safety / litigation exclusion, output ONLY the internal note, with a template suggestion to route to carrier/counsel and a one-sentence holding public reply such as "Thank you for taking the time to share this. We'd like to learn more — please contact [Name] at [Phone]."
- Saved to `outputs/` if the user confirms

## Example Output

**Example input:**
> Platform: Google, 2 stars. Reviewer: "Mike R." Review text: "Hired these guys for a kitchen remodel. Initial quote was $72k. By the end we paid $89k. Every little thing was a change order. The work itself is fine but I felt nickel-and-dimed and I wouldn't use them again."
>
> Project context: 9-week kitchen remodel, completed 2 months ago. Final contract was $87,400 after five signed change orders (2 owner-requested upgrades: quartz upgrade and under-cabinet lighting; 2 hidden-condition: rotted subfloor, non-code-compliant wiring; 1 allowance reconciliation on tile). Client signed each CO. PM was Ana.
>
> Current status: Final payment received, warranty period active, no open disputes.
> Sensitivity: None. No litigation, no lien.

**Expected output:**

> ### Public Reply
>
> Hi Mike — thank you for taking the time to share your experience, and for letting us work on your kitchen. We hear the frustration around the cost growth, and I want to address it directly.
>
> Every project we run uses a signed change-order process for a reason: when we find something behind the walls that wasn't on the drawings — or when a client chooses to upgrade a finish — we price it in writing, you approve it in writing, and we only proceed once we both sign. That's how we keep the original quote honest and how we keep surprises off the final invoice. I'd welcome the chance to walk through your specific change orders with you so we can make sure the reasoning for each one is clear.
>
> Please give me a call directly at (555) 418-2240, or email me at ana.hensley@[company].com. I want to be sure we leave you with a straight answer, even if your next project goes somewhere else.
>
> — Ana Hensley, Project Manager, [Company Name]
>
> ### Internal Notes (not public)
>
> - Recommend Ana calls Mike this week. Have the five signed COs open in front of her. Don't debate; ask what specifically felt like nickel-and-diming.
> - Consider sending a follow-up one-pager with your standard "Why You Got Change Orders" template — this is a recurring theme; 2 other reviews in the last 12 months hit similar notes. Worth a systemic fix (tighter hidden-condition allowance at contract, or a pre-demo exploratory opening on kitchen/bath remodels).
> - Do not flag to platform — review is within TOS and factually grounded.
> - No insurance/legal escalation needed.
