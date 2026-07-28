---
name: "Emissions Service-Info & Tool Access Request Documenter"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min per request + escalation packet, if needed"
version: 1.0
last_eval_score: null
---

# 🔓 Emissions Service-Info & Tool Access Request Documenter

## Purpose

When a manufacturer, dealer, or OEM support line won't hand over the **emissions-related service information, diagnostic tool access, training material, or reprogramming capability** a shop needs to diagnose or repair a vehicle — most often a DEF (Diesel Exhaust Fluid) fault, an emissions-control code, or a reflash the shop can't get without dealer-level access — this skill builds the paper trail to get it. It drafts the initial written request citing the shop's actual legal footing, and, if that request is ignored or refused, escalates it into a documented case: a follow-up demand, a National Automotive Service Task Force (NASTF) Service Information Request (SIR), and, if that still doesn't resolve it, a final escalation note for the owner and counsel.

This is a **request-and-escalation packet builder, not a legal opinion and not a guarantee of access.** It gets the shop's ask in writing, on the record, citing the right federal guidance, in a form a manufacturer's service-information department or NASTF can act on quickly — instead of a frustrated phone call that leaves no trail when the shop needs to escalate.

## When to Use

Use this skill when:

- A technician hits a wall on an emissions-related repair — most commonly a DEF/SCR system fault, an emissions-control DTC, or an emissions-related reflash/reprogram — because the shop can't get the service information, diagnostic tool, training material, or software the repair requires.
- The manufacturer's dealer network or support line has declined, delayed, or ignored a request for that information or tool.
- The shop wants to make its **first** request the right way — citing the actual current federal basis — instead of waiting for a denial to escalate.
- A previous informal request (phone call, email to a rep) went nowhere and the shop needs a documented, escalatable record.
- The shop needs to explain to a customer why a repair is taking longer than expected because a manufacturer hasn't provided a needed tool or procedure.

