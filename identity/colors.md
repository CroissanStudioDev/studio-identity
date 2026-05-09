# Colors

Single source of truth for the **named** color system. The actual hex values live in
[`../design-system/design-tokens.css`](../design-system/design-tokens.css) — that file
is canonical for what each token resolves to. If hex disagrees between this doc and
`design-tokens.css`, **the CSS file wins**. **Never hardcode hex** in component code
when a token exists.

## Brand palette

| Role | Token | Value |
|------|-------|-------|
| Primary (CTA, accents) | `--brand-primary` | `#2727CA` |
| Primary hover | `--brand-primary-hover` | `#2424B4` |
| Brand dark (main text) | `--brand-dark` | `#150E47` |
| Brand black (premium covers, high-contrast) | `--brand-black` | `#0E0E14` |
| Brand graphite (case-study slides) | `--brand-graphite` | `#252527` |
| Error | `--color-error` | `#E53935` |
| Background (light neutral canvas) | `--background` | `oklch(0.98 0.01 260)` |

The brand is built on a **deep blue-violet** (`#2727CA`) against four approved background
tiles: **white**, **brand primary**, **brand black**, and **graphite**. Dark UI text
(`#150E47`) is the same hue as the primary, just much darker — that's what gives the
brand a coherent, slightly moody feel without going monochrome.

**Black is a brand background**, not a fallback. It's used for premium-feeling deck
covers, video title cards, and high-contrast social posts. We use `#0E0E14` (slight
hue toward the brand) on screens; pure `#000` is fine for print.

**Graphite (`#252527`) is the fourth surface** — exclusively for case-study slides
where product screenshots need a softer-than-black backdrop. It's not a fallback for
black; pick deliberately when a slide is product-screenshot-led.

In product UI we still default to the light `--background`. Mid-greys (`#404040`–`#909090`)
are never a brand surface — pick darker or lighter.

## Tailwind utilities (use these, not raw hex)

| Need | ✅ Use | ❌ Don't |
|------|-------|---------|
| CTA background | `bg-brand` | `bg-[#2727CA]` |
| CTA hover | `hover:bg-[var(--brand-primary-hover)]` | `hover:bg-[#2424B4]` |
| Accent text | `text-brand` | `text-[#2727CA]` |
| Dark text | `text-brand-dark` | `text-[#150E47]` |
| Error text | `text-error` | `text-red-500` |

## Text opacity scale

For body copy on the light background, we vary the dark color's opacity rather than introducing greys.

```
text-primary      /* 100% — headlines, critical info */
text-primary-90   /* 90%  — subheadings, emphasis */
text-primary-80   /* 80%  — regular body */
text-primary-70   /* 70%  — secondary body */
text-primary-60   /* 60%  — descriptions, captions */
text-primary-50   /* 50%  — placeholders ONLY */
```

**Rule**: anything `text-primary-50` or below is below WCAG AA on our background. Use it only for
decorative placeholders, never for content a user is expected to read.

## Surfaces

| Surface | Class |
|---------|-------|
| Page background | `bg-background` |
| Standard card | `bg-white` with `border border-black/5` |
| Glass card (navbar, forms) | `rounded-[20px] bg-background/80 backdrop-blur-md` |
| Heavy-glass CTA card | `rounded-3xl bg-gradient-to-br from-white/10 to-white/5 shadow-sm backdrop-blur-[100px]` |
| Subtle tag/badge | `bg-black/5` |

## Charts and data viz

`oklch`-based scale, hue around 260° (matches the brand):

```
--chart-1: oklch(0.55 0.25 260);   /* primary */
--chart-2: oklch(0.65 0.20 200);   /* cyan */
--chart-3: oklch(0.60 0.25 320);   /* magenta */
--chart-4: oklch(0.70 0.20 150);   /* green */
--chart-5: oklch(0.65 0.25 30);    /* orange */
```

Order matters: `chart-1` is always the primary series.

## Dark mode

We don't ship dark mode in `croissan-landing` today. If a future project needs it, define
counterparts for `--brand-dark` (becomes light), `--background` (becomes near-black with the same
hue), and the text-opacity scale, and document them here before shipping.

## Don'ts

- No raw hex in JSX/CSS where a token exists.
- No `text-gray-*`, `text-zinc-*`, `text-slate-*` for body text — use `text-primary-NN`.
- No new accent colors without adding a token. If you find yourself reaching for orange/teal/pink,
  it's probably a chart color, and it should come from the `--chart-*` scale.
