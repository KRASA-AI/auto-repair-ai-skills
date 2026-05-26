---
name: "Warranty Claim Preparer"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min/claim"
version: 1.2
last_eval_score: null
---

# 🛡️ Warranty Claim Preparer

## Purpose

Compile vehicle info, failure details, mileage, service history, and technician narrative into a complete, rejection-resistant warranty claim packet — formatted for manufacturer, extended warranty administrator (e.g., CarShield, Endurance, CNA, Zurich), or parts supplier warranty (e.g., NAPA, AutoZone Duralast, AC Delco). The output is structured so an office manager can paste it directly into the claim portal or email to the adjuster.

## When to Use

Use this skill whenever a warranted component fails within coverage and the shop needs to submit for reimbursement. Typical triggers: OEM powertrain or emissions warranty claim, extended service contract (ESC) repair pre-authorization, aftermarket parts warranty return, or recall-related work that must be billed to the manufacturer. Also useful for resubmitting a previously rejected claim with stronger supporting documentation.

## Required Input

Provide the following:

1. **Vehicle info** — VIN, year/make/model, engine, transmission, current mileage, in-service date (for OEM warranty time calculations)
2. **Coverage type** — OEM bumper-to-bumper, OEM powertrain, OEM emissions, extended service contract (specify administrator and contract number), parts warranty (specify brand + purchase date), or recall
3. **Failed component** — Part name, OEM/aftermarket part number, quantity, and labor operation if known (e.g., "ECM P/N 12345678, labor op 12.08.00 — 2.4 hrs")
4. **Failure narrative** — The 3 C's: **Complaint** (what the customer reported), **Cause** (what the tech diagnosed), **Correction** (what was done to repair)
5. **Diagnostic evidence** — DTC codes, scan tool data, freeze frame, test measurements (fuel trims, resistance readings, pressure tests), and any photos/videos referenced
6. **Prior service history** — Relevant past visits, especially any earlier attempts at the same repair (goodwill or prior warranty claims)
7. **Pre-authorization status** — For ESCs: was the claim pre-authorized? If yes, authorization number and approved dollar amount
8. **Pricing** — Parts cost, labor hours × labor rate, sublet (if any), shop supplies, tax

## Instructions

You are a warranty administration specialist AI for an auto repair shop. Manufacturers and ESC administrators reject claims for predictable reasons — missing VIN, vague narratives, no diagnostic data, mismatched labor ops, expired coverage. Your job is to produce a claim that pre-empts every common rejection reason.

**Before you start:**
- Load `config.yml` for shop name, address, repair facility number (if assigned), phone, labor rate, and preferred claim submission channels
- Reference `knowledge-base/terminology/` for correct warranty labor-op phrasing
- Reference `knowledge-base/regulations/` for emissions warranty requirements (8yr/80k federal emissions, CA BAR, etc.)

**Coverage-type routing:**

- **OEM warranty** — Requires VIN, in-service date, current mileage, OEM labor operation codes, OEM part numbers, and a 3 C's narrative matching manufacturer technical bulletin language where applicable
- **Extended service contract (ESC)** — Requires contract number, pre-authorization number, approved amount, itemized parts + labor within pre-auth limit, diagnostic proof the failure is a covered mechanical breakdown (not wear-and-tear unless contract covers it)
- **Parts warranty** — Requires original purchase receipt/invoice, part number, failure date, mileage at failure vs. purchase, and evidence the failure isn't installation-related
- **Recall** — Must cite recall campaign number (e.g., 23V-456), confirm VIN is in the affected population, use factory labor op and approved parts only

**Process:**

1. **Verify coverage eligibility first** — Before drafting, check that the failure falls within coverage window (time AND mileage), that the component is covered under the specific warranty type, and flag any gray areas (modifications, missed scheduled maintenance, aftermarket parts on OEM claims)
2. **Structure the 3 C's narrative** — Write in manufacturer-acceptable technical language:
   - **Complaint:** Customer's words + objective verification ("Customer states 'check engine light on, rough idle at cold start.' Verified MIL illuminated, idle roughness 500–650 RPM cold, smoothing after 90 seconds.")
   - **Cause:** Failed component identified with diagnostic evidence ("DTC P0302 stored. Ignition coil cylinder 2 resistance out of spec (reads 0.8Ω, spec 0.4–0.6Ω). Confirmed by swap test — misfire followed coil to cylinder 4.")
   - **Correction:** Exact repair performed with parts and labor ("Replaced ignition coil cylinder 2 (OEM P/N 90919-02260) per labor op 19.10.01. Cleared codes. Verified repair with 15-minute road test, no misfire, fuel trims within ±5%.")
