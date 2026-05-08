# SF Pro Text — reference only, NOT bundled

Some Figma annotations and iOS-flavored mockups use **SF Pro Text** (Apple's system
typeface). It's not part of our regular brand — it just shows up when someone exports a
mockup that includes a real iOS UI.

## Why this folder is empty

Apple's [SF Pro license](https://developer.apple.com/fonts/) restricts redistribution.
The license text:

> The Apple Font Software... may be used and reproduced solely for use in the design,
> development and production of an application... You may not export the Apple Font
> Software from a Macintosh-based application.

In plain English: you can use SF Pro on a Mac to design things, but you can't bundle
the font files in a product, repo, or distributed asset. So this folder stays empty in
the public repo.

## Where to obtain

- Download directly from Apple at https://developer.apple.com/fonts/.
- macOS users: SF Pro is preinstalled on every Mac since macOS 10.13 — Figma and Sketch
  pick it up automatically, no separate download needed for **Figma editing**.

If you need the font files locally for non-Figma work (e.g. Linux server-side rendering
of an iOS-mockup PDF), download from the link above and drop into this folder.
**Do not commit the binaries.** [`../../.gitignore`](../../../.gitignore) covers this.

## Use rules

- **iOS mockups only.** Don't use SF Pro on the marketing site, our slides, our docs,
  or anywhere it would replace Golos Text.
- **Don't substitute Helvetica or San Francisco system fallback** if SF Pro isn't
  available — better to render the iOS UI in Golos Text and label the mockup as
  "stylized" than to ship a half-Apple-half-system look.

## What this means for agents

If a brief asks for "iOS-style preview" or "iPhone mockup", an agent should use
SF Pro Text **only if the user explicitly confirms they have a license**. Default
behavior: render the iOS frame with Golos Text and call out the substitution in the
hand-off. This is the same conservative-redistribution rule as Golos UI.
