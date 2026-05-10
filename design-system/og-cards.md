# OG / social cards

How we render Open Graph images and social cards. The implementation lives in
[`croissan-landing/lib/og/render.tsx`](https://github.com/CroissanStudioDev/croissan-landing/blob/main/lib/og/render.tsx);
this doc is the spec.

## Canvas

| Param | Value |
|-------|-------|
| Size | **1200 × 630 px** (the OG / Twitter / LinkedIn standard — fits everywhere) |
| Background | `linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%)` — the *only* surface where we use a soft 2-stop gradient, because OG is a print-medium-like static asset, not a hero |
| Padding | 80 px on every side |
| Format | PNG, generated on demand by `@vercel/og` (`next/og`) — never hand-exported |

## Type

OG cards run server-side at the edge — Google Fonts isn't reachable. We use **Noto Sans**
(bundled at [`../assets/fonts/noto-sans/`](../assets/fonts/noto-sans/)). It's not Golos
Text but it covers Cyrillic + Latin without subsetting hassles, and at OG size the
visual difference is acceptable.

| Role | Family | Size | Weight | Color |
|------|--------|------|--------|-------|
| Title | Noto Sans | 72–96 px | 700 | `#150E47` |
| Subtitle | Noto Sans | 32 px | 400 | `#150E47` |
| Description | Noto Sans | 22 px | 400 | `#666` |
| Mark | inline SVG | ~64 px | — | `#2727CA` |

## Layout

```
┌────────────────────────────────────────┐  1200×630
│                                        │
│         [mark, ~64 px]                 │
│                                        │
│         Croissan Studio                │  ← title, 72–96 px Bold, dark
│                                        │
│         Ваша заботливая AI-студия      │  ← subtitle, 32 px Regular
│                                        │
│         Мы студия полного цикла,       │  ← description, 22 px Regular,
│         помогаем компаниям...          │     muted, max-width ~800 px
│                                        │
└────────────────────────────────────────┘
```

Center-aligned vertically and horizontally. **No** decorative chrome — no badges, no
"shared on Croissan Studio" footer. The card is the message.

## API surface

```tsx
import { renderOgImage, OG_SIZE, OG_CONTENT_TYPE } from "@/lib/og/render";

// Per-route opengraph-image.tsx
export const size = OG_SIZE;          // { width: 1200, height: 630 }
export const contentType = OG_CONTENT_TYPE;  // "image/png"
export const alt = "...";

export default function Image() {
  return renderOgImage({
    title: "Page-specific title",
    subtitle: "Optional subtitle",
    description: "1–2 sentences about this page",
    titleFontSize: 96,  // optional, defaults to 96
  });
}
```

## Per-route customization

Drop an `opengraph-image.tsx` in any route. Next 16 picks it up at build, generates a
unique OG image per URL. Examples already in `croissan-landing`:

- `/` (homepage) — studio overview
- `/brief` — the AI brief generator tool
- Add a new route → add a new `opengraph-image.tsx` next to `page.tsx`

## Don'ts

- ❌ **Don't use `--brand-primary` as the OG background.** A solid Croissan-blue OG is a
  miss-read at thumbnail size in feeds; the soft gradient on near-white reads as a
  neutral document. Reserved as a deliberate exception to the "flat surfaces only"
  rule.
- ❌ **No real photography or rendered illustrations** in OG images. Type + mark only.
  Photos compress badly at 1200×630 in feed previews.
- ❌ **No emoji.** Including in titles. Replace with the mark or a Lucide icon.
- ❌ **No drop shadows or glassmorphism.** The card is a typography exercise.
- ❌ **No A/B variants per route.** One canonical OG per URL; revisions ship via PR.

## Verifying

After deploying a route, check the OG renders correctly:

- Twitter card validator: https://cards-dev.twitter.com/validator (or post a tweet
  draft with the URL)
- OpenGraph debugger: https://www.opengraph.xyz/?url=https://croissanstudio.ru/your-route
- Just open the route's `/opengraph-image` URL directly in a browser
