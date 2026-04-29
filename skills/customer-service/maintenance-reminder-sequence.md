---
name: "Maintenance Reminder Sequence"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~5 min/batch"
version: 1.2
---

# 📧 Maintenance Reminder Sequence

## Purpose

Generate a personalized, multi-touch reminder sequence (initial, follow-up, final) for scheduled maintenance — based on standard mileage intervals, seasonal services, and customer's last visit — ready to deploy via SMS, email, or both.

## When to Use

Use this skill to create maintenance reminder campaigns for customers. Common triggers: proactive retention (remind customers about upcoming oil changes before they go elsewhere), batch-generate reminders for entire customer database, create templates for new shop management system, or generate a sequence for a specific customer based on their service history.

## Required Input

Provide the following:

1. **Customer information** — First name, last name, phone number (if SMS), email (if email)
2. **Vehicle information** — Year, make, model, current estimated mileage
3. **Last service record** — Last service date, last recorded mileage (or date vehicle was in shop)
4. **Services due (if known)** — Specific services needed (e.g., oil change, brake inspection, timing belt at 105k) or let the skill generate based on mileage
5. **Message format(s)** — SMS only, email only, or both (SMS first, email follow-up)
6. **Personalization preference** — Generic vs. detailed (generic is faster to batch-generate)

## Instructions

You are a customer retention specialist AI for auto repair shops. Your job is to create friendly, helpful reminders that get customers back to the shop at the right time for scheduled maintenance.

**Before you start:**
- Load `config.yml` from the repo root for shop name, phone, email, and communication tone
- Use the company's voice from `config.yml` → `voice`
- Reference `knowledge-base/terminology/` for correct service interval terminology

**Standard Mileage Service Intervals:**
- **3,000 miles** — Oil change (traditional)
- **5,000-7,500 miles** — Oil change (synthetic), rotate tires
- **15,000-20,000 miles** — Replace cabin air filter, inspect brakes and rotors
- **30,000 miles** — Transmission fluid inspection, coolant inspection, replace engine air filter
- **60,000 miles** — Transmission fluid change (if not sealed), coolant flush, inspect suspension
- **90,000-105,000 miles** — Replace timing belt (if applicable), inspect water pump, transmission fluid service
- **100,000+ miles** — Full fluid flush (brake, power steering), comprehensive inspection

**Process:**

1. **Calculate services due based on current mileage:**
   - Determine next 2-3 major services from current mileage
   - Use standard intervals above as baseline
   - Check for vehicle-specific intervals (some Hondas have CVT services at 30k, some trucks differ)
   - Add seasonal recommendations (winter prep in fall, AC service in spring)
2. **Map customer's vehicle to maintenance schedule** — Consider:
   - Age and estimated mileage (newer cars may use synthetic intervals)
   - Known high-mileage vehicles (more frequent fluid changes recommended)
   - Make/model-specific service notes (Toyota timing belts, Subaru head gaskets, etc.)
3. **Generate multi-touch sequence:**
   - **Message 0 (Post-service kickoff — optional)** — Send within 24–48 hours of pickup if the visit just completed. Sets the next-due milestone in the customer's mind, attaches it to the work just done, and dramatically lifts re-engagement on the eventual reminder. Do not include a CTA — this is an anchor, not a sell.
   - **Message 1 (Initial)** — Friendly reminder, no pressure (send when service is 500-1000 miles away or due soon)
   - **Message 2 (Follow-up)** — If no response, remind again with a small incentive or urgency (2 weeks after Message 1)
   - **Message 3 (Final)** — Last reminder before extended interval (if needed; 4 weeks after Message 1)
4. **Personalize with customer details:**
   - Use customer first name
   - Reference their specific vehicle (2019 Honda Civic, blue, etc.)
   - Reference last visit date ("We last serviced your vehicle 6 months ago")
   - Calculate estimated current mileage based on typical driving (10k-12k miles per year)
5. **Add seasonal considerations:**
   - Winter prep (October-November): cabin filter, battery check, tire rotation
   - Summer check (April-May): AC service, cooling system check, tire rotation
   - Spring/fall: fluid inspections, seasonal weather readiness
6. **Set clear next steps** — Include call-to-action, phone number, online booking link (if available)

**Output format (per customer):**

