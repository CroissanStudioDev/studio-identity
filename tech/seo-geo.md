# SEO & GEO

Rules for traditional search (Google, Yandex) **and** AI search engines (ChatGPT, Perplexity,
Claude, Gemini). GEO = Generative Engine Optimization.

## What moves the needle (Princeton research, 2024)

| Tactic | Visibility lift |
|--------|-----------------|
| Cite sources / add citations | **+40.4%** |
| Use concrete statistics | **+39.5%** |
| Quote experts directly | **+38.1%** |
| Improve readability (fluency) | **+35.2%** |
| Use technical terms appropriately | **+32.7%** |
| Authoritative tone with evidence | **+30.1%** |

**Keyword stuffing HURTS visibility.** Don't repeat the same phrase. Once is enough.

## File structure

```
app/
├── layout.tsx              # Global metadata + Organization + WebSite JSON-LD
├── page.tsx                # Per-page metadata
├── sitemap.ts              # Dynamic sitemap (include every page)
├── robots.ts               # Bot rules (allow GPTBot, PerplexityBot, ClaudeBot)
├── opengraph-image.tsx     # Dynamic OG (per route, unique)

components/seo/
└── schemas/                # One file per JSON-LD schema

public/
└── llms.txt                # Sitemap-equivalent for AI crawlers (2026 standard)
```

## JSON-LD schemas to ship

| Schema | Purpose |
|--------|---------|
| `Organization` | Company entity recognition |
| `WebSite` | Site metadata |
| `LocalBusiness` | Trust signals + local SEO |
| `HowTo` | Process steps → rich snippets |
| `Service` | Pricing/offerings discovery |
| `FAQPage` | Q&A → **+40% AI citation rate** |
| `SoftwareApplication` | Tools (e.g., `/brief`) |
| `BreadcrumbList` | On every non-home page |

Check the live versions in `croissan-landing/components/seo/schemas/`.

## `robots.ts` — explicitly allow AI bots

```ts
export default function robots(): MetadataRoute.Robots {
  return {
    rules: [
      { userAgent: "*", allow: "/", disallow: ["/api/", "/_next/", "/admin/"] },
      { userAgent: "GPTBot", allow: "/" },          // OpenAI
      { userAgent: "PerplexityBot", allow: "/" },   // Perplexity
      { userAgent: "ClaudeBot", allow: "/" },       // Anthropic
      { userAgent: "Google-Extended", allow: "/" }, // Gemini training
    ],
    sitemap: `${SITE_URL}/sitemap.xml`,
  };
}
```

## `llms.txt`

A 2026 emerging standard — a Markdown file at `/llms.txt` that lists key URLs for AI crawlers with
short descriptions. Treat it like a curated sitemap aimed at LLMs. Include the most important pages
plus key facts (what we do, where, how to contact).

## Meta description rules

- Length: **140–160 chars.** Anything longer gets truncated by Google; shorter wastes SERP space.
- Pack 3–5 GEO signals: statistics, named entities (clients), technical terms, timeline, authority.
- Sample (153 chars):
  > AI-студия из Иннополиса: 15+ проектов для МТС, Ростелекома, Яндекса. Внедряем ИИ-агенты,
  > RAG-системы и чат-боты под ключ за 2-4 недели. 3+ года на рынке.

## Single source of truth for facts

All numbers, names, and contacts live in `lib/seo/facts.ts`. **Never hardcode** «15+ проектов» in
a component. When the number changes, update once and watch it propagate to:
- Stats sections
- Meta descriptions
- JSON-LD schemas
- Sitemap
- `llms.txt`

See [`../brand/facts.md`](../brand/facts.md) for the canonical values.

## Pre-ship SEO checklist

- [ ] `metadata` export in every page with `description`, `openGraph`, `alternates.canonical`.
- [ ] Page added to `app/sitemap.ts`.
- [ ] Meta description is 140–160 chars and includes ≥3 GEO signals.
- [ ] If structural (about, services, etc.) → matching JSON-LD schema in `components/seo/schemas/`.
- [ ] If important → mentioned in `public/llms.txt`.
- [ ] One `<h1>`, hierarchy intact, named entities (МТС, Ростелеком, Яндекс) appear in body copy.
- [ ] Stats match across every consumer (sections, JSON-LD, llms.txt).