**Do not use this skill for:** general mechanical/body repair information outside the emissions system (that's a broader right-to-repair landscape this skill does not cover — see Scope below), OEM position-statement lookups for ADAS/structural work (see `operations/adas-calibration-documenter.md`), or warranty reimbursement (see `admin/warranty-claim-preparer.md`).

## ⚠️ Scope & Legal Disclaimer

**This skill covers emissions-related service information and tools specifically** — the category EPA's guidance and the Clean Air Act (CAA) actually reach. It does **not** establish, and must never claim, a general right to all mechanical repair data; that broader question is still working through Congress (the REPAIR Act / SAFE Repair Act / Motor Vehicle Modernization Act) and is unresolved as of this writing. Conflating the two is the single biggest way this skill could mislead a shop, so the AI must never do it.

- **Ground every request in what is actually confirmed, and flag what isn't.** As of July 1, 2026, EPA issued guidance — following a Presidential Memorandum, "Lowering the Cost of Living by Promoting the Freedom to Fix" — affirming that under the Clean Air Act, manufacturers of light-, medium-, and heavy-duty vehicles must provide independent shops and vehicle owners the **same emissions-related service information, diagnostic tools, training materials, and reprogramming capability** they give their own branded dealers, on reasonable terms. This explicitly includes DEF and other emissions-control systems. It explicitly does **not** extend to proprietary designs, software code, or other confidential/IP-protected manufacturer material. This is new executive-branch guidance, not new legislation — it clarifies EPA's reading of existing law, and guidance can be revised. Treat the exact letter/citation language as something to confirm against the shop's own printed copy of the July 1, 2026 guidance before quoting it to a manufacturer, not something this skill quotes verbatim.
- **Never assert a specific statute section, CFR citation, penalty, or deadline as settled fact.** If the shop or manufacturer needs the precise citation, flag it as "pull the exact citation from the guidance document / confirm with counsel" rather than inventing one.
- **Generic-parts note, stated accurately:** the guidance confirms manufacturers cannot require branded parts for emissions-system repairs and generic/equivalent parts may be used — but it does **not** guarantee warranty coverage if the customer's vehicle is still under a manufacturer warranty and a noncertified part is used. Say this plainly to the shop; don't oversell it to the customer.
- **Never guarantee an outcome.** This skill produces a well-documented request and escalation path. It cannot promise the manufacturer will comply on any particular timeline, and it must never tell the shop "you are legally entitled to this, full stop" — it says what the current federal guidance affirms, cites it accurately, and lets the manufacturer, NASTF, or counsel resolve any dispute.
- **NASTF process details are treated as background, not asserted fact.** NASTF (a nonprofit, industry-run body) operates a Service Information Request (SIR) process and a Dispute Resolution Panel for exactly this kind of access dispute, and EPA's July 2026 announcement referenced NASTF as a model for industry collaboration. Specific figures about NASTF's request volume or resolution rate are industry-reported, not verified by this skill — flag them as "confirm NASTF's current process and expected timeline" rather than quoting a number to the manufacturer.

## Required Input

Provide the following:

1. **What's blocked** — the specific service information, diagnostic tool, training material, or reprogramming capability the shop needs and can't get (e.g., "SCR/DEF dosing-module reflash procedure and access," "emissions-control module pinout and calibration ID list," "factory scan-tool bidirectional access to run a forced regen").
2. **Vehicle** — year/make/model, VIN, engine, and whether it's light-, medium-, or heavy-duty (the guidance covers all three, but say which).
3. **The repair it's blocking** — what the tech is trying to diagnose or fix, and why the missing info/tool is the specific obstacle (not solvable with a generic scan tool or aftermarket procedure).
4. **What's been tried so far** — nothing yet / informal call or email to a dealer or manufacturer rep / a formal written request already sent and ignored or refused. If something was already sent, include the date, channel, and any response received (or "no response").
5. **Manufacturer / contact** — the OEM's service-information department if known, or the dealer/rep the shop has been dealing with.
6. **Shop info** — for the request letterhead: shop name, address, phone, and the requester's name/title.
7. **Urgency** — is a customer's vehicle sitting on this right now (state the impact — loaner cost, missed pickup date), or is this a standing capability gap the shop wants resolved before it comes up again.

## Instructions

You are drafting a documented request-and-escalation packet for an independent shop that has been unable to get emissions-related service information or tools from a vehicle manufacturer.

**Before you start:**
- Load `config.yml` for shop name, address, phone, and the requester's default title.
- Load `knowledge-base/regulations/` for any captured notes on the EPA Freedom to Fix guidance or related right-to-repair tracking — treat it as background to confirm, not as the source of truth; this skill's own Scope section above is the current baseline.
- Confirm the request is actually **emissions-related** (DEF/SCR, emissions-control DTCs, emissions-system reprogramming, OBD/emissions diagnostic access). If the technician's ask is broader — general mechanical repair data unrelated to emissions — say so plainly: this skill's federal grounding doesn't reach that request, and the packet should be scoped down to the emissions-specific piece, with the rest flagged as outside current federal guidance.

**Process:**

1. **Classify the stage.** Is this a first request, a follow-up after a prior request was ignored, or an escalation after an explicit refusal? Each gets a different packet.
2. **Draft Stage 1 — the written request** (use even if a prior informal ask was made, so there's finally a dated, citable record): identifies the shop and vehicle, states exactly what's needed and why it's covered under the July 2026 EPA guidance, cites the guidance by name and date (not by inventing a section number), and asks for a response by a specific reasonable date the shop sets (this skill does not assert a legally required response window — the shop picks a business-reasonable date, e.g., 10 business days, and says so).
3. **If Stage 1 was already sent and ignored/refused, draft Stage 2 — the NASTF Service Information Request.** Restates the request in NASTF's terms, attaches/references the Stage 1 request and any manufacturer response (or lack of one), and asks NASTF to engage the manufacturer.
4. **If NASTF engagement doesn't resolve it, draft Stage 3 — the escalation note for the owner and counsel**, not a customer-facing document: what was requested, what was tried, what NASTF's Dispute Resolution Panel path looks like next, and what the customer-facing impact has been (vehicle downtime, cost) in case the shop wants to pursue a complaint with EPA or consult counsel.
5. **Keep a running documentation log** — every contact, date, channel, and response (or non-response) — because the value of this packet compounds; a manufacturer or NASTF panel responds differently to "I called once" than to "here is the dated record of three attempts."
6. **Flag anything the shop should confirm before sending** — the manufacturer's actual service-information department contact (if not supplied), the current NASTF SIR submission process, and the accurate citation for the July 2026 guidance pulled from the shop's own copy.

**Output format:**

```
# Emissions Service-Info Access Request — [Vehicle] — [Date]

## Request Summary
- **Vehicle:** [Year/Make/Model, VIN, engine, duty class]
- **What's needed:** [specific info/tool/training/reprogramming access]
- **Blocking:** [the repair this is preventing, and current status — e.g., vehicle on-site since X]
- **Stage:** [1 — First Request / 2 — NASTF SIR / 3 — Escalation Note]

## Regulatory Basis (cite-or-flag)
[States what's confirmed: EPA guidance dated July 1, 2026, issued pursuant to the Presidential Memorandum "Lowering the Cost of Living by Promoting the Freedom to Fix," affirming manufacturers of light/medium/heavy-duty vehicles must provide independent shops the same emissions-related service info/tools/training/reprogramming they give their own dealers, including DEF systems, on reasonable terms — excluding proprietary software/IP. Flags: exact citation language to be pulled from the shop's own copy of the guidance before it's quoted to the manufacturer.]

## Stage 1 — Written Request to Manufacturer
[Full letter/email text: shop letterhead info, vehicle detail, specific ask, citation to the guidance, requested response date, shop contact]

## Stage 2 — NASTF Service Information Request (if applicable)
[Only included if Stage 1 was sent and unresolved. Restates the request in NASTF's terms, references the Stage 1 request and manufacturer response/non-response, asks NASTF to engage.]

## Stage 3 — Escalation Note for Owner & Counsel (if applicable)
[Internal only. Summary of what was requested, tried, and unresolved; the Dispute Resolution Panel path; customer-facing cost/downtime impact; explicit statement that this is a decision point for the owner, not a legal opinion.]

## Documentation Log
| Date | Channel | Contact | Content | Response |
|------|---------|---------|---------|----------|
| [date] | [call/email/portal] | [name] | [what was asked] | [what came back, or "none as of [date]"] |

## Flags to Confirm Before Sending
[Manufacturer's actual service-info department contact if not supplied; current NASTF SIR submission process; exact guidance citation pulled from the shop's own copy; anything from the Required Input that was missing]
```

**Output requirements:**
- Every vehicle detail (VIN, engine, duty class) is exactly as provided — never fabricated.
- The regulatory-basis section never invents a statute section, CFR citation, or deadline — it cites the guidance by name and date and flags the rest for confirmation.
- Stage 2 and Stage 3 are included only when the input indicates the prior stage was actually attempted and unresolved — never generate an escalation for a request that hasn't been tried yet.
- The Stage 3 escalation note is explicitly internal (owner/counsel), never phrased as something to hand a customer.
- If a required input is missing, list it under "Flags to Confirm Before Sending" rather than guessing.
- Saved to `outputs/` if the user confirms.

## Example Output

**Inputs:**

- What's blocked: Bidirectional scan-tool access and the current DPF/SCR forced-regeneration procedure — the shop's aftermarket tool can read codes but can't command a forced regen, and the printed service literature the shop has is out of date for this model year.
- Vehicle: 2023 Freightliner Cascadia, VIN `3AKJHHDR8PSFR4471`, DD13 engine, Class 8 heavy-duty
- Repair it's blocking: Truck derated and in limp mode on a stored SCR-efficiency code (P20EE); tech has isolated it to a DEF-quality/dosing issue via manual data but cannot complete the repair verification without running a forced regen and clearing the derate through the dealer-level procedure
- What's been tried: Shop called Freightliner's dealer service-info line on 2026-07-14, was told to "bring it to a dealer"; no written response to a follow-up voicemail left 2026-07-16
- Manufacturer/contact: Daimler Truck North America (Freightliner) — shop does not have a direct service-information department contact, only the general dealer line
- Shop info: Ridgeline Fleet Service, 4410 Depot Road, Elkhart, IN 46514, (574) 555-0198, requester Marcus Webb, Shop Foreman
- Urgency: Customer's truck (regional fleet, owner-operator) has been down since 2026-07-13 — four days lost revenue, currently on a loaner arrangement the customer is unhappy about

**Output:**

```
# Emissions Service-Info Access Request — 2023 Freightliner Cascadia (DD13) — 2026-07-18

## Request Summary
- **Vehicle:** 2023 Freightliner Cascadia, VIN 3AKJHHDR8PSFR4471, DD13 engine, Class 8 heavy-duty
- **What's needed:** Bidirectional scan-tool access to command a forced DPF/SCR regeneration, and the current dealer-level procedure to clear the active derate/limp-mode condition tied to stored code P20EE (SCR NOx-conversion efficiency below threshold)
- **Blocking:** Truck has been down at Ridgeline Fleet Service since 2026-07-13. Manual diagnostics (DEF quality test, dosing-module wiring/pressure checks) point to a DEF-quality/dosing fault; the shop can complete the repair but cannot verify it or clear the derate without dealer-level bidirectional access to run the forced regen and reset procedure. Four days downtime and counting on a regional-fleet customer's primary truck.
- **Stage:** 1 — First Written Request (a phone call on 2026-07-14 and a follow-up voicemail on 2026-07-16 went unanswered — see Documentation Log; this is the first *written*, dated request)

## Regulatory Basis (cite-or-flag)
On July 1, 2026, EPA issued guidance — pursuant to the Presidential Memorandum "Lowering the Cost of Living by Promoting the Freedom to Fix" — affirming that under the Clean Air Act, manufacturers of light-, medium-, and heavy-duty vehicles must provide independent repair shops and vehicle owners the same emissions-related service information, diagnostic tools, training materials, and reprogramming capability they provide their own branded dealers, on reasonable terms — explicitly including Diesel Exhaust Fluid (DEF) and other emissions-control systems. The guidance also clarifies that a temporary override of an emissions control system for the purpose of completing a repair is permitted under existing law. It does not extend to Daimler's proprietary software code or other confidential design information. **Flag: pull the exact citation language from Ridgeline's own printed copy of the July 1, 2026 EPA guidance (available via epa.gov) before quoting it verbatim in the final letter — this summary is accurate to the public EPA announcement but is not a substitute for citing the primary document directly.**

## Stage 1 — Written Request to Manufacturer

To: Daimler Truck North America — Service Information Department (contact to be confirmed — see Flags below; sent via the dealer service-info line pending a direct contact)
From: Marcus Webb, Shop Foreman, Ridgeline Fleet Service, 4410 Depot Road, Elkhart, IN 46514, (574) 555-0198
Date: July 18, 2026
Re: Emissions service-information and tool-access request — 2023 Freightliner Cascadia, VIN 3AKJHHDR8PSFR4471

Ridgeline Fleet Service is an independent commercial repair facility currently servicing a customer's 2023 Freightliner Cascadia (VIN 3AKJHHDR8PSFR4471, DD13 engine) that has been in limp-mode/derate since July 13, 2026 on stored code P20EE (SCR NOx-conversion efficiency below threshold). Our diagnosis indicates a DEF-quality/dosing-module fault, which we are equipped to repair. To verify the repair and clear the active derate, we need:

1. Bidirectional scan-tool access sufficient to command a forced DPF/SCR regeneration on this vehicle, and
2. The current dealer-level procedure for clearing the P20EE-associated derate/limp-mode condition following repair.

We understand that under EPA's July 1, 2026 guidance affirming the "Freedom to Fix" for emissions-related service information under the Clean Air Act, manufacturers are expected to make this category of emissions service information and tool access available to independent repair facilities on the same terms provided to franchised dealers. We are not requesting any proprietary software code or confidential design information — only the emissions-service access and procedure described above.

We attempted to reach Daimler Truck's service-information line by phone on July 14, 2026, and left a follow-up voicemail on July 16, 2026; we have not received a response as of this letter. Given the vehicle has now been down for five days with a fleet customer waiting, we're asking for a response by **July 25, 2026** (one week), and would appreciate knowing the fastest path to the access described above — direct tool access, a dealer referral for this specific procedure only, or another resolution path Daimler Truck can offer.

Please contact me directly at (574) 555-0198 or [shop email] to discuss.

Marcus Webb
Shop Foreman, Ridgeline Fleet Service

## Documentation Log

| Date | Channel | Contact | Content | Response |
|------|---------|---------|---------|----------|
| 2026-07-14 | Phone | Freightliner dealer service-info line | Requested bidirectional access / forced-regen procedure for VIN ...R4471 | Told to "bring it to a dealer"; no ticket number or contact given |
| 2026-07-16 | Voicemail | Same line, follow-up | Restated request, asked for a callback | No response as of 2026-07-18 |
| 2026-07-18 | Written letter (this document) | Daimler Truck NA Service Information Dept. (via dealer line pending direct contact) | Formal written request, cites July 2026 EPA guidance, requests response by 2026-07-25 | Pending |

## Flags to Confirm Before Sending

- **No direct Daimler Truck service-information department contact on file.** Confirm the correct email/portal for commercial-vehicle service-information requests (check Daimler Truck's dealer/service-info site or ask NASTF for the current contact) rather than routing only through the general dealer phone line again.
- **Exact EPA guidance citation:** this packet describes the July 1, 2026 guidance accurately based on the public EPA announcement, but pull the shop's own copy from epa.gov/ve-certification/freedom-fix and cite it directly in the final letter rather than relying on this summary.
- **If no response by 2026-07-25:** this packet is ready to convert to a Stage 2 NASTF Service Information Request — confirm NASTF's current SIR submission process (nastf.org) before filing, since this skill does not verify NASTF's process details in real time.
- **Customer communication:** the customer has not been told about this specific escalation step yet — consider looping them in on the timeline once a response deadline is set, so the four-plus days of downtime has a next step attached to it.
```

**Why this example works (skill self-check):**

- The regulatory basis is stated accurately to what EPA's public announcement actually says — scope (light/medium/heavy-duty, emissions-related info/tools/training/reprogramming, DEF explicitly included, proprietary software explicitly excluded) — and it flags the exact citation as something to pull from the primary document rather than asserting invented section numbers.
- The request is scoped tightly to the emissions-specific access that's actually blocking the repair (forced-regen access + derate-clearing procedure) rather than a vague "give us everything" ask that would be easy for a manufacturer to deflect.
- The documentation log turns two ignored informal contacts into a dated record — the exact thing a manufacturer's service-info department, or a NASTF panel, needs to see to treat the request as a real, escalating case rather than a first-time question.
- The letter sets its own reasonable response date rather than asserting a legally mandated deadline that isn't confirmed.
- The Flags section is honest about what the skill doesn't know (the correct department contact, NASTF's current process) instead of inventing a contact or a process step to make the packet look more complete than the input supports.
- The next step (Stage 2 NASTF SIR) is pre-staged but not written yet — it only gets drafted once the Stage 1 deadline actually passes unanswered, keeping the escalation honest to what's actually happened.

## Related Skills

- Distinct from `admin/warranty-claim-preparer.md` (that's a reimbursement claim after a covered repair is done; this is an access request that has to succeed *before* certain emissions repairs can be completed or verified).
- Distinct from `operations/adas-calibration-documenter.md` and `operations/adas-disclosure-authorization-builder.md` (those cover ADAS/structural OEM position statements and customer disclosure, not emissions-system data access).
- If the blocked repair isn't emissions-related, this skill's regulatory grounding doesn't apply — flag that to the shop rather than stretching the citation to cover it.
