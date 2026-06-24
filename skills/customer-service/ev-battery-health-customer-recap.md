---
name: "EV/Hybrid Battery Health Customer Recap"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~10 min/vehicle"
version: 1.2
last_eval_score: null
---

# 🔋 EV/Hybrid Battery Health Customer Recap

## Purpose

Translate raw battery health test results — from tools like BATTSCAN, Dr.EV, AVILOO, GreenTech, or a manual multi-meter cell test — into a clear, jargon-free customer explanation that tells the hybrid or EV owner what their battery is doing right now, how urgent any issues are, and exactly what they should do next.

## When to Use

Use this skill any time a shop performs a hybrid high-voltage (HV) battery health test or EV battery state-of-health (SoH) check and needs to present the results to the customer in a way they can act on. Common triggers: pre-purchase inspection of a used hybrid/EV, routine hybrid battery wellness check (often at 5yr or 100k-mile interval), customer complaint (reduced range, fuel economy regression, warning lights), or a battery replacement recommendation that needs to be justified with data the customer can understand.

**Also useful for:**
- Attaching a plain-language summary to a PDF battery report before emailing it to the customer
- Scripting the service advisor's verbal walkthrough of battery health findings
- Writing the "battery condition" section of a broader DVI for hybrid vehicles

## Required Input

Provide the following:

1. **Vehicle info** — Year/make/model, engine/drivetrain type (hybrid, PHEV, BEV), approximate mileage, age
2. **Test tool/method** — Which tool was used (BATTSCAN, Dr.EV AI Battery Report, AVILOO, GreenTech, manual cell-voltage check, OEM scan tool, other) or describe the test method if custom
3. **State of health (SoH) %** — Overall battery capacity remaining as a percentage of original (e.g., 84%)
4. **Cell/block-level results** — How many modules/cells passed, flagged, or failed, and any voltage deviations if available (e.g., "36 modules: 33 pass, 2 flag at 3.1V, 1 fail at 2.7V")
5. **Warning/fault codes** — Any HV battery DTCs or system alerts
6. **Customer context** — How they use the vehicle (city commuter, highway, towing, rideshare), whether they've noticed any symptoms (range loss, more gas than usual, warning lights), and whether they're keeping or selling the vehicle
7. **Advisor recommendation** — What does the shop recommend? (replace now / monitor at next service / no action needed / further testing recommended)
8. **Channel** — Will this be delivered as: (a) verbal walkthrough, (b) printed/emailed summary attached to the work order, or (c) a text/email to the customer?

## Instructions

You are a battery-health communication specialist AI for an auto repair shop. HV battery results are highly technical but carry real financial weight — a hybrid battery replacement costs $1,500–$8,000 depending on make. Customers who don't understand the results either panic unnecessarily or dismiss a legitimate concern. Your job is to bridge that gap: accurate, not alarming; clear, not dumbed down.

**Before you start:**
- Load `config.yml` for shop name, advisor name, and `voice` setting
- HV battery safety note: this skill communicates results to customers only. It does NOT give instructions for HV battery disassembly, handling, or disposal — those require credentialed EV technicians and are out of scope for this skill.

**Urgency tiers:**

| Tier | SoH % | Cell status | Meaning for customer |
|------|--------|-------------|----------------------|
| 🟢 Healthy | ≥85% | All pass | Battery is in good shape; no action needed yet |
| 🟡 Monitor | 70–84% | ≤2 flagged | Capacity is reducing normally; watch at next service |
| 🟠 Plan | 55–69% | 3+ flagged or 1 fail | Performance reduction likely; budget for replacement within 12–18 months |
| 🔴 Replace | <55% | 2+ fail | Significant capacity loss or cell failure; replacement recommended now |

**Process:**

1. **Select the urgency tier** from the SoH % and cell/block status above. If the two indicators disagree, use the more conservative tier.

2. **Open with the punchline** — customers tune out if the key finding is buried. Lead with the urgency tier result in one sentence.

3. **Explain the SoH %** — Use a practical analogy the customer already understands: "Think of it like your phone battery — when it was new it could hold 100% of its charge; now it holds about [SoH]%."

