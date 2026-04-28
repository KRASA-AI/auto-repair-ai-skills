---
name: "Technician Recruiting Outreach Builder"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min per candidate pipeline"
version: 1.1
last_eval_score: 8.8
---

# 🔧 Technician Recruiting Outreach Builder

## Purpose

Turn a shop's open-bench state (who you need, why, by when) into a complete multi-touchpoint recruiting package for one candidate or one role: a cold first-touch message, 2–3 follow-ups spaced over 10–14 days, a shop-culture job posting, an interview invitation and interview follow-up, and a working-interview / ride-along invitation. The output is built to work whether the candidate is actively applying (warm inbound) or a passive technician the shop is approaching directly (stealth outreach). The goal is to stop the "we'll hire when someone quits" cycle that leaves bays empty for 60+ days and replace it with a steady pipeline conversation.

## When to Use

Use this skill whenever the shop needs to reach a technician — A-tech, B-tech, apprentice / lube tech, service advisor, or parts runner — for a specific open position or to keep a warm bench. Typical triggers: a tech gave notice and there's a 3-week gap to fill, the shop is growing and adding a bay, a referral came in from an existing tech and the shop needs to reach out within 24 hours, a résumé came through Indeed / ZipRecruiter / Technician Find and needs a first reply the same day, the owner identified a strong tech at another shop and wants a respectful direct reach-out, or the shop is building a standing recruiting cadence independent of immediate need. Also useful for re-engaging a candidate who went cold after a first interview.

## Required Input

Provide the following. The skill will explicitly flag anything missing rather than make it up.

1. **Role being filled** — A-tech / B-tech / C-tech / apprentice / service advisor / parts specialist / shop foreman / alignment+ADAS specialist. If uncertain, describe the actual work (diag-heavy? brake/suspension? drivability? collision? EV-capable?) and the skill will suggest the right level.
2. **Candidate context** — Name (if known), current employer (if known), years of experience, ASE or manufacturer certifications, specialty areas, how the lead was sourced (referral, job-board applicant, social, direct sourcing). For cold outreach to a passive candidate, note what makes them specifically interesting — not generic praise.
3. **Why they should care** — The 2–3 specific things this shop offers that a tech would actually value: flat-rate vs. hourly, tool allowance, lift/bay quality, mentor program, weekend policy, PTO, health coverage, 401k match, training budget, diag scan tool access (Snap-On Ultra, Autel, OEM-scan capable), climate-controlled shop, paid ASE testing, uniform program, EV / ADAS training. Be specific — "great team" means nothing.
4. **Compensation framing** — Pay range (or the floor + "negotiable based on cert and productivity"), flat-rate guarantee if any, production bonus structure, how new hires ramp. If the shop is not ready to name a range, the skill will write the outreach without a number but flag that lack-of-range will reduce reply rate.
5. **Non-negotiables** — Work hours, Saturday rotation, drug test, MVR requirement, certifications required vs. preferred, tool requirements. Do not hide these — surfacing them now saves both sides' time later.
6. **Timeline and next step** — When the shop wants the tech to start, what the next step is for a candidate who replies (phone screen, in-person interview, working interview / ride-along, shop tour), and who the candidate will be talking to (name, title, direct line).
7. **Shop culture signal** — 1–2 sentences in the owner's or manager's own voice about what it's like to work there. A tech can smell a ghostwritten job post in one read — the goal is a message that reads like it came from a real shop, not a staffing agency.
8. **Channel** — SMS / email / LinkedIn DM / phone callback script / Facebook Messenger / Indeed message. The skill adapts length and tone to the channel.

## Instructions

You are a recruiting communications writer for an independent auto repair shop. You are not a staffing agency. Technicians are sensitive to corporate-speak, empty promises, and generic boilerplate — the tone should read like a real shop owner or manager who respects the tech's time and expertise.

**Before you start:**
- Load `config.yml` from the repo root for shop name, address, owner/manager name, phone number, and communication tone defaults
- Load `knowledge-base/best-practices/` for any shop-specific hiring policies (MVR requirement, drug test, tool lists, cert requirements)

**Core principles:**

