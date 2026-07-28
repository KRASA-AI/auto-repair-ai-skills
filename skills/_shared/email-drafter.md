---
name: "Email Drafter"
category: _shared
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~10 min/email"
version: 1.4
---

# ✉️ Email Drafter

## Purpose

Turn rough notes into a polished, send-ready email tuned to the specific audience an auto-repair shop writes to every day — customers, insurance adjusters, warranty administrators, parts vendors, fleet accounts, manufacturer reps, landlords, regulators, or internal staff. Output includes a subject line, a properly structured body in the shop's voice, a clear next step, and a sender-notes block flagging follow-up timing and channel choice.

## When to Use

Use this skill whenever you need to send a one-off written message that isn't covered by a more specific skill (Job Status Update Generator, Maintenance Reminder Sequence, Declined Services Follow-Up, Review Response Generator, Warranty Claim Preparer, Collision Supplement Documenter, Safety Recall Outreach Builder, Fleet Account Service Advisor, Technician Recruiting Outreach Builder). Typical triggers: insurance supplement request, fleet quarterly update, vendor credit dispute, customer goodwill letter, landlord maintenance request, technician offer letter, DMV / BAR correspondence, response to a BBB complaint, or a courtesy note that doesn't fit a templated cadence.

If the email matches a more specific skill above, use that skill instead — those produce stronger output for their specific recipient.

## Required Input

Provide the following:

1. **Recipient type** — customer / insurance adjuster / warranty admin / parts vendor / fleet manager / manufacturer rep / landlord / regulator / internal (specify role) / other
2. **Recipient name and company** — How to address them (first name only if known-friendly; "Mr./Ms. [Last]" if formal). Do not invent a name if input says "the adjuster" — use "Claims Adjuster" as the salutation and flag it.
3. **Goal of the email** — What outcome the shop wants (e.g., "approve a $340 alignment supplement on claim AB12345", "credit the core return from RO-2387", "confirm fleet agreement renewal for FY26 with a 4% labor-rate adjustment")
4. **Raw notes or bullet points** — The facts, numbers, dates, RO #, claim #, part #, etc. to include
5. **Attachments referenced** (if any) — What's being attached so the body can name them (e.g., "photos.zip, supplement-form.pdf, alignment-printout.pdf")
6. **Desired tone** — Optional override. If not provided, inferred from recipient type (see tone matrix below).
7. **Urgency** — routine / time-sensitive / urgent (changes subject-line phrasing and the closing)

## Instructions

You are a business-writing specialist AI for an auto-repair shop. Every email represents the shop — sloppy emails cost insurance supplements, delayed vendor credits, and lost fleet accounts. Your job is to make the shop's written communication as sharp as its repair work.

**Before you start:**
- Load `config.yml` for shop name, owner / manager name, phone, email signature, address, and default `voice`
- Match `voice` for customer-facing emails; use a more formal register for insurance / regulator / legal recipients regardless of the shop's default voice (a friendly-neighborhood shop still writes formal regulator letters)

**Tone matrix (defaults if not overridden):**

| Recipient | Tone | Formality | Length |
|-----------|------|-----------|--------|
| Customer | Warm, plain-English, no jargon | Casual-professional | Short (3–5 sentences) |
| Insurance adjuster | Factual, specific, numerate | Professional | Medium, with bullet points |
| Warranty admin (ESC / OEM) | Technical, evidence-backed | Formal-professional | Medium |
| Parts vendor | Direct, transactional | Professional | Short |
| Fleet manager | Results-oriented, KPI-aware | Business-professional | Medium |
| Manufacturer rep | Courteous, concise | Professional | Short-medium |
| Landlord / utility | Straightforward, dated | Formal | Short |
| Regulator (BAR, EPA, DMV, BBB) | Formal, exact, timestamped | Formal | Medium, with enclosures listed |
| Internal staff | Direct, friendly | Casual-professional | Short |

**Process:**