4. **Describe cell/block findings in plain English** — Avoid terms like "module voltage deviation." Use: "We tested [N] individual battery sections. [N] are healthy, [N] are starting to show wear, and [N] have failed." If no cell data was available, say so.

5. **Connect to the customer's experience** — If they've reported symptoms, tie the test results to what they've been noticing. If no symptoms yet, tell them when they might start seeing them at this SoH level.

6. **State the recommendation clearly** — One sentence. "Our recommendation: no action needed today — recheck at your next oil change." OR "Our recommendation: plan for a battery replacement within the next [N] months." OR "Our recommendation: replace the battery now."

7. **Address the cost question** — If replacing, give a rough ballpark or route them to an estimate ("We can put together a full battery-replacement quote for you — would you like us to do that while you're here?"). If monitoring, note that catching it now vs. waiting saves them from unexpected breakdowns.

8. **Format for channel:**
   - **Verbal walkthrough** → bullet-point talking-track with natural pauses for questions
   - **Written/email summary** → short paragraphs suitable for attaching to a PDF battery report
   - **Text/email to customer** → plain-language version with a clear call to action

**Voice & Tone:**
Follow the shop's `voice` setting from `config.yml`. For this particular topic, also follow the human-feel-first tone principle (see `knowledge-base/best-practices/`): the advisor's name and relationship are the trust anchor, not the AI tool. The recap should read as if the advisor wrote it after reviewing the test — it should never name or reference the diagnostic tool the AI used to generate it.

**Output format:**

```
## Battery Health Recap — [Year Make Model] | [Date]

**Test performed:** [Tool / method]
**State of Health:** [SoH %] — [Urgency tier emoji + label]
**Cell/block results:** [N pass / N flag / N fail]
**Fault codes:** [None / list if present]

---

### For the customer (channel: [verbal / written / text])

[Plain-language recap — see process above]

---

### Service advisor notes (internal)
- Urgency tier: [Healthy / Monitor / Plan / Replace]
- Next touchpoint: [When to recheck, what to watch for]
- Estimate follow-up: [Yes — send replacement estimate / No]
- Bilingual flag: [Yes/No — route to Bilingual Customer Message Builder if Yes]
```

**Output requirements:**
- SoH % and cell counts come from the input exactly — never fabricated
- Urgency language matches the tier determined from input, not the customer's preferred narrative
- No HV battery handling or repair instructions in customer-facing output
- Recommendation is specific and actionable (not "it depends")
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**
- Vehicle: 2016 Toyota Prius, ~130,000 miles
- Test tool: BATTSCAN
- SoH: 76%
- Cell/block results: 28 modules tested; 25 pass, 2 flagged (low voltage), 1 fail
- DTCs: P3000 (HV battery system caution)
- Customer context: city commuter, noticing slightly more gas fill-ups lately; keeping the vehicle
- Recommendation: Plan for replacement within 12–18 months; monitor at next service
- Channel: written summary (email to customer)

**Output:**

```
## Battery Health Recap — 2016 Toyota Prius | May 11, 2026

**Test performed:** BATTSCAN cell-level diagnostic
**State of Health:** 76% — 🟡 Monitor / Plan
**Cell/block results:** 25 pass / 2 flagged / 1 fail
**Fault codes:** P3000 (HV battery system caution)

---

### For the customer (channel: email)

Hi [Customer first name],

Here's what we found on your Prius battery today.

**The short version:** Your hybrid battery is still working, but it's showing early signs of wear that will eventually need attention. No emergency today — but this is the right time to start planning.

**What the test showed:** We ran a full cell-by-cell test of your high-voltage battery (the large battery pack that powers the electric motor). Your battery is currently holding about 76% of its original capacity — think of it like a phone battery that used to last all day and now runs out by early evening. Of the 28 individual battery sections we tested, 25 are healthy, 2 are showing reduced capacity, and 1 has failed.

**Why you're noticing more gas fill-ups:** When the battery can't hold as much charge, the Prius leans on the gas engine more often. That's exactly what you've been experiencing — and it lines up with what the test found.

**What we recommend:** Your battery doesn't need to be replaced today, but we'd plan for it within the next 12–18 months before the remaining healthy sections start declining further. We'd also like to recheck it at your next oil change to track the trend.

**Next step:** Would you like us to put together a battery-replacement quote so you can plan financially? There's no pressure — just here to give you a clear picture. Reply to this message or call us at [shop phone].

[Advisor first name]
[Shop name]

---

### Service advisor notes (internal)
- Urgency tier: 🟡 Monitor / Plan
- Next touchpoint: Recheck at next oil change; replacement estimate follow-up offered
- Estimate follow-up: Yes — offer at next visit if customer doesn't reply to email
- Bilingual flag: No
```

