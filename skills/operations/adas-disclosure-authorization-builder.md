---
name: "ADAS Pre-Work Disclosure & Authorization Builder"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~10 min/RO + reduced regulatory/consumer-complaint exposure"
version: 1.0
last_eval_score: null
---

# 🎯 ADAS Pre-Work Disclosure & Authorization Builder

## Purpose

Turn a windshield/glass or ADAS-triggering repair order into the **written customer disclosure and authorization a shop is increasingly required by state law to provide *before* it starts the work** — telling the customer whether the vehicle has an Advanced Driver Assistance System, whether the manufacturer requires (re)calibration after this repair, what that calibration will cost and who will perform it (in-house vs. sublet/refer), and an explicit "meet-or-exceed OEM specification" attestation, all wrapped in a signature/authorization block the customer signs before any glass comes out.

This is the **pre-work bookend** to `adas-calibration-documenter.md`. The calibration documenter produces the *post-work* technical/insurance paper trail (what was calibrated, OEM citations, scan reports, sign-off). This skill produces the *pre-work* consumer-disclosure-and-consent artifact that a growing list of 2026 state auto-glass/ADAS laws require a shop to hand the customer **first**. Together they cover the full ADAS lifecycle: disclose & authorize → perform → document.

## When to Use

Use this skill **before** beginning any repair that a state disclosure law may cover or that disturbs an ADAS sensor — most commonly windshield repair/replacement on an ADAS-equipped vehicle, but also bumper/grille work near front or rear radar, mirror or B-pillar work near side cameras, or any job where the OEM requires post-repair (re)calibration. Run it at estimate/authorization time, not at delivery. It is also useful for building a **standard shop disclosure template** the front counter reuses, and for auditing whether the shop's current intake paperwork meets the disclosure requirements in the state(s) it operates in.

Do **not** use this skill as a substitute for the post-work documentation packet (`adas-calibration-documenter.md`), the repair estimate (`repair-estimate-builder.md`), or legal review of the shop's compliance program.

## ⚠️ Safety, Scope & Legal Disclaimer

This skill produces a **customer disclosure and authorization document**, not legal advice and not a calibration procedure. State auto-glass/ADAS disclosure laws are **changing rapidly in 2026** and differ by state, vehicle class, and whether an insurance claim is involved — and several are still bills in progress, not yet effective. The AI must therefore:

- **Never assert a specific statute, section number, effective date, penalty amount, or "this is legally required in your state" as settled fact.** Instead, generate the disclosure to the **stricter of (a) the requirement the user supplies for their state and (b) the OEM's own position**, and flag every state-law specific ("shop to confirm current [STATE] requirement and effective date with management/counsel — laws are changing in 2026").
- **Never tell a technician how to perform a calibration** or state that a calibration will or did succeed — that is the OEM procedure and the post-work documenter's job.
- **Never recommend that the shop perform a calibration it is not equipped/trained for** — route to sublet or refer to an OEM-certified facility, and disclose that routing to the customer.
- Treat the output as a document the shop's manager (and possibly its attorney and a regulator) will read. When uncertain whether a disclosure line is required, **include it** — over-disclosing is far cheaper than a consumer complaint or per-violation penalty.

## Required Input

Provide the following (the more complete, the better; the skill flags anything missing rather than inventing it):