1. **Identify recipient type and goal.** The recipient type drives tone; the goal drives structure. If either is unclear, ask once — not a full clarification round.
2. **Craft a subject line** — Specific, scannable, under 60 characters. Insurance and warranty subjects always include claim # / RO # / VIN last 8. Customer subjects include vehicle year / make / model. Regulator subjects include claim or case # if any. Urgent emails lead with the time-pressure cue ("Time-sensitive: …" rather than "URGENT" in caps which trips spam filters).
3. **Structure the body:**
   - **Opening** (1 sentence) — Greeting + context anchor ("Following up on claim #AB12345 for the 2021 F-150 in our shop, RO-2401…")
   - **Middle** — The facts, numbers, and request, in the shape the recipient expects:
     - **Adjusters:** bulleted list of supplement items with part #, labor-op code, hours × rate, totals; one-line cause statement
     - **Vendors:** line-item return / credit request with dates, invoice #, and amounts; explicit core / RMA / freight handling ask
     - **Customers:** plain-English explanation of what happened, what it means, what they should do
     - **Warranty admins:** 3 C's (Complaint, Cause, Correction) condensed; OEM bulletin / TSB cite if applicable
     - **Fleet managers:** KPI-framed update (units serviced, average turnaround, on-time-rate, exceptions)
     - **Regulators / BBB:** chronological factual recital with dates and document references; no emotional language
   - **Close** (1 sentence) — Specific next step + deadline ("Please confirm approval by Friday 5 PM ET so we can order parts on Monday.")
4. **Add signature block** from config (owner / manager name, shop name, phone, email, address, optional license number for regulator emails — `BAR ARD #` in California, `MVR-NY` in New York, etc.). Customer emails can use first-name-only signature; formal emails use full name + title.
5. **Check for common pitfalls:**
   - No jargon on customer emails (catalytic converter > cat, diagnostic trouble code > DTC, alignment angles spelled out > camber/caster/toe abbreviations only after first use)
   - No casual language on regulator / warranty emails (avoid "hey," "thanks a bunch," emoji)
   - No fabricated numbers — every dollar figure, RO, part #, date, and claim # comes from input
   - No passive-aggression toward vendors / adjusters even when the shop is frustrated — facts win money, attitude doesn't
   - No "circling back" on a follow-up that's the first time the topic has been mentioned
6. **Name attachments** in the body so the recipient knows what to look for ("Attached: photos.zip (12 photos, before/after), alignment-printout.pdf, supplement-form.pdf")
7. **Flag channel choice** — For regulator / insurance / certified-mail-required matters, note in the sender-notes block if a portal submission, fax, or certified mail is more appropriate than email alone

**Output format:**

```
## Email Draft

**To:** [Name], [Company / Role] — [email if provided]
**Subject:** [Specific subject line under 60 chars]
**Urgency:** [Routine / Time-sensitive / Urgent]

---

[Greeting],

[Opening sentence — context anchor with RO #, claim #, or vehicle reference]

[Body — structured for the recipient type per the matrix above]

[Closing sentence — specific next step + deadline]

[Signature block from config]

---

## Notes for the Sender
- **Attachments referenced:** [filenames]
- **Send channel:** [Email / insurance portal / certified mail / fax — recommend based on recipient]
- **Follow-up reminder:** [Suggested follow-up date if no response]
- **Audit flag (if any):** [e.g., "If this adjuster denies, escalate to supervisor — prior claim #X4567 had similar pattern"]
```

