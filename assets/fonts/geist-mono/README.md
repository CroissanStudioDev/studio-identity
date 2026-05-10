# Geist Mono

Monospace for code blocks, technical readouts, and anywhere else we need fixed-width.

## Files

| File | What |
|------|------|
| `GeistMono-VariableFont_wght.ttf` | Variable font — weights 100–900. |
| `OFL.txt` | The license. |

## Loading (web)

```tsx
import { Geist_Mono } from "next/font/google";

const geistMono = Geist_Mono({
  subsets: ["latin"],
  variable: "--font-geist-mono",
});
```

In `croissan-landing` this maps to the `--font-geist-mono` Tailwind 4 token (declared
in `app/globals.css` under `@theme inline`).

## License

OFL 1.1 — see [`OFL.txt`](OFL.txt). Designed by Vercel; published by Vercel and now
mirrored on Google Fonts.

## Provenance

- Source: [google/fonts/ofl/geistmono](https://github.com/google/fonts/tree/main/ofl/geistmono)
- Upstream design: [vercel/geist-font](https://github.com/vercel/geist-font)

## Use rules

- Code blocks (web + slides).
- Tabular numerals in technical readouts where monospace helps — never for body copy.
- Don't use on body, headlines, or anything readable longer than ~12 characters.
  Monospace at body length tires the eye.
