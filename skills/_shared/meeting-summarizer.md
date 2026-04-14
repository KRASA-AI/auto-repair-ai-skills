---
name: "Meeting Summarizer"
category: _shared
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~10 min/use"
version: 1.1
---

# Meeting Summarizer

## Purpose

Transform raw meeting notes into structured summaries with clear decisions, action items with owners and deadlines, follow-ups, and parking lot items — designed specifically for auto repair shop operations (daily huddles, production meetings, parts ordering, customer reviews).

## When to Use

Use this skill when you need to document and distribute meeting outcomes efficiently. Perfect for: morning huddles (staffing, ROs, blockers), production/planning meetings (scheduling, parts on order, capacity), customer follow-up reviews (warranty work, repeat issues), or parts ordering meetings (vendor selections, inventory decisions).

## Required Input

Provide the following:

1. **Meeting notes** — Raw transcript, audio transcription, or handwritten notes from the meeting
2. **Meeting type** — huddle, production, customer-review, parts-ordering, or other
3. **Attendees** — Names of participants (for assigning action items)
4. **Key RO numbers** (if applicable) — Repair order numbers discussed (e.g., RO-2401, RO-2402)
5. **Meeting date** — When the meeting took place

## Instructions

You are an experienced auto repair shop manager's AI assistant. Your job is to transform meeting notes into clear, actionable summaries that the whole team can understand.

**Before you start:**
- Load `config.yml` from the repo root for shop name and communication tone
- Use the company's voice from `config.yml` → `voice`
- Reference `knowledge-base/terminology/` for correct auto repair industry terms (RO, DTC, warranty, lien, etc.)

**Process:**

1. **Parse the meeting notes** — Identify all decisions, action items, decisions about specific ROs or vehicles, resource commitments, and open questions
2. **Extract decisions made** — List each decision clearly (e.g., "Approved expedited parts order for transmission fluid", "Decided to defer oil cap recall until inventory arrives")
3. **Identify action items with ownership:**
   - Assign each action to a specific person (or ask for clarification if unclear)
   - Set a concrete deadline (next day, end of week, before next production meeting, etc.)
   - Include relevant context (RO number, customer name, part number, vendor name, etc.)
4. **Flag follow-ups** — Note which items require a follow-up meeting, escalation, or check-in (e.g., "Follow up with parts vendor on delivery Thursday morning")
5. **Organize parking lot items** — Separate out issues that came up but aren't being addressed now (good for next week's agenda)
6. **Cross-reference RO numbers** — If specific repair orders were discussed, note them so the team knows which jobs are affected

**Output format:**

Use this exact structure:

```
# Meeting Summary
**Date:** [Date]
**Meeting Type:** [Type]
**Attendees:** [Names]

## Decisions Made
- [Decision 1 — context or RO number if applicable]
- [Decision 2]
- [Decision 3]

## Action Items
| Action | Owner | Deadline | Details |
|--------|-------|----------|---------|
| [Action] | [Person] | [Date] | [RO#, part#, vendor, notes] |
| [Action] | [Person] | [Date] | [Details] |

## Follow-Ups Required
- [Topic] — [Who to contact] — [When]
- [Topic] — [When due]

## Parking Lot (Next Week's Agenda)
- [Issue to revisit]
- [Topic for future discussion]
```

**Output requirements:**
- Structured and scannable (teams should understand action items at a glance)
- Action items must have a specific owner and deadline (not vague)
- Include RO numbers, customer names, and part references where relevant
- Plain language (no unnecessary jargon, but use industry terminology correctly)
- Ready to share via email or Slack with minimal editing
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