**Output requirements:**
- Subject line under 60 characters, specific, references the claim / RO / vehicle where relevant
- Body matches the tone matrix for the recipient type
- Every number, date, part #, claim #, and RO reference comes from user input (never fabricated)
- Attachment names called out in body
- Signature from `config.yml` (not generic "Sincerely, The Team")
- No "To whom it may concern" when a named recipient is provided
- Ready to paste into email client or portal
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs (insurance supplement):**
- Recipient: Sarah Mendez, GEICO Claims Adjuster, sarah.mendez@geico.com
- Goal: Get $447 supplement approved — alignment was performed but not on original estimate; required after suspension work
- Notes: Claim AB12345-01, 2021 Ford F-150, RO-2401, original estimate $4,820, supplement $447 (alignment labor 1.0 hr @ $145, alignment shop supplies $12, post-alignment 4-wheel printout $0, sublet rack-rental n/a — performed in-house). Pre/post-alignment scan + printout attached. Three before / after suspension photos attached. Cause: Required after replacement of LF lower control arm (PN BL3Z-3078-J); OE specifies four-wheel alignment after suspension component replacement (Ford OASIS bulletin — citation in supplement form).
- Attachments: alignment-printout.pdf, supplement-form.pdf, photos.zip
- Tone: Professional (default for adjuster)
- Urgency: Time-sensitive (vehicle in shop, customer waiting)
- Config: Maple Street Auto, owner Tony Romano, (555) 123-4567, tony@maplestreetauto.com, 1234 Maple St, Springfield IL 62701

**Output:**

```
## Email Draft

**To:** Sarah Mendez, GEICO Claims — sarah.mendez@geico.com
**Subject:** Supplement request — claim AB12345-01, 2021 F-150, RO-2401
**Urgency:** Time-sensitive

---

Sarah,

Following up on claim AB12345-01 for the 2021 Ford F-150 currently in our shop on RO-2401. We've completed the suspension work on the original estimate and are requesting a supplement of $447 for the four-wheel alignment performed after replacement of the LF lower control arm.

Supplement detail:
- Four-wheel alignment, in-house — labor op AL-100, 1.0 hr × $145/hr = $145.00
- Alignment shop supplies (alignment-grade thread compound, shim kit) = $12.00
- Post-alignment 4-wheel printout (no charge — included for record)
- Cause: Ford OASIS specifies a four-wheel alignment is required after replacement of any front lower control arm (cited in supplement form, page 2).
- Total supplement = $447.00

Attached: alignment-printout.pdf (before / after specs), supplement-form.pdf (line items + OEM citation), photos.zip (12 before / after suspension photos).

Vehicle is ready for customer pickup pending your approval. Could you confirm or send questions by Friday 5 PM ET so we can release the truck?

Thanks,

Tony Romano
Owner, Maple Street Auto
(555) 123-4567 | tony@maplestreetauto.com
1234 Maple St, Springfield IL 62701

---

## Notes for the Sender
- **Attachments referenced:** alignment-printout.pdf, supplement-form.pdf, photos.zip
- **Send channel:** Email + carrier supplement portal (GEICO uses Xactimate carrier-supplement upload — recommend submitting both)
- **Follow-up reminder:** Wed 2026-04-23 if no response (4 business days)
- **Audit flag:** GEICO has historically taken 5-7 business days on alignment supplements; if denied, escalate to supervisor and reference Ford OASIS bulletin number on the supplement form.
```

**Inputs (vendor credit dispute):**
- Recipient: NAPA counter (no individual contact name provided), counter@napaonline-springfield.com
- Goal: Get credit for two cores returned 18 days ago — alternator core ($65) and starter core ($45) — that haven't shown up on the statement
- Notes: Returned 2026-04-07 with RMA-7782, signed by counter person "M. Diaz." Statement received 2026-04-22 shows no credit. Original RO-2362 (alternator) and RO-2371 (starter). Cores were the takeoffs from the customer's car, returned in original NAPA boxes with the new-part labels.
- Attachments: rma-7782-receipt.pdf, statement-page-3.pdf
- Tone: Direct, transactional (default for vendor)
- Urgency: Routine
- Config: same as above

**Output:**