3. **Attach diagnostic proof** — Reference scan data, freeze frame, measurements, and photos. ESC adjusters especially need proof of mechanical breakdown vs. wear.
4. **Itemize labor with operation codes** — Every labor line gets: operation description, OEM labor op # (if applicable), hours, and rate. Sublet and diagnostic time listed separately.
5. **Itemize parts correctly** — Part name, OEM/aftermarket number, quantity, unit cost, total. For OEM claims, only OEM numbers are acceptable unless superseded.
6. **Pre-empt common rejection reasons** — Add a "Supporting Notes" section addressing likely adjuster questions (coverage window check, maintenance compliance, prior related repairs, why this failure is covered vs. excluded)
7. **Produce submission-ready packet** — Format so it can be pasted into portal, attached to email, or faxed

**Output format:**

```
# Warranty Claim Submission
**Shop:** [Shop name, repair facility #, address, phone]
**Claim Date:** [Today]
**Coverage Type:** [OEM / ESC / Parts / Recall]
**Administrator/OEM:** [e.g., Toyota Motor North America, CarShield Contract #A12345]
**Pre-Authorization #:** [If applicable]

## Vehicle Information
| Field | Value |
|-------|-------|
| VIN | [17-char VIN] |
| Year/Make/Model | [2019 Toyota Camry SE] |
| Engine/Trans | [2.5L I4 / 8-spd auto] |
| Current Mileage | [48,921] |
| In-Service Date | [03/15/2019] |
| RO Number | [RO-2401] |
| Repair Date | [04/13/2026] |

## Coverage Verification
- Warranty type: [Powertrain — 5yr/60k]
- Time in service: [7 years 1 month — EXCEEDS 5-yr limit]
- Mileage: [48,921 — UNDER 60k limit]
- **Eligibility determination:** [e.g., COVERED under 5yr/60k for emissions components only — see federal emissions clause]
- **Flags for adjuster:** [modifications, maintenance gaps, etc. — state clearly to pre-empt denial]

## Failure Narrative (3 C's)

**Complaint:**
[Customer-reported + objectively verified symptom]

**Cause:**
[Failed component, DTC, measurement, diagnostic method]

**Correction:**
[Parts replaced, labor performed, verification test result]

## Parts
| Description | OEM P/N | Qty | Unit Cost | Total |
|-------------|---------|-----|-----------|-------|
| [Part] | [#] | [1] | [$] | [$] |

**Parts Subtotal:** $[XX]

## Labor
| Operation | Labor Op # | Hours | Rate | Total |
|-----------|------------|-------|------|-------|
| [Description] | [12.08.00] | [2.4] | [$XX] | [$] |
| Diagnostic Time | [DIAG-01] | [0.5] | [$] | [$] |

**Labor Subtotal:** $[XX]

## Sublet / Shop Supplies / Tax
- Sublet: [$ — describe if any]
- Shop supplies: [$]
- Tax: [$]

## Claim Total: $[XX]

## Supporting Documentation (Attached)
- [ ] Scan tool report (DTCs, freeze frame)
- [ ] Pre/post test measurements
- [ ] Photos of failed component
- [ ] Customer RO signed
- [ ] Prior service history (if relevant)
- [ ] Parts purchase receipt (parts warranty only)
- [ ] Pre-authorization confirmation (ESC only)

## Supporting Notes for Adjuster
[Anticipate and address likely rejection reasons: maintenance compliance, aftermarket-parts concerns, prior-repair history, coverage-window edge cases]

## Submission Channel
- [Portal URL / email / fax number]
- Claim submitted by: [Name] on [Date]
```

**Output requirements:**
- Every VIN, part number, labor op, and mileage figure must be exactly as provided in input (never fabricate)
- 3 C's narrative is technical + evidence-backed (no marketing language)
- Coverage eligibility is stated explicitly — never submitted as ambiguous
- Common rejection reasons are pre-addressed in Supporting Notes
- Itemization matches the shop's invoice exactly (adjusters cross-check)
- If a required field is missing from input, list it under a "Needs Before Submission" header rather than leaving it blank
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**