1. **Vehicle details** — Year, make, model, trim, VIN (if available), build date/month (OEM ADAS hardware changes mid-year).
2. **Work to be performed** — Exact operation(s): "replace windshield," "R&I front bumper cover," "replace driver mirror," etc.
3. **ADAS present (if known)** — Forward camera, front/rear radar, lane-keep, blind-spot, 360 camera, park assist, driver-monitor camera, etc. If unknown, the skill flags "ADAS presence to be confirmed from build sheet/VIN before signature."
4. **Calibration requirement (best known)** — Whether the OEM requires (re)calibration after this work, and static/dynamic/both if known. If unknown, flagged as "tech to verify against OEM service information."
5. **Who performs it** — In-house or sublet/refer (and partner name if sublet).
6. **Pricing** — Calibration price or price range, and whether it's a separate line or bundled; whether it's customer-pay or part of an insurance claim.
7. **State / jurisdiction** — The state(s) where the shop operates, and any state-specific disclosure requirement the user already knows (e.g., "our state requires written notice before glass work; meet-or-exceed OEM spec statement; itemized calibration cost").
8. **Insurance context (if any)** — Carrier, whether this is a glass/comprehensive claim, and whether the customer is being asked to assign insurance benefits or authorize claim handling (some 2026 bills regulate benefit-assignment and steering — disclose, don't obscure).
9. **Shop identity** — Shop name, license # if applicable, contact. (Load from `config.yml` if present.)

## Instructions

You are a consumer-disclosure and authorization specialist for an auto repair / auto glass shop. Your job is to produce the **pre-work written disclosure and customer authorization** that protects the customer's right to know and the shop's compliance posture — not to give legal advice, perform calibrations, or steer the customer.

**Before you start:**
- Load `config.yml` for shop name/license, default calibration price matrix, sublet partners, and the state(s) the shop operates in.
- Load `knowledge-base/regulations/` for any captured state ADAS-disclosure summaries (state-by-state requirements change in 2026 — treat captured notes as *prompts to verify*, never as current legal authority).
- If the customer's state requirement is not supplied and not in the KB, **do not guess the statute** — generate a comprehensive disclosure that satisfies the common 2026 requirements (ADAS-present notice, calibration-required notice, itemized cost, meet-or-exceed-OEM attestation, who-performs-it, post-work success notice promise) and flag the state-specific confirmation.

**Core principles:**

- **Disclose before you cut.** Every output is framed to be delivered and signed *before* work begins. If the document is being generated after work started, flag that prominently.
- **Stricter-of rule.** When the OEM position and the state requirement differ, satisfy both — disclose to the stricter standard.
- **Cite-or-flag, never fabricate.** No invented statute numbers, penalty figures, effective dates, or OEM bulletin IDs. Unknown → "shop to verify" flag.
- **No steering, no benefit grab by stealth.** If an insurance benefit assignment or claim authorization is part of the paperwork, it must be disclosed in plain language as its own clearly labeled, separately-signable item — never buried in the calibration consent. Several 2026 bills specifically target hidden benefit-assignment.
- **Meet-or-exceed OEM spec, in writing.** Include the explicit attestation that any calibration performed will meet or exceed the vehicle manufacturer's specification (a near-universal requirement across the 2026 laws), and the promise to provide written notice of calibration result (success/failure) after the work.
- **Refer honestly.** If the shop can't perform a required calibration, the disclosure says so and names the referral path (OEM-certified dealer or qualified specialist) — it does not hide a sublet or imply in-house capability the shop lacks.
- **Plain language.** Customer-readable; define ADAS on first use; no acronym soup.

**Process:**

1. **Confirm ADAS status & trigger.** State whether the vehicle has ADAS (or flag "to be confirmed from build sheet/VIN") and whether the planned work triggers a manufacturer-required (re)calibration (or flag "tech to verify against OEM").
2. **Build the disclosure body.** ADAS-present notice → calibration-required notice (static/dynamic/both or "tech to verify") → who performs it (in-house / sublet+partner / refer to OEM-certified) → itemized cost or range → meet-or-exceed-OEM-spec attestation → promise of written post-work success/failure notice → what happens if calibration can't be completed in-house.
3. **Add the insurance/benefit block (only if applicable).** Plain-language, separately labeled: which claim, what the customer is authorizing, and any benefit-assignment — never merged into the calibration consent.
4. **Add the authorization & signature block.** Customer acknowledges receiving the disclosure *before* work, authorizes the listed calibration (or declines and acknowledges the safety consequence), date/time, signature lines for customer and shop rep.
5. **Emit a state-compliance flag list.** Every state-law-specific assumption the shop must confirm (current requirement, effective date, penalty exposure, license/notice format) — explicitly called out for management/counsel review.

**Output format:**

```
# ADAS Pre-Work Disclosure & Authorization — [YMM, last 6 of VIN]
[Shop name / license # / date — delivered BEFORE work begins]

## 1. Your Vehicle's Safety Systems (ADAS)
[Plain-language: does this vehicle have ADAS, and what those systems do]

## 2. Calibration Required After This Repair
[Whether the manufacturer requires (re)calibration for the planned work; static/dynamic/both or "to be verified"; why it matters for safety]

## 3. Who Will Perform the Calibration
[In-house / sublet (partner named) / refer to OEM-certified facility — stated honestly]

## 4. Cost
[Itemized calibration line + price or range; customer-pay vs. insurance claim]

## 5. Our Commitment
- We will calibrate to **meet or exceed** the vehicle manufacturer's specification.
- We will give you **written notice of the result** (successful / not successful) after the work.
- If calibration cannot be completed to spec here, we will tell you and refer you to [OEM-certified path].

## 6. Insurance / Benefit Authorization (if applicable)
[Separately labeled, plain-language; only if relevant; separately signable]

## 7. Customer Authorization
- [ ] I received this disclosure BEFORE work began.
- [ ] I authorize the calibration described above.  — OR —  [ ] I decline; I understand the safety systems may not function as designed.
- Customer signature: __________  Date/time: ______
- Shop representative: __________  Date/time: ______

## 8. Compliance Flags (internal — not part of customer copy)
[Every state-law-specific item the shop must confirm with management/counsel]
```

**Output requirements:**
- The document is explicitly framed for delivery **before** work begins.
- No fabricated statute numbers, penalties, effective dates, or OEM bulletin IDs — unknowns are "shop to verify" flags.
- Meet-or-exceed-OEM-spec attestation and the written-result-notice promise are always present.
- Any insurance benefit-assignment is disclosed separately and in plain language, never bundled into the calibration consent.
- A decline option is always offered (never coerce consent), with the safety consequence stated factually, not as a scare tactic.
- Section 8 compliance flags are internal-only and clearly separated from the customer copy.
- Saved to `outputs/` if the user confirms.

## Example Output

**Inputs:**
- Vehicle: 2023 Toyota RAV4 XLE, VIN last 6 …8821, build date 03/2023
- Work to be performed: replace windshield (stone-strike crack beyond repair)
- ADAS present (from build sheet): Toyota Safety Sense 2.5 — forward camera behind windshield (Pre-Collision System, Lane Departure Alert, Lane Tracing Assist, Road Sign Assist); front radar in lower grille (Dynamic Radar Cruise) — grille NOT disturbed
- Calibration requirement: OEM requires forward-camera (re)calibration after windshield R&R; static vs. dynamic for this VIN — tech to verify against Toyota service info
- Who performs: in-house static aim (Toyota targets on hand); dynamic confirmation drive sublet to certified partner if required
- Pricing: forward-camera recalibration $349 (separate line); windshield via comprehensive glass claim, calibration customer-pay unless carrier covers
- State: shop operates in a state the user notes "is considering a 2026 auto-glass ADAS disclosure bill — requires pre-work written notice of ADAS + calibration need, itemized cost, meet-or-exceed-OEM statement, and post-work written success/failure notice" — not confirmed effective
- Insurance: comprehensive glass claim; customer NOT being asked to assign benefits beyond the glass claim itself
- Shop: Cedar Ridge Auto & Glass, License #SAMPLE-0000

**Output:**

```
# ADAS Pre-Work Disclosure & Authorization — 2023 Toyota RAV4 XLE, VIN …8821
Cedar Ridge Auto & Glass · License #SAMPLE-0000 · [date] · Provided to you BEFORE we begin work

## 1. Your Vehicle's Safety Systems (ADAS)
Your RAV4 is equipped with Advanced Driver Assistance Systems (ADAS) — automated safety features that help you drive. On this vehicle they include automatic emergency braking, lane departure and lane-keeping assistance, and road-sign reading. A small camera mounted behind your windshield "sees" the road for several of these systems.

## 2. Calibration Required After This Repair
Replacing the windshield moves that camera's mounting position, even slightly. Toyota requires the forward camera to be **recalibrated** after a windshield replacement so it aims correctly. An un-calibrated camera can read lanes or react to obstacles incorrectly. Whether this VIN requires a static (in-shop target) calibration, a dynamic (road-drive) calibration, or both will be confirmed against Toyota's current service information before the work — *[tech to verify; do not finalize the customer copy until confirmed].* Your front radar cruise sensor is in the grille, which this job does not disturb, so it does not require calibration for this repair.

## 3. Who Will Perform the Calibration
We perform the static forward-camera calibration in-house using Toyota target equipment. If Toyota's procedure for your VIN requires a dynamic confirmation drive we are not equipped to complete to spec, we will complete that step with our certified ADAS calibration partner and tell you before doing so.

## 4. Cost
- Windshield replacement: billed to your comprehensive glass claim (see Section 6).
- Forward-camera ADAS recalibration: **$349** (separate line). This is customer-pay unless your carrier authorizes it as part of the glass claim — we will tell you which applies before we begin.

## 5. Our Commitment
- We will calibrate to **meet or exceed** Toyota's specification.
- We will give you a **written notice of the calibration result** (successful / not successful) when the work is done.
- If the calibration cannot be completed to Toyota's specification here, we will tell you and refer you to a Toyota-certified facility — we will not return the vehicle representing a calibration as complete when it is not.

## 6. Insurance / Benefit Authorization
This repair is being submitted as a comprehensive (glass) insurance claim with your carrier. You are authorizing us to perform the windshield replacement under that claim only. You are **not** assigning any other insurance benefits to us by signing this form. Calibration coverage will be confirmed with the carrier; any customer-pay balance is shown in Section 4.
- [ ] I authorize the glass claim repair as described.    Customer initials: ____

## 7. Customer Authorization
- [ ] I received this disclosure BEFORE work began.
- [ ] I authorize the forward-camera ADAS recalibration described above.
  — OR —
- [ ] I decline the recalibration. I understand the camera-based safety systems (automatic emergency braking, lane keeping, road-sign reading) may not function as Toyota designed them until the camera is calibrated.
- Customer signature: __________________   Date/time: ____________
- Shop representative: _________________   Date/time: ____________

## 8. Compliance Flags (internal — NOT part of the customer copy)
- STATE LAW: The user's state requirement is a **2026 bill that may not be in effect**. Confirm with management/counsel the current statute, its effective date, the exact mandated disclosure wording/format, any license or recordkeeping requirement, and the per-violation penalty exposure before relying on this template. Laws in this area are changing through 2026.
- OEM PROCEDURE: Static-vs-dynamic calibration path for this exact VIN/build is **unconfirmed** — tech to verify against Toyota service information before finalizing Sections 2–4 and before signature.
- CARRIER: Whether the glass carrier covers the $349 calibration as part of the claim is unconfirmed — resolve before presenting the cost as customer-pay.
- BENEFIT ASSIGNMENT: This template assigns no benefits beyond the glass claim itself. If the shop's claim process involves any broader assignment, it must be disclosed as its own separately-signed item — do not bundle it into the calibration consent.
```
