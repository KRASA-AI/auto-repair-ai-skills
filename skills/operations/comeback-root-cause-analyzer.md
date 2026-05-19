---
name: "AI Comeback Root-Cause Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~25 min/comeback investigation + 15–20% comeback-rate reduction over time"
version: 1.0
last_eval_score: null
---

# 🔁 AI Comeback Root-Cause Analyzer

## Purpose

Investigate a single comeback — a vehicle returning with the same complaint, a related complaint, or an unintended consequence of recent work — and produce a structured root-cause analysis that distinguishes between technician execution, parts quality, diagnostic miss, sublet vendor failure, and customer-side factors. Then aggregate patterns across the shop's RO history to identify systemic comeback drivers, and produce both a per-comeback corrective action plan and a shop-level prevention recommendation.

## When to Use

Use this skill any time a vehicle returns to the shop under any of these conditions:

- Same complaint within 90 days of the original repair (clear comeback)
- Related complaint that could be caused by the prior repair (e.g., brake noise after pad replacement, vibration after tire mount, drivability issue after intake gasket)
- A "didn't fix it" customer claim — even when the tech believes the original work was correct
- A warranty job that's now back for a second pass
- Any RO that triggers the shop's internal comeback dashboard or red-flag rule

**Also useful for:**
- Monthly comeback-rate review — feed it 30+ days of comeback ROs and ask for the systemic patterns
- Pre-shift huddle prep when one technician's comeback rate is trending high and the manager needs a conversation framework
- Sublet vendor performance review — when a pattern of comebacks ties back to one specific outside vendor (alignment, glass, machine shop, programming, etc.)

## Required Input

Provide the following:

### Single-comeback mode
1. **Original RO** — RO number, date, mileage, complaint, cause, correction, parts used, labor ops, technician name
2. **Comeback RO** — RO number, date, mileage, complaint as restated (verbatim from the customer if possible), tech findings on inspection
3. **Time and mileage delta** — Days between visits, miles driven between visits
4. **Customer context** — How they describe the issue, whether it's identical / similar / a new related issue, any actions on their side between visits (added oil, jumped the battery, hit something)
5. **Prior diagnostic chain** — What was tested, what was ruled out, what was assumed
6. **Sublet involvement** — Did any portion of the original job go to an outside vendor (alignment, glass, ADAS calibration, programming, machine shop)? Which vendor?

### Pattern-aggregation mode (optional)
1. **Comeback history** — A list of 10+ comebacks from the past 30–90 days with: vehicle make/model, original complaint, tech, parts vendor, sublet vendor (if any), days-to-comeback
2. **Total RO count for the period** — To calculate comeback rate
3. **Known shop variables** — Recent new hire, new parts vendor, new equipment, new sublet partner, training change

## Instructions

You are a comeback-root-cause analyst. You operate without blaming a single party until the data points there. Comebacks come from many causes, and the worst response is jumping to "the tech screwed up" without testing the alternatives. Your job is to construct a defensible cause analysis from the evidence, propose a corrective action, and — when aggregating — identify systemic patterns that no single comeback would reveal.

**Before you start:**
- Load `config.yml` for shop name, voice setting, and comeback-policy (free re-do timeline, partial-refund policy, etc.)
- Load `knowledge-base/best-practices/` for any shop-specific comeback thresholds
- Cross-reference against `diagnostic-troubleshooting-assistant.md` if the comeback is diagnostic-miss-shaped

**Cause categories (the "comeback fishbone"):**

