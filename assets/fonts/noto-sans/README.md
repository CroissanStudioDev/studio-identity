# Noto Sans

Used for **server-side rendering** — OG images and PDF generation — where Google Fonts
isn't reachable from the runtime (e.g., inside `@vercel/og`'s edge environment, or
inside `pdf-lib` running in a Docker container without DNS access).

For everything that runs in a browser, use Golos Text instead.

## Files

| File | What |
|------|------|
| `NotoSans-Regular.ttf` | Regular weight, full Cyrillic + Latin. Used as default body face in OG images. |
| `NotoSans-Bold.ttf` | Bold weight, full Cyrillic + Latin. Used as headline face in OG images. |

These are the same two TTF files that ship in `croissan-landing/assets/fonts/` and are
loaded by the brief generator at `lib/brief/pdf.ts` and the OG renderer at
`lib/og/render.tsx`.

## Loading (server-side)

```ts
import path from "node:path";
import fs from "node:fs/promises";
import { ImageResponse } from "next/og";

const fontsDir = path.join(process.cwd(), "assets/fonts/noto-sans");
const [regular, bold] = await Promise.all([
  fs.readFile(path.join(fontsDir, "NotoSans-Regular.ttf")),
  fs.readFile(path.join(fontsDir, "NotoSans-Bold.ttf")),
]);

return new ImageResponse(<MyTemplate />, {
  fonts: [
    { name: "Noto Sans", data: regular, weight: 400 },
    { name: "Noto Sans", data: bold, weight: 700 },
  ],
});
```

## License

OFL 1.1 — Google. Free to redistribute, embed, modify.

## Why Noto Sans for server-side and Golos Text for browser?

- `@vercel/og` runs at the edge with no network. Bundled font files are required.
- `Noto Sans` covers full Cyrillic + Latin without subsetting hassles, so OG images
  render identically across language variants.
- For browser-rendered text (the marketing site, the live HTML deck preview), Golos
  Text via Google Fonts is faster (CDN-cached, subsetted) and matches the spec.
- The visual difference between Noto Sans and Golos Text at OG-image size (1200×630)
  is acceptable. We trade a tiny bit of off-brand weight for reliability.

If we ever want to fix the cosmetic mismatch, swap the OG renderer to load
`../golos-text/GolosText-VariableFont_wght.ttf`. The variable TTF supports all weights.
We haven't migrated yet because Noto's been working fine.

## Provenance

- Source: [google/fonts/ofl/notosans](https://github.com/google/fonts/tree/main/ofl/notosans)
- These specific TTFs were copied from `croissan-landing/assets/fonts/`.
