# Logo usage

The Croissan brand mark is a stylized croissant — three crescent strokes around an offset
rotated ellipse. It exists in two visual modes (flat 2D and dimensional 3D) and pairs with the
**Croissan Studio** wordmark in three lockup variants.

> Source of truth: Figma file [`Branding`](https://www.figma.com/design/5evQ6yHHzqQoqu8N40m54s/Branding).

## Mark variants

| Variant | When to use | File |
|---------|-------------|------|
| **2D flat — brand primary** | Default. Light or neutral surfaces. | [`../../assets/logos/croissan-logo.svg`](../../assets/logos/croissan-logo.svg) |
| **2D flat — white** | Brand-primary, dark, or photographic surfaces. | [`../../assets/logos/croissan-logo-white.svg`](../../assets/logos/croissan-logo-white.svg) |
| **3D rendered (mascot)** | Decorative hero accents, deck covers, social posts. Never as a UI control. | TODO — export from Figma |

The **3D mark** is the dimensional purple-blue rendered croissant visible in deck covers and
brand collateral. Treat it as a mascot / illustration, not a logo. Don't use it in dense UI
contexts; use the 2D flat mark.

## Wordmark + lockups

The full lockup is **«Croissan Studio»** set in a heavy geometric sans (Right Grotesk Bold,
matching our H1 typeface) with the small 2D flat mark inline at the right of the word
«Studio». The wordmark sits on two stacked lines.

Three approved background tiles:

| Background | Wordmark color | Use for |
|------------|----------------|---------|
| **Brand primary** (`#2727CA`) | white | Marketing covers, deck title slides, ads |
| **White** (`--background`) | brand primary (`#2727CA`) | Default — letterheads, navbar, light UI |
| **Black** (`#000`) | brand primary (`#2727CA`) | Premium / contrast covers, social, video |

Black is a **brand background**. Don't use mid-greys or off-blacks — the wordmark looks weak.

## Sub-brand: Croissan Community

A second identity, **«Croissan Community»**, uses the **same lockup system** (same typeface,
same mark, same three background tiles). Use it for:
- Community events, meetups, edu programs
- Open-source projects, public artifacts not tied to commercial work

Studio and Community are siblings, not parent/child — don't combine the two wordmarks in one
artifact.

## Construction

- Always use the SVG. Don't re-export to PNG unless a target system can't accept SVG; if you
  must, render at 2× minimum.
- Don't redraw or "clean up" the path data — the asymmetry is intentional.
- Don't recolor outside the approved combinations above. Brand primary, white, or black only.

## Sizing

| Context | Size |
|---------|------|
| Minimum (anywhere) | **24×24** px (below this curves blur) |
| Navbar | 32–40 px |
| Hero / about | 64–96 px |
| Deck cover (3D mark) | 200–600 px depending on slide width |

Always preserve the aspect ratio — viewBox is square; render at `height=N width=N`.

## Clear space

Reserve **at least 25% of the mark's height** as clear space on every side. For wordmark
lockups, give the equivalent of **one mark-width** of clear space around the entire lockup.

## In code

```tsx
import Image from "next/image";

<Image alt="Круассан Студио" height={32} width={32} src="/logo.svg" priority />
```

Always include `alt`. For decorative duplicates of an already-named logo, use `alt=""` +
`aria-hidden="true"`.

## Don'ts

- ❌ Mid-grey backgrounds. Pick darker or lighter.
- ❌ Busy patterns directly behind the mark. Add a solid plate.
- ❌ Recoloring the mark to non-brand hues.
- ❌ Combining "Studio" and "Community" wordmarks in one composition.
- ❌ Using the 3D mark as a clickable UI element.
- ❌ Stretching, skewing, or rotating the wordmark.
