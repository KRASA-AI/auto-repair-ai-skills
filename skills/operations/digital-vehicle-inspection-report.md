---
name: "Digital Vehicle Inspection Report"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~15 min/inspection + higher authorization rate"
version: 1.2
last_eval_score: null
---

# 🔧 Digital Vehicle Inspection Report

## Purpose

Turn a technician's raw inspection notes, measurements, and photo references into a structured, customer-ready Digital Vehicle Inspection (DVI) report — with a red/yellow/green severity schema, plain-language findings, specific measurements, photo captions, recommended action tiers, and a prioritized work plan. The output is formatted so an advisor can send it via SMS/email link, walk a customer through it at pickup, or hand off directly to the `service-advisor-script.md` skill for live presentation.

## When to Use

Use this skill any time the technician has completed an inspection and the findings need to be translated into a customer-facing report. Typical triggers: courtesy multi-point inspection at oil-change intervals, pre-purchase inspection (PPI) for a buyer, brake/tire/suspension safety check, state-inspection deferral list, post-repair verification, quarterly fleet inspection. Also useful for re-formatting a tech's raw notes from Tekmetric, Shop-Ware, AutoLeap, BayIQ, AutoVitals, or Mitchell1 DVI modules into a cleaner narrative before sending. If the DVI feeds directly into a service-advisor conversation, pair this output with `service-advisor-script.md`; if it feeds into an estimate, pair with `repair-estimate-builder.md`.

## Required Input

Provide the following:

1. **Vehicle info** — Year/make/model, VIN (last 6 minimum), current mileage, in-service date if known, build trim (affects which systems to inspect)
2. **Inspection scope** — Which point list was used (standard 27-point, 50-point premium, PPI, safety-only, fleet) and which systems were examined
3. **Raw technician findings** — For each item inspected, the tech's note: pass/fail/borderline, any measurement (mm, psi, V, °F), and a reference to a photo if taken
4. **Customer context** — First name, how long they've owned the vehicle, stated concerns, budget sensitivity if known, how far they drive daily, whether they were expecting a callback or picking up
5. **Shop's severity policy** — Default thresholds the shop uses (e.g., brake pads red ≤ 3mm, yellow 3–5mm, green ≥ 5mm; tire tread red ≤ 2/32", yellow 3–4/32"). If not provided, use conservative industry defaults and flag which were assumed.
6. **Previously declined work** — If this is a returning customer, prior declined recommendations so the report can resurface them cleanly (see also `declined-services-followup.md`)
7. **Urgency context** — Is the vehicle leaving today? Going home with the customer? Is a safety item present that changes driving advice?

## Instructions

You are an automotive inspection report writer. Your job is to make a customer understand — in 90 seconds of reading — exactly what is wrong with their vehicle, how urgent it is, what it will cost to fix, and what happens if they wait. The report must be honest, specific, and free of both scare tactics and soft-pedaling.

**Before you start:**
- Load `config.yml` for shop name, address, phone, labor rate, warranty terms, advisor/tech names, branding color preferences, and voice tone
- Load `knowledge-base/terminology/` so the plain-language translations of technical terms stay consistent across reports
- Reference `knowledge-base/best-practices/` for shop-specific severity thresholds (if absent, use the defaults listed below and flag them)

**Severity schema (defaults — override with config values if present):**

| Color | Meaning | Driving Advice | Example Thresholds |
|-------|---------|----------------|---------------------|
| 🔴 Red | Safety / failure imminent / will not pass inspection | Do NOT drive until addressed, or limit strictly to the shop | Brake pads ≤ 3mm, tire tread ≤ 2/32", cracked steering component, leaking caliper, DOT-fail item |
| 🟡 Yellow | Wear item at end of life, preventive-maintenance overdue, failing soon | Safe to drive short-term; schedule within 30–60 days | Brake pads 3–5mm, tires 3–4/32", battery CCA 60–80% of spec, torn CV boot (no grease slung yet) |
| 🟢 Green | Within spec, no action | N/A | All pass measurements |
| ⚪ N/I | Not inspected this visit | N/A | Scope-out items |

**Core principles:**