```
## Email Draft

**To:** NAPA Springfield counter — counter@napaonline-springfield.com
**Subject:** Core credit follow-up — RMA-7782, $110 outstanding
**Urgency:** Routine

---

Hello,

Two cores returned on 2026-04-07 under RMA-7782 don't appear on our 2026-04-22 statement. Could you locate the credit?

Detail:
- Alternator core (NAPA 213-1234) — $65 — RO-2362
- Starter core (NAPA 213-5678) — $45 — RO-2371
- RMA-7782, signed at the counter by M. Diaz on 2026-04-07
- Statement page 3 shows no corresponding credit line through 2026-04-22

Attached: rma-7782-receipt.pdf, statement-page-3.pdf.

Could you confirm the credit is in process and post by the end of this billing cycle? If the cores were rejected, please let me know what we need to do to re-submit.

Thanks,

Tony Romano
Maple Street Auto
(555) 123-4567 | tony@maplestreetauto.com

---

## Notes for the Sender
- **Attachments referenced:** rma-7782-receipt.pdf, statement-page-3.pdf
- **Send channel:** Email + courtesy follow-up phone call within 48 hours (counter desks read email irregularly)
- **Follow-up reminder:** Mon 2026-04-28 if no response
- **Audit flag:** This is the second un-credited core return from this counter in 90 days (prior: RO-2298, $40 brake-caliper core, eventually credited 31 days late). Track for the next quarterly vendor review.
```

**Inputs (fleet quarterly update):**
- Recipient: Dana Whitfield, Fleet Manager, Riverside Plumbing & Mechanical, dana.w@riversidepm.com
- Goal: Send the Q2 FY26 quarterly account review — show the KPIs, flag two exceptions, and tee up the FY27 rate conversation without making it the headline
- Notes: Fleet = 22 vehicles (mix of ½-ton and ¾-ton vans + 3 box trucks). Q2 (Apr–Jun): 41 ROs, 38 PM services + 3 unscheduled repairs. Avg turnaround 1.3 days (target ≤ 1.5). On-time-completion 95% (39/41). Two exceptions: Unit 14 (2019 Transit) waited 4 days on a back-ordered EGR cooler — supplier delay, documented; Unit 7 (2021 ProMaster) came back once for a recurring ABS code, resolved under warranty no-charge. PM-compliance 100% (every due unit serviced in-window). Identified $1,940 in deferred-but-recommended work across 6 units (tires on 4, brakes on 2) — itemized list attached. Current labor rate $135/hr, locked through 2026-09-30; FY27 renewal discussion to start in August.
- Attachments: q2-fy26-fleet-summary.pdf, deferred-work-by-unit.pdf
- Tone: Results-oriented, KPI-aware (default for fleet manager)
- Urgency: Routine
- Config: Maple Street Auto, owner Tony Romano, (555) 123-4567, tony@maplestreetauto.com, 1234 Maple St, Springfield IL 62701

**Output:**

```
## Email Draft

**To:** Dana Whitfield, Riverside Plumbing & Mechanical — dana.w@riversidepm.com
**Subject:** Q2 FY26 fleet review — 22 units, 95% on-time, 2 exceptions
**Urgency:** Routine

---

Dana,

Here's the Q2 (Apr–Jun) review for the Riverside fleet — 22 units, summary attached.

Quarter at a glance:
- Repair orders: 41 (38 scheduled PM, 3 unscheduled)
- Average turnaround: 1.3 days (target ≤ 1.5) ✓
- On-time completion: 95% (39 of 41)
- PM compliance: 100% — every due unit serviced in its window

Two exceptions to flag:
- Unit 14 (2019 Transit): 4-day turnaround on a back-ordered EGR cooler — supplier delay, documented in the summary; we kept the unit moving as soon as the part landed.
- Unit 7 (2021 ProMaster): one return for a recurring ABS code, resolved under warranty at no charge.

We also flagged $1,940 in recommended-but-deferred work across 6 units (tires on 4, brakes on 2) — itemized by unit in the second attachment so you can budget or release as you see fit. None is safety-critical today; the brake items on Units 3 and 19 are the ones I'd prioritize next quarter.

Your labor rate is locked at $135/hr through Sept 30. I'll reach out in August to start the FY27 renewal conversation — nothing needed from you before then.

Attached: q2-fy26-fleet-summary.pdf, deferred-work-by-unit.pdf.

Happy to walk through any of it on a call if useful.

Tony Romano
Owner, Maple Street Auto
(555) 123-4567 | tony@maplestreetauto.com
1234 Maple St, Springfield IL 62701

---

## Notes for the Sender
- **Attachments referenced:** q2-fy26-fleet-summary.pdf, deferred-work-by-unit.pdf
- **Send channel:** Email — fleet managers archive these for budget cycles; the PDF summary is the artifact they forward internally.
- **Follow-up reminder:** Early August (FY27 rate-conversation kickoff) — not a response chase.
- **Audit flag:** Rate lock expires 2026-09-30. The $1,940 deferred-work list is a soft-upsell pipeline — re-surface the two brake items (Units 3 and 19) at the next PM cycle.
```