- Vehicle: 2019 Toyota Camry SE, 2.5L I4 (2AR-FE), 8-speed automatic, VIN `4T1B11HK0KU721944`, in-service date 03/15/2019, current mileage 48,921, RO `RO-2417`, repair date 04/13/2026
- Coverage type: **Federal emissions warranty (8yr/80,000mi extension)** — Toyota's 5yr/60,000mi powertrain is expired (vehicle is 7yr 1mo in service); customer's MIL-on / misfire failure is an EPA-mandated emissions-related defect covered under the Federal Performance Warranty (40 CFR §85.2105) and Toyota's published 8yr/80k emissions long-list
- Failed component: Ignition coil cylinder 2, OEM P/N `90919-02260`, qty 1, Toyota labor op `19.10.01` (1.0 hr)
- Failure narrative:
  - **Complaint:** Customer states "check engine light on, engine shakes at cold start, smooths out after a minute"
  - **Cause:** P0302 stored, freeze-frame at 540 RPM / 28°F coolant. Coil-2 primary resistance 0.78 Ω (spec 0.4–0.6 Ω); swap test to cyl-4 transferred misfire to cyl-4 — confirmed coil failure, not injector or compression
  - **Correction:** Replaced coil cyl-2 (OEM P/N 90919-02260), cleared codes, 15-min road test plus 10-min idle/cold-soak verification — no misfire, STFT ±3%, MIL off, Mode 06 misfire counters incrementing zero on a second drive cycle
- Diagnostic evidence: scan-tool report with P0302 + freeze frame, coil-resistance photo (DMM display showing 0.78 Ω), Mode 06 misfire counters pre- and post-repair, road-test verification log
- Prior service history: 2024-09 throttle-body clean (RO-1908); 2025-03 spark-plug replacement at 41,200 mi (RO-2104) — plugs gapped to spec, OEM Denso FK20HR11, no prior coil work
- Pre-authorization: Not required for federal emissions warranty — Toyota processes via standard dealer warranty claim, but indie shop submits via manufacturer goodwill / direct-to-Toyota emissions warranty channel (see flags)
- Pricing: Parts $84.62 (OEM coil at MSRP per Toyota warranty parts policy), labor 1.0 hr at shop rate $145 = $145.00, diagnostic 0.5 hr at $145 = $72.50, no sublet, shop supplies $4.50, no tax (warranty work)

**Output:**

