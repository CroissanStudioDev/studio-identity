# Sections and layout

## Section skeleton

Every page section follows this shape:

```tsx
<section className="py-16 md:py-32">
  <div className="mx-auto max-w-7xl px-6">
    {/* Section heading */}
    <div className="mx-auto mb-6 max-w-2xl px-2 md:mb-24 md:text-center">
      <h2 className="font-semibold text-3xl tracking-tight md:text-5xl">
        Заголовок
      </h2>
    </div>

    {/* Content */}
  </div>
</section>
```

## Spacing & widths

| What | Mobile | Desktop |
|------|--------|---------|
| Vertical padding | `py-16` | `md:py-32` |
| Horizontal padding | `px-6` (or `px-8` on hero) | — |
| Container | `max-w-7xl mx-auto` | — |
| Text column | `max-w-2xl` (sections) · `max-w-[680px]` (hero) | — |

`max-w-7xl` = 80rem = 1280px. This is the canonical content column width across the site. Don't widen
the column unless the content genuinely needs it (e.g., a wide chart).

## Hero

```tsx
<section className="flex min-h-screen flex-col justify-center py-16">
  <div className="mx-auto flex max-w-7xl flex-1 flex-col justify-center px-8 py-16 md:p-16">
    <div className="mx-auto max-w-[680px] space-y-8 md:text-center">
      {/* H1, lead paragraph, CTAs */}
    </div>
  </div>
</section>
```

- `min-h-screen` — hero owns the first viewport.
- `space-y-8` between blocks (heading, lead, CTA row).
- CTAs: column on mobile (`flex-col`), row on `sm:` and up.

## Page-level structure

```
app/
├── layout.tsx              # Fonts, analytics, navbar/footer, Org+WebSite JSON-LD
├── page.tsx                # Home — page-specific JSON-LD here
├── about/                  # AboutPage + Breadcrumb JSON-LD
├── brief/                  # SoftwareApplication + Breadcrumb JSON-LD
├── api/                    # POST endpoints (route handlers)
├── error.tsx               # Route-level error boundary
├── global-error.tsx        # Root-level error boundary
├── not-found.tsx           # Custom 404
├── opengraph-image.tsx     # Dynamic OG (one per route)
├── sitemap.ts
└── robots.ts
```

## Order of sections (landing)

For the home page, the canonical order is:

1. **Hero** — H1, lead, primary + secondary CTA, brand strip.
2. **Cases** — 3–5 recent shipped projects with cover images.
3. **Focus** — what we do (AI agents, RAG, chatbots, …).
4. **Process** — 4 steps, plain language.
5. **Pricing / engagement** — typical packages or ranges.
6. **CTA** — repeat the hero CTA in a heavy-glass card.
7. **Footer** — contacts, founders, legal.

Polaroids and background videos are accents, not sections — they live inside other sections.

## Don'ts

- Don't break out of `max-w-7xl` for marketing content.
- Don't pad sections more aggressively than `md:py-32` — it makes the page feel padded with air.
- Don't center body text on mobile. `md:text-center` only — leave mobile left-aligned.
