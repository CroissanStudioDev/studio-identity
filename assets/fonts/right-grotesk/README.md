# Right Grotesk

Used for **H1 on the marketing site**. Studio's display typeface — bold, geometric,
slightly cheeky. Right Grotesk is the only place we let display type do its own thing;
everything else (body, sub-headings, slide titles) uses Golos Text.

## Files

| File | What |
|------|------|
| `accent-typeface.woff2` | The exact woff2 already shipped publicly in [`croissan-landing/app/accent-typeface.woff2`](https://github.com/CroissanStudioDev/croissan-landing/blob/main/app/accent-typeface.woff2). Single weight (Bold). Generic filename is intentional — keeps the licensing footprint discreet across surfaces. |

## Loading (web)

In a Next.js project, via `next/font/local`:

```tsx
// app/layout.tsx
import localFont from "next/font/local";

const rightGrotesk = localFont({
  src: "./accent-typeface.woff2",
  variable: "--font-right-grotesk",
});

<html className={rightGrotesk.variable}>
```

Then in components:

```tsx
<h1
  className="font-bold text-5xl text-primary leading-[1] -tracking-[1.2px] md:text-7xl"
  style={{ fontFamily: "var(--font-right-grotesk)" }}
>
  Зовите нас, когда нужен продукт с ИИ
</h1>
```

## Use rules

- **H1 on marketing pages only.** Lower in the hierarchy it gets noisy.
- **Don't use on slides.** Slides use Golos Text / Golos UI Bold at 90 px instead.
- **Don't substitute.** Inter / system-ui on display H1s is a P0 anti-slop tell — see
  [`agents/anti-ai-slop.md`](../../../agents/anti-ai-slop.md).

## Provenance

This file already lives in the public `croissan-landing` repo. The studio licenses the
typeface for use across studio properties; the file in this identity repo is a copy of
that exact woff2, named with the same `accent-typeface.woff2` filename to keep
parity.

If you're adopting a new project under the studio brand, copy the file from here (or
from croissan-landing — same content).
