# Open Design integration

Plug-in artifacts for [`nexu-io/open-design`](https://github.com/nexu-io/open-design).
The folder layout mirrors open-design's expected paths exactly — copy the contents of
each subdirectory into the matching path in your open-design checkout, and the studio's
brand becomes available as a first-class design system inside open-design's UI.

## What's inside

| Path | Purpose | Open-design equivalent |
|------|---------|------------------------|
| `design-systems/croissan/DESIGN.md` | Studio brand as a 9-section open-design spec — color, typography, components, layout, do/don't, agent prompt guide. | `design-systems/croissan/` |
| `templates/croissan-deck.html` | Single-file 11-slide HTML deck. Forks `templates/deck-framework.html` verbatim, swaps the token block, adds croissan slide primitives. | `templates/croissan-deck.html` |
| `skills/croissan-kp/SKILL.md` | Skill that produces a КП for a Croissan client engagement. Triggered by "кп", "коммерческое предложение", "croissan", "круассан", "pitch deck". | `skills/croissan-kp/` |

The skill's `references/` and `assets/` are **symlinks** to the live source-of-truth
files in this repo:

```
skills/croissan-kp/
├── SKILL.md
├── assets/
│   └── croissan-deck.html       → ../../templates/croissan-deck.html
└── references/
    ├── DESIGN.md                → ../../design-systems/croissan/DESIGN.md
    ├── proposal-structure.md    → ../../../../brand/proposal-structure.md
    ├── voice-and-tone.md        → ../../../../brand/voice-and-tone.md
    ├── facts.md                 → ../../../../brand/facts.md
    └── creative-latitude.md     → ../../../../agents/creative-latitude.md
```

This keeps a single source of truth: when you update [`brand/facts.md`](../../brand/facts.md)
or [`design-system/decks.md`](../../design-system/decks.md), the open-design skill picks
up the change automatically without a separate sync step.

## Install

### Option A — symlink into open-design (recommended for active development)

From the root of your open-design checkout:

```bash
SI=~/Dev/studio-identity   # adjust to wherever this repo lives

# Croissan design system
ln -s "$SI/integrations/open-design/design-systems/croissan" \
      design-systems/croissan

# Croissan deck template
ln -s "$SI/integrations/open-design/templates/croissan-deck.html" \
      templates/croissan-deck.html

# Croissan KP skill
ln -s "$SI/integrations/open-design/skills/croissan-kp" \
      skills/croissan-kp
```

Edits in studio-identity propagate to open-design instantly.

### Option B — copy snapshot (recommended for shipping)

```bash
cp -r integrations/open-design/design-systems/croissan       /path/to/open-design/design-systems/
cp    integrations/open-design/templates/croissan-deck.html  /path/to/open-design/templates/
cp -r integrations/open-design/skills/croissan-kp            /path/to/open-design/skills/
```

You'll need to **resolve the symlinks** after copying so open-design sees real files:

```bash
cd /path/to/open-design/skills/croissan-kp
for link in references/* assets/*; do
  if [ -L "$link" ]; then
    target=$(readlink -f "$link")
    rm "$link"
    cp "$target" "$link"
  fi
done
```

This fork is now self-contained but will drift from studio-identity over time. Re-run on
brand updates.

### Option C — fork open-design's skill registry path

If you maintain your own open-design fork or namespace (e.g. internal-only skills), drop
the same three artifacts into your fork's matching paths. open-design's skill registry
scans `~/.claude/skills/`, `./skills/`, and `./.claude/skills/` — anywhere on that list
works.

## Verifying the install

Inside open-design's web UI:

1. Open the **Design system** dropdown in the top bar. You should see:
   ```
   Agency & Studio
     Croissan Studio
   ```
2. Pick it as the active system.
3. Open a chat and prompt: *"Сделай КП для AI-чатбота на 4 недели"*.
4. The skill registry should route to `croissan-kp` (triggers: "кп", "коммерческое
   предложение", "круассан"). Output is a single `index.html` rendered live in the
   iframe preview, themed with cobalt + Golos + the pill/card vocabulary.
5. Press `←` / `→` in the preview to navigate slides. `Esc` shows the overview grid.
6. Export → PDF for client delivery.

If step 1 fails: the design system isn't being detected. Check that
`design-systems/croissan/DESIGN.md` exists and the **first H1** is exactly
`# Design System Inspired by Croissan Studio` and the line immediately after starts with
`> Category:`. open-design parses those two lines for the dropdown.

If step 4 routes to a different skill: trigger conflicts. The default `simple-deck` skill
matches on "deck", "slides", "ppt", "presentation". `croissan-kp` matches on "кп",
"croissan", "круассан". Use a Russian trigger word in your prompt to disambiguate.

## What this gives you (vs running `simple-deck` with our DESIGN.md)

`simple-deck` reads any `DESIGN.md` and uses its tokens. That gets you the colors and
typography. **`croissan-kp` adds**:

- The 11-slide canonical КП narrative baked into the seed.
- Pre-styled component classes for our specific patterns (number-box, polaroid,
  slides-tag, stage-row, final-price).
- Russian-default copy patterns and the voice + facts + proposal-structure references
  symlinked into the skill's context.
- A `creative-latitude` reference so the agent knows what to invent freely.

If you want a marketing landing instead of a КП, use `simple-landing` (or the existing
open-design landing skills) with the **`croissan` design system selected** — that's the
clean separation.

## Updating

When you update brand artifacts in this repo, propagate to deployed open-design:

| You changed… | …and the change reaches open-design via |
|--------------|------------------------------------------|
| `brand/facts.md` | symlink (Option A) — instant. Snapshot (B) — re-run snapshot script. |
| `design-system/decks.md` | not auto-propagated — `decks.md` documents internal patterns; the spec the agent reads is `integrations/open-design/design-systems/croissan/DESIGN.md`. Update both. |
| `integrations/open-design/design-systems/croissan/DESIGN.md` | symlink (A) — instant. Snapshot (B) — re-copy file. |
| `integrations/open-design/templates/croissan-deck.html` | symlink (A) — instant. Snapshot (B) — re-copy file. |

If open-design itself updates its `templates/deck-framework.html` (e.g. the runtime fixes
a new iframe-nav bug), re-fetch and **diff** their version against the verbatim block at
the top of our `croissan-deck.html`. Apply matching changes — but only inside the
"DO NOT EDIT" framework block, never in our token / per-deck styles.

## License & attribution

This integration is internal to Croissan Studio. The open-design framework conventions
it follows are MIT-licensed (see [`nexu-io/open-design/LICENSE`](https://github.com/nexu-io/open-design/blob/main/LICENSE)).
The `templates/deck-framework.html` runtime that we copy verbatim into our deck is
attributed in-file.
