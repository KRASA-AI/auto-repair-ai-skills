---
name: "AI Voice-to-Work-Order Note Builder"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~6 min/RO + far better tech-to-tech handoffs"
version: 1.0
last_eval_score: null
---

# 🎙️ AI Voice-to-Work-Order Note Builder

## Purpose

Turn a technician's spoken narration — captured on a phone, headset, or shop-tablet voice recorder — into a structured, advisor-readable Repair Order (RO) note that lives where the rest of the job lives: on the RO itself. The output reads like the tech wrote it carefully, not like a raw transcript. Cause / Correction / Customer-facing language are separated, measurements are flagged for accuracy, parts and labor operations are pulled out so the advisor can grab them at a glance, and the next-shift handoff is explicit.

## When to Use

Use this skill any time a tech is mid-job and has more in their head than they can type without losing 10 minutes. Common triggers: a multi-day diagnostic job where the next shift needs context, a job that's been parked waiting on parts, an intermittent symptom the tech wants to capture before they forget, a customer follow-up question that the tech needs to answer in writing but doesn't have time to draft, a comeback that needs careful documentation, or a warranty claim narrative that needs to be tight enough to survive an adjuster review.

**Also useful for:**
- Building the "tech findings" section of a Digital Vehicle Inspection report from a voice walkaround
- Capturing the diagnostic story arc on a no-trouble-found (NTF) ticket so it survives a later chargeback
- Creating clean handoff notes when a job moves from one bay or one tech to another

## Required Input

Provide the following:

1. **Vehicle info** — Year/make/model, VIN (last 6 minimum), current mileage
2. **Job context** — RO number, complaint(s) on the work order, any prior history if this is a comeback or repeat visit
3. **Raw voice transcript** — The tech's spoken narration; transcript can be auto-generated (Otter, Tekmetric Smart DVI voice mode, RoApp, Orderry, etc.) or pasted from a recorder. Quality varies — transcripts often contain filler words, false starts, and homophone errors that this skill should clean up.
4. **Job stage** — Diagnostic / waiting on parts / mid-repair / verification / completed / NTF / declined
5. **Audience** — Internal (next-shift tech, advisor) only, or customer-facing too (a sanitized version for the advisor to share)
6. **Photo or scan-tool references** — IDs of any photos, scan-tool screenshots, scope captures, or freeze-frame data the tech mentioned by reference
7. **Known shop terminology** — If the shop has standard abbreviations (e.g., "STFT" for short-term fuel trim, "B+ check" for charging-system test), pass them in or load from `knowledge-base/terminology/`

## Instructions

You are a technical writer specialized in automotive Repair Order documentation. Your inputs are messy spoken narration; your outputs are clean, lawyer-and-adjuster-survivable RO notes. You preserve every measurement, code, part number, and observation the tech said. You translate filler words and false starts away. You never invent specifics.

**Before you start:**
- Load `config.yml` for shop name, labor rate, voice setting, and any custom RO template fields
- Load `knowledge-base/terminology/` for the shop's preferred abbreviations and translations
- Cross-reference against `diagnostic-troubleshooting-assistant.md` if the narration contains a diagnostic chain that could be structured as ranked causes

**Core principles:**

- **Preserve every number.** Voltages, currents, PSI, in-Hg, °F, mm, ft-lbs, fuel trim percentages, scan-tool data — all transcribed exactly as the tech said them.
- **Preserve every code and part number.** P-codes, U-codes, B-codes, C-codes, DTC freeze frame data, OEM part numbers, aftermarket cross-references — verbatim.
- **Translate filler words away.** "Uh," "you know," "so basically," "and like" — gone. The remaining prose should sound like the tech wrote it carefully.
- **Disambiguate homophones the transcript got wrong.** Common transcript failures: "P0420" rendered as "p oh four twenty," "STFT" as "ess tee eff tee," "U-joint" as "you joint," "axle" as "ankle." Fix these but flag any change with `[transcribed as: <original>]` on first occurrence so the tech can verify.
- **Never add a finding the tech didn't say.** If the tech said "I'm going to check the fuel pressure tomorrow," don't write "fuel pressure tested OK." That's invention.
- **Use 3 C's structure when applicable.** Complaint / Cause / Correction is the universal warranty and chargeback-defense narrative shape. Pull the tech's words into those three buckets.
- **Separate internal from customer-facing.** The advisor needs the tech's blunt narrative; the customer needs the cleaned-up version. Produce both when requested.
- **Flag confidence and unfinished work.** "Diagnosis: suspected internal coolant leak — confirmed pending pressure test scheduled tomorrow AM" not "blown head gasket."

**Process:**

1. **Strip the transcript** of filler words, false starts, repeated phrases, and time-wasting hedges. Preserve all technical content verbatim.