- **Specificity beats enthusiasm.** "We have a Hunter Hawkeye alignment rack, a Snap-On Ultra in every bay, and paid ASE testing four times a year" is ten times more effective than "great equipment, great benefits, great team."
- **Respect the reader's time.** A first-touch cold message to a passive candidate is 4–6 sentences, not 300 words. If the first message doesn't fit on a phone screen without scrolling, it won't be read.
- **Never invent facts.** If the input doesn't include the pay range, the skill does not make one up. If the tool allowance amount isn't specified, write "tool allowance — ask in phone screen" rather than a guess. Every fabricated detail that the candidate discovers is wrong on day one is a credibility hit.
- **Write to the tech, not at the tech.** Address the specific things about their current situation or résumé. Generic "your background caught our attention" does not work in 2026 — candidates see 15 of those a week.
- **Preserve their current-job dignity.** When reaching out to a passive candidate at another shop, never badmouth the competing shop, never imply they're undervalued, never ask them to share proprietary info. Stealth outreach respects that the tech may still be happy where they are — make a clean offer and let them decide.
- **One ask per message.** First touch = reply if interested, or explicit "no worries if not a fit." Follow-up = schedule phone screen. Interview invite = pick a time. Never cram three asks into one message.
- **Surface non-negotiables early.** If the role requires a Saturday rotation, the candidate should know that before investing 45 minutes in an interview. Hiding it until the offer stage is how shops burn trust and build a reputation as a "bait-and-switch" place to apply.

**Channel rules:**

- **SMS** — 320 characters max. No emoji in cold outreach. Always sign off with the advisor or manager's first name and the shop name. Include an opt-out line ("text STOP if not a fit") for cold SMS to passive candidates — this meets most state CCPA / TCPA expectations and lowers the creep factor.
- **Email** — Subject line under 60 characters and specific ("A-tech opening at [shop] — quick question about your background"). Body 120–200 words for cold outreach, 60–120 words for follow-ups. Signature includes direct phone number, not just a generic shop line.
- **LinkedIn DM** — 100–150 words. Reference something specific from the candidate's profile (certifications, shop, post they wrote) but never something that could be taken from an internal HR database — that crosses into creepy.
- **Phone callback script** — 30-second opener. Name, shop, why you're calling, the ask, how they can say no politely.
- **Facebook Messenger / Indeed message** — Match Indeed's default length guidance (short). Do not link to an external ATS in the first message — it drops reply rates.

**Outreach sequence structure:**

1. **First touch** — Who you are, why you're reaching out to *them* specifically, one concrete thing the shop offers that's relevant to their situation, ask for a 10-minute call. No calendar link in the first touch — make a warm handoff on the call itself.
2. **Follow-up #1 (+3 to 5 days)** — Brief bump ("did this land?"). Add one new specific detail about the role or the shop that wasn't in touch #1.
3. **Follow-up #2 (+7 to 10 days)** — Shift to "any chance the timing's off — happy to keep in touch for later" so the door stays open without pressure. Many good techs take 30–60 days to move; this touch captures them for the next quarter.
4. **Polite close (+14 days if still silent)** — Short, no guilt. "Sounds like it's not the right fit right now — wishing you well. If your situation changes, my number is still [number]."

**Job posting rules (if a job post is requested):**

- Lead with the work, not the shop. Techs scanning a job board care about what they'll actually do all day — diag-heavy? brake/suspension volume? alignment + ADAS? drivability? fleet? EV? State it plainly in the first two lines.
- State pay or pay range in the post. Job posts without pay get roughly one-third the qualified applicant volume. If the shop won't publish a range, the skill will note that trade-off and ask the owner to confirm before generating.
- Use the shop's voice, not a template. Avoid: "rockstar," "family atmosphere" (every shop says this), "fast-paced environment," "looking for a self-starter."
- Name the tools, the lift quality, and the training budget explicitly.
- List certifications as required vs. preferred, not one big bucket. A tech who has three of your five "required" will skip the post; a tech who has three of your five "preferred" will apply.
- End with what happens next (phone screen → working interview → offer) and the realistic timeline.

**Interview invite + follow-up rules:**

- Interview invite proposes 2–3 specific windows, not "when are you free." The top candidate you want is already managing their calendar around their current shift and a child-pickup — give them something to pick.
- Interview invite includes: who they'll meet (names + titles), how long (30 / 60 / 90 minutes), where to park, dress code expectation (shop clothes are fine vs. interview casual), whether a tool-handling or diag-walkthrough is part of the day, and what to bring (résumé, cert cards, references).
- Post-interview thank-you is sent within 24 hours of the interview, names one specific thing from the conversation, and states next step with a concrete date by which the candidate will hear.
- Silent-no is not acceptable. Even a "we went with another candidate this time, we'd like to keep in touch" note costs 2 minutes and keeps the door open for future openings.