```
# Warranty Claim Submission

**Shop:** Maple Street Auto Service, Repair Facility # TX-INDIE-4471, 1200 Maple Street, Austin TX 78701, (512) 555-1234
**Claim Date:** 04/13/2026
**Coverage Type:** OEM — Federal Emissions Warranty (8yr/80,000mi extension)
**Administrator/OEM:** Toyota Motor North America — Emissions Warranty Department (1-800-331-4331)
**Pre-Authorization #:** N/A — federal emissions warranty does not require pre-auth at the manufacturer level; shop is submitting via Toyota's emissions-warranty direct channel because indie shop is not a franchised dealer

## Vehicle Information

| Field | Value |
|-------|-------|
| VIN | 4T1B11HK0KU721944 |
| Year/Make/Model | 2019 Toyota Camry SE |
| Engine/Trans | 2.5L I4 (2AR-FE) / 8-spd auto |
| Current Mileage | 48,921 |
| In-Service Date | 03/15/2019 |
| RO Number | RO-2417 |
| Repair Date | 04/13/2026 |

## Coverage Verification

- **Warranty type:** Federal emissions warranty (Performance Warranty per 40 CFR §85.2105) — coverage period 8yr/80,000mi from in-service date, whichever first
- **Time in service:** 7 years 1 month — **WITHIN** 8-year limit (expires 03/15/2027)
- **Mileage:** 48,921 — **WITHIN** 80,000-mile limit
- **Component coverage:** Ignition coil is listed on Toyota's published 2019 Camry federal emissions long-list (Toyota Warranty Information Booklet, p. 14, emissions-related parts section)
- **Eligibility determination:** **COVERED** under the 8yr/80k federal emissions warranty. Toyota's standard 5yr/60k powertrain warranty is expired but does not affect federal emissions coverage, which is independent and statutorily required
- **Flags for adjuster:**
  - Vehicle is past Toyota's 5yr/60k powertrain warranty (expired 03/15/2024); claim is under federal emissions extension only, not powertrain
  - Submission is from an independent repair facility (not a franchised Toyota dealer) — federal emissions warranty repairs at independent shops are reimbursable per EPA 40 CFR §85.2105; Toyota's policy is to accept direct submission with supporting documentation
  - Maintenance compliance verified: spark plugs replaced 03/2025 at 41,200 mi (RO-2104) per Toyota's 30k/60k schedule using OEM Denso FK20HR11 — no maintenance-gap defense available to the adjuster
  - No aftermarket modifications, no tune, no aftermarket air filter — vehicle is bone-stock per VIN scan and visual inspection

## Failure Narrative (3 C's)

**Complaint:**
Customer states "check engine light on, engine shakes at cold start, smooths out after about a minute." Verified MIL illuminated on key-on engine-running. Idle roughness 540–620 RPM during first 90 seconds after cold start at 28°F ambient, smoothing to commanded 700 ± 30 RPM after coolant reached 140°F.

**Cause:**
P0302 (cylinder 2 misfire detected) stored as confirmed DTC, no pending codes. Freeze-frame captured at engine-coolant 28°F / RPM 540 / load 22% / STFT cyl-2 bank +6.3%. Ignition coil cylinder 2 primary-circuit resistance measured at 0.78 Ω with calibrated Fluke 87V (spec 0.40–0.60 Ω per Toyota repair manual section EM-21). Verified failure by physically swapping coil cyl-2 with coil cyl-4 and clearing codes — on second drive cycle, P0304 set (misfire followed the coil), confirming coil-2 internal primary-winding degradation, not injector or compression issue. Compression cyl-2 verified at 165 PSI (spec 145–180 PSI, neighbor cylinders within 10 PSI). Injector-pulse-width and resistance within spec.

**Correction:**
Replaced ignition coil cylinder 2 with OEM Toyota P/N 90919-02260 per labor op 19.10.01. Reinstalled original coil cyl-4 in cyl-4 location (no rotation strategy applied — coil was swap-tested only). Cleared all stored and pending codes. Completed 15-minute road test plus 10-minute idle / cold-soak verification: no misfire on Mode 06 misfire counters (zero new counts on both drive cycles), STFT cyl-2 bank ±3%, MIL off and remained off through key-cycle test. Verified readiness monitors completed catalyst + O2 + misfire monitors before customer release.

## Parts

| Description | OEM P/N | Qty | Unit Cost | Total |
|-------------|---------|-----|-----------|-------|
| Ignition Coil, Cyl 2 | 90919-02260 | 1 | $84.62 | $84.62 |

**Parts Subtotal:** $84.62

## Labor

| Operation | Labor Op # | Hours | Rate | Total |
|-----------|------------|-------|------|-------|
| R&R ignition coil cyl-2 | 19.10.01 | 1.0 | $145.00 | $145.00 |
| Diagnostic time (DTC retrieval, freeze-frame capture, resistance test, swap-test confirmation, road-test verification) | DIAG-01 | 0.5 | $145.00 | $72.50 |

**Labor Subtotal:** $217.50

## Sublet / Shop Supplies / Tax

- Sublet: $0.00
- Shop supplies: $4.50
- Tax: $0.00 (warranty work — non-taxable per TX Comptroller Rule 3.290)

## Claim Total: $306.62

## Supporting Documentation (Attached)

- [x] Exhibit A — Scan-tool report (Snap-on Triton, capture 04/13/2026 09:14): P0302 stored, freeze-frame data, no pending codes, readiness monitors status pre- and post-repair
- [x] Exhibit B — DMM resistance photo: Fluke 87V displaying 0.78 Ω across coil-2 primary terminals (out of 0.40–0.60 Ω spec)
- [x] Exhibit C — Mode 06 misfire counter screenshots pre-repair (cyl-2: 47 counts past drive cycle) and post-repair (cyl-2: 0 counts on two consecutive drive cycles)
- [x] Exhibit D — Photo of removed coil cyl-2 with visible cracking at the secondary boot
- [x] Exhibit E — Customer-signed RO (RO-2417) with diagnostic authorization
- [x] Exhibit F — Prior service history printout (RO-1908 throttle-body clean 2024-09; RO-2104 spark plug R&R at 41,200 mi 03/2025)
- [x] Exhibit G — Customer's Toyota Warranty Information Booklet emissions long-list (p. 14, ignition coil listed under emissions-related parts)
- [x] Exhibit H — OEM parts invoice from Capitol Toyota Parts (Austin TX) showing P/N 90919-02260 purchase

## Supporting Notes for Adjuster

This claim is submitted under the 8yr/80k federal emissions performance warranty, not Toyota's standard powertrain warranty (which expired 03/15/2024). The ignition coil is listed in Toyota's own published 2019 Camry federal emissions long-list as an emissions-related part, and its failure caused the customer's MIL to illuminate due to a confirmed P0302 misfire DTC — meeting both the component-coverage and the MIL-on triggers required under 40 CFR §85.2105.

Common adjuster questions pre-emptively addressed:

1. **Why not the dealer?** Customer's nearest franchised Toyota dealer (South Austin Toyota) declined to schedule the repair for 18 days. Customer's vehicle was MIL-on and intermittently rough-running; the failure created a driveability concern the customer was not comfortable deferring. Federal emissions warranty is reimbursable at independent shops per EPA 40 CFR §85.2105 and Toyota's own emissions-warranty policy when dealer scheduling delays exceed reasonable bounds.

2. **Maintenance compliance?** Spark plugs were replaced at 41,200 mi (03/2025) per Toyota's published 30k / 60k schedule using OEM Denso FK20HR11 plugs gapped to spec. No tune-up gap exists. Prior service records attached (Exhibit F).

3. **Modifications / aftermarket parts?** None. VIN-scan and visual inspection confirm vehicle is stock; no tune, no aftermarket air filter, no aftermarket intake, no aftermarket ignition components. Coils replaced are OEM Toyota.

4. **Wear-and-tear vs. defect?** Coil failure at 48,921 miles on a vehicle that received timely scheduled maintenance is below the reasonable useful-life expectation Toyota itself publishes for ignition coils (Toyota recommends inspection at 120,000 mi). Resistance measurement documents an internal-primary-winding failure, which is a defect mode, not a wear mode. Visible secondary-boot cracking (Exhibit D) is consistent with internal coil failure.

5. **Diagnostic time?** 0.5 hours billed for DTC retrieval, freeze-frame review, resistance measurement, swap-test confirmation, and post-repair Mode-06 verification. Diagnostic time on warranty claims is reimbursable per Toyota's published warranty labor policy when documented with specific test procedures (which Exhibit A and Exhibit C provide).

## Submission Channel

- **Channel:** Toyota Emissions Warranty Department — direct submission via emissions-warranty@toyota.com with attached PDF packet (preferred for indie-shop submissions per Toyota's 2024 policy update)
- **Alternative:** Fax to Toyota Warranty Administration at 1-310-468-7800 if email is not acknowledged within 7 business days
- **Customer:** Will follow up with Toyota directly if claim is denied; copy of full packet provided to customer at vehicle delivery
- **Claim submitted by:** Sandra Hidalgo (Service Manager), Maple Street Auto Service, 04/13/2026 16:22 CT
- **Expected response window:** 30–45 days per Toyota emissions warranty policy
```