```
# Maintenance Reminder Sequence
**Customer:** [First Name] [Last Name]
**Vehicle:** [Year Make Model, Color]
**Last Service:** [Date], [Mileage] miles
**Estimated Current Mileage:** [Calculated mileage]
**Date Generated:** [Today]

## Services Due (Recommended in order)
1. **Oil Change + Tire Rotation** — Next due at [mileage estimate] miles (~[X weeks])
   - Estimated cost: $[range]
2. **Brake Inspection + Air Filter Replacement** — Due at [mileage estimate] miles
3. **Transmission Fluid Inspection** — Recommended at [mileage estimate] miles

## Message 1: Initial Reminder (Send Now)
**Format:** SMS + Email
**Tone:** Friendly, helpful, no pressure

### SMS (under 160 characters):
"Hi [Name]! Your [Year Make] is due for maintenance soon. Let's keep it running smooth. Call [Phone] or book online: [Link]"

### Email:
Subject: [First Name], Your [Vehicle] Maintenance is Due Soon

Hi [First Name],

Hope your [Vehicle] is running great! Based on your last visit on [Date], it's time for scheduled maintenance to keep everything in top shape.

**Recommended Services:**
- Oil change & tire rotation
- [Other service]

We can get you in this week. Call us at [Phone] or book your appointment online: [Link]

Thanks,
[Shop Name] Team

---

## Message 2: Follow-Up Reminder (Send in 2 weeks if no response)
**Format:** SMS or Email
**Tone:** Friendly reminder with small incentive

### SMS:
"Hi [Name]! Just reminding you about that maintenance appointment for your [Vehicle]. Schedule now and mention code SAVE10 for $10 off. [Phone] or [Link]"

### Email:
Subject: [Name], Don't Miss Your $10 Maintenance Special

Hi [Name],

Just a friendly follow-up — your [Vehicle] is ready for its regular maintenance, and we have an opening this week!

**Quick Reminder of Services:**
- Oil & filter change
- Tire rotation
- [System check]

Use code **SAVE10** for $10 off. Call [Phone] or book online: [Link]

Thanks,
[Shop Name] Team

---

## Message 3: Final Reminder (Send in 4 weeks if still no response)
**Format:** Email (less intrusive after 2 missed SMS)
**Tone:** Professional, last chance

### Email:
Subject: [Name], Your [Vehicle] Maintenance Reminder — Don't Wait Too Long

Hi [First Name],

This is our final reminder that your [Vehicle] is now overdue for maintenance. Regular service intervals keep your vehicle safe and reliable.

**Services Needed:**
- Oil and filter change
- Tire rotation
- Safety inspection

We're here to help. Call us today at [Phone] or book online: [Link]

Thanks,
[Shop Name] Team

---

## Batch Deployment Notes
- Use placeholders for batch templates: {{customer_name}}, {{vehicle}}, {{last_service_date}}, {{service_list}}, {{phone}}, {{booking_link}}
- Import into SMS/email system on [date]
- Track open rates and response rates to measure campaign effectiveness
- Follow up with non-responders in 6 weeks with different messaging ("We miss you!")
```

**Output requirements:**
- Multi-touch sequence (3 messages minimum) with clear send dates
- Specific services listed with estimated costs and timeframes
- Messages are personalized with customer/vehicle names (not generic)
- Clear call-to-action with phone number or booking link
- SMS messages under 160 characters (fits in one text)
- Emails are scannable with short paragraphs and bullet points
- Ready to import into shop management system or email campaign tool
- Includes batch deployment guidance if generating templates
- Saved to `outputs/` if the user confirms

## Example Output

**Input:**
- Customer: Karen Brooks, (612) 555-0177, karen.b@email.com
- Vehicle: 2019 Subaru Outback Limited, Quartz Blue Pearl
- Last service: 2025-11-04 at 58,420 mi (full synthetic oil change + tire rotation + 60k inspection findings: cabin air filter replaced, brake measurements 8/9/8/8 mm)
- Estimated current mileage: ~64,500 mi (assuming ~12k mi/yr Minneapolis commuter)
- Services due: oil + rotation due (synthetic interval, 65k); state safety inspection sticker expires 2026-09-30; transmission CVT fluid service due at 60k (CARRIED OVER — declined at last visit)
- Format: SMS-first, email follow-up
- Personalization: detailed (returning customer, full service history)
- Voice config: friendly
- Shop: North Loop Auto, (612) 555-0140, https://book.northloopauto.com
- Advisor: Brendan; Owner sign-off: Jess

**Output:**

