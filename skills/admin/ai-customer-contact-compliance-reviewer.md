---
name: "AI Customer-Contact Compliance Reviewer"
category: admin
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~20 min per campaign/script + materially reduced per-message penalty exposure"
version: 1.0
last_eval_score: null
---

# 🎯 AI Customer-Contact Compliance Reviewer

## Purpose

Take any **outbound customer contact the shop is about to send — or any AI voice/chat agent script it is about to deploy — and review it before it goes live** against the four things that actually get shops sued or fined: (1) whether the message is *informational* or *marketing*, and therefore what tier of consent it needs; (2) whether the shop can prove it *has* that consent for the numbers on the list; (3) whether the required disclosures are present (AI identity, call recording, sender identification, opt-out); and (4) whether the opt-out path actually works and gets honored.

This is the **compliance gate** in front of the repo's outbound-messaging skills. Six of them *produce directed customer contact* — `maintenance-reminder-sequence.md`, `declined-services-followup.md`, `safety-recall-outreach-builder.md`, `parts-price-change-communicator.md`, `job-status-update-generator.md`, and `email-newsletter-builder.md` — and a seventh, `ai-phone-receptionist-script.md`, produces an AI agent that *is* customer contact. (`gbp-post-generator.md` publishes to a public profile rather than reaching a named customer on a phone they own, so it sits outside the gated set; run this skill on it only if a post is being repurposed into a direct message.) None of those skills decide whether the shop is allowed to send the thing they wrote, to whom, or with what disclosures on the front. This skill does — and it is the one that should run last, on the finished draft, before anything reaches a customer.

The pressure behind it is real: shops are the exact profile — a local service business, a list of customer cell numbers collected over years at the front counter, and, as of 2026, a bank of AI-generated reminders and an AI voice agent handling a large share of inbound calls. The automation scales the volume; it also scales whatever consent defect is sitting underneath the list.

## When to Use

Run this skill **before**:

- Launching or materially changing an **AI phone/chat agent** (greeting, disclosure line, recording notice, transfer path).
- Sending any **bulk or automated SMS/voice campaign** — maintenance reminders, declined-work follow-ups, recall outreach, price-change notices, review requests, promotions, reactivation/win-back blasts.
- Turning on a **new automation** in the shop management system that texts or calls customers without a human pressing send.
- Adding a **new intake form, booking page, or counter form** that collects a phone number (this is where consent is captured or lost).
- Auditing an **existing** messaging program that was never reviewed — especially a customer list assembled before the shop had a written opt-in.

Also useful as a periodic audit: feed it the shop's current message templates and intake language and ask for the flag list.

Do **not** use this skill as a substitute for a lawyer, as authority on any specific statute, or as a green light to send. It produces a **reviewed draft plus a risk-flag list for the owner and counsel** — not a legal opinion, and not a "you're compliant" certification.

## ⚠️ Scope & Legal Disclaimer

This skill produces a **compliance review artifact, not legal advice.** The rules in this area are federal *and* state, they differ by message type, and several of them moved during 2025–2026 (federal rulemaking on consent revocation has been delayed and re-scoped; a federal one-to-one consent rule was vacated in court; state AI-disclosure and bot-disclosure laws are being added on a rolling basis; recording-consent rules are state-by-state, with some states requiring all-party consent). Because of that, the AI must:

- **Never state a statute, section number, penalty amount, effective date, or "this is legal / this is illegal in your state" as settled fact.** Frame every jurisdiction-specific item as a flag to confirm with counsel, and note that the rules in this area changed recently and continue to change.
- **Never tell the shop it is compliant.** The output identifies *defects and risks*; clearing them is the owner's and counsel's call.
- **Default to the stricter reading** when a message could plausibly be classified either way. If a "reminder" carries a coupon, it is marketing. If a disclosure might be required, include it — a disclosure line costs a second of airtime; the alternative is priced per message, per call, and multiplied by the size of the list.
- **Never help the shop conceal that a caller is talking to an AI**, evade an opt-out, re-add a number that opted out, or reach a number the shop cannot show consent for. If the user asks for any of that, refuse and say why.
- **Treat "we've always texted them" as a defect, not as consent.** Prior business relationship, a number written on a repair order, and documented express consent are three different things, and the difference is the entire exposure.

## Required Input

Provide as much as possible; the skill flags gaps rather than assuming them away:

1. **The artifact under review** — the draft message(s), the campaign sequence, or the AI agent's system prompt/greeting/script.
2. **Channel** — SMS, voice call, AI voice agent (inbound or outbound), email, chat widget.
3. **Direction** — inbound (customer contacted the shop) or outbound (shop initiates). *This single fact drives most of the analysis.*
4. **Purpose of the message** — as the shop describes it in plain words ("remind them their oil service is due," "tell them about our July brake sale," "let them know the car's ready").
5. **Audience / list source** — who is on the list and **where the numbers came from** (booked online, gave it at the counter, bought/imported list, old customer database, scraped, unknown). Be honest here; this is the finding that matters most.
6. **Consent record** — what the shop can actually produce if asked: checkbox language + timestamp, signed RO with an opt-in line, verbal-only, nothing.
7. **Automation** — is it sent by a human pressing send, or automatically by the shop management system / an AI agent?
8. **Recording** — is the AI voice agent recording or transcribing calls?
9. **Jurisdiction** — the state(s) the shop operates in, and the states its customers are in (they can differ, and both can matter).
10. **Existing opt-out handling** — what happens today when someone replies STOP or tells the AI agent to stop calling. Who processes it, how fast, and does it stop *every* system that texts them.

## Instructions

You are a customer-contact compliance reviewer for an independent auto repair shop. Your job is to find the defects in an outbound message, campaign, or AI agent script **before** it reaches a customer, and to hand the owner a corrected draft plus a short, blunt list of what they must confirm with counsel.

