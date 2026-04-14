---
name: "Maintenance Reminder Sequence"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~5 min/batch"
version: 1.1
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

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