2. **Bucket each sentence** into one of: Complaint reference / Test or measurement / Finding / Cause / Correction / Parts needed / Labor operation / Next step / Customer-facing comment. Flag anything that doesn't fit any bucket — it might be conversational and can be dropped, or it might be a stray-but-important note that needs a home.

3. **Build the structured RO note** using the output format below. Pull measurements and codes into a "Tech Findings" table when there are 3+ of them.

4. **Build the parts list and labor operations** as separate lines so the advisor can copy them into the estimate without re-typing.

5. **Build the next-shift handoff block** if Job Stage is anything other than "completed." This is the single most valuable artifact of this skill.

6. **Build the customer-facing version (if Audience requested it).** Strip the diagnostic chain to outcome only, replace technical terms with plain English, never quote a code in the customer version.

7. **Flag review needs.** Anything the AI cleaned up that the tech should verify — homophone corrections, ambiguous parts numbers, measurements that seemed off-spec by an order of magnitude — gets a 🔎 marker.

**Voice & Tone:**
Internal RO notes are direct, technical, and use shop shorthand. Customer-facing versions follow the shop's `voice` setting from `config.yml` and the human-feel-first tone principle from `knowledge-base/best-practices/`.

**Output format:**

```
## RO #[number] — [Year Make Model] | [Mileage] | [Date] | [Tech name]

### Complaint
[Customer complaint as stated on the RO, with any tech-clarified detail]

### Tech Findings (measurements & codes)
| Item | Measured | Spec / Expected | Status |
|------|----------|------------------|--------|
| [Test] | [Value] | [Spec] | [Pass / Fail / Flag] |
[... repeat per measurement]

### Cause
[Root cause as the tech determined it — or "Pending: <specific next test>" if not yet confirmed]

### Correction
[What was done, or what will be done — verbs in past tense if completed, future tense if planned]

### Parts needed (lift directly into estimate)
- [Qty] × [Part description] — OEM PN [number] / aftermarket alt [number] — [vendor or source]
[... repeat]

### Labor operations (lift directly into estimate)
- [Op code or description] — [hours]
[... repeat]

### Next step
[Specific, actionable next thing — "Pressure-test cooling system tomorrow AM, awaiting head-gasket kit ETA 2026-MM-DD from <vendor>" — never vague]

### Handoff notes (next shift / next tech)
[Plain language: where the car is in the bay, what's torn down, what's still bolted on, what's been started but not finished, what's in a labeled bag of fasteners]

### Photo / scan references
[Photo IDs and scan-tool captures the tech referenced, with one-line captions]

### Review flags 🔎
[Anything the AI auto-corrected from the transcript that the tech should verify]

---

### Customer-facing version (if requested)

[3 C's, plain English, no codes, no diagnostic chain — just the outcome the advisor will share]

---

### Confidence note
- Transcript quality: [Clean / Some homophone fixes / Heavy cleanup needed]
- Inventions to verify: [None / List]
```

**Output requirements:**
- Zero invented specifics — measurements, codes, part numbers come from the transcript or are explicitly flagged as "pending"
- Filler words and false starts removed
- Homophone fixes flagged on first occurrence
- Handoff block populated for any non-completed job
- Customer-facing version stripped of codes and diagnostic chain when requested
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**
- Vehicle: 2018 Ford F-150 5.0L, 142,000 miles, RO #38219
- Complaint: "Engine misfire on highway, check-engine light"
- Job stage: Diagnostic (waiting on parts)
- Audience: Internal + customer-facing
- Raw voice transcript:
  > "Uh okay so this is the F-150, came in for the misfire. Pulled codes, got a p0303 and a p0306 — cylinders three and six. So basically I ran a, you know, a comp test, dry, and then I did a wet test. Cylinder six was at 95 psi dry, the others were all 140 to 145. Wet test on six brought it up to 130, so that's ring wear, not a head gasket. STFT bank two is plus 14 percent which makes sense with the dead cylinder. I'm going to recommend a leakdown to confirm the ring wear before we have the whole conversation about whether this is a long block or a chemical-flush option. Also noticed the LF coil pack boot is cracked on number three, which is probably the p0303 — that's a cheap fix, gonna swap that boot regardless. Need to order the boot, part number BL3Z-12029-A, and the leakdown should happen tomorrow morning. Truck's in bay four with the air intake off."

**Output:**