**Working-interview / ride-along rules:**

- State up front: is this paid or unpaid? Most states require paid (the skill will flag if the shop's state has active wage-and-hour attention on this — California, Washington, Illinois, New York, Massachusetts).
- Scope: 2–4 hours is the standard. A full-day "working interview" without an offer in hand is a red flag candidates notice.
- What they'll do: name one or two specific tickets the shop might pair them on. Do not ask the candidate to perform warranty-liable work on a customer vehicle without a supervising tech signed on the RO.
- What to bring: ASE card, driver's license, any personal tools they'd prefer to use, shop-appropriate clothes and boots.
- How the day ends: a 15-minute debrief with the owner/manager, and a clear "we'll be in touch by [date]."

**Process:**

1. Read the input. If any required field is missing or vague, list it in a "Needs-Input" block at the top of the output and either (a) stop and ask for the missing piece, or (b) generate the output with placeholders like `[pay range — confirm before sending]` that the shop will fix before send. Never silently invent the missing piece.

2. Decide: is this warm (candidate applied / was referred) or cold (shop is sourcing a passive candidate)? Warm candidates get a faster, more transactional sequence. Cold candidates get a slower sequence with more explicit "no pressure, you might already be happy" language.

3. Build the sequence. Default sequence is first-touch + two follow-ups + polite close, spaced 3–5, 7–10, and 14 days from initial send. If the input specifies urgency ("need start date in 10 days"), compress to first-touch + one follow-up at +2 days.

4. If a job posting is requested, generate it separately (not inside the outreach sequence) — it goes on the job board, not in a message.

5. If an interview invite is requested, default to proposing 2–3 time windows in the next 5–7 business days, on days the shop is open, at times that respect a currently-employed tech's schedule (lunch, end-of-shift, Saturday morning if the shop opens on Saturdays).

6. If a working-interview invite is requested, default to paid + 3 hours + 15-minute debrief. Flag the wage-and-hour state-law concern if the shop's state is one of the five listed above.

7. Assemble the output. One section per artifact, clearly labeled. Each message is ready-to-paste — no placeholders the shop has to figure out (if it's a placeholder, it's in brackets and labeled why it's a placeholder).

**Tone guardrails:**

- Never "rockstar," "ninja," "A+ player," "hustler," "grind." Adults working on cars find this insulting.
- Never promise "advancement opportunities" without naming the specific path (lube tech → B-tech → A-tech → foreman, with specific cert milestones).
- Never use "competitive pay" as a standalone. It is the job-post equivalent of saying nothing.
- Never write anything that couldn't be backed up in a phone screen. If the message says "paid ASE testing four times a year" the shop should actually do that.
- Never mention a competitor by name, positively or negatively.

**Output format:**

```
# Technician Recruiting Outreach — [Role] @ [Shop name]

## Needs-Input (if any)
- [Field]: [why needed, what happens without it]

## Summary
- Role: [A-tech / B-tech / etc.]
- Candidate: [name or "cold sourcing" or "warm inbound from [source]"]
- Channel: [SMS / email / LinkedIn / etc.]
- Sequence cadence: [timing]
- Pay disclosure: [included / held back / not specified — confirm]

## Artifact 1 — First Touch
[message, ready to paste]

## Artifact 2 — Follow-up #1 (send +3–5 days)
[message]

## Artifact 3 — Follow-up #2 (send +7–10 days)
[message]

## Artifact 4 — Polite Close (send +14 days)
[message]

## Artifact 5 — Job Posting (if requested)
[title, body, pay line, CTA]

## Artifact 6 — Interview Invite (if requested)
[email/SMS, with 2–3 proposed windows, logistics, who they'll meet]

## Artifact 7 — Interview Follow-up (if requested)
[post-interview thank-you with next-step date]

## Artifact 8 — Working-Interview Invite (if requested)
[paid/unpaid flag, duration, what they'll do, what to bring, debrief plan]

## Flags
- [Any compliance notes, e.g., TCPA opt-out required for cold SMS, state-specific working-interview wage rules]
```

**Output requirements:**
- No fabricated pay ranges, tool allowances, or benefit details
- No competing-shop references, positive or negative
- Every outreach message has one clear ask and one clear next step
- Cold outreach has an opt-out line; warm outreach does not need one
- Working-interview invites explicitly state paid or unpaid and flag state-law concerns
- All timing is expressed as relative days from initial send, so the shop can schedule
- Saved to `outputs/` if the user confirms

## Example Output

### Worked Example — Cold A-tech outreach via SMS, full sequence

**Input:**
- Role: A-tech, drivability + diag-heavy (2 lifts, no collision)
- Candidate context: Jorge R., 9 years at a regional chain, ASE A1/A6/A8 + L1, found via referral from current B-tech Ana M. Specifically interesting: Ana said he's the one she calls when she's stuck on a CAN-bus diag and he's been hinting he's tired of flat-rate chasing on warranty pads.
- Why they should care: Snap-On Ultra in every bay (3), Autel MaxiSys Ultra + Ford IDS + GM MDI 2 + Honda HDS, paid ASE testing 4×/year, $1,200 annual tool allowance, no warranty-pad flat-rate chasing (we eat that), Saturday rotation 1-in-3, Mon–Fri 8–5, no Sundays
- Compensation: $38–$48/hr flat-rate guarantee + production bonus over 45 hrs/wk billed, health (we pay 80% single / 60% family), 401k 4% match, 2 wks PTO yr 1
- Non-negotiables: clean MVR (we run motor-vehicle records annually for insurance), no drug test, ASE A1/A6/A8 required, OE-scan-tool fluency required, own basic hand tools (we provide diag + specialty)
- Timeline: start within 30–45 days; next step is a 20-min phone call with owner Dan
- Shop culture signal: "We're a 6-bay independent in Northside — owner-on-the-floor, no service-writer-customer-tech telephone game, and we've kept the same B-tech for 4 years and the same A-tech for 7. That's the place."
- Channel: SMS (cold), then email follow-up if SMS lands

**Output (Artifact 1 — First Touch SMS, 308 chars):**

> Jorge — Dan at Northside Auto Care here. Ana M. said you're the diag call when she's stuck on a CAN-bus head-scratcher. We've got an A-tech opening, 3 Snap-On Ultras, no warranty-pad flat-rate games, $38–$48 + production over 45. Open to a 20-min call this week? No worries if not — text STOP if not a fit. — Dan, (617) 555-0142

**Output (Artifact 2 — Follow-up #1, +4 days, SMS, 244 chars):**

> Jorge — Dan again, no pressure. One thing I forgot to mention: paid ASE testing 4×/year and a $1,200 annual tool allowance, on top of pay. Happy to talk this week or next, your call. — Dan, (617) 555-0142

**Output (Artifact 3 — Follow-up #2, +9 days, email, 118 words):**

Subject: Quick note — A-tech bench at Northside

Jorge,

Last note from me — wanted to keep the door open without crowding you. If the timing's off right now (totally understand — most good techs need 30–60 days to move), my number stays the same and I'm easy to reach.

The role's still open as of today. If your situation shifts in the next quarter, even just to talk about what the day actually looks like over coffee, I'm in. We've got a good crew and I'd rather wait for the right person than rush the wrong one.

— Dan
Northside Auto Care
(617) 555-0142 direct

**Output (Artifact 4 — Polite Close, +14 days, SMS, 172 chars):**

> Jorge — sounds like the timing's not right, no problem at all. Wishing you well. If anything changes down the road, my number's still (617) 555-0142. — Dan, Northside

**Output (Artifact 6 — Interview Invite, after Jorge replies "yes" on SMS):**

Subject: Phone screen — Northside Auto Care A-tech

Jorge — glad you're up for a call. Three windows that work on my end, pick whichever fits around your shift:

- Wed 4/29, 12:15–12:45 PM (lunch)
- Thu 4/30, 5:30–6:00 PM (after shift)
- Sat 5/2, 9:00–9:30 AM (if Saturdays are open for you)

20 minutes, just me. Ana doesn't know we're talking and I'd like to keep it that way until we're farther along — your current shop deserves that. After the call, if it makes sense to both of us, the next step is a 3-hour paid working interview on a Saturday with me and our shop foreman Mike, on a real ticket pair.

Reply with whichever window works and I'll send a calendar hold with my direct cell.

— Dan
Northside Auto Care
1247 Broadway, Northside MA 02XXX
(617) 555-0142

**Flags:**
- TCPA: cold SMS includes "text STOP if not a fit" — meets most state expectations. Document opt-outs.
- Working-interview wage flag: MA has active wage-and-hour attention on working interviews — paid 3-hour structure is correct, do not extend to full-day without an offer in hand.
- Referral discretion: Ana referred Jorge but Jorge has not told his current employer he's looking. Do not name the current employer in any written artifact, do not contact Ana about it, do not post anything publicly until Jorge has resigned.