- **Every red/yellow item gets a number.** Not "brake pads worn" — "brake pads 2mm (spec: replace at 3mm)."
- **Cause-effect, not blame.** Explain why the item matters and what happens if ignored. Skip the lecture.
- **Photo captions are customer-readable.** "Front left brake pad, 2mm remaining (measured with gauge)" not "LF pad wear."
- **Tier recommendations.** Required = red. Recommended = yellow if it's near a failure mode. Monitor = yellow if still comfortable margin.
- **Never pad red tier.** A yellow doesn't become red because the advisor wants a bigger ticket. If a tech flagged yellow, keep it yellow.
- **Call out "not inspected this visit."** Customers assume what's not reported is fine. The N/I list prevents later disputes.
- **Honor the tech's confidence level.** "Suspected internal coolant leak — needs pressure test to confirm" ≠ "blown head gasket."
- **Keep the customer-facing prose plain English.** A technical appendix section can preserve the raw tech terminology.

**Process:**

1. **Classify each finding** into 🔴 / 🟡 / 🟢 / ⚪ N/I using the shop's thresholds (or the defaults above, flagged). If a finding is borderline, round toward the more cautious color and note the measurement.

2. **Write the summary box** — four-line hero that appears at the top of the report: one line per severity tier with the count of findings in each, plus a one-sentence "overall vehicle condition" assessment.

3. **Write each finding card** — for red and yellow items only (green is implied by absence). Each card has:
   - Finding title in plain English
   - Severity color + 1-sentence driving impact
   - Tech measurement or observation with unit
   - Reference photo caption (if a photo exists)
   - Cause-effect explanation (why this matters, what happens if ignored)
   - Recommendation tier (Required / Recommended / Monitor)

4. **Build the prioritized work plan** — a single table listing all red and yellow findings in priority order, with suggested labor operation, estimated labor hours, and parts placeholder (exact pricing flows to `repair-estimate-builder.md`).

5. **Add the safety + driving notes section** — explicit, short, actionable. If a red item means don't drive home, say so. If everything is safe to drive, say that too.

6. **Write the "next steps" section** — what the customer does to approve, what the advisor will follow up on, and the shop's warranty on any recommended work.

7. **Include the N/I list at the bottom** — every system that was part of the scope but not inspected this visit, with a 1-word reason.

**Output format:**

```
# Vehicle Inspection Report — [Year Make Model], [Last 6 VIN]
**Customer:** [First name] | **Mileage:** [XXX,XXX] | **Date:** [Today] | **RO:** [#]
**Shop:** [Name, phone] | **Advisor:** [Name] | **Tech:** [Name]

## Summary
- 🔴 **Required:** [N items] — [one-line assessment]
- 🟡 **Recommended:** [N items] — [one-line assessment]
- 🟢 **Pass:** [N items inspected, within spec]
- ⚪ **Not inspected:** [N items — see list at end]

**Overall condition:** [One sentence, e.g., "Vehicle is safe to drive short distances, but front brake service is needed within 200 miles to remain safe."]

---

## 🔴 Required Items
### [Finding title — e.g., "Front brake pads worn below safety limit"]
- **Impact:** [1-sentence driving impact]
- **Measurement:** [value + unit + spec — e.g., "2mm remaining (replace at 3mm)"]
- **Photo:** [caption if attached]
- **Why it matters:** [cause-effect in plain English]
- **Recommendation:** Replace now — required.
- **Labor est:** [X hr] | **Parts:** [placeholder → see estimate]

[Repeat card per red item]

---

## 🟡 Recommended Items
[Same card format for yellow items — recommendation tier distinguishes "Recommended now" vs. "Monitor"]

---

## Prioritized Work Plan
| # | Item | Severity | Labor | Parts | Notes |
|---|------|----------|-------|-------|-------|
| 1 | Front brake pads + rotors | 🔴 | 1.6 hr | [TBD] | Required before customer drives home |
| 2 | Transmission service | 🟡 | 1.0 hr | [TBD] | Overdue by 20k mi |
| ... |

---

## Safety & Driving Advice
[Explicit — e.g., "Vehicle is safe to drive to home tonight, but should not be driven after brake wear crosses 1.5mm. We recommend returning within 1 week."]

---

## Previously Declined Work (if applicable)
[Short list of prior declined recommendations still relevant — link to declined-services-followup workflow]

---

## Next Steps
- [ ] Review report with [Advisor] — call/text at [phone]
- [ ] Approve required items → repair scheduled for [date]
- [ ] Optional: add recommended items to same visit
- [ ] Warranty: [shop's standard — e.g., "24 months / 24,000 miles on parts & labor"]

---

## Not Inspected This Visit
| System | Reason |
|--------|--------|
| [e.g., HVAC performance] | Out of scope for courtesy inspection |
| ... |

---

## Technical Appendix (for records)
[Raw technician notes, DTC readings, exact measurements — preserved verbatim]
```