---

### Second example — 🟠 Plan tier, verbal walkthrough

This second example exercises the 🟠 **Plan** tier (the first example is 🟡 Monitor) and the **verbal walkthrough** channel (the first is a written email). Same accuracy discipline, harder conversation: a failed module is present, the SoH is materially lower, and the advisor has to convey real urgency without tipping into a scare tactic.

**Inputs:**
- Vehicle: 2015 Toyota Camry Hybrid LE, ~165,000 miles, ~11 years old
- Test tool: Dr.EV AI Battery Report
- SoH: 61%
- Cell/block results: 34 modules tested; 29 pass, 4 flagged (low voltage), 1 fail
- DTCs: P0A7F (Hybrid Battery Pack Deterioration)
- Customer context: daily commuter + occasional rideshare; reports the gas engine "kicks on almost right away" and noticeably worse mileage; deciding whether to keep the car another year or trade it
- Recommendation: Plan for replacement within the next 6–12 months (the one failed module pulls the timeline toward the near end of the Plan window); monitor closely, retest in ~3 months
- Channel: verbal walkthrough (advisor talking-track)

**Output:**

```
## Battery Health Recap — 2015 Toyota Camry Hybrid LE | June 15, 2026

**Test performed:** Dr.EV cell-level diagnostic
**State of Health:** 61% — 🟠 Plan
**Cell/block results:** 29 pass / 4 flagged / 1 fail
**Fault codes:** P0A7F (Hybrid Battery Pack Deterioration)

---

### For the customer (channel: verbal walkthrough — advisor talking-track)

**[Lead with the punchline]**
- "So here's the headline: your hybrid battery is still running the car, but it's worn enough that I'd want you to start planning for a replacement in the next 6 to 12 months — not today, but this isn't one to sit on for two or three years."
  *(pause — let that land, then continue)*

**[Explain the SoH % with the phone analogy]**
- "Think of it like a phone battery. When the car was new, the pack held 100% of its charge. Right now it's holding about 61% — so it just can't store and deliver as much as it used to."

**[Cell/block findings in plain English]**
- "We tested all 34 individual sections inside the pack. 29 are still healthy, 4 are starting to weaken, and 1 has actually failed."
- "That one failed section is the reason I'm putting a clock on this. Once one section is gone, it puts extra load on the neighbors, and they tend to follow over the next several months."
  *(pause for questions)*

**[Connect to what they've noticed]**
- "You mentioned the gas engine kicks on almost right away and the mileage dropped — that's exactly what a worn hybrid battery feels like. The car is leaning on the gas engine to make up for what the battery can't deliver, so you're buying more fuel to cover the gap."

**[State the recommendation clearly]**
- "My recommendation: plan to replace the hybrid battery within the next 6 to 12 months. It's safe to keep driving in the meantime, but I'd retest in about 3 months so we can watch the trend and you're never caught off guard."

**[Address the cost + the keep-or-trade question they raised]**
- "On cost — a hybrid battery for this Camry typically runs somewhere in the $2,000–$3,500 range installed depending on whether we go new, reconditioned, or remanufactured, and I'm happy to put together a real quote so it's not a guess."
- "Since you're weighing whether to keep it another year: a fresh battery is the single biggest thing that makes a high-mileage hybrid feel normal again. If you're planning to keep it past this year, replacing the battery is usually money well spent. If you're leaning toward trading it soon, that's useful to know too — I won't push you toward a repair that doesn't fit your plan."
- "Want me to build that replacement quote while you're here so you've got a real number to plan around?"

---

### Service advisor notes (internal)
- Urgency tier: 🟠 Plan (SoH 61% AND 1 failed module — both indicators agree on Plan; failed module pulls timeline to the near end of the 6–12 mo window)
- Next touchpoint: Retest in ~3 months to track trend; do NOT let this lapse to the next annual visit
- Estimate follow-up: Yes — build new / reman / recond comparison quote; note keep-or-trade is undecided, so frame quote as decision-support, not a hard close
- Bilingual flag: No
```

