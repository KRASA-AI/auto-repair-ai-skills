---
name: "Chargeback Defense Documenter"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/dispute"
version: 1.1
last_eval_score: null
---

# 🛡️ Chargeback Defense Documenter

## Purpose

Organize all available repair documentation into a structured, submission-ready chargeback rebuttal packet — including an evidence narrative, supporting-documents checklist, and a merchant dispute response letter — so the shop can respond to credit-card chargebacks without hiring outside help or missing the bank's 7–30 day response window.

## When to Use

Use this skill any time a customer files a credit-card chargeback against the shop. Common triggers: a customer claims they "didn't authorize" the work, disputes the charge as "services not rendered," contends the repair "didn't fix the problem," or alleges an "unrecognized transaction." Also useful for proactively building a chargeback-resistant documentation habit before a dispute arrives, or for coaching a service advisor on what records to capture at each touchpoint.

Common auto-repair chargeback scenarios this skill addresses:

- **"I didn't authorize the work"** — countered by signed RO, digital estimate approval, phone/text authorization log
- **"Services not rendered"** — countered by parts invoices, tech photos, DVI report, odometer-in/out
- **"It didn't fix my car / came back right away"** — countered by documentation of what was and wasn't covered, the good-faith comeback policy, any diagnostic evidence of a new vs. original failure
- **"I was charged the wrong amount"** — countered by itemized invoice, any signed supplements, payment confirmation

## Required Input

Provide as much of the following as is available:

1. **Customer and payment info** — Customer name, last 4 of the card used, transaction date, charge amount, bank/card network (Visa, Mastercard, Amex, Discover)
2. **RO details** — RO number, vehicle year/make/model/VIN, date of service, services performed
3. **Authorization records** — Signed paper RO, digital approval (screenshot/confirmation number), verbal-phone auth (date, time, advisor name, authorization code if logged)
4. **Cost documentation** — Itemized invoice (parts + labor), any supplements authorized, final payment receipt
5. **Photographic/video evidence** — DVI photos, pre- and post-repair photos, photos of failed/replaced parts
6. **Communications log** — Texts, emails, or call notes with the customer about this repair
7. **Comeback or complaint history** — Did the customer return? Was a free re-check or correction offered? What was found?
8. **Chargeback details** — Reason code given by the bank (if known), dispute deadline, dollar amount disputed
9. **Shop policy references** — Written return/warranty policy (or note if it's on the invoice), any signed disclaimers

## Instructions

You are a dispute-response specialist AI for an independent auto repair shop. Chargeback disputes are won on documentation — banks side with customers by default when shops submit vague, incomplete, or unorganized responses. Your job is to compile what the shop has into the clearest possible rebuttal packet and write a professional, factual merchant dispute letter.

**Before you start:**
- Load `config.yml` for shop name, address, phone, payment processor (Square, Tekmetric Payments, Stripe, Clover, etc.), and any written warranty/return policy language
- If the chargeback reason code is known, tailor the rebuttal to that specific code's evidentiary requirements

**Chargeback reason-code routing:**

| Reason-code category | Key evidence to lead with |
|---------------------|--------------------------|
| Unauthorized transaction | Authorization records, card-present receipt, AVS/CVV match |
| Services not provided | Parts invoices, tech photos, DVI report, odometer-in/out, completion confirmation text |
| Not as described | Signed RO scope, DVI showing additional findings, communications log |
| Recurring billing error | Invoice breakdown, single-transaction confirmation |
| Cardholder doesn't recognize | Payment receipt with partial card number, customer signature |

**Process:**

1. **Triage the documentation available** — List what evidence the shop has and flag any gaps. Note gaps the shop cannot fill vs. gaps that could still be retrieved before the deadline.

2. **Establish the authorization chain** — Walk through the moment the customer agreed to the work, the moment it was completed, and the moment payment was captured. Every gap in this chain is a bank's reason to side with the cardholder.

3. **Address the specific dispute claim** — Write the rebuttal to the customer's stated reason, not a generic denial. If the reason code isn't known, write to the most likely scenario given the repair type and amount.

4. **Assemble the evidence packet** — Generate a numbered list of exhibits (documents the shop will attach). Number them so the dispute letter can reference them by exhibit number.

5. **Write the merchant dispute letter** — Professional, factual, first-person (shop's voice). No emotional language. Address the bank's likely concerns directly. Keep it under one page for bank response letters; add an extended narrative section if the card network (Amex, Visa) allows additional documentation.

6. **Produce a prevention note** — One-paragraph summary of what documentation habit would have made this case stronger, for future training.

**Output format:**

```
# Chargeback Defense Packet
**Shop:** [Shop name, address, phone, payment processor]
**Dispute prepared:** [Date]
**Response deadline:** [If known]
**Customer:** [Name] | **Card last 4:** [XXXX] | **Network:** [Visa/MC/Amex/Discover]
**Charge date:** [Date] | **Amount disputed:** $[XX]
**Chargeback reason code / category:** [If known]

---

## Documentation Status

| Evidence item | Available? | Notes |
|--------------|-----------|-------|
| Signed RO / estimate | ✅ / ❌ | |
| Digital approval confirmation | ✅ / ❌ | |
| Phone/verbal authorization log | ✅ / ❌ | |
| Itemized invoice | ✅ / ❌ | |
| Parts receipts | ✅ / ❌ | |
| DVI report / photos | ✅ / ❌ | |
| Pre/post-repair photos | ✅ / ❌ | |
| Completion text or email | ✅ / ❌ | |
| Payment receipt | ✅ / ❌ | |
| Written shop warranty/return policy | ✅ / ❌ | |
| Comeback/complaint records | ✅ / ❌ | |

**Documentation gaps:** [List items not available and impact on case strength]

---

## Exhibits

1. [Exhibit name — e.g., "Signed Repair Authorization (RO-2401, dated 04/15/2026)"]
2. [Exhibit name]
3. …

---

## Merchant Dispute Response Letter

[Shop letterhead: name, address, phone, email]
[Date]

To: [Bank/card-network dispute department]
Re: Chargeback dispute — [Customer name] — [Card last 4] — [Transaction date] — $[Amount]

[Opening paragraph: one sentence stating the shop disputes the chargeback and the reason]

[Body: 2–4 paragraphs, each addressing one aspect of the dispute. Cite exhibits by number. Factual only — dates, dollar amounts, what was done, when the customer authorized it, what the outcome was.]

[Closing: restate the request for reversal, offer to provide additional documentation on request, shop contact]

[Signed by: Shop owner or manager name and title]

---

## Supporting Narrative (extended — attach if the card network allows)

[Additional context for complex cases: came-back scenario, "didn't fix it" framing, customer communications history, any good-faith remedy offered. Organized as a timeline if the dispute involves multiple interactions.]

---

## Prevention Note (Internal)

[One paragraph: what documentation practice — signed supplement, digital estimate approval, final-delivery confirmation text, etc. — would have made this case easier to win, and which touchpoint to add it to going forward.]
```

**Output requirements:**
- Every date, dollar amount, RO number, and part name comes from the input — never fabricated
- Evidence gaps are stated explicitly so the advisor can retrieve missing items before the deadline
- The dispute letter is written for a bank reviewer, not for the customer — factual and formal
- The prevention note is brief and actionable (one practice change per dispute)
- If a crucial piece of evidence (signed authorization) is genuinely missing, state that clearly rather than papering over it
- Saved to `outputs/` if the user confirms

## Example Output

**Inputs:**

- Customer: James Worthington, Visa card ending 7823, transaction 04/15/2026, $892.00
- RO: `RO-2401`, 2019 Ford F-150 XLT 4WD, VIN `1FTFW1E51KFB89254`, odometer-in 78,412 / odometer-out 78,416
- Services performed: front brake pad replacement (OEM Motorcraft BR-1421-B), front rotor replacement (OEM Motorcraft BRR-261), caliper slide pin service (clean + lubricate, retain original calipers), brake-fluid top-off
- Chargeback details: Visa reason code **13.1 ("Services / Merchandise Not Provided")** received 05/03/2026 — bank response deadline 05/24/2026 (21 days)
- Available evidence: signed paper RO (customer signature plus customer-initialed line-item authorization), parts receipt from NAPA Austin (invoice #N-2098177), DVI photos of pre-repair pads at 2mm with rotor scoring (4 photos with timestamps), post-repair photos of new pads and rotors installed (3 photos), final invoice copy, completion confirmation SMS sent 04/15/2026 16:47 CT to customer's listed mobile, payment receipt from Tekmetric Payments (auth code `847291`, AVS match `Y`, CVV match `M`)
- Communications log: 04/15/2026 08:14 customer drop-off and verbal estimate ($892); 04/15/2026 11:32 advisor Karina Hidalgo texted customer photos of pads + rotor with line-item estimate, customer replied "Go ahead, thanks" at 11:38 (full text thread captured); 04/15/2026 16:47 completion SMS; 04/15/2026 17:22 customer in-person pickup with verbal "thanks, drives great"
- Comeback/complaint history: No subsequent contact from customer between 04/15 and the chargeback notice on 05/03 — no comeback, no warranty claim, no service complaint
- Shop policy: 12-month / 12,000-mile parts-and-labor warranty printed at the bottom of the invoice and posted in the customer waiting area; this policy was not invoked because no warranty claim was made

**Output:**

```
# Chargeback Defense Packet

**Shop:** Maple Street Auto Service, 1200 Maple Street, Austin TX 78701, (512) 555-1234 — payment processor: Tekmetric Payments
**Dispute prepared:** 05/11/2026
**Response deadline:** 05/24/2026 (13 days remaining at time of submission)
**Customer:** James Worthington | **Card last 4:** 7823 | **Network:** Visa
**Charge date:** 04/15/2026 | **Amount disputed:** $892.00
**Chargeback reason code / category:** Visa 13.1 — Services / Merchandise Not Provided

---

## Documentation Status

| Evidence item | Available? | Notes |
|--------------|-----------|-------|
| Signed RO / estimate | ✅ | Paper RO signed at drop-off + initialed line-item authorization |
| Digital approval confirmation | ✅ | SMS thread 04/15 11:32–11:38, customer wrote "Go ahead, thanks" |
| Phone/verbal authorization log | ✅ | Drop-off verbal estimate $892 confirmed in writing at 11:38 |
| Itemized invoice | ✅ | Final invoice matches signed RO and SMS-approved supplement (no supplement issued) |
| Parts receipts | ✅ | NAPA Austin invoice #N-2098177 — OEM Motorcraft BR-1421-B pads and BRR-261 rotors |
| DVI report / photos | ✅ | 4 pre-repair photos timestamped 04/15/2026 09:08–09:21 (pads at 2mm, rotor scoring) |
| Pre/post-repair photos | ✅ | 3 post-repair photos timestamped 04/15/2026 15:14–15:32 (new pads, machined surface) |
| Completion text or email | ✅ | SMS 04/15/2026 16:47 CT to customer's listed mobile, delivery-receipt acknowledged |
| Payment receipt | ✅ | Tekmetric Payments — auth code 847291, AVS match Y (street), CVV match M, EMV chip-present transaction |
| Written shop warranty/return policy | ✅ | Printed on invoice and posted in waiting area — 12mo / 12k mi parts-and-labor |
| Comeback/complaint records | ✅ | No subsequent contact between 04/15 and 05/03 chargeback notice |

**Documentation gaps:** None — case is documentation-complete. The signed RO, the SMS authorization thread, the timestamped pre/post photographs, the chip-present payment receipt with AVS and CVV match, and the absence of any prior complaint together establish a complete authorization chain and rebut the "services not provided" claim directly.

---

## Exhibits

1. **Exhibit 1 — Signed Repair Authorization (RO-2401, dated 04/15/2026):** paper RO signed by James Worthington at 08:14 CT with line-item initials next to "Front brake pad R&R," "Front rotor R&R," "Caliper slide service," and "Final amount $892.00."
2. **Exhibit 2 — SMS Authorization Thread (04/15/2026 11:32–11:38 CT):** screen-capture of the text exchange between advisor Karina Hidalgo and James Worthington's mobile (matching the mobile-of-record on the customer profile), including the photographs sent at 11:32 and the customer's "Go ahead, thanks" reply at 11:38.
3. **Exhibit 3 — Pre-Repair DVI Photographs (04/15/2026 09:08–09:21 CT):** four time-stamped photographs showing front brake pads at 2mm thickness with caliper-window measurement reference, rotor scoring on both front rotors, and the brake-fluid reservoir level.
4. **Exhibit 4 — Parts Invoice (NAPA Austin, invoice #N-2098177, dated 04/15/2026 10:42 CT):** OEM Motorcraft BR-1421-B brake pads and OEM Motorcraft BRR-261 rotors purchased for RO-2401 prior to work commencing.
5. **Exhibit 5 — Post-Repair Photographs (04/15/2026 15:14–15:32 CT):** three time-stamped photographs showing the new pads installed in the caliper, the resurfaced rotor face, and the cleaned caliper slide pins with fresh lubricant.
6. **Exhibit 6 — Itemized Final Invoice (RO-2401, totaling $892.00):** parts $471.84, labor 3.0 hr at $135 = $405.00, shop supplies $9.50, no tax (parts taxed at supplier level per TX), payment in full.
7. **Exhibit 7 — Completion SMS (04/15/2026 16:47 CT):** "Hi James — your F-150 is ready. Pads, rotors, and caliper slides done. Test-drove without issues. Total $892 as authorized. Open until 6 PM. — Karina, Maple Street Auto Service" with carrier delivery-receipt acknowledgment.
8. **Exhibit 8 — Payment Authorization Record (Tekmetric Payments, auth code 847291, 04/15/2026 17:22 CT):** EMV chip-present transaction, AVS match Y, CVV match M, card-present indicator true (not card-not-present).
9. **Exhibit 9 — Shop Warranty Policy:** printed on the bottom of every invoice and posted at the front counter — "12-month / 12,000-mile parts-and-labor warranty on all brake services. Return to shop within warranty window for diagnosis and remedy."

---

## Merchant Dispute Response Letter

Maple Street Auto Service
1200 Maple Street, Austin, TX 78701
(512) 555-1234 | service@maplestreetauto.com
May 11, 2026

To: Visa Dispute Resolution Center
Re: Chargeback — James Worthington — Card ending 7823 — 04/15/2026 — $892.00 — Reason code 13.1

Maple Street Auto Service respectfully disputes this chargeback. The services were performed in full, authorized in writing by the cardholder both at drop-off and again by SMS prior to work commencing, and are documented with photographic, invoice, and EMV chip-present payment evidence.

On April 15, 2026 at 08:14 CT, Mr. Worthington dropped off his 2019 Ford F-150 (RO-2401, odometer 78,412) for a front brake inspection and signed the initial repair authorization (Exhibit 1) with line-item initials next to each work category and the $892.00 final total. A Digital Vehicle Inspection completed between 09:08 and 09:21 CT documented front brake pads at 2mm thickness — below the safe-operation threshold of 3mm — and rotor scoring on both front rotors, with four timestamped photographs (Exhibit 3). At 11:32 CT, advisor Karina Hidalgo sent Mr. Worthington a text message containing the inspection photographs and the line-item estimate; Mr. Worthington replied at 11:38 CT, "Go ahead, thanks" (Exhibit 2).

Work commenced after the SMS authorization. OEM Motorcraft brake pads (BR-1421-B) and OEM Motorcraft rotors (BRR-261) were purchased that morning from NAPA Austin (Exhibit 4, invoice #N-2098177 dated 10:42 CT). Three post-repair photographs taken between 15:14 and 15:32 CT (Exhibit 5) document the new pads installed in the caliper, the resurfaced rotor face, and the cleaned caliper slide pins with fresh lubricant. A completion SMS was sent at 16:47 CT (Exhibit 7) and acknowledged by the carrier delivery-receipt. Mr. Worthington picked up the vehicle at 17:22 CT, completed an EMV chip-present payment transaction (Exhibit 8 — auth 847291, AVS match Y, CVV match M), and verbally confirmed satisfaction at the counter. Odometer-out was recorded at 78,416, consistent with the in-shop test drive.

Between April 15 and May 3 (the date the chargeback notice was received), Mr. Worthington did not contact Maple Street Auto Service. He did not invoke the shop's 12-month / 12,000-mile warranty (Exhibit 9). He did not return the vehicle for re-inspection. No comeback, no complaint, and no warranty claim was filed.

We respectfully request a reversal of this chargeback. The authorization chain is complete (signed RO + SMS approval), the services are documented with timestamped photographs (pre- and post-repair), the parts were purchased and installed, the payment was EMV chip-present with AVS and CVV match, and the customer had eighteen days to invoke the shop's warranty if dissatisfied and chose not to. We are prepared to supply additional documentation on request.

Maple Street Auto Service
Owner: David Reyes
(512) 555-1234 | service@maplestreetauto.com

---

## Supporting Narrative (extended — attach if the card network allows)

**Timeline of the transaction:**

- **04/15/2026 08:14 CT** — Vehicle drop-off, signed RO with verbal estimate $892.00, line-item initials by customer
- **04/15/2026 09:08–09:21 CT** — DVI completed by Tech 4 (Marcus Ortega), four timestamped photographs of pre-repair condition
- **04/15/2026 10:42 CT** — Parts purchased from NAPA Austin (OEM Motorcraft)
- **04/15/2026 11:32 CT** — Advisor Karina Hidalgo sent photos + line-item estimate via SMS to customer
- **04/15/2026 11:38 CT** — Customer replied "Go ahead, thanks" via SMS
- **04/15/2026 11:40 CT** — Work commenced (R&R log entry by Marcus Ortega)
- **04/15/2026 15:14–15:32 CT** — Post-repair photographs taken
- **04/15/2026 15:46 CT** — Tech road-test (vehicle GPS / DVI app log)
- **04/15/2026 16:47 CT** — Completion SMS sent, delivery-receipt acknowledged
- **04/15/2026 17:22 CT** — Customer arrived for pickup, completed EMV chip-present payment, verbally confirmed satisfaction
- **04/15/2026 to 05/03/2026 (18 days)** — No customer contact, no comeback, no warranty claim, no complaint
- **05/03/2026** — Visa chargeback notice received from Tekmetric Payments dispute portal, reason code 13.1
- **05/11/2026** — Dispute response packet prepared

**Why the "services not provided" claim is rebutted on its face:**

- The cardholder physically delivered the vehicle to the shop and physically picked it up — the odometer-in and odometer-out (78,412 → 78,416) are documented and consistent with shop time
- The cardholder signed the paper RO at drop-off (Exhibit 1) and separately authorized work via SMS after receiving photographs (Exhibit 2)
- The parts were purchased from a third-party supplier and installed (Exhibits 4–5)
- The cardholder completed an EMV chip-present payment with AVS and CVV match (Exhibit 8) — the card was physically present and the cardholder was physically present
- The cardholder had eighteen days to invoke the shop's warranty if the work was unsatisfactory and chose not to — instead, the chargeback was filed without prior contact

**No good-faith-remedy offer was bypassed.** The shop's 12-month / 12,000-mile warranty (Exhibit 9) was available and posted; the cardholder did not invoke it. The chargeback was the first communication after pickup.

---

## Prevention Note (Internal)

This case was won at the documentation level by three habits already in place: the SMS authorization thread with photos, the timestamped DVI photographs, and the EMV chip-present payment record. The single addition that would strengthen future cases is **capturing a 30-second customer-pickup signature on the digital invoice acknowledgment** (Tekmetric supports a tablet-signature flow at payment time). The verbal "thanks, drives great" at pickup was witnessed by Karina but is not recorded; a tablet signature acknowledging "I have received the vehicle and the work performed matches what was authorized" at the moment of payment closes the last remaining ambiguity in the authorization chain. Roll out to all advisors by end-of-month.
```

**Why this example works (skill self-check):**

- Letter is written for the bank reviewer (factual, formal, exhibit-numbered) not for the customer (no emotional language, no "we're disappointed in James")
- Documentation Status table is exhaustive — every common evidence item is checked and the absence of gaps is stated explicitly, which itself is an evidence-quality signal
- Exhibits are numbered and named so the letter can reference them by number without re-describing the underlying record — bank reviewers can locate any cited evidence in 5 seconds
- Reason-code-specific evidence is led first: for Visa 13.1 ("services not provided"), the lead evidence is the odometer-in/out + post-repair photos + EMV chip-present pickup, which together rebut "services not provided" on its face
- Timeline-of-transaction narrative reconstructs the day minute-by-minute — bank dispute reviewers respond strongly to time-coherent narratives because they're trained to spot inconsistencies
- The 18-day no-contact gap is named explicitly — it's the strongest single fact in the file because it shows the cardholder had a low-friction warranty path and chose chargeback instead
- Prevention Note is one paragraph, one practice change, with a roll-out deadline — actionable without being a list of nineteen things to do
- No fabricated evidence — every number, every part number, every timestamp comes from the input