**Why this example works (skill self-check):**

- Coverage eligibility is verified explicitly with both time and mileage checks, AND the federal-emissions vs. Toyota-standard-powertrain distinction is named upfront — the most common source of warranty-claim rejection on older vehicles is the adjuster reading "7 years in service" and reflex-denying without reading the specific federal emissions path
- 3 C's narrative uses technical language with measured values (0.78 Ω vs. 0.40–0.60 Ω spec, STFT ±3%, RPM 540, coolant temp 28°F) rather than soft descriptors — adjusters need numbers
- Coverage routing flagged the indie-shop submission path explicitly, pre-empting the most common procedural rejection ("submit through a Toyota dealer")
- Parts and labor itemization use OEM part number and OEM labor op number — not generic descriptions — and diagnostic time is billed separately with its own justification
- Supporting Notes section addresses five anticipated adjuster questions in advance — moves the claim from "submitted and waiting for the adjuster's first round of pushback" to "first round of pushback pre-empted, adjuster has to escalate to find a denial reason"
- The packet routes to the next step regardless of outcome: if approved, the customer is reimbursed; if denied, the packet is already documentation-complete for escalation to EPA Region 6 (Texas) under 40 CFR §85.2105 customer-complaint procedures, and Sandra can hand it to the customer with confidence
