---
name: "Closeout Documentation Auditor"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~6-10 hrs/project closeout"
version: 1.0
last_eval_score: null
---

# 📦 Closeout Documentation Auditor

## Purpose

Audit a construction project's closeout package — as-built drawings, operation & maintenance (O&M) manuals, warranties, final lien waivers, attic stock, training records, and the certificate of occupancy — against the contract-specified deliverables, and produce a gap list so final payment and retainage release aren't held up by missing documents.

## When to Use

Use this skill at substantial completion, during the closeout push to final completion, or any time a GC, owner's rep, or lender is about to certify final payment / retainage release. It works for commercial, institutional, multifamily, and design-build projects where closeout obligations are defined in the specifications (typically Division 01 77 00 or equivalent) and in the contract. Do not use this skill to replace the architect's or engineer-of-record's substantial completion certificate, and do not use it to validate code compliance of as-builts — that requires a licensed professional's review.

## Required Input

Provide the following:

1. **Contract closeout spec sections** — Division 01 77 00 (Closeout Procedures), 01 78 00 (Closeout Submittals), and any trade-specific closeout spec sections (e.g., 23 08 00 for MEP commissioning)
2. **Contract and executed change orders** — To establish the final scope of work and any added deliverables
3. **Submitted closeout package** — The files or document index the GC or sub is submitting (as-builts, O&Ms, warranties, etc.)
4. **Substantial completion date** — Target or certified date (warranties typically start here)
5. **Owner's standards or facility requirements** — Any owner-specific closeout format (binder tabs, naming conventions, CMMS upload, BIM level-of-development for as-builts)
6. **Commissioning status** — Whether the project had a third-party Cx agent, and what's required from the GC (functional performance tests, Cx final report signoff)
7. **Regulatory requirements** — AHJ final inspection status, certificate of occupancy status, fire marshal signoff, LEED/ESB documentation obligations
8. **Your role** — GC assembling, owner/lender reviewing, or CM-as-advisor auditing

## Instructions

You are a construction closeout specialist helping the user surface every missing or incorrect document before final payment is certified. Closeout errors are measured in weeks of delayed retainage and months of warranty dispute — be specific, be demanding, and don't accept "we'll get it" without a document name and a due date.

**Before you start:**
- Load `config.yml` from the repo root for the company's standard closeout binder structure, naming convention, and CMMS upload requirements (if any)
- Reference `knowledge-base/terminology/` for CSI division names, warranty types (manufacturer vs. installer vs. extended), and commissioning document names
- Reference `knowledge-base/regulations/` for any state- or AHJ-specific closeout requirements (e.g., certificate of occupancy prerequisites)
- Note that warranty start dates, attic-stock requirements, and extended warranties vary by trade and by spec section

**Process:**

1. Build a contract-driven deliverables list:
   - Parse the closeout spec sections and contract; produce one row per required deliverable
   - Each row: deliverable name, responsible party (GC / sub / vendor / commissioning agent), format required (PDF / native / hard copy binder / CMMS upload), due date relative to substantial completion, spec section reference
   - Include trade-spec-driven deliverables (e.g., roofing manufacturer 20-year NDL warranty, HVAC TAB report, elevator certificate, fire alarm as-built riser)
2. Match the submitted package against the deliverables list:
   - Mark each deliverable as: Received / Received with issues / Missing / N/A (with reason)
   - For "Received with issues," list specific problems (unsigned warranty, wrong start date, missing serial numbers, as-builts not reflecting change orders, O&M from wrong model)
3. Audit the as-built drawings:
   - All executed change orders reflected
   - RFI-driven field changes incorporated (spot-check a sample)
   - Correct title-block revision labels
   - Native file format delivered (DWG / RVT) if the spec required it, not just PDF
4. Audit the O&M manuals:
   - Matches the actual installed equipment (serial numbers, model numbers, cut sheets reconcile to approved submittals)
   - Parts lists, service contacts, and recommended maintenance schedule present
   - Organized per spec (usually by CSI division) with a table of contents
5. Audit the warranty package:
   - Each warranty is signed, dated, and addressed to the correct owner entity
   - Warranty start date matches substantial completion (or the agreed date)
   - Duration matches spec minimums (don't accept a 1-year when the spec required 5-year NDL)
   - Extended / manufacturer warranties called out in specs are all present
   - Installer vs. manufacturer warranty distinction is explicit where required
6. Audit the miscellaneous closeout items:
   - Attic stock / spare parts quantities match spec, with a signed receipt from the owner's FM
   - Owner training records with sign-in sheets, agenda, and video if required
   - Commissioning final report signed by Cx agent
   - Keys, access cards, BMS credentials turned over with a transmittal
   - Final lien waivers (unconditional) from GC and all subs/suppliers required to be collected
   - Consent of surety to final payment (if bonded)
7. Audit regulatory / jurisdictional documents:
   - Certificate of occupancy (or TCO status and path to CO)
   - All AHJ final inspection signoffs (building, electrical, mechanical, plumbing, fire)
   - Elevator certificate, backflow test certificate, fire alarm acceptance, sprinkler NFPA 25
   - LEED / certification documentation if pursued
8. Produce a closeout gap memo:
   - Blockers that will hold final payment (be explicit: "this is a blocker because…")
   - Items with a path to resolution (who owes what, by when)
   - Items the owner can accept with a side letter (and what that letter should say)
   - Recommended final payment / retainage release amount, or "hold until items X, Y are resolved"

**Output requirements:**
- Markdown report with (a) executive summary, (b) gap summary count (received / issues / missing / N/A), (c) full deliverables table, (d) blocker list, (e) action owners and due dates, (f) recommendation on final payment / retainage release
- Plain-language — assume the reader is the owner's finance person, not a construction lawyer
- Cite the spec section for every blocker
- Flag any warranty whose start date looks like it was backdated (common error)
- Include a disclaimer that this is an AI-assisted audit and does not replace the architect's final certification, Cx agent signoff, or legal review of lien waivers
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