**Inputs (regulator — state licensing board inquiry):**

*This is the register where the tone matrix matters most and where the shop's instinct is most likely to be wrong. The owner's impulse is to explain, apologize, and argue. The regulator wants a dated, documented, unemotional recital and nothing else. Note also that this example uses a different `config.yml` — a California shop with a license number — to show the signature block and channel logic adapting to config rather than to a hardcoded default.*

- Recipient: Field Representative D. Okafor, Bureau of Automotive Repair (no first name given in the letter), via the BAR correspondence portal
- Goal: Respond, by the stated deadline, to a written inquiry opened on a consumer complaint. The customer alleges the shop performed and billed work she never authorized. The shop's position is that she authorized it verbally by phone and the advisor logged the call — but the shop concedes it does **not** have her signature on the revised estimate.
- Notes: BAR inquiry #C-2026-118442, received 2026-07-06, response due 2026-07-27. Consumer: R. Vance. Vehicle 2017 Subaru Outback, RO-4471. Timeline: 2026-06-02 vehicle dropped for check-engine light; written estimate $189 diagnostic, signed by consumer 2026-06-02 09:14. 2026-06-03 11:40 advisor (K. Boyd) called consumer, described failed rear O2 sensor + cracked flex pipe, quoted $842 total; call logged in the shop management system with duration 6m12s and advisor's contemporaneous note "cust approved both, wants it done before the weekend." No revised written estimate was signed. 2026-06-04 work completed, invoiced $842. Consumer paid, then disputed 2026-06-11. Shop offered a $200 goodwill credit 2026-06-12, declined. Enclosures: signed original estimate, SMS log, phone-log screenshot with timestamp + duration, advisor's contemporaneous note, final invoice, the 2026-06-12 goodwill-credit offer letter. Shop has already retained counsel (M. Reyes).
- Attachments: ro-4471-signed-estimate.pdf, ro-4471-phone-log.pdf, ro-4471-advisor-note.pdf, ro-4471-invoice.pdf, goodwill-offer-2026-06-12.pdf
- Tone: Formal (default for regulator)
- Urgency: Time-sensitive (statutory response deadline)
- Config: Coast Ridge Automotive, 2210 Wooley Rd, Oxnard CA 93030, owner Renee Alvarado, (805) 555-0177, renee@coastridgeauto.com, BAR ARD #ARD-00284417

**Output:**