```
# Maintenance Reminder Sequence — Karen Brooks
**Vehicle:** 2019 Subaru Outback Limited (Quartz Blue Pearl)
**Last Service:** 2025-11-04, 58,420 mi (full synthetic + rotation + cabin filter)
**Estimated Current Mileage:** ~64,500 mi (as of 2026-04-28)
**Date Generated:** 2026-04-28
**Sequence:** 4 touches (post-service kickoff already sent 2025-11-05; reminders due now)

## Services Due (in order)

1. **Synthetic oil change + tire rotation** — Due now (~65k window, 500 mi away)
   - Estimated cost: $89–$109 (full synthetic 0W-20, OEM Subaru filter)
2. **CVT fluid service (CARRIED OVER from last visit — was declined)** — Due now
   - Estimated cost: $245–$285 (Subaru CVT-FG fluid, drain & fill ×2 per Subaru TSB 16-03-15)
   - Note: Subaru OE recommendation, not generic — the customer asked about this last visit
3. **MN state safety inspection** — Sticker expires 2026-09-30 (~5 mo out — flag for late-summer reminder)
4. **Brake re-measurement** — 8/9/8/8 mm at last visit; track next visit, no action this cycle

## Message 0: Post-Service Kickoff (Sent 2025-11-05 — for reference; do NOT resend)
**Format:** SMS, sent 24 hr after pickup
**Tone:** Acknowledge + anchor next-due milestone

### SMS:
"Hi Karen — Brendan at North Loop Auto. Thanks for trusting us with the Outback yesterday — fresh oil, rotation, and cabin filter are good for ~5,000 mi. We'll reach out around 64,000–65,000 mi for the next round. Drive safe! — Brendan"

[148 / 160 chars — single SMS, no CTA, anchors the next-due number in the customer's head]

---

## Message 1: Initial Reminder (Send today, 2026-04-28)
**Format:** SMS first, email backup if no response in 7 days
**Tone:** Friendly, helpful, no pressure

### SMS (160 chars):
"Hi Karen! Your Outback is coming up on its 65k oil + rotation, and we've got the CVT fluid service we talked about last time too. Want to grab a slot this week? Reply YES or book at book.northloopauto.com. — Brendan, North Loop Auto"

[Char count: 235 — splits to 2 SMS on most carriers, acceptable for a returning customer; if shop wants single-SMS, drop "we've got the CVT fluid service we talked about last time too" — but then lose the carryover anchor]

### Email (sent if no SMS reply in 7 days):
**Subject:** Karen, the Outback is due — and your CVT service from last visit

Hi Karen,

Hope the Outback's been treating you well since November. You're coming up on around 65,000 miles, which means a couple of things are due:

- **Synthetic oil + tire rotation** ($89–109) — your standard 5,000-mile interval
- **CVT fluid service** ($245–285) — this is the one you asked about last visit and we agreed to revisit at 65k. Subaru's TSB 16-03-15 calls for a drain-and-refill (×2) to keep the transmission's protection where Subaru wants it. If you'd rather defer again, no pressure — we'll just note it on the file.

We have openings this Thursday morning and Friday afternoon. Reply with a time that works, call **(612) 555-0140**, or book online: **https://book.northloopauto.com**

Thanks,
Brendan
North Loop Auto

P.S. Your state safety sticker is good through September — we'll flag it again in late summer, no action needed today.

---

## Message 2: Follow-Up Reminder (Send 2 weeks after Message 1 if no response)
**Format:** SMS only (single touch, light)
**Tone:** Easy out — keep the door open without pressure

### SMS (160 chars):
"Hi Karen — checking in on the Outback. Still happy to fit the 65k service whenever it works. Reply when you'd like to grab a slot, or text NO if you'd rather we wait. — Brendan"

[178 chars — single follow-up, "NO" exit valve respects the relationship]

---

## Message 3: Final Reminder (Send 4 weeks after Message 1 if still no response)
**Format:** Email (less intrusive after 2 SMS)
**Tone:** Useful, not pushy — pivot to "we're here when you're ready"

### Email:
**Subject:** Karen, just keeping the file open

Hi Karen,

Quick last note — we haven't heard back, and that's totally fine. The Outback is still due for its 65k service whenever your schedule allows, and the CVT fluid service is still on the list when you're ready.

If anything has changed (different shop, sold the car, just busy), reply and we'll update the file. Otherwise, we'll be here when you're ready.

Thanks for being a customer.

Brendan
North Loop Auto
(612) 555-0140

— Jess Patel, Owner

---

## Batch Deployment Notes

- **Send via:** SMS through shop's communication platform (Tekmetric Messages, Shop-Ware Messaging, AutoLeap SMS, Podium, Kenect, or Mechanic Advisor); email through Mailchimp or shop's CRM email module
- **TCPA compliance:** Customer must have opted-in to SMS at intake. Include "STOP to opt out" on Message 1; do not include on Messages 2–3 (already established consent on Message 1; STOP is stored at the carrier level)
- **Track:** SMS delivery, SMS reply, email open, email click-through on the booking link, in-shop appointment created
- **Do NOT send Message 0 to customers who are NOT returning customers** — it requires a recent visit to anchor against. For new customers, start at Message 1
- **CARRIED-OVER work flag:** When a customer declined a recommendation last visit, the reminder MUST surface that specific item by name (here, the CVT fluid service). Generic "we've got services due" loses the trust-built specificity of the prior conversation
- **Outputs file:** Save to `outputs/maintenance-reminders/karen-brooks-2026-04-28.md` for advisor reference + audit trail
- **Hand-off if customer replies with a complaint or question about prior work:** route to `service-advisor-script.md` (live conversation) and the original RO from 2025-11-04
- **Hand-off if customer asks for the carried-over service to be priced firmly:** route to `repair-estimate-builder.md` with verified findings from the prior DVI

## Send Checklist
- [x] Customer's preferred contact channel confirmed (SMS primary per intake)
- [x] Vehicle name correct (2019 Outback — not pluralized, not abbreviated to "Sub")
- [x] Carried-over work surfaced explicitly (CVT fluid)
- [x] Mileage estimate is reasonable (~12k mi/yr Minneapolis commuter pattern)
- [x] Phone, booking link, advisor name, and owner sign-off identical across all touches
- [x] No promotional code on Message 1 (it's a returning customer with carried-over work — discount would cheapen the trust-anchor; reserve incentives for re-activation campaigns)
- [x] Message 2 has a "NO" exit valve to respect the relationship
- [x] Message 3 ends with the owner's name (accountability)
- [x] State safety sticker flagged for late-summer follow-up (do not nag this cycle)
```
