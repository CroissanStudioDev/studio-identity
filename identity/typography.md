# Typography

## Typefaces

| Role | Family | License | Source | CSS variable |
|------|--------|---------|--------|--------------|
| Headlines (H1, web) | **Right Grotesk** | studio-licensed | bundled — [`../assets/fonts/right-grotesk/`](../assets/fonts/right-grotesk/) | `--font-right-grotesk` |
| Body, sub-headings, slide content | **Golos Text** | OFL (Yandex/Paratype) | bundled — [`../assets/fonts/golos-text/`](../assets/fonts/golos-text/), or `next/font/google` | `--font-geist-sans` |
| Mono | **Geist Mono** | OFL (Vercel) | bundled — [`../assets/fonts/geist-mono/`](../assets/fonts/geist-mono/), or `next/font/google` | `--font-geist-mono` |
| Slide metric chips (case-study) | **Inter** | OFL (rsms) | bundled — [`../assets/fonts/inter/`](../assets/fonts/inter/) | `--font-inter` |
| OG images / PDFs (server-side) | **Noto Sans** | OFL (Google) | bundled — [`../assets/fonts/noto-sans/`](../assets/fonts/noto-sans/) | — |
| Older Figma slide masters | **Golos UI** | commercial (ParaType) | **NOT bundled** — Figma serves it server-side; for new work prefer Golos Text | — |
| iOS-flavored mockups in Figma | **SF Pro Text** | Apple, no redistribution | **NOT bundled** — only edit on a Mac where it's preinstalled | — |

> **Why Right Grotesk only on H1?** It carries the brand voice — bold, slightly cheeky, modern.
> Using it lower in the hierarchy makes it noisy. H2/H3 use the body font in heavier weights.

> **Golos UI vs Golos Text — for new work, prefer Golos Text.** Same family DNA; Golos Text is OFL
> and bundled, Golos UI is commercial and can't be redistributed. Older Figma slide masters use
> Golos UI for historical reasons; the visual difference at H1 sizes is negligible. See
> [`../assets/fonts/golos-ui/README.md`](../assets/fonts/golos-ui/README.md).

Every font folder has its own `README.md` explaining provenance, license, and how to load it.
Index: [`../assets/fonts/README.md`](../assets/fonts/README.md).

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