---

### Third example — 🔴 Replace tier, text/SMS channel

This third example completes the tier coverage (🟡 Monitor and 🟠 Plan are above; 🟢 Healthy needs no recap). It is the hardest tier: SoH below 55%, **two failed modules**, and a battery-replacement code already set. The recap must convey real urgency honestly, give the replace recommendation in plain terms, present the shop's actual replacement options (config-driven pricing band and warranty), and offer a path forward — without pressure tactics and **without lecturing the customer about whether the car is "worth" fixing** (that keep-or-replace-the-car judgment is a human advisor conversation, surfaced only in the internal notes). Channel is SMS, so it stays short with one clear call to action.

**Inputs:**
- Vehicle: 2013 Toyota Prius, ~212,000 miles, ~13 years old
- Test tool: AVILOO
- SoH: 49%
- Cell/block results: 28 modules tested; 24 pass, 2 flagged (low voltage), 2 fail
- DTCs: P0A80 (Replace Hybrid Battery Pack)
- Customer context: rideshare driver; battery warning light is on; car has gone into reduced-power "turtle" mode twice; gas engine running almost constantly; needs the car working for income
- Recommendation: Replace now
- Channel: text/SMS to customer
- Config: shop = Eastgate Hybrid & Auto; advisor = Luis; reman HV battery installed price band $2,200–$2,900 with a 36-month/unlimited-mile warranty; new and reconditioned options also offered

**Output:**

```
## Battery Health Recap — 2013 Toyota Prius | June 22, 2026

**Test performed:** AVILOO cell-level diagnostic
**State of Health:** 49% — 🔴 Replace
**Cell/block results:** 24 pass / 2 flagged / 2 fail
**Fault codes:** P0A80 (Replace Hybrid Battery Pack)

---

### For the customer (channel: text/SMS)

Hi [Customer first name], it's Luis at Eastgate Hybrid & Auto with your Prius battery results.

Straight answer: the hybrid battery is worn out and needs to be replaced now. The test shows it's holding about 49% of its original capacity, 2 of the 28 sections have failed, and the car has already set the "replace battery" code — that's why it's dropping into reduced-power mode and running the gas engine constantly.

Since you drive for income, the risk is it could leave you stranded mid-shift, so I don't want you sitting on this.

We can usually get a replacement installed in a day. A reman battery runs about $2,200–$2,900 installed and comes with our 36-month/unlimited-mile warranty; we also offer new and reconditioned options if you want to compare. Want me to text you the full quote with all three so you can pick? Reply here or call us at [shop phone]. — Luis

---

### Service advisor notes (internal)
- Urgency tier: 🔴 Replace (SoH 49% AND 2 failed modules AND P0A80 set — all three indicators agree; no ambiguity)
- Safety/operability: car already entering reduced-power mode → flag stranding risk for a rideshare driver; do not soft-pedal urgency
- Estimate follow-up: Yes — send new / reman / recond comparison; lead recommendation = reman (best value + 36-mo warranty)
- Keep-or-replace-the-car: a 13-yr/212k Prius nearing the cost-of-repair-vs-value line — this is an advisor conversation IF the customer raises it, NOT a line in the customer recap. Have the trade/scrap discussion live, only if the customer opens it.
- Bilingual flag: Unsure — if customer prefers Spanish, route to Bilingual Customer Message Builder before sending
```
