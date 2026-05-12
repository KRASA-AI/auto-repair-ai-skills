---
name: "Chargeback Defense Documenter"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/dispute"
version: 1.0
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
- Customer: James Worthington, Visa card ending 7823, transaction 04/15/2026, $892
- RO: RO-2401, 2019 Ford F-150, front brake pads + rotors + caliper slide service
- Chargeback claim: "Services not rendered"
- Available: signed RO scan (customer signature), parts receipt, DVI photos of worn pads (pre-repair), invoice, completion text

**Output (partial — letter section):**

```
## Merchant Dispute Response Letter

Maple Street Auto Service
1200 Maple Street, Austin, TX 78701
(512) 555-1234 | service@maplestreetauto.com
May 11, 2026

To: Visa Dispute Resolution Center
Re: Chargeback — James Worthington — Card ending 7823 — 04/15/2026 — $892.00

Maple Street Auto Service respectfully disputes this chargeback. The services were performed in full, authorized in writing by the cardholder prior to work, and documented with photographic and invoice evidence.

On April 15, 2026, Mr. Worthington dropped off his 2019 Ford F-150 (RO-2401) for a front brake inspection. A Digital Vehicle Inspection (Exhibit 3) documented front brake pads at 2mm (below safe threshold of 3mm) and rotor scoring, with photographs. Mr. Worthington reviewed and signed the repair authorization (Exhibit 1) for front brake pads, rotors, and caliper slide service at $892 before any work commenced. Work was completed the same day. A completion confirmation text was sent at 4:47 PM (Exhibit 5), and Mr. Worthington picked up the vehicle.

Parts invoices (Exhibit 4) confirm all components were purchased and installed. Photographs taken before and after the repair (Exhibits 3–4) document the condition of the removed pads and rotors and the completed installation.

We respectfully request a reversal of this chargeback and are prepared to supply additional documentation on request.

Maple Street Auto Service
Owner: David Reyes
```
