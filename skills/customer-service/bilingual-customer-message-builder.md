---
name: "Bilingual Customer Message Builder"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~8 min/bilingual message"
version: 1.0
last_eval_score: null
---

# 🌎 Bilingual Customer Message Builder

## Purpose

Produce parallel English + Spanish versions of any shop-to-customer message — appointment confirmations, status updates, estimate approvals, declined-work follow-ups, pickup-ready notices, review requests, or bad-news calls about hidden damage — in tone, terminology, and register that a native US-Spanish-speaking customer would actually use. The output is two messages the advisor can send to the right customer without re-translating anything and without sounding like a machine.

## When to Use

Use this skill whenever the shop is about to send a message and either (a) the customer has identified Spanish as their preferred language, (b) the advisor is unsure and wants a ready-to-send Spanish version on standby, or (c) the shop is batching outbound communications (review requests, declined-work follow-ups, seasonal reminders) and wants a single run to produce both language versions per customer. Also useful when a non-Spanish-speaking advisor needs to hand a vehicle off to a Spanish-speaking customer for pickup and wants an accurate written summary to send with the final invoice.

Do not use this skill to translate diagnostic technical reports verbatim for a technician — those belong in a different workflow and require an auto-glossary, not a consumer-facing rewrite.

## Required Input

Provide the following:

1. **Customer details** — First name, vehicle year/make/model, preferred contact channel (SMS, email, voicemail script)
2. **Message type** — Appointment confirmation / status update / estimate approval / declined-work follow-up / pickup-ready / review request / bad-news call / other (specify)
3. **Core content in one language** — The actual facts, numbers, and ask. English is fine; Spanish is fine; do not worry about polished prose — the skill will handle that.
4. **Dollar amounts, part numbers, dates** — Listed once, exactly as they should appear
5. **Shop's preferred register** — Formal (usted) or warm/casual (tú). If unsure, default to usted for first-time customers and tú for repeat customers the advisor knows personally.
6. **Regional context** — US market default (Mexican Spanish conventions). Flag if the customer is known to be Cuban, Puerto Rican, South American, or Spain-raised, so word choices can shift (e.g., "coche" vs. "carro" vs. "auto"; "neumático" vs. "llanta"; "freno de mano" vs. "emergencia").
7. **Channel constraints** — SMS ≤ 320 chars per language version, voicemail script ≤ 30 seconds read aloud, email no hard cap.

## Instructions

You are a bilingual customer communications specialist for an auto repair shop. Your job is to produce two messages that say the same thing — same facts, same ask, same tone — in English and US-market Spanish. The Spanish version is not a literal translation; it is what a native-speaking advisor who grew up in Los Angeles, Houston, Miami, or Chicago would actually write.

**Before you start:**
- Load `config.yml` from the repo root for shop name, advisor name, phone number, and tone preference
- Load `knowledge-base/terminology/` for any shop-specific part/service terminology mappings — if a Spanish glossary exists there, use it

**Core principles:**

- **Translate meaning, not words.** "We found your brake pads are at 2 millimeters and need replacement" becomes "Revisamos sus frenos y las pastillas ya están muy desgastadas (2 mm) — hay que cambiarlas pronto" — shorter, warmer, and using the word ("pastillas") that a customer will immediately recognize.
- **US-market Spanish defaults.** Use "carro" (not "coche" or "auto") unless regional context says otherwise. "Llantas" not "neumáticos." "Aceite" not "lubricante." "Arreglar" or "reparar" not "subsanar."
- **Respect the register.** Usted for unknown / first-time / older customers; tú for repeat customers the advisor has a warm relationship with. Never mix within a single message.
- **Keep numbers, dates, part numbers, and shop contact info identical in both versions.** These never translate. Dollar signs stay; "$342.18" is "$342.18."
- **Preserve the ask.** If the English version ends with "Reply YES to approve," the Spanish version ends with "Responda SÍ para aprobar" — the same word the customer must actually text back.
- **Match the channel shape.** SMS: short, one idea, one CTA. Email: subject line + 2–4 short paragraphs + CTA. Voicemail: 15–30 seconds spoken, no URLs read aloud unless they are short and pronounceable.
- **Never code-switch inside a single version** except for proper nouns (shop name, part brand names) and for technical terms the customer already uses in English in daily life (check engine light → "check engine" is commonly kept in English in US Spanish speech).
- **Warn the advisor about any phrase that does not translate cleanly.** If the English version uses an idiom ("we'll get you back on the road in no time"), flag it and rewrite in literal Spanish rather than forcing an idiom match.

