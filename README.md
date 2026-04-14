# Auto Repair AI Skills

**Free, open-source AI prompts and workflows built for auto repair shops.** Clone this repo, point your AI assistant at it, and start saving hours every week.

> Built and maintained by [KRASA AI](https://krasa.ai) — free AI tutorials and skills for every industry.
> See all industries at [krasa.ai/industries](https://krasa.ai/industries).

---

## What's Inside

This repo is a complete AI toolkit for auto repair. Every skill is a standalone prompt file that works with **Claude, ChatGPT, or any major AI assistant** — no coding required.

| Skill | What it does | Time saved |
|-------|-------------|------------|
| Diagnostic Troubleshooting Assistant | Guide technicians through a structured, step-by-step diagnostic process based on DTC codes, reported symptoms, and vehicle history — producing a ranked list of probable causes with the fastest confirmation tests for each. | ~15 min/diagnosis |
| Digital Vehicle Inspection Report | Turn tech notes and photos into a customer-friendly inspection report with recommendations. | ~15 min/inspection |
| Parts Lookup Assistant | Help identify the correct part name, type, and OEM/aftermarket part numbers from symptom descriptions — then produce a parts order worksheet that the counter person or technician can use to source parts quickly and accurately. | ~10 min/lookup |
| Declined Services Follow-Up | Turn deferred repairs and declined recommendations into booked appointments by generating personalized, non-pushy follow-up messages that reference the specific work the customer passed on, the safety or cost implications of waiting, and a clear, low-friction path back into the shop. | ~8 min/customer |
| Repair Estimate Builder | Generate a detailed estimate from diagnostic findings with parts, labor, and shop supplies. | ~20 min/estimate |
| Job Status Update Generator | Generate clear, friendly customer-facing text or email messages for each stage of a repair job — from vehicle drop-off through job completion and pickup — so service advisors never have to manually compose status updates. | ~3 min/update |
| Maintenance Reminder Sequence | Generate a personalized, multi-touch reminder sequence (initial, follow-up, final) for scheduled maintenance — based on standard mileage intervals, seasonal services, and customer's last visit — ready to deploy via SMS, email, or both. | ~5 min/batch |
| Review Response Generator | Generate thoughtful, on-brand responses to Google, Yelp, and Facebook reviews of the auto repair shop — whether 5-star praise or 1-star complaints — so the owner or service advisor can reply to every review within 24 hours without writing each one from scratch. | ~4 min/review |
| Service Advisor Script | Draft a clear explanation of recommended repairs that builds trust without overselling. | ~5 min/call |
| Profit Leak Detector | Analyze repair orders, vendor invoices, and parts credits to identify missed revenue, unreturned cores, duplicate charges, and billing gaps that silently erode shop profitability. | ~30 min/review |
| Warranty Claim Preparer | Compile vehicle info, failure details, mileage, service history, and technician narrative into a complete, rejection-resistant warranty claim packet — formatted for manufacturer, extended warranty administrator (e.g., CarShield, Endurance, CNA, Zurich), or parts supplier warranty (e.g., NAPA, AutoZone Duralast, AC Delco). | ~20 min/claim |
| Email Drafter | Turn rough notes into a polished, send-ready email tuned to the specific audience an auto repair shop writes to every day — customers, insurance adjusters, warranty administrators, parts vendors, fleet accounts, manufacturer reps, landlords, regulators, or internal staff. | ~10 min/email |
| Meeting Summarizer | Transform raw meeting notes into structured summaries with clear decisions, action items with owners and deadlines, follow-ups, and parking lot items — designed specifically for auto repair shop operations (daily huddles, production meetings, parts ordering, customer reviews). | ~10 min/use |
| Review Responder (Quick) | Fast, single-pass review replies for the shop's routine review queue — 4–5 star reviews and simple acknowledgments — so the owner can clear a weekly backlog in minutes. | ~3 min/review |

**Total time saved per use: ~158+ minutes across all skills.**

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
