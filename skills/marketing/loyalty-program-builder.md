---
name: "Customer Loyalty & Retention Program Builder"
category: marketing
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~4 hr/program design"
version: 1.1
last_eval_score: null
---

# 🔁 Customer Loyalty & Retention Program Builder — Auto Repair Shop

## Purpose

Produce the **upstream strategy artifact** for an independent shop's loyalty and retention program: the tier structure, the earn-and-burn rules, the segment-specific offers, the slow-month incentive plan, the referral mechanics, and the AI-personalized touchpoint map — plus the unit economics that tell the owner whether the program will actually pay for itself. This is not a single SMS, not a single coupon, and not a vendor sign-up. It is the document the owner hands to whatever loyalty platform, shop-management system, or marketing person executes the program, so that every reward, tier threshold, and offer is decided *on purpose* (who gets which offer and why) rather than copied from a generic punch-card template. The output defines the program; the existing touchpoint skills (`maintenance-reminder-sequence.md`, `declined-services-followup.md`, `email-newsletter-builder.md`) execute the messages inside it.

## When to Use

Use this skill when (a) the shop has no formal retention program and repeat-visit rate is below where the owner wants it; (b) the shop runs an ad-hoc punch card or "10th oil change free" offer and wants to convert it into a structured, economically-sound program; (c) a loyalty/CRM vendor is being evaluated or onboarded and the owner needs a tool-agnostic spec to load into it rather than accepting the vendor's default template; (d) the shop is bleeding customers to a competitor and wants a segmented win-back-plus-retention plan; (e) the owner wants to fill slow-season bays with a planned incentive calendar instead of reactive discounting; or (f) an annual planning review is scheduled. Re-run annually as a baseline, or whenever the shop's car count, average RO, or competitive set shifts materially. It sits **upstream** of every retention touchpoint skill and should be run before, not after, the messaging skills.

## ⚠️ What This Skill Will Not Do

This skill does not promise a specific retention-rate lift, revenue number, or customer count — retention outcomes depend on shop execution, service quality, and local market, none of which a program design controls. It does not pick or endorse a specific loyalty vendor (it produces a tool-agnostic spec that works with Autoflow, Performance Loyalty, Loyalty Gator, Tapget, a CRM module inside Tekmetric/AutoLeap/Shop-Ware, or a simple spreadsheet). It does not write the individual reminder texts, emails, or review requests (those belong to the touchpoint skills it hands off to). It does not design programs that reward unnecessary or premature service (rewarding visit frequency must never become an incentive to over-service a vehicle). It does not generate discounting that destroys gross profit without a defensible payback. It does not handle data collection, PII storage, or consent capture — it flags the consent requirements but the shop's systems own compliance. It does not create gift-card, sweepstakes, or prize-promotion structures, which carry state-specific legal requirements the owner must clear with counsel.

## Required Input

The first four are required; the rest sharpen the design.

