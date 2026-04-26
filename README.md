# Auto Repair AI Skills

**Free, open-source AI prompts and workflows built for auto repair shops.** Clone this repo, point your AI assistant at it, and start saving hours every week.

> Built and maintained by [KRASA AI](https://krasa.ai) — free AI tutorials and skills for every industry.
> See all industries at [krasa.ai/industries](https://krasa.ai/industries).

---

## What's Inside

This repo is a complete AI toolkit for auto repair. Every skill is a standalone prompt file that works with **Claude, ChatGPT, or any major AI assistant** — no coding required.

| Skill | What it does | Time saved |
|-------|-------------|------------|
| ADAS Calibration Documenter | Turn a repair order, estimate, or inspection note into a structured ADAS-calibration documentation packet — identifying which Advanced Driver Assistance Systems are likely to require calibration based on the work performed, citing the OEM position statements and service procedures that trigger the requirement, and producing a clean paper trail the shop can attach to the RO for insurance billing, liability protection, and customer communication. | ~20 min/RO + reduced rework exposure |
| Diagnostic Troubleshooting Assistant | Guide technicians through a structured, step-by-step diagnostic process based on DTC codes, reported symptoms, and vehicle history — producing a ranked list of probable causes with the fastest confirmation tests for each. | ~15 min/diagnosis |
| Digital Vehicle Inspection Report | Turn a technician's raw inspection notes, measurements, and photo references into a structured, customer-ready Digital Vehicle Inspection (DVI) report — with a red/yellow/green severity schema, plain-language findings, specific measurements, photo captions, recommended action tiers, and a prioritized work plan. | ~15 min/inspection + higher authorization rate |
| Parts Lookup Assistant | Translate a technician's symptom description or verified diagnosis into a clean, counter-ready parts order worksheet — with correct part name, OE and aftermarket part number patterns, fitment warnings for trim/engine/drive variations, supersession flags, a related-parts-usually-replaced-together list, a vendor sourcing plan mapped to the shop's preferred suppliers, and the labor-op code that will feed the Repair Estimate Builder. | ~15 min/lookup + fewer wrong-part returns |
| Technician Onboarding SOP Generator | Turn the tribal knowledge locked in a senior technician's head into a written, repeatable Standard Operating Procedure that a new hire or apprentice can follow without shoulder-surfing. | ~2-3 hours/SOP authored |
| Declined Services Follow-Up | Turn deferred repairs and declined recommendations into booked appointments by generating personalized, non-pushy follow-up messages that reference the specific work the customer passed on, the safety or cost implications of waiting, and a clear, low-friction path back into the shop. | ~8 min/customer |
| Repair Estimate Builder | Turn verified diagnostic findings and a technician's job plan into a clean, itemized, customer-ready repair estimate — with parts, labor, sublet, shop supplies, tax, disclaimers, warranty terms, and optional tiered pricing (required / recommended / deferred). | ~20 min/estimate + fewer billing disputes |
| AI Phone Receptionist Script | Generate the full system prompt, conversation-flow tree, and escalation rules for an AI voice or SMS receptionist that answers every inbound call to the shop 24/7 — capturing appointment requests, qualifying emergencies, collecting vehicle and customer details, and handing off cleanly to a human advisor when the situation requires judgment. | ~$108k/yr recovered per shop (industry benchmark) |
| Bilingual Customer Message Builder | Produce parallel English + Spanish versions of any shop-to-customer message — appointment confirmations, status updates, estimate approvals, declined-work follow-ups, pickup-ready notices, review requests, or bad-news calls about hidden damage — in tone, terminology, and register that a native US-Spanish-speaking customer would actually use. | ~8 min/bilingual message |
| Fleet Account Service Advisor | Turn a single open RO (or a batch of open ROs for the same fleet account) into the complete B2B communications package the shop needs to run that account cleanly: an approval request to the fleet's maintenance decision-maker (with a clear recommended action and the cost delta against the account's authorization threshold), status updates routed to the right fleet contact (not the driver), a consolidated multi-vehicle weekly report, and an exception / escalation note for anything outside the account's routine-approval rules. | ~20 min per fleet RO |
| Job Status Update Generator | Generate clear, friendly customer-facing text or email messages for each stage of a repair job — from vehicle drop-off through completion and pickup — so service advisors never have to compose status updates from scratch and customers always know where their vehicle stands. | ~3 min/update |
| Maintenance Reminder Sequence | Generate a personalized, multi-touch reminder sequence (initial, follow-up, final) for scheduled maintenance — based on standard mileage intervals, seasonal services, and customer's last visit — ready to deploy via SMS, email, or both. | ~5 min/batch |
| Parts Price Change Communicator | Write clear, calm, and respectful customer messages when parts costs change between estimate and invoice — whether because of tariff pass-through, a vendor price increase, a superseded part number, a backorder substitution, or an OEM-vs.-aftermarket swap. | ~10 min/affected customer |
| Review Response Generator | Generate thoughtful, on-brand responses to Google, Yelp, and Facebook reviews of the auto repair shop — whether 5-star praise or 1-star complaints — so the owner or service advisor can reply to every review within 24 hours without writing each one from scratch. | ~4 min/review |
| Safety Recall Outreach Builder | Turn an open NHTSA or OEM safety recall (or a list of open recalls across the shop's active customer database) into a complete, compliance-safe multi-touchpoint outreach sequence: an initial SMS + email on Day 0, a voicemail drop on Day 1–2, a follow-up text at Day 4, a follow-up email at Day 7, a final text at Day 14, and a monthly nudge thereafter until the recall is closed or the customer explicitly opts out. | ~25 min per recall campaign |
| Service Advisor Script | Draft the exact words a service advisor should use when presenting diagnostic findings and recommended work to a customer — structured as a live phone or in-person script, not a written estimate. | ~5 min/call + higher authorization rate |
| Collision Supplement Documenter | Turn a teardown finding (hidden damage revealed after disassembly of a visibly damaged area) plus the original estimate plus a set of timestamped teardown photos into a clean, insurer-ready supplement request: line items with correct operation descriptions, labor times cited to the published labor guide (CCC, Mitchell, Audatex), parts cited with source and price, a cause-and-effect narrative tying the impact pattern to the hidden damage, an OEM-position-statement citation line for every structural or safety-system component, a photo index keyed to each line item, and a carrier-specific formatting variant (State Farm Select Service, GEICO ARX, Progressive DRP, Allstate Good Hands, Nationwide Blue Ribbon, Farmers Circle of Dependability, USAA Preferred, or non-DRP). | ~35 min per supplement + fewer rejection round-trips |
| Profit Leak Detector | Audit a batch of closed repair orders, vendor invoices, credit memos, labor timecards, and sublet receipts to surface the money the shop is quietly leaving on the table — unreturned cores, missed vendor credits, duplicate charges, unbilled labor, missing shop supply fees, under-marked-up sublet, warranty-rate shortfalls, and diag-fee write-offs. | ~45 min/review + recovered revenue the shop would have missed |
| Technician Recruiting Outreach Builder | Turn a shop's open-bench state (who you need, why, by when) into a complete multi-touchpoint recruiting package for one candidate or one role: a cold first-touch message, 2–3 follow-ups spaced over 10–14 days, a shop-culture job posting, an interview invitation and interview follow-up, and a working-interview / ride-along invitation. | ~45 min per candidate pipeline |
| Warranty Claim Preparer | Compile vehicle info, failure details, mileage, service history, and technician narrative into a complete, rejection-resistant warranty claim packet — formatted for manufacturer, extended warranty administrator (e.g., CarShield, Endurance, CNA, Zurich), or parts supplier warranty (e.g., NAPA, AutoZone Duralast, AC Delco). | ~20 min/claim |
| Email Drafter | Turn rough notes into a polished, send-ready email tuned to the specific audience an auto-repair shop writes to every day — customers, insurance adjusters, warranty administrators, parts vendors, fleet accounts, manufacturer reps, landlords, regulators, or internal staff. | ~10 min/email |
| Meeting Summarizer | Transform raw meeting notes — voice-memo transcript, advisor handwriting, foreman bullet points — into a structured summary with clear decisions, action items with named owners and concrete deadlines, follow-ups, and parking-lot items. | ~10 min/use |
| Review Responder (Quick) | Fast, single-pass review replies for the shop's routine review queue — 4-star and 5-star reviews and simple acknowledgments — so the owner, manager, or marketing coordinator can clear a weekly stack in one short session. | ~3 min/review · full weekly queue in one session |

**Total time saved per use: ~341+ minutes across all skills.**

## Quick Start

### 1. Clone this repo

```bash
git clone https://github.com/KRASA-AI/auto-repair-ai-skills.git
cd auto-repair-ai-skills
```

### 2. Open a skill with your AI assistant

Open any file in `skills/` with Claude, ChatGPT, or any major AI assistant. Each skill is a self-contained prompt with clear instructions — no coding required.

The first time you use a skill, your AI assistant will ask for your business details (company name, service area, rates, tools you use, etc.) so it can personalize the output. Save those details to a `config.yml` at the repo root and every future skill will use them automatically.

## Repo Structure

```
auto-repair-ai-skills/
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

- **Auto Repair AI guide**: [krasa.ai/industries/auto-repair](https://krasa.ai/industries/auto-repair)
- **All industry AI skills**: [krasa.ai/industries](https://krasa.ai/industries)
- **About KRASA AI**: [krasa.ai](https://krasa.ai)

## License

MIT — use these skills however you want.
