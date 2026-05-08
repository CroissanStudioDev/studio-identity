# Inter

Used on **case-study slide metric chips**. Figma's design-context exports show
`font-['Inter:Medium',sans-serif]` on slide 173 (the «Брендформанс» case-study
template). Inter Medium reads cleaner at the 18 px chip size on graphite (`#252527`)
than Golos at the same size — Cyrillic numeral spacing is tighter.

For **everything else**, use Golos Text.

## Files

| File | What |
|------|------|
| `Inter-VariableFont_opsz_wght.ttf` | Variable font — opsz (optical size) + wght (100–900) axes. |
| `OFL.txt` | The license. |

## Loading (web)

```tsx
import { Inter } from "next/font/google";

const inter = Inter({
  subsets: ["cyrillic", "latin"],
  variable: "--font-inter",
  weight: ["500"],   // we only ship Medium
});
```

## License

OFL 1.1 — see [`OFL.txt`](OFL.txt). Free to redistribute, embed, modify.

## Provenance

- Source: [google/fonts/ofl/inter](https://github.com/google/fonts/tree/main/ofl/inter)
- Upstream design: [rsms/inter](https://github.com/rsms/inter)

## Use rules

- **Slide metric chips on case-study slides only.** 18 px Medium, white on the chip
  background.
- **Don't introduce on the web.** Web stays on Golos Text. Inter on the web is a
  classic AI-default tell — see [`agents/anti-ai-slop.md`](../../../agents/anti-ai-slop.md)
  rule #4.