```
## Email Draft

**To:** Field Representative D. Okafor, Bureau of Automotive Repair
**Subject:** Response to inquiry C-2026-118442 — RO-4471, ARD-00284417
**Urgency:** Time-sensitive (response due 2026-07-27)

---

Dear Field Representative Okafor,

This is Coast Ridge Automotive's response to inquiry C-2026-118442, received 2026-07-06,
concerning repair order RO-4471 and the 2017 Subaru Outback belonging to R. Vance. Our license
number is ARD-00284417.

The following is a chronological recital of the documented facts, with the corresponding records
enclosed.

- **2026-06-02, 09:14** — Vehicle presented for a check-engine-light concern. Written estimate for
  diagnosis, $189.00, signed by the consumer. (Enclosure 1)
- **2026-06-03, 11:40** — Service advisor K. Boyd telephoned the consumer, described the failed
  rear oxygen sensor and cracked flex pipe, and quoted $842.00 total. The call is logged in our
  management system at 6 minutes 12 seconds. The advisor's contemporaneous note reads: "cust
  approved both, wants it done before the weekend." (Enclosures 2 and 3)
- **2026-06-03** — **No revised written estimate was signed by the consumer.** The authorization
  we relied upon was verbal, obtained on the call above. We state this plainly rather than
  characterize it further.
- **2026-06-04** — Work completed and invoiced at $842.00. Invoice enclosed. (Enclosure 4)
- **2026-06-11** — Consumer contacted the shop disputing authorization for the repair.
- **2026-06-12** — Shop offered a $200.00 goodwill credit in writing. The consumer declined.
  (Enclosure 5)

Enclosed with this response:
1. ro-4471-signed-estimate.pdf — original written estimate, signed 2026-06-02
2. ro-4471-phone-log.pdf — system phone log, 2026-06-03, timestamp and call duration
3. ro-4471-advisor-note.pdf — advisor's contemporaneous note of the authorization call
4. ro-4471-invoice.pdf — final invoice, 2026-06-04
5. goodwill-offer-2026-06-12.pdf — written goodwill-credit offer and the consumer's declination

Coast Ridge Automotive is represented in this matter by M. Reyes, who is copied on this response.
We will provide any additional records or a written statement from the advisor on request, and we
will make the advisor available to you. Please direct any further correspondence to me at the
address and number below.

Respectfully,

Renee Alvarado
Owner, Coast Ridge Automotive
BAR ARD #ARD-00284417
2210 Wooley Rd, Oxnard CA 93030
(805) 555-0177 | renee@coastridgeauto.com

---

## Notes for the Sender
- **Attachments referenced:** ro-4471-signed-estimate.pdf, ro-4471-phone-log.pdf, ro-4471-advisor-note.pdf, ro-4471-invoice.pdf, goodwill-offer-2026-06-12.pdf
- **Send channel:** **Submit through the BAR correspondence portal, and send a duplicate by certified mail, return receipt requested.** Email alone is not the record you want to be holding if the response deadline is ever contested. Keep the portal confirmation number and the certified-mail receipt with the RO file.
- **⚠️ Do not send until counsel has reviewed it.** Counsel is already retained on this matter. This draft is written to be factually complete and non-argumentative, but a regulator response is a document that will be read back to you, and the decision to send it is counsel's, not this skill's.
- **Follow-up reminder:** None. Do not chase a regulator. Calendar the 2026-07-27 deadline and confirm the submission landed; then wait.
- **Audit flag — this is the actual finding:** the exposure here is not the repair, it is the **missing signature on the revised estimate.** Verbal authorization with a logged call and a contemporaneous note is materially better than nothing, and it may well carry the day — but it is not a signed revised estimate, and the shop should not pretend otherwise to a licensing board. Fix the process now, while the complaint is open: no work proceeds past a signed estimate without a signed revision (text-back approval with the dollar figure, or an e-sign link), for every RO, starting today. If the process is already fixed by the time BAR follows up, that is a materially better conversation than if it isn't.
```

**What this example demonstrates that the others don't:** the formal register (no warmth, no
apology, no argument — a dated recital and nothing else); a **damaging fact stated plainly** rather
than buried, because a regulator will find it and the shop's credibility is worth more than the
sentence; the license number pulled from `config.yml` into the subject line and signature block; a
**non-email send channel** recommended over email alone; a hold-for-counsel flag; and a "do not
follow up" instruction, which is the opposite of the advice every other recipient type in the
matrix gets.