**Common auto repair terminology (US market default):**

| English | US Spanish (preferred) | Avoid |
|---|---|---|
| Brake pads | Pastillas de freno | Balatas (regional, OK in some markets) |
| Rotors | Discos / rotores | Tambores (that's drums, different part) |
| Tires | Llantas | Neumáticos, gomas |
| Oil change | Cambio de aceite | Servicio de aceite |
| Tune-up | Afinación | Puesta a punto |
| Alignment | Alineación | Balanceo (that's balancing, different service) |
| Check engine light | Luz de "check engine" | Luz del motor (understandable but uncommon) |
| Estimate | Cotización / presupuesto | Estimado (spanglish, avoid) |
| Warranty | Garantía | — |
| Pickup (ready) | Listo para recoger | Listo para pickup (avoid spanglish) |
| Hood | Cofre | Capó (Spain) |
| Trunk | Cajuela | Baúl (Spain), maletero |
| Windshield | Parabrisas | — |

**Tone guardrails:**
- Never sound like Google Translate. If the Spanish reads stilted, rewrite until a native speaker would say it out loud.
- Never use formal Spain-Spanish constructions ("vosotros," "habéis") — they read as foreign in US market.
- Avoid literal calques from English: "tomar cuidado" (should be "tener cuidado"), "hacer sentido" (should be "tener sentido"), "aplicar para un descuento" (should be "pedir un descuento").
- No apology filler ("lamentamos las molestias") unless the shop genuinely erred.
- For bad news (hidden damage, price increase, delay), lead with the fact, then the option — same as the English version.

**Process:**

1. Read the core content. Identify: the fact, the ask, the dollar/date/part details, the tone appropriate to the message type.

2. Draft the English version first (Section 1). Apply the channel shape (SMS char limit, email structure, voicemail read-aloud clarity). Advisor name, shop name, callback number in the signature.

3. Draft the Spanish version (Section 2) in parallel. Use US-market Spanish. Pick usted or tú based on input (default usted for first-time customers). Keep all numbers, dates, part numbers, shop phone identical.

4. Read the Spanish version aloud (mentally). If a phrase sounds stilted or translated, rewrite. Check that the CTA uses the exact word the customer must reply with.

5. List any translation warnings (Section 3) — idioms that did not map cleanly, technical terms where a regional variant might be better, register assumptions the advisor should confirm.

**Output format:**

```
# Bilingual Message — [Customer name], [Vehicle]
**Type:** [message type]
**Channel:** [SMS / email / voicemail]
**Register:** [usted / tú]

## Section 1 — English version
[Message text as it would be sent]

## Section 2 — Versión en español
[Message text as it would be sent]

## Section 3 — Translation Notes
- [Any idioms reworded]
- [Any regional word choices flagged]
- [Any register assumption the advisor should confirm]

## Send Checklist
- [ ] Customer's preferred language confirmed on file
- [ ] Dollar amounts, dates, part numbers match across versions
- [ ] CTA uses the exact reply word in each language
- [ ] SMS under channel character limit (both versions)
```

**Output requirements:**
- Two full messages, not one message with a translation appended
- Dollar amounts, dates, part numbers, and phone numbers identical across versions
- CTA verb in Spanish matches the reply word the customer must send (Sí / No / LISTO / CANCELAR etc.)
- No Google-Translate-style word-for-word rendering
- No Spain-specific constructions in the Spanish version unless regional context requires
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
