# Open Design integration

Plug-in artifacts for [`nexu-io/open-design`](https://github.com/nexu-io/open-design):
the studio brand as a first-class design system, plus a КП-deck skill and a single-file
deck template.

> Works with **open-design run from source** (a local clone like `~/Dev/opendesign/`).
> The packaged desktop app bundles its skills at build time and offers no extension
> point — see [Desktop app](#desktop-app) below.

## What's inside

| Path | What it adds to open-design |
|------|------------------------------|
| `design-systems/croissan/DESIGN.md` | "Croissan Studio" entry in the Design system dropdown — full 9-section spec (color, typography, components, layout, do/don't, agent prompt guide). |
| `templates/croissan-deck.html` | Single-file 11-slide HTML deck. Forks `templates/deck-framework.html` verbatim, swaps the token block. |
| `skills/croissan-kp/SKILL.md` | КП-deck skill. Triggered by "кп", "коммерческое предложение", "croissan", "круассан", "pitch deck". |

## Install

```bash
curl -sL https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/bin/install | bash
```

The installer auto-detects open-design at `~/Dev/open-design`, `~/Dev/opendesign`,
`~/Code/open-design`, etc., and copies the three artifacts into the right paths. Re-run
any time to update.

If your open-design checkout is somewhere unusual:

```bash
bash ~/.croissan/identity/bin/sync-opendesign /path/to/your/open-design
```

## Verifying

1. Restart open-design's dev server (or refresh the browser tab).
2. Open the **Design system** dropdown — under **Agency & Studio**, pick **Croissan Studio**.
3. Prompt: *«Сделай КП для AI-чатбота на 4 недели»*. The `croissan-kp` skill picks it up and renders a deck in the preview pane.
4. `←` / `→` to navigate slides, `Esc` for the overview grid, **Export → PDF** for client delivery.

If the dropdown doesn't show **Croissan Studio**: confirm the first line of
`<open-design>/design-systems/croissan/DESIGN.md` is exactly `# Design System Inspired by Croissan Studio` and the next line begins with `> Category:` — open-design parses those two lines for the dropdown.

If the prompt routes to `simple-deck` instead of `croissan-kp`: include a Russian
keyword («кп», «круассан») to disambiguate from the generic deck-skill triggers.

## What this gives you (vs running `simple-deck` with the DESIGN.md alone)

`simple-deck` reads any `DESIGN.md` and uses its tokens — colors and typography only.
**`croissan-kp` adds**:

- The 11-slide canonical КП narrative baked into the seed.
- Pre-styled component classes (number-box, polaroid, slides-tag, stage-row, final-price).
- Russian-default copy patterns and the voice / facts / proposal-structure references
  bundled into the skill's context.
- The `creative-latitude` reference so the agent knows what to invent freely.

For a marketing landing instead of a КП, use any open-design landing skill with the
**`croissan` design system selected** — clean separation.

## Updating

After editing anything in `studio-identity` (brand voice, facts, deck spec, the skill
itself), re-sync:

```bash
bash ~/.croissan/identity/bin/sync-opendesign
```

Then refresh open-design's browser tab. What propagates:

| You changed… | Reaches open-design after sync |
|--------------|-------------------------------|
| `brand/facts.md` | yes |
| `brand/voice-and-tone.md`, `brand/proposal-structure.md` | yes |
| `agents/anti-ai-slop.md`, `agents/creative-latitude.md` | yes |
| `integrations/open-design/design-systems/croissan/DESIGN.md` | yes |
| `integrations/open-design/templates/croissan-deck.html` | yes |
| `integrations/open-design/skills/croissan-kp/SKILL.md` | yes |
| `design-system/decks.md` (internal-only doc) | no — update `DESIGN.md` for the agent-facing spec |

## Desktop app

The packaged desktop build of open-design bundles its skills and design systems inside
the app's read-only resources at build time. There is no settings UI to install
external skills, no support for `~/.claude/skills/`-style external scanning, and no
"install from URL" feature.

For desktop, run open-design from a local clone (the `~/Dev/opendesign/` setup the
installer targets) instead of using the packaged `.app`. That's the only path where
adding our skill is non-destructive and survives upgrades.

## License & attribution

This integration is internal to Croissan Studio. open-design itself is MIT
([nexu-io/open-design](https://github.com/nexu-io/open-design/blob/main/LICENSE)). The
`templates/deck-framework.html` runtime we copy verbatim into our deck is attributed
in-file.