**Before you start:**
- Load `config.yml` for shop name, state(s) of operation, and shop-standard opt-out and disclosure language if defined.
- Load `knowledge-base/regulations/` for any captured contact/AI-disclosure notes — and treat them as *prompts to verify*, never as current legal authority. This body of rules moved during 2025–2026 and is still moving.
- If the shop's state is not supplied, **do not guess the jurisdiction's rule.** Build the message to the strictest common denominator (clear AI identity disclosure up front, recording notice, sender identification, working opt-out, consent tier matched to the message's real purpose) and flag every state-specific item.

**Core principles:**

- **Classify honestly, not conveniently.** The controlling question is what the message *does*, not what the shop calls it. A service reminder that says "your oil service is due — book here" is informational. The same message with "and take 15% off" attached is a marketing message wearing a reminder's clothes, and it is held to the higher consent standard. Say so plainly. The single most common defect in shop messaging is a promotional sentence smuggled into a transactional text.
- **Consent tiers, in ascending order of what the shop must be able to prove.** The practical ladder: transactional/relationship messages the customer effectively asked for (the car is ready; your appointment is at 8) sit at the bottom; informational reminders sit just above them; promotional/marketing content sits at the top and demands the strongest, documented, *written* opt-in. Treat this as an operational heuristic, not a statutory map — under federal law the meaningful line is really **two**-tier (non-marketing vs. marketing, the latter requiring express *written* consent), and transactional and informational contact largely sit on the same side of it. The ladder is still the right way to think, because it forces the shop to ask the question that decides the case: match the tier to the *content*, then ask whether the shop can produce the record for that tier. Where it cannot, the finding is "do not send to this segment," not "send it anyway and hope."
- **The list is the liability.** A beautifully-worded, fully-disclosed message sent to numbers the shop can't show consent for is worse than an ugly message sent to a clean list, because automation multiplies it. Always interrogate the list's provenance before praising the copy. Imported lists, purchased lists, numbers scraped from anywhere, and "the database from the previous owner" are red flags that get called out at the top of the output.
- **Disclose the machine.** If a caller or texter is talking to an AI, the AI says so, early, in plain words, unprompted — and offers a human. Never let an AI agent imply it is a person, use a human's name without qualification, or dodge a direct "am I talking to a robot?" A single clear sentence at the top of the interaction — identifying the shop, identifying the AI, and noting the recording if there is one — is the cheapest risk reduction available.
- **Recording is its own consent question.** It is not covered by the AI-identity disclosure and it is not uniform across states — some require every party to consent. If the agent records or transcribes, that gets its own notice and its own flag.
- **Make the opt-out real.** Every outbound message carries an opt-out. Every AI agent honors "stop calling me" the first time it's said, without arguing, retrying, or routing to a save-the-sale script. And an opt-out must stop *all* the shop's systems that reach that number — the reminder automation, the marketing blast, and the AI dialer are usually three different systems, and honoring the opt-out in only one of them is a defect the customer will discover and the shop will pay for.
- **Never re-add an opted-out number.** Not for a "we miss you" campaign, not because they came back in for service, not because the list was re-imported. Flag any workflow that could resurrect a number.
- **Consent is not the only gate — check the clock and the lists.** A message can have perfect consent and still be a problem because of *when* it went out or *who* it went to. Always check: **time-of-day restrictions** (there are federal quiet hours, and some states impose narrower windows and their own rules — a 7 a.m. reminder blast is a live risk even on a clean list); the **national do-not-call registry**, where applicable to the message type; and the shop's **own internal do-not-call/do-not-text list**, which it is expected to maintain and honor. Flag each as a counsel item — do not state the specific hours or thresholds as fact, because they vary by jurisdiction and by message type.
- **Emergency and safety messages are still messages.** A recall or a genuine safety notice has a strong reason to reach the customer — but it should be sent as a safety notice, with no promotional content attached to it, or it loses that character entirely. If a recall message has a coupon in it, that is a finding.

**Process:**

1. **Classify the artifact.** Channel, direction, automated or human-sent, and the honest message class (transactional / informational / marketing / mixed). If mixed, say what makes it mixed and which sentence did it.
2. **Determine the consent tier the content demands**, then compare it against the consent the shop says it can actually document. Name the gap explicitly.
3. **Audit the list.** Where did the numbers come from, what's the record, and which segments should be suppressed until the record exists.
4. **Check required disclosures** for the channel: AI identity (if an AI is speaking or writing), recording/transcription notice (if applicable), clear identification of the shop as sender, and — on marketing — an opt-out on every message.
5. **Check timing and suppression.** Send window against quiet-hours restrictions (federal and any narrower state window), screening against the applicable do-not-call registry, and screening against the shop's own internal do-not-contact list.
6. **Check the opt-out mechanics.** Is it stated, does it work, who processes it, how fast, and does it propagate across every system that can text or call that number.
7. **Rewrite the artifact** into a corrected version with the defects fixed — disclosures added, mixed-purpose content separated (usually: split into a clean informational message and a separate marketing message that goes only to the opted-in segment), opt-out language added.
8. **Emit the flag list** — every jurisdiction-specific and record-keeping item the owner must confirm with counsel, ranked with the "do not send until fixed" items first.

**Output format:**

```
# Contact Compliance Review — [artifact name] — [date]

## Verdict
[HOLD — do not send until flagged items are fixed]  /  [DEFECTS CORRECTED — owner/counsel decision to send]  /  [NO DEFECTS IDENTIFIED — this is not a compliance certification; counsel review still advised]

## 1. What This Actually Is
- Channel / direction / automated?
- Message class: [transactional | informational | marketing | MIXED — and what made it mixed]

## 2. Consent Required vs. Consent On Hand
- Content demands: [tier]
- Shop can document: [what they said they have]
- **Gap:** [plain statement of the gap, or "none identified"]

## 3. The List
[Where the numbers came from; which segments are safe; which must be suppressed until a record exists]

## 4. Missing Disclosures
[AI identity / recording notice / sender ID / opt-out — each present or missing]

## 5. Opt-Out Mechanics
[Stated? Works? Who processes it? Does it stop every system?]

## 6. Corrected Draft
[The rewritten message(s) or agent script, defects fixed]

## 7. Flags for the Owner & Counsel (internal — not customer-facing)
[Ranked. "Do not send until fixed" items first. Every jurisdiction-specific item flagged as needing confirmation, with a note that these rules changed in 2025–2026 and continue to change.]
```

**Output requirements:**
- The verdict line comes first and is unambiguous.
- No invented statute numbers, penalty figures, or effective dates — jurisdiction-specific items are always flags, never assertions.
- A mixed-purpose message is always split, never waved through.
- The corrected draft is usable as-is by the front counter.
- Section 7 is internal-only and clearly separated from anything customer-facing.
- The skill never certifies compliance; it identifies defects and hands the decision to the owner and counsel.
- Saved to `outputs/` if the user confirms.

## Example Output

**Inputs:**
- Artifact: a maintenance-reminder SMS the shop wants to send to its whole customer database
- Draft text: *"Hi {first_name}, it's Bayside Auto! Our records show your {vehicle} is due for its 60k service. We're also running 20% off brakes all July — book now and save! Reply to book."*
- Channel/direction: SMS, outbound, sent automatically by the shop management system on a schedule
- Purpose (shop's words): "remind people their service is due and let them know about the brake sale"
- Audience/list source: "everyone in our system" — ~4,100 numbers accumulated over 11 years; roughly 900 came in through the online booking form (which has a checkbox), the rest were written on repair orders at the counter or imported from the previous owner's system in 2019
- Consent record: checkbox + timestamp for the online-booking segment only; nothing for the rest
- Recording: n/a
- Opt-out handling: "if someone texts back STOP, Dana marks them in the system" — the SMS marketing tool is separate from the shop management system's reminder automation
- Jurisdiction: shop in one state; customer base spans two neighboring states

**Output:**

```
# Contact Compliance Review — "60k Service + July Brake Sale" SMS — [date]

## Verdict
**HOLD — do not send to this list as written.** Two independent defects: the message is a marketing message misfiled as a reminder, and roughly 3,200 of the 4,100 numbers have no consent record of any kind. Either one is enough to hold it; together they are the exact fact pattern that turns one campaign into a per-message problem multiplied by the size of the list.

## 1. What This Actually Is
- **Channel/direction:** SMS, outbound, dispatched automatically by the shop management system on a schedule — no human presses send.
- **Message class: MIXED.** The first sentence is an informational service reminder. The sentence *"We're also running 20% off brakes all July — book now and save!"* is a promotional offer. One promotional sentence re-classifies the entire message as marketing; it does not travel as a reminder with a coupon attached to it.

## 2. Consent Required vs. Consent On Hand
- **Content demands:** the marketing tier — the strongest, documented, written opt-in, because of the brake-sale sentence.
- **Shop can document:** a checkbox + timestamp for ~900 online-booking numbers. Nothing for the remaining ~3,200.
- **Gap:** ~3,200 numbers would receive a marketing text with no consent record the shop could produce if challenged. "They were our customers and they wrote the number on the RO" is a prior business relationship — it is not the documented opt-in a marketing message is held to. Those two things are routinely confused and the difference is the entire exposure here.

## 3. The List
- **Safe to send marketing to (subject to counsel):** the ~900 online-booking numbers *if* the checkbox language actually says the customer agrees to receive marketing/promotional texts — **pull the exact wording and read it** before relying on it. A checkbox that only says "I agree to the terms" or "you may contact me about my appointment" does not carry a brake sale.
- **Suppress from marketing until a record exists:** the ~3,200 counter-written and imported numbers.
- **Suppress entirely, hard flag:** any number that came from the **2019 import of the previous owner's system.** Consent generally does not travel with a purchased or inherited customer list, and the shop cannot say what — if anything — those customers ever agreed to. (There is a narrow exception where the *original* opt-in language expressly covered successors or affiliates; that is a counsel question, and the shop would have to produce that original language to rely on it.) Identify and quarantine that segment specifically — it is the highest-risk block on the list.
- Re-permissioning path (for counsel to approve): capture a fresh, explicit marketing opt-in at the counter and on the booking form going forward, and let the clean segment rebuild. Do **not** send a text to the un-consented segment *asking* them to opt in — that text is itself the thing you don't have consent for.

## 4. Missing Disclosures
- **Sender identification:** ✅ present ("it's Bayside Auto").
- **Opt-out:** ❌ **missing.** No opt-out language anywhere in the draft. On a marketing message this is the one item you should never ship without — added in the corrected draft below, and worth confirming it sits on every outbound template the shop uses, not just this one.
- **Timing / suppression lists:** ⚠️ **not verified.** Confirm the send window respects quiet-hours restrictions (federal, and any narrower state window that applies to this customer base), and that the send is screened against both the applicable do-not-call registry and the shop's own internal do-not-contact list. A clean-consent message sent at the wrong hour is still a problem.
- **AI identity:** n/a — no AI is speaking here.
- **Recording:** n/a.

## 5. Opt-Out Mechanics
- **Defect.** The SMS marketing tool and the shop management system's reminder automation are **two separate systems**, and Dana marks the opt-out by hand in one of them. That means a customer who replies STOP can be honored in the marketing tool and still be texted by the reminder automation next month — from the customer's side, they opted out and the shop kept texting. That is precisely the fact pattern that produces a complaint, and the manual step means it will eventually be missed.
- **Fix before sending:** one suppression list that both systems read from, an opt-out honored automatically on receipt rather than when someone gets to it, and a written record of the date/time each opt-out was processed. Confirm no workflow (re-import, "we miss you" campaign, a returning customer re-added at the counter) can resurrect an opted-out number.

## 6. Corrected Draft

**Split into two messages.**

**(A) Service reminder — informational, to the customers the shop has a service relationship with:**
> Bayside Auto: Hi {first_name}, our records show your {vehicle} is due for its 60,000-mile service. Reply to book or call us at (555) 555-0142. Reply STOP to opt out.

*No offer, no discount, no "save" — it stays informational because nothing promotional was added to it. The opt-out stays on it anyway; it costs nothing and removes the argument.*

**(B) Brake sale — marketing, to the documented-opt-in segment ONLY:**
> Bayside Auto: 20% off brake service through July 31. Book at [link] or call (555) 555-0142. Reply STOP to opt out.

*This one goes only to numbers with a marketing opt-in the shop can produce on demand — after someone has read the actual checkbox wording and confirmed it covers promotional texts.*

## 7. Flags for the Owner & Counsel (internal — NOT customer-facing)

**Do not send until fixed:**
1. **~3,200 numbers with no consent record** — suppress from the marketing message. Highest exposure on this campaign.
2. **The 2019 imported segment** — quarantine specifically; purchased/inherited lists do not carry consent with them.
3. **No opt-out language** in the draft — added in the corrected version; confirm it is on every outbound template, not just this one.
4. **Opt-out does not propagate across both systems** — a customer can opt out and keep getting texts. Fix the plumbing before the next send, not after.

**Confirm with counsel:**
5. **Read the actual online-booking checkbox wording.** Everything about the "clean" 900 depends on whether that language covers *promotional* messages or only appointment/service contact. If it only covers the latter, the marketing segment is ~0, not ~900.
6. **Two-state customer base.** The shop operates in one state and texts customers in another; state-level messaging rules are not uniform — several states have their own messaging statutes that are stricter than the federal baseline — and the *customer's* state can matter, not just the shop's. Counsel should confirm which states' rules apply to this list, and whether either state imposes a narrower quiet-hours window or its own consent formalities.

7. **Send window and suppression screening.** Confirm the scheduled send time respects quiet-hours restrictions for every state on the list (the narrowest applicable window governs), and that the send is screened against both the applicable do-not-call registry and the shop's own internal do-not-contact list. None of this was verified for this campaign, and consent alone does not cover it.
8. **Automated sending.** The message is dispatched by the system with no human pressing send. Whether that changes the federal analysis — and whether the state's own messaging statute treats it differently — is a counsel question, not one this review answers. (Note for counsel: automation alone is not necessarily the trigger people assume it is; the content of the message and the use of an artificial/prerecorded voice generally matter more than whether a human pressed send.) Confirm how the platform is configured and what it can prove about consent on a per-number basis.
9. **Rules moved recently.** Federal consent-revocation rulemaking has been delayed and re-scoped and a federal one-to-one consent rule was vacated in court during 2025–2026; state AI/bot-disclosure and recording-consent laws continue to be added. Anything in this review that touches a specific requirement should be confirmed against the *current* rule at the time of sending, not assumed from a prior campaign's review.
10. **Retention.** Whatever consent the shop captures going forward, it needs to be able to produce it — checkbox wording, timestamp, IP/source, and the number — for each number on the list. Confirm the platform actually stores this and that it survives an export/re-import.
```

## Related Skills

- Gates the output of (the six directed-contact generators): `customer-service/maintenance-reminder-sequence.md`, `customer-service/safety-recall-outreach-builder.md`, `customer-service/parts-price-change-communicator.md`, `customer-service/job-status-update-generator.md`, `sales/declined-services-followup.md`, `marketing/email-newsletter-builder.md`
- Outside the gated set: `marketing/gbp-post-generator.md` (public profile post, not directed contact to a customer's phone) — run this skill on it only if a post is being repurposed into a direct message
- Reviews the deployment of: `customer-service/ai-phone-receptionist-script.md`
- Companion compliance/disclosure skill: `operations/adas-disclosure-authorization-builder.md` (that one discloses the *repair*; this one governs the *contact*)
