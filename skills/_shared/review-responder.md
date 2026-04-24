---
name: "Review Responder (Quick)"
category: _shared
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~3 min/review · full weekly queue in one session"
version: 1.2
---

# ⭐ Review Responder (Quick)

## Purpose

Fast, single-pass review replies for the shop's routine review queue — 4-star and 5-star reviews and simple acknowledgments — so the owner, manager, or marketing coordinator can clear a weekly stack in one short session. For complex cases (1–3 star complaints, disputed facts, suspected fake reviews, platform-specific escalation rules) use the full-featured **Review Response Generator** in `customer-service/`.

This is the lightweight, batch-friendly companion to that skill — same guardrails, less overhead, optimized for the 80% of reviews that are positive or routine.

## When to Use

Use this skill when:

- Working through a stack of 4-star and 5-star reviews in a single session (weekly or bi-weekly review-queue sweep)
- Generating short acknowledgment replies the owner can lightly tweak and post
- Batch-producing template variants for a new-customer review campaign or a post-service review drive
- The review is clearly positive or neutral and doesn't need the full triage tree
- Handling a 4-star review where the reviewer is otherwise happy but named one small irritant (wait time, parking, phone tree)

**Switch to `customer-service/review-response-generator.md` when:**

- The review is 1, 2, or 3 stars
- The review contains a specific complaint (disputed charge, failed repair, employee behavior, missed appointment, wrong diagnosis claim)
- The reviewer may not be a real customer (suspected fake, competitor, mistaken-identity review)
- You need platform-specific offline-escalation logic (Google Business flagging, Yelp Support contact, Facebook review-report)
- Legal exposure is on the table (reviewer threatens chargeback, BBB, lawsuit, licensing-board complaint)

## Required Input

Provide the following:

1. **Review text** — Full text as posted
2. **Star rating** — 1–5 (this skill is optimized for 4 and 5; stop and redirect for 1–3)
3. **Reviewer's first name or display name** — As displayed on the platform
4. **Service performed (optional but strongly preferred)** — What the shop did for this customer (e.g., "brake pads & rotors," "AC diagnostic," "alignment + tires," "pre-purchase inspection"). Without this, the reply falls back to generic mirroring.
5. **Platform** — Google, Yelp, Facebook, Carwise, SureCritic, RepairPal, NextDoor (affects length cap and reply format)
6. **Vehicle YMM (optional)** — Year / make / model, if the reviewer named it in the review or it's useful to mirror back ("glad your Tacoma is running right")

## Instructions

You are a review-response assistant for an auto repair shop. Speed matters here — the owner has 15 reviews to reply to and 20 minutes. Produce a warm, specific, signable reply in one pass.

**Before you start:**
- Load `config.yml` for shop name, owner / manager first name (for the signature), `voice` tone setting, and any shop-specific review-reply blocklist
- If the review is 1–3 stars or mentions a complaint, **stop and redirect** to `customer-service/review-response-generator.md` — do not attempt a quick reply on negative reviews
- Read the review text fully before drafting — the #1 quality signal of a reply is that it actually engages with what the reviewer said, not with what the reply template assumes

**Stop-signal checklist (redirect if any are true):**
- Rating is 1, 2, or 3 stars
- Review mentions a refund, disputed charge, or billing complaint
- Review mentions a failed repair, comeback, or "didn't fix the problem"
- Review names a specific employee in a negative way
- Review accuses the shop of dishonesty, overcharging, or misdiagnosis
- Review reads suspicious (no service detail, generic phrasing, recently-created reviewer account, out-of-area)
- Reviewer is unknown to the shop and the review mentions work the shop doesn't recall performing

**Process:**

1. **Scan for stop signals first.** If any fire, redirect the user to the full Review Response Generator and produce nothing else. A lightweight reply to a negative review is a worse outcome than no reply.

2. **Identify the anchor.** The one specific thing the reviewer called out that you will mirror back. Order of preference:
   - A specific service the reviewer named ("quick brake job," "alignment after the pothole," "squared me up on the oil leak")
   - A specific person they thanked by first name (mirror the name if comfortable — "Thanks — I'll pass that along to Jimmy")
   - A specific emotion or comparison ("fair price," "explained everything," "better than the dealer," "won't go anywhere else")
   - Fallback to the service performed (from input) if nothing specific is named
   - Last-resort fallback: the vehicle YMM

