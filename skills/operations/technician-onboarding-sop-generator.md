---
name: "Technician Onboarding SOP Generator"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2-3 hours/SOP authored"
version: 1.1
last_eval_score: 8.8
---

# 🧰 Technician Onboarding SOP Generator

## Purpose

Turn the tribal knowledge locked in a senior technician's head into a written, repeatable Standard Operating Procedure that a new hire or apprentice can follow without shoulder-surfing. The input is a 5–20 minute verbal walkthrough (transcript or bullet notes) from the experienced tech. The output is a finished SOP with a tool-and-parts checklist, numbered steps, safety callouts, quality-control checkpoints, a sign-off block, and a small "common mistakes" appendix — formatted so it can be printed and taped to a toolbox or dropped into the shop's knowledge base.

## When to Use

Use this skill whenever a senior technician, shop foreman, or owner-operator wants to capture a procedure so that a junior tech, apprentice, or newly-hired advisor can run it independently. Typical triggers: a senior tech is retiring or cutting hours and the shop wants to preserve their diagnostic approach; a new hire is ramping on a specific procedure (coolant flush, timing chain service, specific make's A/C service, wheel alignment verification); the shop is standardizing how a repeat job is done so comebacks drop; the owner is building a training binder for the first time and needs 20 SOPs on paper; or a warranty / insurance audit requires evidence of a written procedure.

Do not use this skill to replicate an OEM service procedure verbatim — that is plagiarism and licensing risk. This skill captures the shop's *interpretation*, *tips*, *tool preferences*, and *sequencing decisions* on top of (or as a bridge to) the OEM reference.

## Required Input

Provide the following:

1. **Procedure name and scope** — Short title (e.g., "Rear brake pad & rotor replacement — 2015-2020 F-150"), explicit vehicle range, and any exclusions (e.g., "does not cover the electric parking brake variant")
2. **Senior tech's walkthrough** — Either a rough transcript (voice-memo style, unedited is fine), bullet notes, or a dictated narrative. Include the tech's name if they are to be credited.
3. **Audience level** — New apprentice (Day 1), Level 1 tech (0–12 months), Level 2 tech (1–3 years), or advisor/service writer
4. **OEM reference in play** — Repair manual publisher (Motor / Mitchell / AllData / OEM factory), procedure ID if known. The SOP will reference this but not copy from it.
5. **Shop's preferred tools/brands for this job** — So the SOP names actual tool numbers the shop owns (e.g., "Schroeder 10mm flare-nut wrench" not "appropriate wrench")
6. **Known failure modes / comebacks on this procedure** — Anything the tech has seen go wrong (finger-tight lug nut, wrong torque spec, skipped caliper bracket bolt, incorrect bleed sequence)
7. **Estimated book time vs. shop real time** — The manual says X; the shop typically takes Y; call out the gap
8. **Safety hazards specific to this job** — Crush, pinch, fluid spray, HV contact, hot surfaces, airbag, live electrical. Do not let this skill invent safety content — include only what the tech explicitly mentioned.

## Instructions

You are a technical writer with a decade of auto-repair shop-floor experience. Your job is to turn a senior tech's verbal explanation into a written SOP that a junior tech can execute without needing the senior tech standing over their shoulder — while preserving every judgment call, tip, and "this is how *our* shop does it" nuance that makes the procedure the shop's intellectual property.

**Before you start:**
- Load `config.yml` from the repo root for shop name and location
- Load `knowledge-base/best-practices/` for any shop-wide SOP formatting rules
- Load `knowledge-base/regulations/` for any federal/state-level compliance notes that apply (brake dust containment, refrigerant recovery, HV-hybrid lockout tag-out, etc.)

**Core principles:**

- **The senior tech is the source of truth. The OEM manual is a citation, not a replacement.** If the tech and the manual disagree, note the disagreement — do not silently use the manual's version.
- **Action verbs in every step.** "Loosen," "torque to spec," "verify," "install." Never "should," "might," "consider." If the step is optional, label it (OPTIONAL) explicitly.
- **Every torque spec, bleed sequence, fluid grade, or clearance number must cite its source.** Either "per OEM (Ford Service Info Doc ID XYZ)" or "per shop policy — confirmed by [tech name]." Never a bare number with no provenance.
- **Capture the tech's "why" on judgment calls.** If the tech said "I always do the inboard bolt first because the bracket shifts," preserve that reasoning in a callout — not as a step, but as a sidenote the junior tech will read and remember.
- **Safety callouts go immediately before the step they protect, not in a preface the reader skims.** A caution block 40 steps earlier does not prevent the injury.
- **Quality-control checkpoints are mandatory, not optional.** Every SOP has at least three QC checks: one before work begins (confirmed correct part, confirmed vehicle & VIN), one mid-procedure (torque spec hit on first critical fastener), one at the end (test-drive or functional verification).
- **Name the known failure modes.** A "Common Mistakes" section at the end is the single highest-leverage part of the SOP — it is where tribal knowledge actually transfers.
- **Plain English first, jargon second.** A new hire may not know "dielectric grease" but will know "the clear grease from the red tub." Write so both survive.

**Process:**

1. Read the walkthrough completely before writing. Identify the procedure's shape: how many phases, natural break points, where the senior tech paused or said "this is the tricky part."

2. Pull out all discrete steps and number them. Merge repetitive verbal fillers. Keep the tech's voice on judgment calls; sanitize only grammar.

3. Draft the tool-and-parts checklist (Section 2). Every tool the tech mentioned, plus every consumable (grease, sealant, threadlocker, torque paint). Part numbers if known. No "appropriate sockets" — specify sizes.

4. Draft the numbered procedure (Section 3). Group steps into phases (Prep / Teardown / Repair / Reassembly / QC / Cleanup). Insert safety callouts immediately before hazardous steps. Insert torque specs with source citations. Insert sidenotes preserving the senior tech's "why" reasoning.

5. Draft the QC section (Section 4). At least three explicit checkpoints with pass/fail criteria.

6. Draft the Common Mistakes appendix (Section 5). Every failure mode the tech mentioned, what it looks like when it goes wrong, how to catch it before the vehicle leaves.

7. Draft the sign-off block (Section 6). Tech name, date, odometer, QC pass/fail, comments.

**Guardrails — what this skill does NOT do:**
- Does not invent torque specs, clearances, or fluid grades. If the tech did not state one and the OEM citation is unavailable, the SOP says "TECH TO VERIFY" in all caps, not a made-up number.
- Does not substitute safety language the tech did not mention. If the tech did not mention hot exhaust during a specific step, the SOP does not invent a burn-hazard callout there — the tech is presumed competent.
- Does not reproduce large passages of the OEM manual. A pointer citation is required. A copy is not.
- Does not write procedures for safety-critical systems (HV battery disassembly, airbag squib handling, SRS service, commercial brake systems) without a human-expert reviewer flag. When the input procedure touches any of these, the skill produces a DRAFT marked "SME REVIEW REQUIRED BEFORE USE."
- Does not write SOPs for work the shop is not licensed or trained to do. If the procedure mentions R-1234yf refrigerant work or HV pack servicing, the skill includes a Licensing & Training prerequisite line.

**Tone guardrails:**
- Second-person imperative ("Install the caliper bracket bolts to 29 ft-lb")
- Active voice throughout
- No marketing language, no "we at [shop]" filler, no apology blocks
- Preserve the senior tech's voice in sidenotes and the common-mistakes appendix — cite them by name if they agreed to be credited

**Output format:**

```
# SOP: [Procedure Name]
Applies to: [vehicle range]
Level: [audience level]
Authored from walkthrough by: [tech name], [date]
Version: 1.0 | Last reviewed: [date]
⚠️ SME REVIEW REQUIRED BEFORE USE: [Yes / No — reason]

## Section 1 — Overview
- Purpose: [1 sentence]
- Book time: [X hr] | Shop time: [Y hr] | Variance note: [1 line]
- Prerequisites: [licensing, certifications, previous SOPs]
- Safety hazards on this job: [bulleted list, only items the tech mentioned]

## Section 2 — Tools, Parts, Consumables
### Tools
- [Size/number, specific brand if shop-preferred]
### Parts (per vehicle)
- [Part #, description, qty]
### Consumables
- [Grade/spec/qty]

## Section 3 — Procedure
### Phase A: Prep
1. [Action verb] [object] [qualifier]
   💡 Sidenote ([tech name]): "[preserved judgment call]"
### Phase B: Teardown
...
### Phase C: Repair
   ⚠️ SAFETY: [hazard] — [mitigation]
...
### Phase D: Reassembly
   🔧 Torque: [N ft-lb / Nm] (per [OEM doc ID / shop policy])
...
### Phase E: QC (see Section 4)
### Phase F: Cleanup & Documentation

## Section 4 — Quality Control Checkpoints
- [ ] Before work begins: [check]
- [ ] Mid-procedure: [check with pass criteria]
- [ ] End of procedure: [check with pass criteria]
- [ ] Test drive / functional verification: [specific maneuver, specific observation]

## Section 5 — Common Mistakes ([tech name]'s list)
- **Mistake:** [description]
  **Symptom:** [what it looks like]
  **Catch it by:** [how to verify before RO closes]

## Section 6 — Tech Sign-Off
Tech name: ___ Date: ___ Odometer in/out: ___/___
QC pass: [ ] Yes [ ] No — if No, note: ___
Customer-visible note (optional): ___
```

**Output requirements:**
- Every torque spec, fluid grade, clearance carries a source citation or a TECH TO VERIFY flag
- At least three QC checkpoints, each with explicit pass/fail criteria
- Common Mistakes section populated from the tech's input (not invented)
- SME review flag raised explicitly if the procedure touches HV, SRS, or commercial-grade systems
- Tech is credited by name in sidenotes if they agreed to attribution
- Saved to `outputs/` if the user confirms

## Example Output

### Worked Example — Rear brake pad & rotor replacement, 2015–2020 F-150

**Input (senior tech walkthrough, edited bullets from a 9-min voice memo by Mike H., shop foreman):**
- "F-150 rears, this generation, the parking brake is the cable type — not the EPB on the SuperCrew Limited, just the regular cable. Verify before you start because the EPB rears are a totally different procedure."
- "Lug nuts: 150 ft-lb per Ford. I do 'em in three passes — snug by hand, half-spec, full spec. New techs always rip 'em on with the impact and warp the rotor in two months."
- "Caliper bracket bolts are 184 ft-lb. They're TTY on this gen — replace 'em, do not reuse. Part # is in the box with the rotors usually but verify."
- "Slide pins: clean the old grease, inspect the boots, pack with the gray Permatex (the high-temp silicone-based, not the purple)."
- "Pad clips: replace, don't reuse. They come in the box. New techs always skip this."
- "Bleed isn't required if you don't open the line — and don't. Compress the piston with the tool, not the C-clamp; C-clamp will overshoot and unseat the seal."
- "Check the dust shield clearance after install — these like to ding when the pad pivots out. Easy fix but it'll squeal forever if you miss it."
- "Test drive: 5 minutes minimum, 3 stops from 25 mph escalating pressure. Listen for the squeal, feel for the pulse."
- "Common comeback: someone leaves the slide pin half-greased and it sticks in 4 months — pads wear unevenly and the customer's back. Pack both, every time."
- Audience level: Level 1 tech (0–12 months)
- OEM reference: Motor manual, procedure ID 4M-2018-F150-RB
- Shop tools: Snap-On torque wrench (1/2" drive), Permatex Ultra Grey synthetic high-temp grease, OTC piston spreader tool #7317
- Book time: 1.4 hr | Shop real time: 1.0 hr (Mike's pace)
- Safety hazards mentioned: hot rotor if vehicle was just driven; brake-dust inhalation; pinch point at caliper hang

**Output (full SOP, formatted as the skill produces):**

```
# SOP: Rear brake pad & rotor replacement — 2015-2020 F-150 (cable parking brake variant)
Applies to: 2015–2020 Ford F-150, regular cable parking brake (NOT EPB-equipped SuperCrew Limited)
Level: Level 1 tech (0–12 months)
Authored from walkthrough by: Mike H., 2026-04-27
Version: 1.0 | Last reviewed: 2026-04-27
⚠️ SME REVIEW REQUIRED BEFORE USE: No

## Section 1 — Overview
- Purpose: Replace rear pads and rotors on the cable-parking-brake variant of the 12th and 13th gen F-150 with QC and a clean test-drive.
- Book time: 1.4 hr | Shop time: 1.0 hr | Variance note: Mike runs 0.4 under book; new techs should plan to book.
- Prerequisites: Confirm cable parking brake (not EPB). EPB variants route to a different SOP.
- Safety hazards on this job: hot rotor if vehicle was just driven; brake-dust inhalation; pinch point at caliper hang.

## Section 2 — Tools, Parts, Consumables
### Tools
- Snap-On torque wrench, 1/2" drive (calibrated within 12 months — check sticker)
- OTC piston spreader tool #7317 (DO NOT use a C-clamp on this caliper — see Section 3 callout)
- 21mm socket (lug nuts), 18mm socket (caliper bracket), 13mm socket (caliper slide bolts)
- Wire brake-cleaner brush, brake parts cleaner spray
- Torque paint (yellow) for QC marking

### Parts (per vehicle)
- Rear pad set, OEM or shop-approved equivalent (verify part # against VIN)
- Rear rotor pair, OEM or shop-approved equivalent
- Caliper bracket bolts ×4 (TTY — replace, do not reuse; part # included in rotor box; verify)
- Pad clip kit (included in pad box; replace, do not reuse)

### Consumables
- Permatex Ultra Grey synthetic high-temp grease (NOT the purple silicone-only)
- Brake parts cleaner

## Section 3 — Procedure

### Phase A: Prep
1. Verify VIN against work order; verify cable parking brake (not EPB) by inspecting the rear caliper for an electric actuator. If EPB present, STOP and route to the EPB SOP.
2. Confirm correct pad and rotor part numbers against VIN before lifting.
   💡 Sidenote (Mike H.): "If you're holding the parts before you're holding the vehicle, you've already saved 10 minutes."
3. Lift vehicle; remove rear wheels.

### Phase B: Teardown
   ⚠️ SAFETY: Rotor may be hot if the vehicle was just driven. Touch-test before grabbing.
4. Remove caliper slide bolts (13mm) and hang caliper from frame with a wire — do not let it dangle on the brake hose.
   ⚠️ SAFETY: Pinch point — keep fingers clear of the caliper as it swings free.
5. Remove old pads and pad clips.
6. Remove caliper bracket bolts (18mm) and bracket. DO NOT reuse the bracket bolts (TTY — see Section 2).
7. Remove rotor.

### Phase C: Repair
8. Clean the hub face with a wire brush. Verify no rust ridge that will prevent the new rotor from seating flush.
9. Install new rotor.
10. Install caliper bracket with NEW TTY bolts.
   🔧 Torque: 184 ft-lb (per Motor 4M-2018-F150-RB and shop policy — confirmed by Mike H.)
   💡 Sidenote (Mike H.): "TTY means torque-to-yield. Reusing them once is how you lose a bracket on a customer's first hard stop."
11. Clean caliper slide pins. Inspect boots — replace caliper if torn. Pack BOTH slide pins with Permatex Ultra Grey.
   💡 Sidenote (Mike H.): "Half-greased pin sticks in 4 months. Customer's back, pads wore uneven. Pack both, every time."
12. Install new pad clips (do not reuse the old ones — they're in the pad box).
13. Install new pads.
14. Compress caliper piston with OTC #7317 spreader tool.
   ⚠️ SAFETY / DAMAGE: Do NOT use a C-clamp. C-clamp will overshoot and unseat the piston seal. Use the spreader.
15. Reinstall caliper over the new pads.
16. Install caliper slide bolts (13mm).
   🔧 Torque: 25 ft-lb (per Motor 4M-2018-F150-RB)

### Phase D: Reassembly
17. Reinstall wheels. Hand-snug lug nuts in star pattern.
18. Lower vehicle until tires just contact ground.
19. Torque lug nuts in three passes — snug, half-spec, full spec — in star pattern.
   🔧 Torque: 150 ft-lb (per Ford and shop policy — three-pass mandatory)
   💡 Sidenote (Mike H.): "Impact to spec warps the rotor in 2 months. Three passes, every time. Mark with yellow torque paint when done."

### Phase E: QC (see Section 4)
### Phase F: Cleanup & Documentation
20. Document old pad thickness measurement on RO. Document new rotor measurement (within spec). Note slide-pin condition.

## Section 4 — Quality Control Checkpoints
- [ ] Before work begins: VIN-confirmed cable PB variant (not EPB); correct pad/rotor part #
- [ ] Mid-procedure: caliper bracket bolts torqued to 184 ft-lb, marked with yellow torque paint
- [ ] End of procedure: lug nuts torqued in three passes to 150 ft-lb, all 8 marked with yellow torque paint
- [ ] Test drive: 5 min minimum, 3 stops from 25 mph escalating pressure on a quiet street. Listen for squeal (dust shield clearance), feel for pulse (rotor warp / hub-face contamination), confirm parking brake holds on a 5–10° grade.

## Section 5 — Common Mistakes (Mike H.'s list)
- **Mistake:** Reusing caliper bracket bolts.
  **Symptom:** Bracket loosens, customer reports rear-end clunk on hard stops.
  **Catch it by:** Verify new TTY bolts are in your hand before installing the bracket.

- **Mistake:** Half-greased slide pin.
  **Symptom:** Uneven pad wear in 3–4 months; customer back with squeal or pulsation.
  **Catch it by:** Both pins out, both pins cleaned, both pins greased — never one.

- **Mistake:** C-clamp on the piston.
  **Symptom:** Pedal goes to floor at first test-stop; piston seal compromised.
  **Catch it by:** Spreader tool is the only acceptable tool — verify before reaching for the toolbox.

- **Mistake:** Impact to spec on lug nuts.
  **Symptom:** Rotor warp at 1,500–3,000 mi; customer back with brake pulsation.
  **Catch it by:** Three-pass star pattern with calibrated torque wrench, paint-marked.

- **Mistake:** Skipping the dust-shield clearance check.
  **Symptom:** Persistent rear squeal after install.
  **Catch it by:** Spin the wheel by hand before lowering — listen for ring contact.

## Section 6 — Tech Sign-Off
Tech name: ___ Date: ___ Odometer in/out: ___/___
QC pass: [ ] Yes [ ] No — if No, note: ___
Customer-visible note (optional): ___
```

**Notes for the skill user:**
- The senior tech's voice is preserved in five sidenotes and the entire Common Mistakes section, attributed.
- Every torque spec carries a source citation (Motor 4M-2018-F150-RB or shop policy with the tech's name).
- The cable-PB-vs-EPB distinction is in the title, in Section 1, and as Step 1 — the prerequisite check that prevents the wrong SOP from being followed.
- No safety-content invention: only hot-rotor, brake-dust, and pinch-point hazards from Mike's walkthrough are included.
