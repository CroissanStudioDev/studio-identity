# Content rules — hard

Hard rules for any user-facing copy: page text, CTAs, error messages, emails, deck slides, social
posts.

> **SoT split.** [`../brand/voice-and-tone.md`](../brand/voice-and-tone.md) is the
> **single source of truth for voice principles + examples**. This file is the
> **enforcement layer** — the locked rules an agent or reviewer should treat as P0.
> If the two ever drift, voice-and-tone.md wins; reconcile here, then update.

## Default language

- **Russian.** Unless the audience is explicitly English (international clients, English landing).

## Source of truth for facts

- Numbers, names, contacts, addresses → from the project's `lib/seo/facts.ts` (or its equivalent).
  **Never inline** «15+ проектов» or «Сергей Полин» in components or copy.
- Master values: [`../brand/facts.md`](../brand/facts.md).

## Voice

- Tone: caring, smart, slightly bold.
- Partner-not-vendor framing: «в партнёрстве с вами», not «для вас».
- Concrete numbers over fuzzy adjectives: `15+`, not «много».
- **Never blame the user** in error messages.

## CTA copy

- Action-oriented and friendly. «Написать нам», «Создать бриф», «Забронировать звонок».
- Forbidden: «Оставить заявку», «Заказать консультацию», «Получить КП».

## Forbidden phrases

| ❌ Don't write | ✅ Instead |
|---------------|-----------|
| «Революционные решения» | concrete benefit |
| «Комплексные услуги» | what you actually do |
| «Цифровая трансформация» | the specific outcome |
| «Профессиональная разработка» | shipped projects, named clients |
| «Уникальные технологии» | name the technology |

## Emojis

- **Never as icons.** Use Lucide SVG.
- In body copy: avoid. We use words to convey warmth, not emoji.

## Russian typography

- Em-dashes («—»), not hyphens, for parenthetical breaks.
- Russian quotes («…») in body copy. Straight quotes are fine in code/UI.
- Non-breaking spaces (`&nbsp;`) before short prepositions and standalone short words.

## SEO copy rules

- Meta descriptions: **140–160 chars**. Pack ≥3 GEO signals (statistics, named entities, technical
  terms, timeline).
- Don't repeat keywords (Princeton: keyword stuffing **hurts** AI visibility).
- Use technical terms (`ИИ-агент`, `RAG`, `LLM`) where appropriate — they signal expertise.

## Headlines

- Direct, specific, with personality.
- Use «мы» / «вы» to create connection.
- Soft imperatives are fine.
- Avoid corporate hedging («профессиональный», «качественный»).

## When unsure

- Read [`../brand/voice-and-tone.md`](../brand/voice-and-tone.md) examples.
- Compare to live copy in `croissan-landing/components/sections/`.
- Ask the user before shipping copy that doesn't match an existing pattern.