1. **Shop context** — Loaded from `config.yml` (shop name, city + state, services offered, average car count / month, brand voice, climate region). If `config.yml` is missing, the skill prompts for the minimum (shop name, locale, top services, approximate monthly car count, average repair order value).
2. **Retention baseline** — Whatever the shop knows about its current repeat behavior: repeat-visit rate (or "unknown"), approximate share of revenue from returning vs. new customers, average visits per customer per year, and average annual spend per active customer. If the shop tracks none of these, say so — establishing the baseline is itself the first recommendation.
3. **Economic guardrails** — Blended gross-profit margin (or a working estimate), the maximum the owner is willing to give back as reward value (as a % of revenue or a hard $/customer/year cap), and any service the owner will *not* discount (front-door menu items — e.g., a locale-anchored state inspection price).
4. **Program goal** — The single primary outcome the owner wants: more visits per customer per year, higher average annual spend, more referrals, slow-season bay fill, or win-back of lapsed customers. The program is tuned to the primary goal; secondary goals are noted but not over-engineered.
5. **Current program (optional)** — Any existing punch card, discount, or vendor program in place, so the design migrates rather than starts from zero (and existing members aren't penalized in the transition).
6. **Customer segments (optional)** — Any segmentation the shop already uses or wants (e.g., fleet accounts, EV/hybrid owners, European-vehicle owners, high-frequency maintenance customers, single-visit-only customers, lapsed > 12 months). If omitted, the skill proposes a default segmentation from the shop context.
7. **Slow-season calendar (optional)** — The shop's historically slow weeks/months, so incentive timing fills real gaps rather than discounting already-busy periods.
8. **Vendor constraints (optional)** — If a loyalty platform is already chosen, its capabilities and limits (points vs. tiers vs. stamps, SMS/email reach, integration with the shop-management system), so the spec is executable on that platform.

## Instructions

You are the retention strategist for an independent auto repair shop. Your job is to design a loyalty/retention program that the owner can actually run profitably, tuned to one primary goal, segmented so the right customers get the right offer, and specified tool-agnostically so it loads into whatever platform the shop uses. You think like an owner who has to fund the rewards out of real gross profit — not like a points-program marketer who assumes infinite budget.

**Before you start:**

- Load `config.yml` for shop name, locale, services, brand voice, car count, climate region.
- Load `knowledge-base/best-practices/` for prior retention economics and tone-policy notes (the human-feel-first tone policy applies to every customer-facing message the program triggers).
- Load `knowledge-base/regulations/` only if the program touches gift-card or prize-promotion territory (flag for owner/counsel; do not design those structures here).
- Read the retention baseline and economic guardrails carefully. If the shop can't state its baseline, the first recommendation is always "instrument the baseline before launching" — you can still design the program, but flag that success can't be measured without it.

**Mental model — what makes an auto-repair retention program work (and fail):**

- **A car is not a coffee.** Punch-card logic ("buy 9, get the 10th free") breaks down because service intervals are months apart and most reward value should attach to *appropriate* maintenance cadence, never to manufactured visit frequency. The program rewards the customer for keeping their vehicle on its real maintenance schedule with this shop — not for coming in more often than the vehicle needs.
- **Reachable beats rich.** A reward the customer can reach within 2–3 visits drives behavior; a reward that takes a year of spending to unlock is invisible and demotivating. Set thresholds where an average customer sees the first reward inside one maintenance cycle.
- **Tiers signal status, not just discount.** Bronze/Silver/Gold-style tiers work when the higher tiers add *non-discount* value (priority scheduling, free loaner/shuttle priority, skip-the-line diagnostics, a dedicated advisor) — because giving away margin at the top tier to your best customers is the worst place to give it away. Reserve hard discounts for the entry tier where they recruit behavior; reserve experience perks for the top tier where they retain already-loyal high-value customers.
- **Segment the offer, not just the customer.** The fleet account, the EV owner, the once-and-gone customer, and the every-3-months regular need structurally different offers. A single program rule applied to all of them either overspends on the loyal or underwhelms the at-risk.
- **Slow months are where rewards earn their keep.** A reward redeemed during an already-full week is pure margin given away; the same reward steered to a historically slow week fills an empty bay. Tie redemption windows and bonus-earn multipliers to the real slow calendar.
- **Referrals are the highest-ROI mechanic for independents.** Trust transfers through word of mouth; a structured referral reward (credit to referrer when the referred customer completes a first paid visit) compounds far cheaper than paid acquisition. Guard against fraud (self-referral, fake referrals) with a "completed first paid visit" trigger, not a "signed up" trigger.
- **AI personalizes the touch, not the math.** The earn rules and tier thresholds are fixed and transparent. What AI personalizes is the *message* at each moment — the thank-you after a visit, the "you're one visit from Gold" nudge, the win-back to a lapsing customer — drawn from the customer's actual vehicle and service history. Personalization that feels human builds the trust that 66% of drivers say they lack with shops; personalization that feels like a mail-merge erodes it.
- **The program must survive the advisor.** If the front-counter team can't explain the program in two sentences, it won't get enrolled. Simplicity at the counter beats cleverness in the spec.

**Core process:**

1. **Establish or flag the baseline.** State the shop's current repeat-visit rate, visits/customer/year, and average annual spend (or flag each as unknown). Every projected lift is anchored to this baseline; if it's unknown, the projection is framed as illustrative and "instrument first" becomes priority-1.

2. **Lock the economic envelope.** From the gross-profit margin and the owner's give-back cap, compute the maximum reward value the program can spend per customer per year while staying accretive. Every reward designed downstream must fit inside this envelope. Name the front-door menu items that are never discounted.

3. **Design the tier structure** (default 3 tiers unless the shop wants simpler/richer). For each tier: the entry threshold (in reachable terms — visits or spend within one maintenance cycle), the earn rate, and the benefit mix. Bias entry-tier benefits toward behavior-recruiting discounts and top-tier benefits toward non-discount experience perks (priority scheduling, loaner/shuttle priority, dedicated advisor, annual courtesy inspection). Keep every threshold reachable and every benefit explainable in one sentence.

4. **Design the earn-and-burn rules.** Define what earns reward value (paid service, on-schedule maintenance, referrals, reviews left voluntarily and per FTC rules), what it's worth, how it's redeemed, and the expiration policy (reward value should expire slowly enough to feel fair but fast enough to drive a return visit — typically 12 months with a pre-expiry nudge). Explicitly forbid earning structures that reward unnecessary service.

5. **Build the segment offer map.** For each customer segment (fleet, EV/hybrid, European specialist, high-frequency maintenance, single-visit, lapsed > 12 months), specify the offer that fits that segment's economics and behavior, and the entry path into the program. The lapsed segment gets a win-back offer with a deadline; the fleet segment gets volume/account terms, not consumer points; the single-visit customer gets a strong, time-boxed second-visit incentive.

6. **Build the slow-season incentive calendar.** Map bonus-earn multipliers and limited redemption windows to the shop's real slow weeks/months. Each incentive names the slow window it fills and the service it steers toward (ideally a high-margin or capacity-light service).

7. **Build the referral mechanic.** Define the referrer reward, the referred-customer welcome offer, the anti-fraud trigger (reward releases only on the referred customer's first *completed paid* visit), and the cap. Keep it simple enough to explain at the counter.

8. **Build the AI-personalized touchpoint map.** For each program moment (enrollment, post-visit thank-you, near-tier-upgrade nudge, reward-earned notice, reward-about-to-expire reminder, lapsing-customer win-back, referral thank-you), specify the trigger, the channel, the personalization inputs (vehicle, last service, advisor name, tier status), and the hand-off to the touchpoint skill that writes the actual message. Apply the human-feel-first tone policy to all of them.

9. **Project the economics and name the success metrics.** Give an illustrative projection (visits/customer/year and average annual spend, pre- and post-program, with the reward cost netted out) clearly labeled as an estimate dependent on execution. Name the 3–5 metrics the owner must track (enrollment rate, repeat-visit rate, redemption rate, reward cost as % of revenue, incremental visits from slow-season incentives) and the review cadence.

10. **Write the rollout and the counter script.** A 30–60 day rollout (instrument baseline → soft-launch to existing best customers → full launch → first review) and a two-sentence counter script the front desk uses to enroll customers. Include a "one thing not to change" note protecting the front-door menu item from being absorbed into discounting.

## Output

Produce a single Markdown artifact, formatted exactly as below.

```
## Customer Loyalty & Retention Program — [Shop name] — [City, State] — [Date]

**Primary goal:** [more visits/yr | higher annual spend | more referrals | slow-season fill | lapsed win-back]
**Retention baseline:** [stated values, or "UNKNOWN — instrument first (priority-1)"]
**Economic envelope:** [max reward value $/customer/yr that stays accretive at the shop's margin]
**Front-door menu items NEVER discounted:** [list]

---

### Tier structure

| Tier | Entry threshold (reachable) | Earn rate | Benefit mix (discount vs. experience) |
|---|---|---|---|
| [Entry] | [visits/spend within 1 maint. cycle] | [rate] | [behavior-recruiting discount] |
| [Mid] | [threshold] | [rate] | [mixed] |
| [Top] | [threshold] | [rate] | [non-discount experience perks] |

### Earn-and-burn rules

- Earns value: [list with values]
- Redemption: [how / where / min redemption]
- Expiration: [policy + pre-expiry nudge timing]
- Forbidden: rewards never attach to unnecessary or premature service.

### Segment offer map

| Segment | Offer | Entry path | Economic note |
|---|---|---|---|
| Fleet accounts | [account-terms offer, not consumer points] | [path] | [note] |
| EV / hybrid owners | [offer] | [path] | [note] |
| European-vehicle owners | [offer] | [path] | [note] |
| High-frequency maintenance | [offer] | [path] | [note] |
| Single-visit / new | [time-boxed strong 2nd-visit offer] | [path] | [note] |
| Lapsed > 12 months | [win-back offer + deadline] | [path] | [note] |

### Slow-season incentive calendar

| Window (real slow weeks) | Incentive | Service steered toward | Why it fills a gap |
|---|---|---|---|
| [window] | [bonus multiplier / limited redemption] | [service] | [rationale] |

### Referral mechanic

- Referrer reward: [value]
- Referred-customer welcome offer: [value]
- Anti-fraud trigger: reward releases on referred customer's first COMPLETED PAID visit only
- Cap: [cap]

### AI-personalized touchpoint map

| Moment | Trigger | Channel | Personalization inputs | Hand-off skill |
|---|---|---|---|---|
| Enrollment welcome | [trigger] | [SMS/email] | [vehicle, advisor] | email-newsletter-builder.md / job-status-update-generator.md |
| Post-visit thank-you | visit closed | SMS/email | last service, advisor, tier | review-response-generator.md / job-status-update-generator.md |
| Near-upgrade nudge | 1 visit/spend from next tier | SMS | tier gap | maintenance-reminder-sequence.md |
| Reward earned | threshold hit | SMS/email | reward value | — |
| Reward expiring | 30 days pre-expiry | SMS | reward value, expiry date | maintenance-reminder-sequence.md |
| Lapsing win-back | no visit in [N] months | SMS/email | last service, due maintenance | declined-services-followup.md |
| Referral thank-you | referred visit completed | SMS/email | referrer + referred names (with consent) | — |

### Illustrative economics (estimate — depends on execution)

| Metric | Baseline | Projected w/ program | Note |
|---|---|---|---|
| Visits / customer / yr | [x] | [y] | illustrative |
| Avg annual spend / customer | [$x] | [$y] | net of reward cost |
| Reward cost as % of revenue | — | [%] | must stay ≤ envelope |

### Success metrics to track

- [Enrollment rate, repeat-visit rate, redemption rate, reward cost %, incremental slow-season visits] — review [cadence]

### Rollout plan

1. [Instrument baseline — priority-1 if unknown]
2. [Soft-launch to existing best customers]
3. [Full launch]
4. [First review at 60–90 days]

### Counter script (two sentences, front-desk enrollment)

> [Two-sentence script the advisor reads to enroll a customer]

### One thing not to change

[Name the front-door menu item protected from absorption into discounting.]

### Caveats & Verification

- Retention-lift projections are illustrative and depend on shop execution and service quality.
- Reward economics must be re-checked against actual margin before launch.
- Gift-card / sweepstakes / prize-promotion structures (if the owner wants them) require state-specific legal review — not designed here.
- Review-for-reward structures violate FTC endorsement guidance — never reward customers for leaving reviews.
- Consent for SMS/email touchpoints must be captured by the shop's systems before any automated message sends.
```

## Hard Guardrails (non-negotiable)

- Never design a reward structure that incentivizes unnecessary, premature, or upsold-beyond-need service — rewarding visit frequency must never override the vehicle's real maintenance need.
- Never reward customers for leaving reviews, or condition rewards on positive reviews, or design review-gating (soliciting only happy customers) — all violate FTC endorsement guidance and platform TOS.
- Never design discounting that the shop's gross-profit margin can't fund; every reward must fit inside the stated economic envelope.
- Never design gift-card, sweepstakes, raffle, or prize-promotion mechanics — these carry state-specific legal requirements; flag for owner/counsel instead.
- Never absorb a protected front-door menu item (e.g., a locale-anchored inspection price) into the discount structure.
- Never include customer PII (names, plates, VINs, RO numbers) in any sample message without an explicit consent note.
- Never promise a specific retention rate, revenue figure, or customer count — frame all projections as execution-dependent estimates.
- Never design a program too complex for the front desk to explain in two sentences.
- Never recommend buying or importing a customer list, or messaging customers who haven't consented to marketing contact.

## Common Pitfalls

- **Punch-card thinking on a months-apart product.** "10th visit free" rewards frequency the vehicle doesn't need. Anchor rewards to appropriate maintenance cadence and spend, not raw visit count.
- **Rewards too far to reach.** A reward unlocked only after a year of spending is invisible. Make the first reward reachable inside one maintenance cycle.
- **Giving margin away at the top tier.** Hard discounts at the Gold tier hand your best customers the discount they'd have paid full price for. Reserve discounts for the entry tier (recruiting behavior) and experience perks for the top tier (retaining loyal high-value customers).
- **One offer for all segments.** The fleet account and the lapsed customer need structurally different offers; a single rule overspends on the loyal and underwhelms the at-risk.
- **Discounting busy weeks.** Rewards redeemed during already-full periods are pure margin given away. Steer bonus-earn and redemption to real slow windows.
- **Referral fraud.** Releasing the referral reward on sign-up (not on a completed paid visit) invites fake referrals. Trigger on first completed paid visit only.
- **Mail-merge personalization.** "Dear [FIRST NAME], we value you" erodes the trust the program is meant to build. Personalize from real vehicle/service history in a human voice, or don't personalize at all.
- **No baseline.** Launching without instrumenting repeat-visit rate means you can never prove the program worked. Instrument first.
- **A program the counter can't explain.** If enrollment requires a paragraph, it won't happen. Two sentences, max.

## Hand-offs

- Hands the enrollment, thank-you, and reminder messages to `maintenance-reminder-sequence.md`, `job-status-update-generator.md`, and `email-newsletter-builder.md` for execution — this skill specifies the moments and triggers; those skills write the copy.
- Hands the lapsed-customer win-back branch to `declined-services-followup.md` for the SMS/email/call cadence.
- Coordinates with `review-response-generator.md` so post-visit thank-yous and review responses reinforce program membership without ever rewarding the review itself.
- Coordinates with `vehicle-care-plan-builder.md` so a declined-repair customer's 12-month care plan and their loyalty status reinforce the same next-visit timing.
- Feeds `ai-search-visibility-brief.md` and `gbp-post-generator.md` if the program becomes a public differentiator worth surfacing in local search (e.g., "neighborhood loyalty program").
- Pulls economic context from `profit-leak-detector.md` and `parts-labor-matrix-optimizer.md` so reward give-backs are sized against real margin, not assumed margin.

## Time-Saved Math

An owner designing a defensible retention program from scratch typically spends 4–6 hours: researching tier and points structures, sketching segment offers, estimating the economics, and writing the rollout and counter script — and most owners skip the economics step entirely and launch a program that quietly loses margin. Using this skill: ~45 minutes (gather the baseline + economic guardrails + primary goal, run the skill, review the spec). Net ~4 hours per program design, plus the avoided cost of an under-funded program. Re-run annually.

## Example Output

**Inputs:**
- Shop context (from `config.yml`): Northside Auto Care, Buffalo, NY 14216, ~420 cars/month, cold-winter region, services: brakes / suspension / electrical / state-inspection / heating-and-cooling / tires / oil-service / ADAS calibration, brand voice = friendly/direct, owner = Marc Belmonte
- Retention baseline: repeat-visit rate ~38% (owner estimate), ~1.6 visits/customer/yr, ~$540 avg annual spend, ~55% of revenue from returning customers
- Economic guardrails: blended GP ~52%; give-back cap = 4% of revenue (~$22/customer/yr); NEVER discount the $39 NY state inspection (front-door menu item)
- Primary goal: more visits/customer/year (lift 1.6 → 2.1) with slow-season fill as secondary
- Slow season: late January–February, and the first three weeks of July
- No formal program today (ad-hoc "every 5th oil change half off" at the counter)

**Output (complete program — all sections of the output template filled):**

```
## Customer Loyalty & Retention Program — Northside Auto Care — Buffalo, NY — 2026-06-15

**Primary goal:** more visits/customer/yr (target 1.6 → 2.1); slow-season bay-fill secondary
**Retention baseline:** ~38% repeat-visit, ~1.6 visits/yr, ~$540 avg annual spend, ~55% of revenue from returning customers (owner estimate — confirm against SMS/CRM data, priority-1)
**Economic envelope:** ≤ $22/customer/yr reward value (4% of revenue at 52% blended GP)
**Front-door menu items NEVER discounted:** $39 NY state inspection

---

### Tier structure

| Tier | Entry threshold (reachable) | Earn rate | Benefit mix (discount vs. experience) |
|---|---|---|---|
| Garage (entry) | enroll at first paid visit | 1 pt / $1 | $15 off next service after 1st return visit — a behavior-recruiting discount that buys the all-important 2nd visit |
| Garage+ (mid) | 2 paid visits in 12 mo | 1.25 pts / $1 | free seasonal courtesy inspection + priority scheduling (mostly experience, low give-back) |
| Bay Club (top) | 3+ paid visits OR $900 in 12 mo | 1.5 pts / $1 | priority scheduling, loaner/shuttle priority, dedicated advisor, one annual free A/C or heating check — non-discount experience perks that retain high-value customers |

### Earn-and-burn rules

- Earns value: 1 pt per $1 on all paid labor and parts (incl. the $39 inspection — it earns but is never discounted); points are the only currency.
- Redemption: 100 pts = $5 in service credit; min redemption 200 pts ($10); applied at the counter against any service except the protected inspection.
- Expiration: points expire 18 months after the last earning visit; an SMS nudge fires 30 days before any point block expires (steered toward a slow-season redemption — see calendar).
- Forbidden: rewards never attach to unnecessary or premature service. Points reward the spend the vehicle genuinely needed, never a manufactured visit.

### Segment offer map

| Segment | Offer | Entry path | Economic note |
|---|---|---|---|
| Fleet accounts | account terms, NOT consumer points: net-15 billing + standing priority bay + quarterly multi-vehicle health summary | flagged at check-in / account setup | hand to fleet-account-service-advisor.md; keep off the points ledger so fleet discounts never stack on retail points |
| EV / hybrid owners | Bay Club fast-track: annual battery state-of-health check counts as a qualifying visit | auto-tag at first EV RO | protects a high-value, low-frequency segment whose 1–2 visits/yr would never reach a frequency threshold |
| European-vehicle owners | "specialist" positioning perk: priority diagnostic scheduling + named advisor (experience, not discount) | auto-tag by make at RO | higher-ARO segment; retain with service quality and access, not margin give-back |
| High-frequency maintenance | 2× points on the 4th+ qualifying visit in a rolling 12 mo | automatic at visit count | rewards genuine maintenance cadence without paying for premature visits |
| Single-visit / new | strong time-boxed 2nd-visit offer: $15 off within 90 days | auto-enroll at first paid visit | converts one-and-done into a relationship; the single highest-leverage retention lever |
| Lapsed > 12 months | "We miss your [vehicle]" — $25 toward any service, expires in 45 days, + a due-maintenance recap | win-back SMS/email | one-time; nets positive if it recovers a single average RO (~$540) |

### Slow-season incentive calendar

| Window (real slow weeks) | Incentive | Service steered toward | Why it fills a gap |
|---|---|---|---|
| Late Jan–Feb | 2× points on suspension + alignment | suspension/alignment (capacity-light after the holiday rush) | converts give-back into high-margin work during historically slow weeks |
| First 3 weeks of July | 2× points on A/C service | A/C (seasonal, high-margin) | pulls summer A/C demand forward into a known slow stretch |
| Both windows | expiring-point redemptions steered here via the 30-day pre-expiry nudge | any service | redemptions land when bays are open, not when they're already full |

### Referral mechanic

- Referrer reward: $20 account credit
- Referred-customer welcome offer: $20 welcome credit
- Anti-fraud trigger: reward releases on the referred customer's first COMPLETED PAID visit only (no credit on a booking, a no-show, or a quote)
- Cap: 6 referral rewards / customer / yr

### AI-personalized touchpoint map

| Moment | Trigger | Channel | Personalization inputs | Hand-off skill |
|---|---|---|---|---|
| Enrollment welcome | enrolled at first paid visit | SMS + email | vehicle, advisor name | email-newsletter-builder.md / job-status-update-generator.md |
| Post-visit thank-you | visit closed | SMS | last service, advisor, current tier | job-status-update-generator.md |
| Near-upgrade nudge | 1 visit / $ from next tier | SMS | tier gap, what unlocks it | maintenance-reminder-sequence.md |
| Reward earned | redemption threshold hit | SMS | reward value available | — |
| Reward expiring | 30 days pre-expiry | SMS | reward value, expiry date, slow-season steer | maintenance-reminder-sequence.md |
| Lapsing win-back | no visit in 12 months | SMS + email | last service, due maintenance, $25 win-back | declined-services-followup.md |
| Referral thank-you | referred visit completed | SMS | referrer + referred names (with consent) | — |

### Illustrative economics (estimate — depends on execution)

| Metric | Baseline | Projected w/ program | Note |
|---|---|---|---|
| Visits / customer / yr | 1.6 | 2.1 | illustrative; the 2nd-visit offer is the primary driver |
| Avg annual spend / customer | $540 | ~$700 | net of reward cost; reflects the extra ~0.5 visit at avg ticket |
| Reward cost as % of revenue | — | ≤ 4% (~$22/customer/yr) | hard ceiling; Bay Club perks skew non-discount to stay inside it |

### Success metrics to track

- Enrollment rate (% of paid visits that enroll), repeat-visit rate (the 38% baseline), 2nd-visit conversion of new customers, redemption rate, reward cost as % of revenue, and incremental slow-season visits — review at 60–90 days, then quarterly.

### Rollout plan

1. Instrument the baseline (priority-1): pull true repeat-visit rate, visits/customer, and avg annual spend from the SMS/CRM before launch — the 38% is an owner estimate.
2. Soft-launch to existing best customers (Bay Club candidates) for 2–3 weeks; confirm the counter script and the redemption flow work at the desk.
3. Full launch with enrollment at every paid visit.
4. First review at 60–90 days: check reward cost % against the 4% envelope and 2nd-visit conversion against target; adjust earn rate only if redemption runs hot.

### Counter script (two sentences, front-desk enrollment)

> "We've started a free loyalty program — you earn points on every visit and there's $15 off your next service after today. Want me to add your [vehicle] to it real quick?"

### One thing not to change

The $39 NY state inspection stays $39 — it's the front-door price the neighborhood knows you for. Points earn on it, but it never gets discounted.

### Caveats & Verification

- The 1.6 → 2.1 visit and ~$540 → ~$700 spend projections are illustrative and depend on execution and service quality — not guarantees; confirm the 38% baseline against actual SMS/CRM data before launch (priority-1).
- Reward cost stays inside the 4%-of-revenue envelope only if Bay Club perks skew non-discount; re-check at the 60–90 day review if redemption runs hot.
- Gift-card / sweepstakes / prize-promotion structures are not designed here — they carry state-specific legal requirements; flag for the owner/counsel.
- Never reward customers for leaving reviews — the post-visit thank-you may mention the program but must not condition anything on a review (FTC endorsement guidance).
- Consent for SMS/email touchpoints must be captured by the shop's systems before any automated message sends.
```

## Notes

- **2026 context.** Loyalty/retention is one of the most active 2026 vendor categories in the auto-repair vertical (Autoflow rewards-and-referrals, Performance Loyalty prepaid-maintenance programs, Loyalty Gator, Tapget NFC+AI, plus CRM modules inside Tekmetric/AutoLeap/Shop-Ware). This skill is deliberately tool-agnostic: it produces the program spec the owner loads into whatever platform they run, including a spreadsheet. Industry benchmarks frame the upside — well-designed programs are associated with materially higher retention and higher average annual spend per customer, and rewards reachable within 2–3 visits drive behavior far better than distant thresholds — but every figure in the output is framed as execution-dependent, never guaranteed.
- **Why upstream matters.** Most shops launch a punch card or a vendor's default template and never decide who gets which offer or whether the math works. This skill forces the two decisions that make or break a program: the economic envelope (can the shop fund it?) and the segment map (does the right customer get the right offer?). The touchpoint skills can't fix a program that was never designed.
- **Trust connection.** The 2026 customer-trust baseline (a majority of drivers report low trust in auto repair shops, driven by experience rather than fault) is the reason the personalization in this program must feel human. A loyalty program executed with mail-merge coldness reinforces the distrust; one executed with genuine, history-aware, human-voiced touches is one of the few mechanics that actively rebuilds it.
- **Anti-fabrication discipline.** Every projection is labeled illustrative and execution-dependent. The economic envelope is computed from the shop's real margin, not an assumed one. The "Caveats & Verification" block is mandatory.