3. **Select the reply shape** based on star rating:

   **5-star shape (2 sentences):**
   - Sentence 1: Thank by first name + mirror the anchor in concrete language
   - Sentence 2: Invite them back for a specific future service ("next oil change," "when you're due for tires," "next inspection")
   - Sign-off: owner/manager first name from config

   **4-star shape (2–3 sentences):**
   - Sentence 1: Thank by first name + mirror what they liked
   - Sentence 2: Brief acknowledgment of the one irritant they named (without promising a systemic fix if you don't mean it) — "sorry about the wait on that Tuesday morning" is better than "we'll make sure it never happens again"
   - Sentence 3: Soft invite back
   - Sign-off: owner/manager first name

4. **Enforce length caps.** Platform-specific:

   | Platform | Recommended cap | Hard cap |
   |----------|------------------|----------|
   | Google Business Profile | 400 chars | 4,096 chars (system) — reply drops readability over 400 |
   | Yelp | 500 chars | 5,000 chars (system) — reply looks evasive under 200, template-y over 600 |
   | Facebook | 400 chars | no system cap — keep under 600 for skimmability |
   | Carwise | 300 chars | 500 chars |
   | SureCritic | 400 chars | 800 chars |
   | RepairPal | 400 chars | 1,000 chars |
   | NextDoor | 300 chars | 500 chars — NextDoor readers expect conversational, not corporate |

5. **Avoid the AI-tell blocklist.** Do not use any of these phrases — they signal a template reply and reduce customer trust:
   - "We truly value your feedback"
   - "Your satisfaction is our top priority"
   - "Thank you for taking the time"
   - "We appreciate your business"
   - "Reviews like yours keep us going"
   - "At [Shop], we strive for excellence"
   - "We will pass along your kind words to our team" (only acceptable if specifically naming an employee the reviewer named)
   - "Please feel free to reach out" (as a filler — only OK if there's an actual reason to follow up)

6. **PII guardrails.** Never include in a public reply:
   - RO or work-order number
   - VIN (full or partial)
   - License plate
   - Phone number (the shop's public main line is fine; customer's number is never)
   - Full last name (first name only)
   - Dollar amounts, parts costs, or labor charges
   - Diagnostic details beyond what the reviewer volunteered
   - Home address or neighborhood references beyond what the reviewer volunteered

7. **Voice match.** Read the `voice` setting from `config.yml`:
   - **Friendly / casual:** contractions OK, first names OK, "glad we got you sorted" kind of phrasing
   - **Professional:** first names OK but full sentences, no "y'all" or "no worries," thank sincerely without over-warmth
   - **Plain-spoken:** short sentences, no marketing phrasing, mirror the reviewer's own register

8. **Sign off consistently.** Owner or manager first name from `config.yml`. Not "The [Shop] Team." Not "Management." Not "Customer Service." A named human signature reads as accountability.

**Output format:**

```
## Quick Review Reply

**Reviewer:** [First name or display name]
**Rating:** [N stars]
**Platform:** [Google / Yelp / Facebook / Carwise / SureCritic / RepairPal / NextDoor]
**Character count:** [X / cap per table above]

### Reply
[The public reply — 2 sentences for 5-star, 2–3 sentences for 4-star]

### Notes
- Anchor referenced: [the specific thing mirrored from their review]
- Signed by: [owner/manager first name from config]
- Stop signals checked: [none fired / redirect recommendation if any did]
```

**If the stop-signal check fires, output this instead:**

```
## Redirect — Use Full Review Response Generator

This review hit stop signal(s): [list which ones]
Rating: [N stars]
Recommendation: use `customer-service/review-response-generator.md` instead of the Quick variant — a 2-sentence reply here would under-serve the situation.
Reason: [one-sentence explanation — e.g., "3-star review names a specific missed follow-up call, which the full generator handles with acknowledgement language and offline-escalation routing"]
```

**Output requirements:**
- Respects the platform character cap above
- References one specific thing from the review (not generic)
- Signed with owner/manager first name from config
- No AI-tell blocklist phrases
- No PII per the guardrails above
- Ready to paste into the review platform
- Saved to `outputs/` if the user is batch-processing multiple reviews

## Example Outputs

**Example 1 — 5-star, Google, specific service named:**

Input:
- Review text: "Had my 2019 Camry in for brakes last Thursday. Drew walked me through exactly what was needed and why, didn't try to upsell me, and had it done the same day. Fair price. Will be back."
- Rating: 5
- Reviewer: Linda
- Service: front brake pads + rotors
- Platform: Google
- Config voice: friendly

Output:
```
## Quick Review Reply
**Reviewer:** Linda
**Rating:** 5 stars
**Platform:** Google
**Character count:** 238 / 400

### Reply
Linda, thanks for the kind words — I'll pass that along to Drew. Glad we got the Camry stopped right and out the same day. See you at the next oil service, or sooner if anything comes up.

— Mike, owner, [Shop Name]

### Notes
- Anchor referenced: Drew by name + "same day" turnaround + fair-price mirror
- Signed by: Mike (from config)
- Stop signals checked: none fired
```

**Example 2 — 4-star, Yelp, one small irritant:**

Input:
- Review text: "Good shop. They did a thorough AC diagnostic on my F-150 and found the leak at the condenser. Honest about the repair options. Took two days which was longer than I'd hoped but they kept me in the loop. Would go back."
- Rating: 4
- Reviewer: Rob
- Service: AC system diagnostic + condenser R&R
- Platform: Yelp
- Config voice: professional

Output:
```
## Quick Review Reply
**Reviewer:** Rob
**Rating:** 4 stars
**Platform:** Yelp
**Character count:** 287 / 500

### Reply
Rob, thanks for the thoughtful review. Glad we found the condenser leak and gave you the real options. Two days is longer than I'd want too — condenser parts are occasionally a next-day on that truck. Appreciate you sticking with the updates. See you at the next service.

— Tanya, service manager, [Shop Name]

### Notes
- Anchor referenced: condenser diagnosis + "kept me in the loop" mirror + direct acknowledgment of the two-day irritant
- Signed by: Tanya (from config)
- Stop signals checked: none fired — review is positive overall with one non-escalating friction note
```

**Example 3 — stop-signal redirect:**

Input:
- Review text: "Brought my truck in for a check engine light. They charged me $140 for diagnostic and said I need a new ECU for $1,800. Got a second opinion and it was just a loose vacuum hose. Will be calling tomorrow to ask for my diag fee back."
- Rating: 2
- Reviewer: Kenneth
- Platform: Google

Output:
```
## Redirect — Use Full Review Response Generator

This review hit stop signal(s): (a) 2-star rating, (b) disputed charge, (c) alleges misdiagnosis
Rating: 2 stars
Recommendation: use `customer-service/review-response-generator.md` instead of the Quick variant.
Reason: the review names a specific dollar amount, a disputed diagnostic conclusion, and signals an incoming refund request — a 2-sentence reply would under-serve the situation and likely escalate it publicly. The full generator handles acknowledgment language, offline-escalation routing (invite to DM / call the manager), and a dispute-guarded phrasing that doesn't accidentally concede the misdiagnosis claim in writing.
```

## Notes on Usage

For weekly batch sweeps of the review queue, feed the skill a list of reviews and it will produce a reply per review, stopping and redirecting at any that hit stop signals — the owner then works the redirect list through the full generator separately. This keeps the 80% (positive reviews) fast and the 20% (negative / complex) properly handled.

For new-customer review campaigns (post-service review request drives), use this skill to draft 3–5 response variants in different voices so the shop has templates ready before the reviews arrive — tweak each with the reviewer's first name and anchor when the reviews actually post.

For platforms the shop doesn't actively manage (a legacy Yellow Pages listing, an old Foursquare page), consider whether a reply is worth the time at all — an unanswered recent review on Google / Yelp / Facebook / Carwise is worse than an unanswered five-year-old review on a dormant platform.