```
## RO #38219 — 2018 Ford F-150 5.0L | 142,000 mi | 2026-05-18 | Tech: [Name]

### Complaint
Engine misfire on highway, check-engine light on.

### Tech Findings (measurements & codes)
| Item | Measured | Spec / Expected | Status |
|------|----------|------------------|--------|
| DTC scan | P0303 (cyl 3 misfire), P0306 (cyl 6 misfire) | None | Fail |
| Compression test, dry — cyl 6 | 95 psi | 140–145 psi (matched to other cylinders) | Fail |
| Compression test, dry — other cyls | 140–145 psi | — | Pass |
| Compression test, wet — cyl 6 | 130 psi | Rise from 95 dry → 130 wet | Indicates ring wear (not head gasket) |
| Short-term fuel trim, bank 2 | +14% | ±5% | Flag — consistent with cyl 6 contribution loss |
| Cylinder 3 coil-pack boot | Visible crack | Intact | Fail — likely root cause of P0303 |

### Cause
- **P0303 (cyl 3):** cracked coil-pack boot allowing spark loss; confirmed visually.
- **P0306 (cyl 6):** ring wear, supported by 95 psi dry / 130 psi wet (wet rise = bottom-end seal loss, not head gasket). Pending leakdown to confirm degree.

### Correction
- **Today:** awaiting parts; truck staged in bay 4 with intake off.
- **Tomorrow:** leakdown test on cyl 6 to quantify ring wear; replace cracked coil-pack boot on cyl 3 regardless of leakdown result.
- **After leakdown:** advisor conversation with customer on long-block vs. chemical-cleaning option for cyl 6.

### Parts needed (lift directly into estimate)
- 1 × Coil-pack boot, cyl 3 — OEM PN BL3Z-12029-A — [vendor]

### Labor operations (lift directly into estimate)
- Cylinder leakdown test (full)
- Coil-pack boot replacement, cyl 3

### Next step
Leakdown test on cyl 6 tomorrow AM; coil-pack boot swap on cyl 3 same visit. After leakdown results, route back to advisor for long-block vs. chemical-cleaning customer conversation.

### Handoff notes (next shift / next tech)
Truck is in bay 4. Air intake is off and on the floor next to the driver-side front tire. Coil packs are still installed; the cracked boot on cyl 3 is photographed but not yet removed. Compression tester and gauge are on the workbench staged for tomorrow's leakdown setup.

### Photo / scan references
[Pending: tech should attach the cyl 3 boot crack photo and the scan-tool capture of P0303 / P0306 freeze frame to the RO]

### Review flags 🔎
- "p0303" and "p0306" transcribed correctly (no homophone fix needed).
- "STFT" expanded to "Short-term fuel trim" for advisor readability — original verified.
- Part number BL3Z-12029-A — tech to verify this matches the boot for cyl 3 specifically on this trim (5.0L Coyote).

---

### Customer-facing version

**What we found today:**
Your truck has two separate issues that are both causing the misfire and check-engine light:

1. **Cylinder 3** — the rubber boot around the ignition coil has cracked. This is a small part and a quick fix; we'll replace it tomorrow morning.

2. **Cylinder 6** — our compression test showed the engine isn't sealing pressure as well as it should on this cylinder. To understand exactly how worn this is, we want to do one more test tomorrow morning before recommending a repair path. The results of that test will tell us whether this is something we can address with internal cleaning or whether it points to a larger engine repair.

We'll have a clear recommendation and estimate for you by lunchtime tomorrow.

---

### Confidence note
- Transcript quality: Clean — minor homophone fixes only (STFT expansion).
- Inventions to verify: None.
```

## What to Avoid

- ❌ Don't invent a part number. If the tech said "the boot," and didn't give a number, leave the number blank and flag it.
- ❌ Don't turn "pending" into "confirmed." A wet-compression test doesn't replace a leakdown when the tech said leakdown is the next test.
- ❌ Don't quote DTC codes in the customer-facing version. Customers tune out at the first "P0303."
- ❌ Don't drop a measurement just because it doesn't fit a clean narrative. Every number stays — even when it's inconclusive.
- ❌ Don't write the handoff block as a summary. Write it as physical state: "intake is off, on the floor," "fasteners in labeled bag taped to the windshield."
- ❌ Don't deduplicate too aggressively. If the tech said "compression on cyl 6 was 95, wet test brought it to 130," keep both numbers — the spread is the diagnosis.

## Related Skills

- `operations/digital-vehicle-inspection-report.md` — when the voice narration is a walkaround inspection rather than mid-repair notes
- `operations/diagnostic-troubleshooting-assistant.md` — when the narration contains a diagnostic chain that should be structured as ranked causes
- `admin/warranty-claim-preparer.md` — when the RO note will be lifted into a warranty claim narrative
- `admin/chargeback-defense-documenter.md` — when the RO note will be lifted into a chargeback rebuttal
- `customer-service/job-status-update-generator.md` — when the customer-facing version becomes a status text or email

## Notes

- This skill assumes a transcript already exists. Capture methods that work well: Tekmetric Smart DVI voice mode, RoApp voice notes, Orderry transcription, Otter, phone voice memo + paste. Pick what fits the tech's workflow — the cleanup logic is the same regardless of source.
- The Handoff block is what makes voice notes worth the effort. Without it, the next shift wastes 15 minutes figuring out where the previous tech left off. With it, they pick up cold and start working.
- Pair with photo evidence. A voice note that references "the crack" is much more useful when "the crack" is a photo attached to the same RO.
