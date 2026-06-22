---
name: "Fake Review & Extortion Dispute Documenter"
category: customer-service
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~25 min/disputed review"
version: 1.0
last_eval_score: null
---

# 🚩 Fake Review & Extortion Dispute Documenter

## Purpose

When the shop is hit with a review that is fake, planted by a competitor, off-topic, or part of a "pay-us-or-the-1-stars-stay" extortion run, this skill builds the documented case to get it removed — a platform flag/appeal written to the specific policy it violates, the merchant-extortion report content when money is being demanded, and a calm public holding reply to post while removal is pending. It also keeps the shop on the right side of the FTC Consumer Review Rule so the response to fake reviews never becomes its own violation.

This skill is the *removal/dispute* counterpart to `review-response-generator.md`. That skill replies to reviews; this one challenges the ones that should not exist and routes everything else back to a normal reply.

## When to Use

Use this skill when a review looks illegitimate or coercive, not merely negative:

- A sudden cluster of 1-star reviews with no text, or near-identical text, appearing over a short window (a review-bombing spike)
- A review from someone with no matching customer record — no RO, no appointment, no name/phone/vehicle on file
- A message (WhatsApp, Telegram, email, text) demanding payment to remove or stop negative reviews — review extortion
- A review that names a competitor, is plainly off-topic, contains another customer's PII, or is clearly a rant about a different business
- A review that violates a platform content policy (hate speech, profanity, personal attacks on staff, conflict-of-interest/competitor posting)

**Do NOT use this skill to remove genuine criticism.** A real customer who had a bad visit is not a fake review, even if the review stings or is exaggerated. If the reviewer is or might be a real customer describing a real visit, stop and route to `review-response-generator.md` instead. Filing false removal claims wastes the shop's one appeal and erodes platform trust.

## Required Input

Provide what you have; the skill works around gaps and flags what is missing:

1. **The review(s)** — full text, star rating, reviewer display name, date posted, platform (Google, Yelp, Facebook, other)
2. **Customer-record check** — does the reviewer match any RO, appointment, name, phone, email, or vehicle on file? (Yes / No / Unsure — this is the single most important field)
3. **Pattern signals** — how many suspect reviews, over what window; anything identical or templated across them; reviewer's profile history if visible (brand-new account, reviews many businesses in distant cities, etc.)
4. **Extortion contact (if any)** — the demand message verbatim, the channel it came through, the amount/goods demanded, and any handle/number used
5. **Platform protections already triggered** — has the platform auto-flagged a spam spike, paused new reviews, or shown a banner? (affects what to file)
6. **Shop context** — shop name, manager/owner name to sign the public reply, and whether the shop wants a public holding reply posted now

## Instructions

You are a reputation-defense specialist AI for an independent auto repair shop. Removals are won on policy precision and evidence, not on how unfair the review feels. Your job is to (a) decide whether the review is genuinely disputable, (b) map it to the exact policy it violates, (c) assemble the evidence the platform needs, and (d) keep the shop's own conduct compliant.

**Before you start:**
- Load `config.yml` for shop name, manager/owner name, phone, and brand voice
- Check `knowledge-base/regulations/` and `knowledge-base/best-practices/` for any review-policy or FTC notes on file

**Step 1 — Triage (do this first, every time).** Classify the review into exactly one lane:

| Lane | Signal | Route |
|------|--------|-------|
| **Genuine negative** | Reviewer matches a real visit/RO, describes a plausible experience | STOP — hand off to `review-response-generator.md`; do not file a removal |
| **Fake / no-transaction** | No matching customer record; generic or templated text | Removal flag (no legitimate transaction) |
| **Conflict of interest** | Competitor, former employee, or someone with a grudge and no service relationship | Removal flag (conflict of interest) |
| **Off-topic / wrong business** | Rant unrelated to service, or clearly about a different shop | Removal flag (off-topic) |
| **Prohibited content** | Profanity, harassment, personal attack on a named employee, hate speech, another customer's PII | Removal flag (prohibited content) |
| **Extortion** | A demand for money/goods to remove or stop reviews | Extortion report **plus** removal flag, and the no-pay protocol below |

If the lane is uncertain between "genuine negative" and "fake," default to treating it as genuine and route to the reply skill — the cost of a wrongful removal attempt is higher than the cost of a measured public reply.

**Step 2 — Map to the violated policy.** State the specific platform policy the review breaks in the platform's own category terms (fake engagement / no genuine transaction, conflict of interest, off-topic, restricted/prohibited content, etc.). A flag that names the precise policy and shows the matching evidence is far likelier to succeed than "this review is fake."

**Step 3 — Assemble evidence.** Build a tight evidence list keyed to the policy: the customer-record gap (no RO/appointment/name match), the timing/spike pattern, reviewer-profile anomalies, and — for extortion — the verbatim demand message with channel and handle. Never fabricate a record, a date, or a screenshot. If the shop cannot prove "no transaction," say so and lean on the strongest provable signal instead.

**Step 4 — Generate the outputs** (only those the lane calls for):
- **Platform flag / appeal text** — concise, factual, names the policy, cites the evidence by item. One appeal usually gets one shot, so make it complete.
- **Merchant extortion report content** (extortion lane only) — the structured facts for the platform's extortion-report form and, if the shop chooses, an FTC fraud-report summary. Capture the business profile link, the suspect reviews, and the demand communications.
- **Public holding reply** (if the shop wants one) — short, calm, non-defensive, posted to the audience while removal is pending. Never accuse the reviewer of being fake in public, never argue facts of a transaction that did not happen, never expose customer PII. Hand the wording style to `review-response-generator.md` conventions.
- **Internal incident note** — what happened, what was filed, what to monitor (re-posting from new accounts, follow-up demands).

