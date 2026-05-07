# Company facts

Single source of truth for every number, name, and contact that appears in marketing copy,
JSON-LD schemas, metadata, `llms.txt`, and pitch decks. **Don't duplicate these values in components**
— import them from a shared `facts.ts` (see `croissan-landing/lib/seo/facts.ts` for the pattern).

When a number changes here, update every consumer.

---

## Identity

| Field | Value |
|-------|-------|
| Name (RU) | Круассан Студио |
| Name (EN) | Croissan Studio |
| Legal name | Круассан Студио |
| Founded | 2022 |
| URL | https://croissanstudio.ru |
| Email | hello@croissanstudio.ru |
| Phone | +7 999 562-42-59 |

## Address

```
ул. Университетская, 7, офис 325
Иннополис, Республика Татарстан, 420500
Россия
```

## Short description (RU)

> AI-студия полного цикла из Иннополиса. Внедряем ИИ под ключ за 2–4 недели.

## Marketing metrics

| Metric | Value | Display |
|--------|-------|---------|
| Shipped projects | 15 | `15+` |
| Top-tier clients | 6 | `6` |
| Years active | 3 | `3+` |
| Team size | 10 | `10` |

`valueLabel` is the human-readable form (`"15+"`); `value` is the numeric form for structured data.

## Top clients (in order of recognition)

1. МТС
2. Ростелеком
3. Яндекс
4. T1
5. Positive Technologies
6. Иннополис Университет

Logos live in [`../assets/client-logos/`](../assets/client-logos/).

## Founders

| Name | Role | Telegram |
|------|------|----------|
| Сергей Полин | CEO | [@vilfer](https://t.me/vilfer) |
| Никита Дроздов | COO | [@droz_nik](https://t.me/droz_nik) |
| Яков Сапаров | CTO | [@outrun32](https://t.me/outrun32) |
| Андрей Левада | CPO | [@andrewlevada](https://t.me/andrewlevada) |
| Элеонора Пикало | CMO | [@elpi_tg](https://t.me/elpi_tg) |

## Canonical home meta description (153 chars)

> AI-студия из Иннополиса: 15+ проектов для МТС, Ростелекома, Яндекса. Внедряем ИИ-агенты, RAG-системы и чат-боты под ключ за 2-4 недели. 3+ года на рынке.

Packs 5 GEO signals: statistics, named clients, technical terms, timeline, authority. Stay within
140–160 chars to avoid Google SERP truncation.

## What we sell

- **AI agents** — autonomous task-runners on top of LLMs.
- **RAG systems** — retrieval-augmented Q&A over private corpora.
- **Chatbots** — Telegram, web, voice.
- **AI features inside existing products** — recommendations, classification, generation.
- **Greenfield AI products** — end-to-end from idea to launch.

Default delivery window: **2–4 weeks**. Engagement model: **partner, not vendor**.
