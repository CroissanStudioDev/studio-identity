# Fonts

Every typeface used by Croissan Studio across web, slides, decks, OG images, and PDFs.
One folder per family. Each folder has a `README.md` with provenance and usage.

## Bundled (committable)

| Family | Used for | License | Bundled files |
|--------|----------|---------|---------------|
| **Right Grotesk** | Web H1 (marketing pages) | Licensed via studio · file already shipped publicly in [`croissan-landing`](https://github.com/CroissanStudioDev/croissan-landing) | [`right-grotesk/accent-typeface.woff2`](right-grotesk/accent-typeface.woff2) |
| **Golos Text** | Web body, slides body, deck body | OFL ([Yandex / Paratype](https://github.com/google/fonts/tree/main/ofl/golostext)) | TTF (variable) + 4 subset woff2, [`golos-text/`](golos-text/) |
| **Inter** | Slide metric chips (case-study slides) | OFL ([rsms/inter](https://github.com/rsms/inter)) | TTF (variable), [`inter/`](inter/) |
| **Geist Mono** | Code blocks, monospace surfaces | OFL ([Vercel / Geist](https://github.com/vercel/geist-font)) | TTF (variable), [`geist-mono/`](geist-mono/) |
| **Noto Sans** | OG-image rendering (server-side, no network) | OFL ([Google Fonts Noto](https://fonts.google.com/noto)) | Regular + Bold TTF, [`noto-sans/`](noto-sans/) |

## Reference-only (not committable)

These typefaces appear in older slide masters or in iOS-style mockups but their licenses
**do not allow redistribution**. The folder is empty; the README explains where to obtain.

| Family | Used for | Why not bundled | How to obtain |
|--------|----------|-----------------|---------------|
| **Golos UI** | Older slide masters (H1 90 px Bold/Medium) | Commercial license via ParaType | [`golos-ui/README.md`](golos-ui/README.md) |
| **SF Pro Text** | iOS-style mockups | Apple Developer license forbids redistribution | [`sf-pro/README.md`](sf-pro/README.md) |

> **For new work, prefer Golos Text over Golos UI.** They share the design DNA; Golos
> Text is OFL and ships with this repo, so every implementation surface (web, decks,
> server-side rendering) can use the same file. Older slide masters keep Golos UI for
> historical reasons.

## Where these get used

- **Marketing site** (`croissan-landing`) — fonts loaded via `next/font` (Google Fonts
  for Golos Text, `next/font/local` for Right Grotesk's `accent-typeface.woff2`).
- **HTML deck templates** ([`../deck-template/`](../deck-template/) and
  [`../../integrations/open-design/templates/`](../../integrations/open-design/templates/))
  — Golos Text loaded from Google Fonts CDN at runtime.
- **OG images / PDFs** (`/api/og`, brief PDF generator) — Noto Sans bundled, used by
  `pdf-lib` and `@vercel/og` because they render server-side without network access.
- **Open-design integration** (the `croissan-kp` skill) — bundled woff2 + TTF copied
  alongside the deck template if running offline.

## Adding a font

1. Create a new subfolder named after the family (kebab-case): `assets/fonts/my-font/`.
2. Drop the actual font file(s) inside.
3. Add a `README.md` explaining provenance, license, and which weights/styles are present.
4. If the file is **OFL** or otherwise redistributable, also include the upstream `OFL.txt`
   or license file in the same folder.
5. If the file is **not redistributable**, leave the folder empty and put a `README.md`
   that points at where to obtain it. Do not commit the binary.
6. Update this index and [`../../identity/typography.md`](../../identity/typography.md).

## Why subfolders instead of a flat directory

Earlier the directory was flat (`NotoSans-Bold.ttf`, `NotoSans-Regular.ttf`). With more
families and license caveats per family, a flat layout obscured "is this file licensed
to be here?" Subfolders + per-family READMEs make that question one click instead of
five. Keeps the public repo audit-friendly.
