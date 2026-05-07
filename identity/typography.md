# Typography

## Typefaces

| Role | Family | Source | CSS variable |
|------|--------|--------|--------------|
| Headlines (H1) | **Right Grotesk** | Local font file | `--font-right-grotesk` |
| Body | **Golos Text** | Google Fonts | `--font-geist-sans` |
| Mono | **Geist Mono** | Google Fonts / `next/font` | `--font-geist-mono` |
| OG images / PDFs | **Noto Sans** | Bundled (`assets/fonts/`) | — |

> **Why Right Grotesk only on H1?** It carries the brand voice — bold, slightly cheeky, modern.
> Using it lower in the hierarchy makes it noisy. H2/H3 use the body font in heavier weights.

`Noto Sans` is bundled in [`../assets/fonts/`](../assets/fonts/) for server-side image generation
(OG images, PDFs) where Google Fonts isn't reachable.

## Type scale

Live snippets, copy-paste:

```tsx
// H1 — page hero only, one per page
<h1
  className="font-bold text-5xl text-primary leading-[1] -tracking-[1.2px] md:text-7xl"
  style={{ fontFamily: "var(--font-right-grotesk)" }}
>

// H2 — section headlines
<h2 className="font-semibold text-3xl tracking-tight md:text-5xl">

// H3 — sub-headers within sections
<h3 className="font-medium text-2xl tracking-tight md:text-3xl lg:text-4xl">

// Lead paragraph (sits right under H1)
<p className="text-lg text-primary-60 leading-[150%] md:text-xl">

// Body
<p className="text-primary-60">

// Small / caption
<p className="text-sm text-primary-70">

// Inline emphasis
<span className="font-medium text-primary-90">
```

## Hierarchy rules

- Exactly **one `<h1>`** per page.
- No skip-levels: H1 → H2 → H3 → H4. If you'd skip, the structure is wrong, not the markup.
- Don't fake a heading with a styled `<p>` — it breaks SEO and screen readers.

## Tracking and leading

- H1 uses **negative tracking** (`-tracking-[1.2px]`) and tight leading (`leading-[1]`) for visual punch.
- H2/H3 use `tracking-tight`.
- Lead paragraphs use `leading-[150%]` (1.5).
- Body inherits Tailwind defaults — don't override unless there's a reason.

## Russian-specific niceties

- Use **non-breaking spaces** (`&nbsp;`) before short prepositions and short standalone words:
  `с&nbsp;ИИ`, `за&nbsp;2-4&nbsp;недели`, `на&nbsp;рынке`.
- Use **em-dashes** (`—`) for parenthetical breaks, not hyphens.
- Use **proper Russian quotes** «like this» in body copy. Straight quotes are fine in code or UI.

## Don'ts

- Don't use Right Grotesk anywhere except H1 (and the occasional brand-mark word).
- Don't introduce a third sans-serif. If you need a different feel, use weight/size/tracking.
- Don't go below `text-sm` for content. Anything smaller is decorative or compliance-only.
