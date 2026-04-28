# 📣 Marketing Skills

Local-marketing content generation for the auto repair shop — Google Business Profile posts, short-form video scripts, monthly customer email newsletters, and adjacent local-SEO content. Every skill in this subfolder shares the same inputs, the same anti-fabrication guardrails, and the same hand-off pattern to the customer-service review-response and reminder skills already in the library.

## Skills in this subfolder

| Skill | Difficulty | Time saved | Purpose |
|---|---|---|---|
| `gbp-post-generator.md` | beginner | ~15 min/post | Google Business Profile post (text + photo brief + CTA) |
| `short-form-video-script-generator.md` | beginner | ~25 min/script | 30–90 sec Reel / TikTok / Short script (hook + beats + caption + CTA) |
| `email-newsletter-builder.md` | beginner | ~45 min/issue | Monthly customer email (seasonal services + shop news + customer education) |

## Shared inputs

Every marketing skill takes the same six core inputs (override per skill as needed):

1. **Shop name + locale** — Loaded from `config.yml` (shop name, city, state, climate region, target customer profile)
2. **Services in scope** — Which services are being marketed this month (seasonal PM, ADAS calibration, hybrid / EV, brakes, tires, A/C, heat, alignment, etc.)
3. **Season / occasion** — The month or seasonal trigger driving the content (winter prep, summer road-trip, back-to-school, tax-return, state-inspection-deadline, hurricane prep, etc.)
4. **Brand voice** — Loaded from `config.yml` → `voice` (warm-professional, no-jargon, friendly-direct, etc.)
5. **Customer education focus (if any)** — A specific topic the shop wants to teach (why coolant matters, what ADAS calibration is, why tire rotation matters, etc.)
6. **CTA** — One specific next step the post asks the customer to take (book online, call, text, walk in, schedule a free check)

## Shared guardrails (non-negotiable)

- **Never fabricate reviews, testimonials, or customer quotes.** Real customer words only, with consent. AI-generated synthetic testimonials violate FTC endorsement guidance and several state AI-disclosure laws (NY, CA, EU).
- **Never fabricate promotions, discounts, or pricing.** Promotions must be input by the shop owner with start / end dates and any required disclosures. The AI never invents a "20% off this week" that the shop didn't authorize.
- **Never fabricate stats, claims, or guarantees.** "We're rated #1 in the city" needs a citation. "All our work comes with a lifetime warranty" needs to match what the shop's actual warranty terms say. Default position: don't include unverifiable claims.
- **Never make safety claims that exceed the underlying repair.** "Our brake job will save your life" is over-promising. "Properly maintained brakes are the most important safety system on your vehicle" is a defensible educational statement.
- **FTC endorsement-guide compliance.** Any post that uses a real customer's name, photo, or testimonial must have written consent, must be a real customer, must reflect the customer's actual opinion, and must disclose any compensation given for the testimonial.
- **GBP / Meta / TikTok TOS compliance.** No clickbait, no banned content, no auto-DM-spam patterns, no incentivized review solicitation in violation of platform rules.
- **Plain-text fallback for SMS.** Where applicable, marketing skills produce a plain-text variant for shops that send via SMS or RCS, since formatting strips on those channels.
- **Never imply OEM endorsement.** "Honda-recommended" requires actual OEM authorization. "Recommended by your owner's manual" is fine if the actual owner's manual recommends it; "Honda-approved" implies an authorization that an independent shop typically does not have.

## Hand-off pattern

Marketing skills hand into the customer-facing skills already in the library:

- A GBP post that drives a review → response handled by `review-response-generator.md`
- A short-form-video script that drives a booking → handled by `service-advisor-script.md` and `repair-estimate-builder.md`
- A newsletter that surfaces a deferred-work reminder → routed to `declined-services-followup.md`
- A newsletter that surfaces a state-inspection deadline → routed to `maintenance-reminder-sequence.md`
- A safety-recall mention in a newsletter → routed to `safety-recall-outreach-builder.md`

## When NOT to use a marketing skill

- The post is in response to a real customer's review → use `review-response-generator.md`
- The post is a 1:1 message to a specific customer → use `job-status-update-generator.md`, `maintenance-reminder-sequence.md`, or `declined-services-followup.md`
- The shop has no marketing strategy yet → marketing skills produce content, not strategy. Content without a strategy is noise.
