# Golos Text

Used for **body, sub-headings, and slide content**. The studio's workhorse typeface —
neutral, confident, supports Russian + Latin without compromise.

## Files

| File | What |
|------|------|
| `GolosText-VariableFont_wght.ttf` | Variable font — weights 400–900. Use this for `next/font/local`, `@vercel/og`, `pdf-lib`, or anywhere you need the full weight axis from a single file. |
| `GolosText-cyrillic-ext.woff2` | Subset for cyrillic-extended unicode range. |
| `GolosText-cyrillic.woff2` | Subset for cyrillic. |
| `GolosText-latin-ext.woff2` | Subset for latin-extended. |
| `GolosText-latin.woff2` | Subset for latin. |
| `OFL.txt` | The license. Keep it. |

The 4 woff2 files are the exact subsets Google Fonts CDN serves — same hashes, same
unicode ranges. Use them when you want to load only what's needed for a specific page
language. The `.ttf` is for server-side rendering where subsetting doesn't apply.

## Loading (web)

Easiest path — `next/font/google`:

```tsx
import { Golos_Text } from "next/font/google";

const golos = Golos_Text({
  subsets: ["cyrillic", "latin"],
  variable: "--font-geist-sans",  // existing variable name in croissan-landing
  weight: ["400", "500", "600", "700"],
});
```

This hits Google Fonts CDN at runtime — works for everything except offline
server-side rendering (OG images, PDFs).

## Loading (server-side, OG / PDF)

When `next/font/google` doesn't work (no network on the server), use the bundled TTF:

```ts
import path from "node:path";
import fs from "node:fs/promises";

const golosTtfPath = path.join(
  process.cwd(),
  "assets/fonts/golos-text/GolosText-VariableFont_wght.ttf",
);
const golosBytes = await fs.readFile(golosTtfPath);

// pass golosBytes to @vercel/og or pdf-lib
```

## License

OFL 1.1 — see [`OFL.txt`](OFL.txt). Yandex / ParaType. We can redistribute, embed, and
modify. We cannot sell the font itself (only as part of a larger work, which is fine for
both code and Figma).

## Provenance

- Source: [google/fonts/ofl/golostext](https://github.com/google/fonts/tree/main/ofl/golostext)
- Variable TTF + license were pulled from that repo as-is.
- Subset woff2 files are mirrored from Google Fonts' CDN.

## Use rules

- **Default body face on every surface.** Web body, slide body, deck body, PDF body.
- **Default H2/H3 on web** — `font-semibold`/`font-medium` on top.
- **Default H1 on slides** — Bold at 90 px (matches the Figma master treatment).
- **Prefer over Golos UI** for new work. See [`../golos-ui/README.md`](../golos-ui/README.md)
  for why.
