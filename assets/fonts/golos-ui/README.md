# Golos UI — reference only, NOT bundled

Older slide masters use **Golos UI Bold** and **Golos UI Medium** at 90 px for slide H1s.

## Why this folder is empty

Golos UI is a **commercial typeface licensed via [ParaType](https://www.paratype.com/fonts/pt/golos)**.
The license forbids redistribution, so we cannot commit the `.ttf` / `.otf` files to a
public GitHub repo. If we did, we'd be in violation of the studio's license and
ParaType's terms.

## Where to obtain

If you have a studio Figma seat, Golos UI is already available — the design tool
resolves the font server-side, no local install needed.

If you need the actual font files locally (e.g. for non-design-tool slide rendering,
OG images, server-side PDF), purchase a license at:

> https://www.paratype.com/fonts/pt/golos

Drop the resulting `.ttf` / `.otf` files into this folder. **Do not commit them.** The
[`../../.gitignore`](../../../.gitignore) covers this — see the bottom of the file for
the rule.

## For new work, prefer Golos Text

We **bundle Golos Text** ([`../golos-text/`](../golos-text/)) — same family DNA, OFL
license, freely redistributable. New decks and new web surfaces should use Golos Text
across the board. Golos UI lives on in older slide masters because that's what was
selected when those files were authored.

The visual difference at slide-H1 sizes (90 px) is minor — Golos Text Bold reads
essentially identically to Golos UI Bold. Don't lose sleep over the substitution.

## What this means for agents

If an agent generates an HTML deck or a web page and references `font-family: "Golos UI"`,
**flag it as a substitution recommendation**: prefer `"Golos Text"` (which is bundled
and OFL). Don't refuse the work; do note the substitution.
