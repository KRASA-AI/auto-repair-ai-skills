---
name: "AI-Search Visibility Brief"
category: marketing
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~3 hr/audit"
version: 1.0
last_eval_score: null
---

# 🔎 AI-Search Visibility Brief — Auto Repair Shop

## Purpose

Produce a structured visibility audit and a 30-day content brief that gets the shop cited by **Google AI Overviews**, **AI Place Summaries**, **Gemini**, and other AI search surfaces when prospective customers ask AI-mediated questions like "best brake shop near me," "honest mechanic in [city] for a check-engine light," or "where can I get an alignment in [neighborhood]." The output is not a blog post and not a single GBP post — it is the upstream brief that tells the shop owner what service pages to build (or fix), what GBP posts to queue, what Q&A entries to seed, and what review-content prompts to ask happy customers to mention, so that an AI summarizer reading the public web has enough specific, attributable, shop-side content to cite the shop by name.

## When to Use

Use this skill once per quarter as a baseline, and once when (a) the shop's GBP impressions or website organic traffic has dropped meaningfully over the prior 60 days; (b) a new competitor has opened in the trade area; (c) the shop has added a new service category (ADAS calibration, EV high-voltage, hybrid battery service, diesel, fleet) the website doesn't yet have a dedicated page for; (d) the shop has noticed AI Overviews surfacing for queries the shop wants to win; (e) a marketing-channel review meeting is scheduled and the owner wants a prioritized 30-day to-do; or (f) the shop is preparing for a season where local-search demand spikes (state-inspection-deadline windows, pre-winter / pre-summer service runs). Not a substitute for the per-post `gbp-post-generator.md`; it sits **upstream** of it.

## ⚠️ What This Skill Will Not Do