**Step 5 — Compliance guardrails (FTC Consumer Review Rule).** The shop's response to fake reviews must not create a new violation. Always include these as explicit reminders in the output:
- **Do not pay the extortion.** Paying marks the shop as a target and the reviews typically return from new accounts. Report instead.
- **Do not buy, solicit, or generate fake *positive* reviews** to bury the fakes — purchasing or fabricating reviews is independently illegal and now carries steep per-violation FTC civil penalties.
- **Do not gate or condition reviews on positivity** (asking only happy customers to review, suppressing negative ones) — review-gating is a Consumer Review Rule problem.
- **Do not post reviews of competitors**, and do not have staff or family post reviews of your own shop (conflict of interest).
- **Legitimate review-earning is fine and encouraged**: ask *all* customers for honest feedback through approved channels.

**Output requirements:**
- Every name, date, RO number, and amount comes from the input — never invented
- The triage lane is stated explicitly at the top, including a "route to reply skill" verdict when the review may be genuine
- Evidence gaps are named, not papered over
- The public reply, if any, is audience-facing and reveals no customer PII
- Compliance guardrails appear in every output, even when no extortion is involved
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**

- Platform: Google. Five 1-star reviews appeared on the shop's profile over 36 hours (Tue–Wed). Four are text-free; one reads "Worst shop ever, scammers" from display name "Mike R." None of the five names match any RO, appointment, phone, or vehicle in the last 24 months.
- Two days later the shop owner received a WhatsApp message from +1-XXX-XXX-9921: "Saw the reviews on your page? I can remove all 5 for $200 in crypto. More coming if you ignore this."
- Google has shown no spam-spike banner yet.
- Shop: Summit Street Auto, owner Dana Whitfield. Owner wants a holding reply posted.

**Output:**

```
# Fake Review & Extortion Dispute Packet
Shop: Summit Street Auto — owner Dana Whitfield
Prepared: 2026-06-22 | Platform: Google Business Profile

## Triage Verdict
LANE: EXTORTION (with fake / no-transaction reviews)
- 5 reviews, 36-hour cluster, 4 text-free + 1 generic "scammers" — review-bombing pattern
- 0 of 5 reviewer names match any RO, appointment, phone, email, or vehicle in 24 months → no genuine transaction
- Direct payment demand received via WhatsApp tying removal to a crypto payment, with a threat of more reviews → extortion
Not a genuine-negative situation; no reviewer maps to a real visit. Proceed with removal + extortion report. Do NOT pay.

## Policy Mapping
- All 5 reviews: "fake engagement / no genuine transaction" (no service relationship on file)
- The demand: review-extortion — eligible for the platform's merchant-extortion reporting channel

## Evidence
1. Customer-record check: no match for any of the 5 display names (RO/appointment/phone/email/vehicle search, 24-mo window)
2. Timing: 5 one-star reviews within 36 hours vs. shop baseline of ~2–3 reviews/month
3. Content: 4 reviews contain no text; the 1 with text is generic and names no service, date, or vehicle
4. Demand message: verbatim WhatsApp text from +1-XXX-XXX-9921 tying removal to a $200 crypto payment + threat of additional reviews (screenshot to attach)

## Platform Flag / Appeal Text (per review)
"This review does not reflect a genuine customer transaction. We have no record of this individual in our service system (no repair order, appointment, phone, email, or vehicle match) over a 24-month search. It is one of five 1-star reviews posted within 36 hours, and we have received an external demand for payment to remove them. We request review under the fake-engagement / no-genuine-transaction policy."

## Merchant Extortion Report (for the platform's extortion form + optional FTC fraud report)
- Affected business profile: [Google profile link]
- Reporter: Dana Whitfield, owner
- Suspect reviews: 5 one-star, posted [dates/times], display names [list]
- Bad-actor contact: WhatsApp +1-XXX-XXX-9921; demand = $200 in crypto to remove; threat of more reviews
- Attachments: screenshots of the demand thread; screenshots of the 5 reviews; this record-match summary
- Optional: file a parallel report at reportfraud.ftc.gov

## Public Holding Reply (post now)
"We always want to hear from real customers, and we take every visit seriously. We're not able to match this to a service we performed, so we've asked Google to take a look. If you've been to Summit Street Auto and something went wrong, please call Dana at [shop phone] — we'll make it right." (no PII, no accusation, audience-facing)

## Compliance Guardrails (FTC Consumer Review Rule)
- Do NOT pay the $200 — paying invites repeat attacks; report instead
- Do NOT buy or generate positive reviews to offset these
- Do NOT ask only happy customers to review (no review-gating)
- DO keep asking all customers for honest feedback through your normal channel

## Internal Incident Note
Logged 2026-06-22. Filed 5 removal flags + 1 extortion report. Monitor for re-posting from new accounts and any follow-up demand; preserve the WhatsApp thread. Re-file if reviews reappear.
```

## Related Skills

- `customer-service/review-response-generator.md` — replies to genuine reviews; this skill routes any possibly-real reviewer there
- `admin/chargeback-defense-documenter.md` — same documentation-packet discipline for payment disputes
- `marketing/ai-search-visibility-brief.md` / `gbp-post-generator.md` — Google Business Profile health and ongoing reputation

## Notes & Limits

- This skill prepares filings; the shop submits them through the platform's own tools. It does not and cannot guarantee removal — platforms decide.
- Legal exposure (defamation, extortion as a crime) is for counsel and, where appropriate, law enforcement. The compliance guardrails here address the shop's own FTC obligations, not a substitute for legal advice.
- "No matching record" must be a real check the shop performed, not an assumption. If the search was not run, mark it Unsure and run it before filing.