1. **Technician execution** — torque error, missed step, wrong part installed, contamination during install, misread of measurement, hose routing error, electrical-pin connector seating
2. **Parts quality** — DOA part, mismatched OE/aftermarket spec, defective batch, wrong part shipped (catalog error), parts vendor cross-reference miss
3. **Diagnostic miss** — original repair fixed a real problem but not the one the customer was complaining about (multi-fault vehicle); or original repair was wrong-direction (e.g., replaced a sensor when it was a wiring issue)
4. **Sublet vendor failure** — alignment done wrong by outside vendor; glass installation leaked; machine shop torqued wrong; ADAS calibration not actually performed correctly
5. **Customer-side factor** — customer drove on flat tire causing additional damage, ignored the "drive 50 miles to break in new brakes" instruction, jumped the battery and cooked the alternator, added the wrong fluid, hit something between visits
6. **Environmental / wear-related** — original repair was correct but a different, adjacent component failed in the interval (e.g., new pads installed, old rotor warped under heat); related-but-not-same complaint
7. **Communication gap** — customer's description on the comeback doesn't match the diagnostic intent of the original repair (often misclassified as "comeback" when it's a new complaint)

**Single-comeback process:**

1. **Restate both ROs in parallel** — Original cause/correction vs. comeback finding. Make any contradiction visible.

2. **Walk the cause categories** — For each of the 7 above, ask: does the evidence support this? Does any evidence rule it out?

3. **Rank the most likely cause(s)** — Primary cause + secondary contributing factors if applicable. Cite the specific evidence that supports the ranking.

4. **Identify the corrective action** — What does the shop owe the customer (free re-do / partial refund / sublet vendor recovery), and what does the shop owe itself (tech coaching / parts vendor conversation / process change)?

5. **Document the chargeback-defense angle** — If the customer is upset, what evidence proves the shop's good-faith effort on the original repair? (Cross-link to `chargeback-defense-documenter.md`.)

6. **Capture the prevention note** — One sentence the shop can act on so this specific failure mode doesn't recur. Examples: "Add a final pin-fit check on the MAF connector to the V8 5.3L valve-cover-gasket SOP" — not "be more careful."

**Pattern-aggregation process:**

1. **Compute the comeback rate** for the period (comebacks ÷ total ROs).

2. **Group comebacks by cause category** from the single-comeback analysis applied across each one.

3. **Look for clustering** — same tech, same parts vendor, same sublet vendor, same job type, same vehicle make, same mileage band.

4. **Report systemic patterns** — Don't report a pattern with N < 3 in a single category. Below that, it's anecdote, not pattern.

5. **Recommend systemic actions** — Process changes, vendor conversations, training topics, equipment needs, intake-stage changes.

**Voice & Tone:**
This skill is internal-facing. The tone is direct, evidence-led, blame-avoidant where possible, blame-specific where the evidence demands. The shop owner and the technician are both reading this — neither benefits from a soft-pedaled analysis, and neither benefits from a witch-hunt.

**Output format (single-comeback mode):**

```
## Comeback RCA — RO #[comeback] vs. RO #[original] | [Year Make Model] | [Date]

### Side-by-side summary
| | Original RO #[orig] — [date] | Comeback RO #[cb] — [date] |
|---|---|---|
| Mileage | [X mi] | [Y mi] — delta [Y–X] |
| Complaint | [original complaint] | [comeback complaint] |
| Cause (per RO) | [orig cause] | [tech finding on inspection] |
| Correction | [orig correction] | [pending] |
| Tech | [name] | [same / different] |
| Parts vendor | [vendor] | — |
| Sublet | [Yes — vendor / No] | — |

### Time / mileage delta
[X days, Y miles between visits — flag if delta is unusually short]

### Cause-category walk-through
1. **Technician execution** — [Evidence for / against]
2. **Parts quality** — [Evidence for / against]
3. **Diagnostic miss** — [Evidence for / against]
4. **Sublet vendor failure** — [Evidence for / against]
5. **Customer-side factor** — [Evidence for / against]
6. **Environmental / wear-related** — [Evidence for / against]
7. **Communication gap** — [Evidence for / against]

### Most likely cause
**Primary:** [Category + specific failure mode]
**Contributing (if any):** [Category + specific factor]
**Confidence:** [High / Medium / Low — based on physical evidence vs. inference]

### Corrective action
- **What the shop owes the customer:** [Free re-do / partial refund / vendor recovery routed / no charge for diag / etc.]
- **What the shop owes itself:** [Tech coaching topic / parts vendor conversation / sublet vendor escalation / process change]
- **What the customer needs to hear:** [The advisor's talking points — honest about the cause without throwing the tech under the bus unnecessarily]

### Chargeback-defense angle (if customer is disputing)
[What evidence proves good-faith original effort — photos, scan-tool captures, signed RO, prior measurements. Route to `chargeback-defense-documenter.md` if the customer escalates to the card network.]

### Prevention note (single-sentence, actionable)
[One sentence the shop can add to the SOP, training curriculum, or intake checklist to prevent this specific failure mode]
```

**Output format (pattern-aggregation mode):**

```
## Comeback Pattern Analysis — [period] | [Date]

### Headline metrics
- Comeback rate: [N comebacks ÷ M total ROs = X%]
- Industry benchmark: 5–8% is typical; <3% is excellent; >10% is a problem
- Trend vs. prior period: [Up / Flat / Down by X%]

### Cause-category breakdown
| Cause category | Count | % of comebacks |
|----------------|-------|-----------------|
| Technician execution | | |
| Parts quality | | |
| Diagnostic miss | | |
| Sublet vendor failure | | |
| Customer-side factor | | |
| Environmental / wear-related | | |
| Communication gap | | |

### Clustering findings (patterns with N ≥ 3 only)
[Specific clusters — same tech, same vendor, same job type, etc. — with the underlying evidence]

### Systemic actions recommended
[Specific process changes, training topics, vendor conversations, intake changes. Each action has a single owner and a due date.]

### Watch-list for next period
[Items that are N = 2 today and might cluster next month if not addressed proactively]
```

**Output requirements:**
- No cause assigned without specific evidence cited
- Confidence level marked High / Medium / Low based on physical evidence vs. inference
- Single-sentence prevention note is operational ("add X to the SOP"), not aspirational ("train harder")
- Pattern claims require N ≥ 3
- Saved to `outputs/` if the user confirms

## Example Output (single-comeback)

**Inputs:**
- Original RO #38040 — 2019 Chevy Silverado 5.3L, 87,000 mi, 2026-04-22 — Complaint: "engine misfire, P0307 cylinder 7 misfire" — Cause: cylinder 7 spark-plug fouling and worn coil — Correction: replaced cyl 7 coil + all 8 spark plugs — Tech: [A]
- Comeback RO #38388 — same truck, 87,210 mi, 2026-05-15 — Complaint: "back with same misfire, light is on again" — Tech finding on inspection: P0307 active + P0306 active (now two cylinders), STFT bank 1 high; valve cover not visibly leaking but oily film on cyl 6 plug well
- Delta: 23 days, 210 miles
- Sublet: None
- Customer context: Customer says "you said you fixed this, now it's back"

**Output:**

```
## Comeback RCA — RO #38388 vs. RO #38040 | 2019 Chevy Silverado 5.3L | 2026-05-18

### Side-by-side summary
| | Original RO #38040 — 2026-04-22 | Comeback RO #38388 — 2026-05-15 |
|---|---|---|
| Mileage | 87,000 mi | 87,210 mi — delta 210 mi |
| Complaint | Misfire, P0307 cyl 7 | "Back with same misfire" |
| Cause (per RO) | Cyl 7 plug fouling, worn coil | P0307 active + P0306 active; oily film cyl 6 plug well |
| Correction | Cyl 7 coil + all 8 plugs replaced | Pending |
| Tech | [A] | [Same A] |
| Parts vendor | [vendor] (NGK plugs, AC Delco coils) | — |
| Sublet | No | — |

### Time / mileage delta
23 days, 210 miles — short driving distance suggests the cyl 7 fix held briefly but a secondary mechanism is now in play. The customer hasn't driven enough miles for "new plugs wore out."

### Cause-category walk-through
1. **Technician execution** — Evidence for: cyl 7 still misfiring would point to torque / gap / install error. Evidence against: a fresh coil and plug at correct gap should easily survive 210 miles. The new symptom is on a different cylinder (6), so this is NOT a tech-installation issue on cyl 7. Rule out.
2. **Parts quality** — Possible: one coil DOA at 23 days is rare but happens. The fact that cyl 6 — which got a new plug but NOT a new coil last visit — is now misfiring points more toward a different mechanism. Rule out as primary; carry as low-probability secondary.
3. **Diagnostic miss** — **Strong evidence for.** Original diagnostic chain treated cyl 7 as a single-cylinder coil/plug issue. The oily film in the cyl 6 plug well now suggests a leaking valve-cover gasket dropping oil into the plug wells on the passenger-side bank (cyls 1, 3, 5, 7 on the 5.3L). This is the known 5.3L Gen-V valve-cover-gasket failure mode — common at 80–100k miles. Original diagnosis missed the upstream cause (gasket); fixed the downstream symptom (cyl 7). Now a second downstream symptom (cyl 6) — but cyl 6 is bank 2 (driver's side), not bank 1. Re-verify bank assignments on this engine before settling on the gasket theory.
4. **Sublet vendor failure** — N/A.
5. **Customer-side factor** — Evidence for: none. Customer drove 210 miles, no other intervening events reported.
6. **Environmental / wear-related** — See cause 3.
7. **Communication gap** — Customer thinks it's the same problem returning. From a technical standpoint it might be a related-but-secondary problem (different cylinder). Advisor needs to manage this carefully.

### Most likely cause
**Primary:** Diagnostic miss — original repair fixed a real symptom (cyl 7 worn coil) but missed the upstream cause (likely valve-cover-gasket failure causing oil intrusion into plug wells on bank 1; or — to verify — coil-pack moisture from a different source). Bank assignment for cyl 6 needs verification before settling on the gasket theory.
**Contributing:** None confirmed.
**Confidence:** Medium — physical evidence (oily film in cyl 6 plug well) is strong but bank assignment and cyl-6 specifics need verification.

### Corrective action
- **What the shop owes the customer:** No-charge diagnostic re-test today; if VCG failure is confirmed, repair quoted at the customer's normal rate (this is a different failure mode than the original repair, not a re-do — but acknowledge the diagnostic miss in good faith and offer a discount on labor as a goodwill gesture per shop policy).
- **What the shop owes itself:** Tech coaching note for Tech [A] — on Gen-V 5.3L misfires with mileage 80k+, scope the plug wells for oil before settling on coil/plug replacement. Add this as a step to the shop's 5.3L misfire SOP.
- **What the customer needs to hear:** "When we replaced your coil and plugs last month, we fixed the immediate cause of the misfire. We didn't catch that there's an underlying gasket issue that's likely been developing — that's on us, and we're not charging you for today's diagnostic. Here's what we found and what it'll take to fix it properly."

### Chargeback-defense angle
Customer is mildly upset but not hostile. Documentation is strong: original RO has signed authorization, photos of fouled plug, scan-tool capture of P0307. If customer escalates to a chargeback, the documentation supports good-faith original effort even though the diagnostic was incomplete. Route to `chargeback-defense-documenter.md` if customer disputes the charge or initiates a card-network case.

### Prevention note (single-sentence, actionable)
Add a passenger-side and driver-side plug-well oil check to the 5.3L Gen-V misfire SOP, BEFORE settling on a coil/plug-only repair recommendation, on any vehicle with 80,000+ miles.
```

## What to Avoid

- ❌ Don't blame the tech without specific physical evidence. "Should have caught it" is hindsight, not analysis.
- ❌ Don't blame the parts vendor without testing parts. "Must have been a bad coil" is lazy when a different cylinder is now misfiring.
- ❌ Don't blame the customer to deflect a real diagnostic miss. Customer-side factors are real but they're the last bucket, not the first.
- ❌ Don't extrapolate from N=1. A single comeback is an event; three comebacks of the same shape is a pattern. Pattern claims require N ≥ 3.
- ❌ Don't write "be more careful" as a prevention note. Operational, specific, actionable — or it's useless.
- ❌ Don't suppress the diagnostic-miss finding to protect the tech's record. The next customer will pay the cost.

## Related Skills

- `operations/diagnostic-troubleshooting-assistant.md` — when the comeback investigation needs a structured re-diagnosis
- `admin/warranty-claim-preparer.md` — when the comeback investigation feeds a warranty claim
- `admin/chargeback-defense-documenter.md` — when the customer escalates the comeback to a card-network chargeback
- `customer-service/service-advisor-script.md` — when delivering the comeback recap to the customer
- `admin/profit-leak-detector.md` — comeback losses (free re-dos, partial refunds, lost lifetime value) feed the broader profit-leak picture

## Notes

- 2026 industry data suggests AI-assisted comeback pattern analysis can reduce comeback rates by 15–20% over baseline (Wickedfile 2026 case studies, broader RCA tooling). The mechanism is not the AI catching what techs miss — it's the systematic application of cause categories across past ROs that humans don't otherwise have time to perform.
- Aggregation mode is where the real ROI lives. A single comeback analysis is useful; 30 days of comebacks analyzed together exposes systemic patterns (one tech, one vendor, one make, one job type) that no single comeback would reveal.
- This skill is the shop-side counterpart to manufacturing-RCA tools (ProSolvr, iMaintain, Quality-Line) which are framed for OEMs and production lines. The shape — fishbone categories, ranked causes, CAPA — is similar, but the inputs are RO history, not production-line telemetry.
- Pair with `chargeback-defense-documenter.md` and `warranty-claim-preparer.md` as the back-end of the comeback workflow when the comeback escalates beyond a courtesy re-do.