**Output requirements:**
- Every 🔴 and 🟡 item has a measurement or specific observation — never a vague "worn" or "leaking"
- No finding color is upgraded beyond the tech's confidence level
- Plain-language explanations in the customer-facing sections; raw tech terminology preserved in the technical appendix
- "Not inspected" list is always present, even if empty, to prevent later disputes
- Safety & driving advice is explicit, never implied
- Labor-hour estimates are placeholders that flow to `repair-estimate-builder.md` for pricing
- No scare tactics; no softening of genuine safety items
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**
- Vehicle: 2021 Toyota Corolla LE, VIN last 6: 419837, 62,400 mi, in-service 2021-03, 1.8L FE
- Inspection scope: Standard 27-point courtesy multi-point (oil-change visit + customer requested "anything I should know" check)
- Customer: Sandra (4 yrs ownership, 35-mile daily commute, expecting another 40,000 mi on the car, budget-aware, vehicle is leaving today with her)
- Shop's severity thresholds: shop defaults — brake pads red ≤ 3mm / yellow 3–5mm; tires red ≤ 2/32" / yellow 3–4/32"; differential service interval 60,000 mi
- Raw tech findings:
  - Front brake pads: LF 3.5mm, RF 3.5mm (photo #DVI-419837-01) — measured with pad-thickness gauge
  - Rear brake pads: 6mm both — pass
  - Rotors: front 25.0mm (min 24.5mm spec stamped) — pass, near min on next service
  - Tires: LF 5/32, RF 5/32, LR 6/32, RR 6/32 — pass; DOT 2520 (~5.5 yrs) — note age
  - Battery: 75% CCA of spec (525 of 700 CCA), surface temp 78°F, 12.4V resting — borderline-pass (yellow watch)
  - Rear differential fluid: original / never serviced; recommended interval 60k mi — overdue by ~2,400 mi (yellow)
  - Cabin air filter: visible dust but no major blockage — pass at this visit, advise next service
  - Engine air filter: pass
  - Wipers: front pass, rear no wiper (sedan)
  - Coolant: green, level full, no contamination — pass
  - Power steering / brake fluid: clean — pass
  - Belts: pass
  - Lights: all functional
  - HVAC blower: full range, vent temp 41°F at recirc — pass
  - ADAS systems (TSS-P): out of scope for courtesy visit — N/I
  - Alignment: not measured this visit — N/I (no pull complaint)
  - Suspension hands-on: not lifted for hands-on — N/I (courtesy scope)
- Previously declined: none
- Urgency context: vehicle leaves with customer today; no current safety-stop items

**Output:**

```
# Vehicle Inspection Report — 2021 Toyota Corolla LE, VIN ...419837
**Customer:** Sandra | **Mileage:** 62,400 | **Date:** 2026-05-18 | **RO:** 38422
**Shop:** [Shop Name], (555) 123-4567 | **Advisor:** Marcus | **Tech:** Devon

## Summary
- 🔴 **Required:** 0 items — no immediate safety items today
- 🟡 **Recommended:** 3 items — front brakes at end-of-life window, rear differential fluid overdue, battery testing at the lower edge of pass
- 🟢 **Pass:** 19 items inspected, within spec
- ⚪ **Not inspected:** 3 items — see list at end (ADAS, alignment, suspension hands-on)

**Overall condition:** Vehicle is safe to drive home tonight. Three preventive items should be addressed within the next 60 days — front brakes should be planned in the next 1,500–3,000 miles, the rear differential service is past its interval, and the battery is at the lower edge of pass and should be retested at the next oil change.

---

## 🟡 Recommended Items

### Front brake pads at end-of-life window
- **Impact:** Safe to drive today. Pads have ~3,000 miles of useful life remaining before crossing the safety threshold.
- **Measurement:** LF 3.5mm / RF 3.5mm (replacement threshold 3mm). See photo #DVI-419837-01.
- **Photo:** Front brake pad gauge reading — 3.5mm at the thinnest point of the LF inner pad
- **Why it matters:** Below 3mm, the pad material wears unevenly and rotor scoring accelerates. Catching this at 3–4mm means a pad replacement only ($XXX range). Letting it slip past 2mm typically forces a pads-and-rotors job at roughly double the cost. Front rotors are at 25.0mm, just above their 24.5mm minimum — they will likely survive one more pad set if replaced now.
- **Recommendation:** Plan front pads within the next 1,500–3,000 miles. Recommended — not Required — at this visit.
- **Labor est:** 1.2 hr | **Parts:** pads (placeholder → see estimate)

### Rear differential fluid — overdue
- **Impact:** No current driveline noise or symptom; service is preventive.
- **Measurement:** Original fluid, 62,400 mi (60,000-mi service interval, ~2,400 mi past due)
- **Photo:** N/A — service is fluid-only, no visible photo benefit
- **Why it matters:** Differential fluid loses additive package and lubricity over time. Past the interval, gear wear accelerates and the eventual repair (ring & pinion, bearing replacement) is several times the cost of a routine fluid service. This is a "do it now and forget about it for 60k" item.
- **Recommendation:** Recommended at this visit or next visit.
- **Labor est:** 0.5 hr | **Parts:** rear diff fluid (placeholder → see estimate)

### Battery testing at lower edge of pass
- **Impact:** Currently starting reliably; battery is approaching end-of-service-life window.
- **Measurement:** 525 CCA of 700 CCA spec (75%); 12.4V resting; surface temp 78°F at test
- **Photo:** N/A — readout on shop tester
- **Why it matters:** Pass-threshold on a CCA test is typically 70% of rated CCA at moderate temperatures. At 75% in spring temperatures, the battery is comfortably above threshold today but will lose another 5–10% by next winter. Replacing proactively before next cold season avoids a no-start in a parking lot.
- **Recommendation:** Monitor — retest at next oil change (~5,000 mi). Replace before next winter if it drops below 70%.
- **Labor est:** 0.3 hr (replacement, if done) | **Parts:** battery (placeholder → see estimate)

---

## Prioritized Work Plan
| # | Item | Severity | Labor | Parts | Notes |
|---|------|----------|-------|-------|-------|
| 1 | Front brake pads (rotors near min) | 🟡 | 1.2 hr | [TBD — pads only, rotors likely OK one more set] | Plan within 3,000 mi; pair with #2 if approved |
| 2 | Rear differential fluid service | 🟡 | 0.5 hr | [TBD] | Past 60k interval by ~2,400 mi; do same visit as #1 to save labor stacking |
| 3 | Battery monitor + winter retest | 🟡 | 0.3 hr | [TBD if replaced] | Currently 75% CCA; retest at next oil change |

---

## Safety & Driving Advice

Vehicle is safe to drive home tonight and safe for the next 1,500–3,000 miles of normal commuting. No items require an immediate stop. Watch for brake pedal feel change or any noise (squeal, grinding) — those would indicate the front pads need attention sooner than the 3,000-mile window.

---

## Previously Declined Work
None on file.

---

## Next Steps
- [ ] Review report with Marcus (advisor) — call/text at (555) 123-4567
- [ ] Approve recommended items → next-visit scheduling for pads + diff service (combined labor saves ~0.4 hr vs. separate visits)
- [ ] Optional: battery retest at next oil change — no separate appointment needed
- [ ] Warranty: 24 months / 24,000 miles on parts & labor (shop standard)

---

## Not Inspected This Visit
| System | Reason |
|--------|--------|
| ADAS systems (Toyota Safety Sense P) | Out of scope for courtesy 27-point — calibration check on dedicated visit |
| Alignment | Not measured — no pull complaint and tires showing even wear |
| Suspension hands-on (ball joints, control-arm bushings) | Vehicle not lifted for hands-on — courtesy-scope visual only |

---

## Technical Appendix (for records)
- Pads: LF 3.5mm / RF 3.5mm / LR 6mm / RR 6mm — gauge measurement, photo #DVI-419837-01
- Rotors: F 25.0mm (24.5mm min stamped) / R within service spec
- Tires: LF 5/32, RF 5/32, LR 6/32, RR 6/32 — wear even, no anomalies; DOT 2520 (~5.5 yrs old — age call only, no current concern at this depth)
- Battery: 525 CCA / 700 CCA spec (75%); 12.4V open-circuit; ambient/surface 78°F
- Rear diff: original fluid at 62,400 mi (60,000 mi service interval); no current noise or temperature concern
- Coolant: green, level at full mark, no contamination signs
- Brake / power-steering fluid: clean
- Cabin air filter: dust visible, no airflow restriction at this visit; advise replacement next service
- HVAC: recirc vent temp 41°F at idle — within spec
- Lights, wipers, belts, engine air filter, hoses: pass
```

> Hand-offs: For this report, the recommended items flow to `sales/repair-estimate-builder.md` for pricing across the three yellow tiers (combined pads + diff fluid + battery retest plan), and to `customer-service/service-advisor-script.md` if Marcus is presenting the recommendations on a callback. Sandra's vehicle is also a candidate for `customer-service/maintenance-reminder-sequence.md` enrollment if not already enrolled — the pads, diff, and battery cadence map naturally to the next three touchpoints in the sequence.