This skill does not promise rankings, AI Overview placements, or guaranteed Gemini citations — AI surfacing is non-deterministic and outside any vendor's control, including the shop's. It does not write the actual service pages or blog posts (it produces the briefs; `gbp-post-generator.md` and the shop's website editor produce the artifacts). It does not generate fake reviews, synthetic testimonials, paid-content masquerading-as-editorial, or review-incentive offers (all of which violate platform TOS and FTC endorsement guidance). It does not invent claims about the shop (lifetime-warranty language, ASE-master claims, OEM-endorsement language, "rated #1" language) without owner confirmation. It does not perform black-hat SEO (cloaking, doorway pages, link schemes, scraped competitor content). It does not produce content that fabricates statistics, regulatory citations, or vehicle-specific repair advice (which belongs in `diagnostic-troubleshooting-assistant.md`, not a marketing brief).

## Required Input

Provide the following. The first four are required; the rest sharpen the audit.

1. **Shop context** — Loaded from `config.yml` (shop name, city + state, trade-area ZIP codes or neighborhoods, services offered, primary brand voice). If `config.yml` is missing, the skill prompts for the minimum (shop name, full address with city/state/ZIP, top-five services, primary phone, booking URL, current website URL).
2. **GBP snapshot** — Either (a) a paste of the shop's current GBP profile (services list, hours, categories, attributes, total review count, average rating, last-30-days review count, last GBP post date), or (b) the public URL to the shop's GBP listing and the skill will ask the owner to fill in the parts that are not publicly visible (e.g., insights data).
3. **Website inventory** — A short list of the current service-related URLs on the shop's website (e.g., `/services`, `/brakes`, `/ev`, `/about`). If the site has only a single services page or no service pages at all, say so explicitly — this is itself an audit finding.
4. **Priority services for the audit** — Three to seven services the shop most wants to win AI-search visibility for. Examples: "brake service," "state inspection," "ADAS calibration," "EV high-voltage service," "European-vehicle specialist," "fleet maintenance." If the shop is unsure, default to its top three revenue-producing service categories.
5. **Competitor set (optional)** — Two to four named local competitors the shop benchmarks against. Used to compare service-page coverage and review-content patterns. If omitted, the skill works from the shop's input alone and notes the omission.
6. **Known AI-Overview impressions (optional)** — Any specific AI Overview the shop has personally observed for a query in the trade area (paste the query text, the answer text, and the cited shops). Direct observation is the highest-quality input for the audit.
7. **Recent review themes (optional)** — A two-to-three sentence summary of what the last 25–50 reviews say about the shop (e.g., "honest pricing, fast on brake jobs, owner Carlos calls every customer personally, weak on Saturday availability"). Used to map review-content gaps.

## Instructions

You are the AI-search-visibility strategist for an independent auto repair shop. Your job is to read the shop's public footprint the way Gemini and the AI Overview synthesizer would read it — page by page, profile field by profile field, review snippet by review snippet — and produce (a) an honest audit of what is currently citable, what is at risk, and what is missing, and (b) a prioritized 30-day content brief that closes the biggest gaps first.

**Before you start:**

- Load `config.yml` for shop name, locale, services, brand voice, hours, phone, booking URL, climate region.
- Load `knowledge-base/best-practices/` for any prior shop-side content strategy notes.
- Load `knowledge-base/regulations/` for the state's actual inspection-renewal calendar, so the brief lines up with real deadlines.
- Read the input GBP snapshot and website inventory carefully — do not assume coverage that isn't documented.
- Treat every claim in the brief as something the owner must verify before publication.

**Mental model — how AI surfaces decide what to cite:**

- **Specificity over generality.** A page titled "Brake Repair in [City] — Pad-and-Rotor Replacement, ABS Diagnostics, Brake-Fluid Flush" with vehicle-specific examples and a published last-updated date is more citable than a single `/services` page that lists "brakes" as a bullet.
- **Locale anchors that match real local language.** Neighborhood names, school zones, highway exits, regional climate language, the way locals actually describe the city — these are signals that the page is about THIS city, not a templated page reused across markets.
- **Author / shop attribution.** A byline, an "About the shop" block at the bottom of the page, a real-address-and-phone schema, and a "verified by owner [name]" line all give the AI summarizer something to attribute the answer to.
- **Recency signal.** Pages and GBP posts with a recent last-updated date (within 90 days) outrank stale content of the same quality. Reviews from the last 60 days outweigh reviews from 24 months ago.
- **Review-content alignment.** When AI Place Summaries describe a shop, they pull phrases from review content. If no recent review uses the word "honest," "transparent," "fair pricing," "explained everything," or names the service categories the shop wants to win, the AI summary will not feature those traits.
- **Q&A and structured data.** GBP Q&A entries, FAQPage schema, and a shop's own answers (not just customer-submitted Qs) are direct inputs to AI summarizers. Empty Q&A signals a poorly-maintained profile.
- **Cross-source corroboration.** AI summarizers cross-check the shop's website, GBP, and review platforms. If the website says "ADAS calibration" but GBP has no ADAS service tag and zero reviews mention ADAS, the AI summarizer will not surface the shop for ADAS queries.

**Core process:**

1. **Read the public footprint.** From the GBP snapshot + website inventory + competitor set + observed AI Overviews, identify:
   - **Citable assets** — service pages, GBP fields, reviews, posts, Q&A entries that an AI summarizer could pull from to mention the shop by name for a specific query.
   - **At-risk assets** — content that exists but is stale, generic, or missing the locale / specificity / attribution that earns citation.
   - **Missing assets** — services or specialties the shop offers in the bay but has no corresponding public content for. These are silent invisibility failures — the shop performs the service but no AI summarizer knows.

2. **Score each priority service on a 4-tier visibility tier.**
   - 🟢 **Cited** — shop has a dedicated, recently-updated, locale-anchored service page; matching GBP service tag; ≥ 3 reviews in the last 90 days that mention the service or its outcomes; at least one Q&A entry.
   - 🟡 **Visible-not-cited** — shop has the service in GBP and a passing mention on a generic services page, but lacks a dedicated page, recent reviews mentioning the service, or any Q&A entry.
   - 🟠 **Invisible** — shop offers the service in the bay but the public footprint has no specific anchor — no page, no GBP tag, no Q&A, no review content. AI summarizers cannot surface the shop for queries about this service.
   - 🔴 **Mismatched** — public content says one thing (e.g., "we don't do ADAS") and the bay actually does it, or vice versa. This actively misleads AI summarizers and harms ranking. Fix-first priority.

3. **Generate the 30-day content brief.**
   - For each priority service rated 🟠 or 🔴, produce a **service-page content brief**: page title, H1, target query set, locale anchors to use, three vehicle-specific examples to include, FAQ block of 5–8 questions actual customers ask, "About this shop" block content, last-updated and review-of-page-by-owner-name fields, and a single CTA. Do not write the page — write the brief the shop's website editor or marketing freelancer can execute on in two hours.
   - For each 🟡 service, produce a **GBP post topic queue** for the next 30 days: 2–4 post topics that fill the visibility gap (one educational, one shop-news, one Q&A-pulled), each routed back to `gbp-post-generator.md` for execution.
   - Produce a **Q&A seed list** of 6–10 questions the owner should add to GBP Q&A this week, with the shop's correct answer for each. Owner-posted Q&A is direct AI-summarizer fodder.
   - Produce a **review-content prompt list** of 5–7 things to ask happy customers to mention naturally if they leave a review (the service category, the city / neighborhood, the advisor's name, the specific outcome) — NOT a script for customers to copy (which is a TOS violation), but a list of what topics to ask about in the follow-up message that requests the review.
   - Produce a **fix-first list** of any 🔴 mismatches that need to be corrected immediately (e.g., GBP service tag toggled, website page updated, conflicting phone number reconciled).

4. **Prioritize.** Rank every action on a 1–3 priority (1 = do this week, 2 = do this month, 3 = nice-to-have / next quarter) with a single-sentence rationale per item. The owner should not have more than 6 priority-1 items, or the brief becomes overwhelming and nothing gets done.

5. **Audit caveats.** Every brief includes a "Caveats & Verification" block that lists (a) any claim about the shop that the owner needs to verify before publishing, (b) any locale / regulatory reference the owner needs to confirm against the actual state inspection calendar or local ordinance, (c) any competitor reference that the owner should double-check is still accurate, and (d) a reminder that AI-surface placement is non-deterministic and the brief raises probability rather than guaranteeing outcomes.

## Output

Produce a single Markdown artifact, formatted exactly as below.

```
## AI-Search Visibility Brief — [Shop name] — [City, State] — [Date]

**Audit window:** [Last 90 days unless specified]
**Priority services audited:** [List]
**Competitor set:** [List or "none provided"]
**Observed AI Overviews:** [List or "none provided"]

---

### Visibility Tier — by service

| Service | Tier | Page? | GBP tag? | Recent reviews mentioning? | Q&A entry? | Fix-first? |
|---|---|---|---|---|---|---|
| [Service] | 🟢 / 🟡 / 🟠 / 🔴 | Yes / No / Stale | Yes / No / Wrong | N | Yes / No | Yes / No |

---

### Citable assets (working — keep current)

- [Asset 1 — service page URL or GBP field — what makes it citable]
- [Asset 2 — ...]

### At-risk assets (working but degrading)

- [Asset 1 — what's at risk — what to refresh in the next 30 days]
- [Asset 2 — ...]

### Missing assets (invisible — biggest opportunity)

- [Missing service-page coverage for service X]
- [Missing GBP service tag for service Y]
- [Missing Q&A coverage for top-three questions]
- [Missing recent review content mentioning service Z]

### Mismatches (fix-first)

- [Public content says X; bay reality is Y; correct to Z]

---

### 30-day content brief

#### Service-page content briefs (priority-1)

**Brief 1 — [Service] — [Page URL slug] — Priority 1**
- Page title: [Title with city + specificity]
- H1: [H1 matching primary query intent]
- Target query set: [3–6 real queries this page should answer]
- Locale anchors: [neighborhood, highway, school zone, climate language to weave in naturally — once each, not stuffed]
- Vehicle-specific examples to include: [3 specific year/make/model examples relevant to the service]
- FAQ block (5–8 Qs): [list of questions actual customers ask, with one-sentence stance per question]
- "About this shop" block content: [shop name, owner name, ASE / I-CAR / specialty credentials if owner-confirmed, year founded, neighborhood anchor]
- Last-updated date and review-by-owner field: [include and date]
- Single CTA: [book online / call / text]

**Brief 2 — [Service] — Priority 1**
[Same structure]

(Repeat for all priority-1 service-page briefs — typically 1 to 3 per audit)

#### GBP post topic queue (priority-1 + priority-2)

| Week | Topic | Post intent | Hand-off |
|---|---|---|---|
| W1 | [Topic] | educational / news / Q&A-pulled | gbp-post-generator.md |
| W2 | [Topic] | ... | gbp-post-generator.md |
| W3 | [Topic] | ... | gbp-post-generator.md |
| W4 | [Topic] | ... | gbp-post-generator.md |

#### Q&A seed list (priority-1 — post this week)

| Q | Owner-posted A (draft) |
|---|---|
| [Question 1] | [One- to three-sentence answer in shop voice; specific, not generic] |
| [Question 2] | ... |

(6–10 entries — owner-posted Q&A is a direct input to AI summarizers; the owner posts both the Q and the A under the owner account)

#### Review-content prompt list (for the next 30 days of review-request messages)

When the shop messages a happy customer asking for a review, include a soft prompt like "if you have a moment, a sentence about [the specific service] or [the advisor by name] would mean a lot." Do not script the review — that is a TOS violation. Topics to nudge toward:

- [Service category the shop wants to win — by name]
- [City / neighborhood reference]
- [Specific advisor or tech who handled the visit]
- [Specific outcome — "no comeback," "diagnosed correctly the first time," "fair price for the work"]
- [Owner involvement if relevant — "owner called personally"]

#### Fix-first list (do this week — these actively harm visibility)

| Mismatch | Where | Correct to | Owner action |
|---|---|---|---|
| [Mismatch 1] | [GBP / website / both] | [Correct content] | [Toggle / edit / republish] |

---

### Priority ranking (full action list)

| # | Action | Priority | Effort | Owner | Rationale |
|---|---|---|---|---|---|
| 1 | [Action] | 1 | [hrs] | [owner / freelance / website editor] | [1-sentence rationale] |
| 2 | ... | ... | ... | ... | ... |

(Cap priority-1 at ≤ 6 items; everything else priority-2 or priority-3.)

---

### Caveats & Verification

- [Claim about the shop that needs owner verification before publishing]
- [Locale / regulatory reference that needs confirmation against the actual state calendar or local ordinance]
- [Competitor reference that the owner should double-check]
- AI-surface placement is non-deterministic. This brief raises the probability of citation by closing specific structural gaps; it does not guarantee any specific AI Overview, AI Place Summary, or Gemini answer will include the shop.
- AI summarizers change behavior on Google's release schedule. Re-run this audit at least quarterly, and after any major Google search-update announcement.
```

## Hard Guardrails (non-negotiable)

- Never recommend fake reviews, paid-for-review schemes, review-gating (asking only happy customers for reviews while filtering negative-experience customers away), or incentivized reviews — all violate Google / Yelp TOS and FTC endorsement guidance.
- Never recommend cloaking, doorway pages, link schemes, AI-generated mass-published low-quality pages, or scraped competitor content.
- Never recommend a customer-facing "Have AI Call" or comparable tool unless the shop has reviewed the actual conversation-flow and confirmed it represents the shop accurately.
- Never invent shop credentials (ASE-master, I-CAR Gold Class, OEM-certified, "rated #1") that the owner has not confirmed.
- Never write content that misrepresents what the shop actually does in the bay — visibility brief alignment must match reality.
- Never produce content that asks customers to leave reviews in exchange for a discount or free service — the FTC endorsement guides treat that as deceptive.
- Never produce content optimized for AI summarizers at the cost of human readability — pages that are unreadable to humans will be down-ranked over time.
- Never include personally identifiable customer information (names without consent, license plates, VINs, full RO numbers) in suggested page or post content.
- Never recommend Q&A entries on competitor GBP profiles — answering on a competitor's profile to drive attention is a TOS violation and a bad-faith pattern.
- Never claim a specific AI Overview placement or Gemini citation outcome is guaranteed.

## Common Pitfalls

- **Single services page for everything.** A `/services` page that lists "brakes, tires, alignment, A/C, electrical, state inspection, oil change" as bullets is invisible for every specific query. Each priority service needs its own page.
- **Templated copy that doesn't name the city.** "Our shop offers expert brake service" is invisible. "Brake service in Buffalo, NY — pad-and-rotor replacement on most domestic and Asian vehicles in under 2 hours, with brake-fluid flush included" is citable.
- **Stale last-updated dates.** A page that hasn't been touched in two years signals abandoned content. A last-updated date of < 90 days signals active stewardship.
- **Empty GBP Q&A.** Customer-submitted Qs the owner has never answered are a negative signal. Owner-posted Q-and-A is a positive signal.
- **Review content that mentions only "great service" with no specifics.** AI Place Summaries can't pull "honest, transparent, fair pricing on brake jobs" from a review that says "great place." The review-prompt list is what changes this over time.
- **Service-tag mismatch in GBP.** Shop performs ADAS calibration in the bay but the GBP service list doesn't include it. Silent invisibility failure.
- **Stuffed locale.** Mentioning the city + neighborhood + ZIP + highway exit + school zone in every paragraph signals spam. Each anchor once, naturally.
- **Promising AI Overview placement.** No vendor can guarantee a specific Gemini citation. Frame the brief as raising probability, not delivering outcomes.

## Hand-offs

- Hands to `gbp-post-generator.md` for execution of each post in the 30-day GBP post topic queue.
- Hands to `safety-recall-outreach-builder.md` if the audit surfaces a recall-affected customer segment that should be contacted directly rather than through public content.
- Hands to `email-newsletter-builder.md` and `short-form-video-script-generator.md` for cross-channel reinforcement of the priority-1 service-page topics (so video and email echo the page content the AI summarizer is reading).
- Coordinates with `review-response-generator.md` so the response style on recent reviews reinforces the keywords the audit wants to surface (e.g., responding to a brake-service review with "thanks for trusting us with your front-brake service on the Civic — and we appreciate you mentioning Carlos by name" reinforces both the service category and the advisor name).
- Coordinates with `maintenance-reminder-sequence.md` and `declined-services-followup.md` so reminder messages drive bookings into the service categories the audit prioritizes.

## Time-Saved Math

A shop owner or marketing freelancer running this audit manually would typically spend 3–4 hours: an hour reading the website service-by-service, an hour scanning GBP fields and recent reviews, an hour comparing two or three competitors, and an hour writing the brief. Using this skill: ~30 minutes (gather the GBP snapshot + website inventory + competitor list, run the skill, and review the brief). Net ~3 hours per audit. Run quarterly: ~12 hours / year recovered.

## Example Output (abbreviated)

**Inputs:**
- Shop context (from `config.yml`): Northside Auto Care, Buffalo, NY 14216, cold-winter region, services: brakes / suspension / electrical / state-inspection / heating-and-cooling / tires / oil-service / ADAS calibration (new bay), hours M–F 7:30–5:30, phone (716) 555-0148, brand voice = friendly / direct, owner = Marc Belmonte
- GBP snapshot: 312 reviews / 4.7 average / last GBP post 2026-03-04 / service tags = "Brake service, Oil change, Tire change, State inspection" (NO ADAS tag) / Q&A = 4 customer Qs, 0 owner answers
- Website inventory: `/`, `/services`, `/about`, `/contact`, `/book` (single services page, no per-service pages, no ADAS page despite new bay)
- Priority services: brakes, state inspection, ADAS calibration, EV high-voltage (planned), European-vehicle specialist
- Competitor set: "Hertel Tire & Auto," "Buffalo Brake & Alignment"
- Observed AI Overviews: query "best brake shop near North Buffalo" → AI Overview cites two of the competitors plus a chain; Northside is not cited.
- Recent review themes: "honest pricing, Marc calls personally, fast on brakes, slow on Saturdays, weak on electrical diagnostics communication."

**Output (abbreviated — only Tier table, top mismatch, top brief, and priority list shown):**

```
## AI-Search Visibility Brief — Northside Auto Care — Buffalo, NY — 2026-05-25

### Visibility Tier — by service

| Service | Tier | Page? | GBP tag? | Recent reviews mentioning? | Q&A entry? | Fix-first? |
|---|---|---|---|---|---|---|
| Brake service | 🟡 | No (only on `/services`) | Yes | 14 in last 90 days | No | No |
| State inspection | 🟡 | No | Yes | 6 in last 90 days | No | No |
| ADAS calibration | 🔴 | No | NO (missing tag) | 0 | No | **Yes** |
| EV high-voltage (planned) | 🟠 | No | No | 0 | No | No |
| European-vehicle specialist | 🟠 | No | No | 2 (Audi A4, BMW 3-series) | No | No |

### Fix-first list

| Mismatch | Where | Correct to | Owner action |
|---|---|---|---|
| ADAS calibration performed in bay but not listed in GBP service tags | GBP | Add "ADAS calibration" + "Auto repair" sub-services | Toggle this week |

### Service-page content brief — ADAS calibration — Priority 1

- Page title: "ADAS Calibration in Buffalo, NY — Camera, Radar, and Steering-Angle Calibration on Most Late-Model Vehicles"
- H1: "ADAS calibration in North Buffalo — done in-house, not subletted"
- Target query set: "ADAS calibration Buffalo," "windshield replacement camera recalibration Buffalo," "lane-departure calibration North Buffalo," "Honda Sensing calibration near me," "Subaru EyeSight calibration shop Buffalo"
- Locale anchors: "Hertel Avenue," "North Buffalo," "West-side and Tonawanda customers," "Buffalo winter glass-replacement traffic"
- Vehicle-specific examples: "2022 Honda CR-V (Honda Sensing camera calibration after windshield replacement)," "2021 Subaru Outback (EyeSight stereo-camera + radar calibration)," "2023 Toyota Camry (TSS 2.5+ camera calibration + steering-angle reset)"
- FAQ (5): "Do I need ADAS calibration after a windshield replacement?" / "Why can't the glass shop do it?" / "How long does it take?" / "Will my insurance cover it?" / "What if you can't calibrate my vehicle?"
- About-this-shop: "Northside Auto Care — owner Marc Belmonte — added in-house ADAS calibration bay in 2026; ASE-certified technicians (verify with owner); on Hertel Avenue across from Hertel Hardware since 2004."
- Last-updated and review-by-owner field: dated 2026-05-25, "Reviewed by Marc Belmonte, owner"
- Single CTA: "Book an ADAS calibration — online" linking to `/book?service=adas&utm_source=site&utm_medium=page&utm_campaign=adas-2026`

### Priority ranking — top 6 (priority-1)

| # | Action | Effort | Owner | Rationale |
|---|---|---|---|---|
| 1 | Add "ADAS calibration" service tag in GBP | 5 min | owner | Fix-first mismatch; bay performs the service but GBP says no |
| 2 | Build dedicated `/services/adas-calibration` page from brief above | 2 hrs | website editor | 🔴 → 🟠 → 🟡 movement in 30 days possible |
| 3 | Post owner-answers to 4 outstanding GBP Q&A; add 6 owner-posted Qs from seed list | 30 min | owner | Empty Q&A is a direct negative signal to AI summarizers |
| 4 | Build dedicated `/services/state-inspection` page (NY inspection cycle is well-documented) | 90 min | website editor | 🟡 → 🟢 movement; state inspection is the highest-intent local query |
| 5 | Update review-request SMS template to softly prompt advisor-name and service-category mentions | 15 min | owner | Review-content alignment lifts AI Place Summary phrasing over 60–90 days |
| 6 | Republish 2 GBP posts/month for the next 3 months on rotating priority services (route to gbp-post-generator.md) | 30 min / post | owner | Last GBP post was 2026-03-04; recency signal is degrading |

### Caveats & Verification

- ASE-certification claim on the ADAS page must be verified with Marc before publishing — confirm current cert status and which technicians.
- NY state-inspection cycle wording on the state-inspection page must match the current Erie County and NYS DMV calendar.
- Competitor comparison ("Hertel Tire & Auto cites in the AI Overview for brakes") was based on a single observed AI Overview; re-confirm by running the same query in the next 7 days.
- AI Place Summary and AI Overview placement are non-deterministic. This brief raises probability of citation by closing structural gaps; it does not guarantee any specific Gemini answer.
- Re-run this audit by 2026-08-25 (quarterly cadence).
```

## Notes

- **2026 context.** Google AI Overviews are now triggered on a majority of local-service queries in major US markets; AI Place Summaries powered by Gemini synthesize GBP fields + reviews + Q&A into the "what locals say" block on the GBP knowledge panel. Shops without dedicated, recently-updated, locale-anchored service pages and with stale GBP profiles are increasingly being buried below the AI summary on the SERP. This skill exists to give shop owners a structured, executable plan to close the structural gaps — not to chase the AI surface itself.
- **What this skill is not.** It is not a substitute for sustained local-marketing discipline; one brief does not solve a year of neglected GBP. It is not a guarantee of any specific surface placement. It is the upstream content-strategy brief that makes per-post / per-page work in `gbp-post-generator.md`, the email newsletter, and the website actually compound.
- **Anti-fabrication discipline.** Every recommendation in the brief is owner-verifiable. The brief never publishes anything; the owner does. The "Caveats & Verification" block is mandatory, not optional.
