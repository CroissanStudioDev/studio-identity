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
│   └── croissan-deck.html       → ../../../templates/croissan-deck.html
└── references/
    ├── DESIGN.md                → ../../../design-systems/croissan/DESIGN.md
    ├── anti-ai-slop.md          → ../../../../../agents/anti-ai-slop.md
    ├── creative-latitude.md     → ../../../../../agents/creative-latitude.md
    ├── facts.md                 → ../../../../../brand/facts.md
    ├── proposal-structure.md    → ../../../../../brand/proposal-structure.md
    └── voice-and-tone.md        → ../../../../../brand/voice-and-tone.md
```

These symlinks live **inside studio-identity** and keep a single source of truth here.
When the skill is *deployed* into open-design (`bin/sync-opendesign`), `rsync -L`
dereferences them into real files — necessary because open-design's discovery skips
symlinks. So the source-of-truth is here; the deployed copy is a snapshot.

## Install

### Why we copy instead of symlink

**Symlinks don't work for open-design's discovery.** Both
[`apps/daemon/src/design-systems.ts`](https://github.com/nexu-io/open-design/blob/main/apps/daemon/src/design-systems.ts)
and [`apps/daemon/src/skills.ts`](https://github.com/nexu-io/open-design/blob/main/apps/daemon/src/skills.ts)
scan their root with `readdir({ withFileTypes: true })` and filter on
`entry.isDirectory()`. Node's `Dirent.isDirectory()` returns **false** for
symlinks-to-directories — so symlinked entries are silently skipped.

The fix is a real-file copy with `rsync -L` (which dereferences nested symlinks like
the skill's `references/` pointing back to `brand/facts.md`). Trade-off: edits in
studio-identity don't propagate instantly; you re-run a sync command.

> **TODO upstream:** [submit a PR](https://github.com/nexu-io/open-design) that handles
> symlinks via stat-after-readdir. Once it lands, switch back to the symlink option.

### Option A — `bin/install` does it for you (recommended)

```bash
curl -sL https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/bin/install | bash
```

The installer auto-detects open-design at common paths
(`~/Dev/open-design`, `~/Dev/opendesign`, `~/Code/open-design`, …) and rsyncs the
three artifacts in. Re-run any time to update.

### Option B — manual sync (if open-design is in a non-standard location)

```bash
bash ~/.croissan/identity/bin/sync-opendesign /path/to/your/open-design
```

Or, if you've cloned studio-identity directly:

```bash
bash ~/Dev/studio-identity/bin/sync-opendesign /path/to/your/open-design
```

The script uses `rsync -aL --delete` so deletions in studio-identity also propagate.

### Option C — manual rsync (if you don't want to use our scripts)

```bash
SI=~/Dev/studio-identity
OD=/path/to/open-design

rsync -aL --delete "$SI/integrations/open-design/design-systems/croissan/" \
                   "$OD/design-systems/croissan/"
rsync -aL --delete "$SI/integrations/open-design/skills/croissan-kp/" \
                   "$OD/skills/croissan-kp/"
cp                 "$SI/integrations/open-design/templates/croissan-deck.html" \
                   "$OD/templates/croissan-deck.html"
```

The `-L` flag is critical — without it, the skill's `references/*.md` symlinks
(pointing back to `brand/facts.md` etc.) get copied as broken symlinks instead of
their content.

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

After editing brand artifacts in this repo, run:

```bash
bash ~/.croissan/identity/bin/sync-opendesign        # auto-detects open-design
# or
bash ~/Dev/studio-identity/bin/sync-opendesign /path/to/your/open-design
```

Then refresh open-design's browser tab (or restart its dev server). What propagates:

| You changed… | …reaches open-design after `sync-opendesign` |
|--------------|----------------------------------------------|
| `brand/facts.md` | yes (the skill's `references/facts.md` symlink resolves to it; rsync `-L` dereferences) |
| `agents/anti-ai-slop.md`, `agents/creative-latitude.md` | yes (same path — symlinked into the skill, dereferenced on copy) |
| `brand/voice-and-tone.md`, `brand/proposal-structure.md` | yes |
| `integrations/open-design/design-systems/croissan/DESIGN.md` | yes |
| `integrations/open-design/templates/croissan-deck.html` | yes |
| `integrations/open-design/skills/croissan-kp/SKILL.md` | yes |
| `design-system/decks.md` (internal doc) | NO — decks.md is for humans editing the brand. The spec the open-design agent reads is `DESIGN.md`. Update both deliberately. |

If open-design itself updates its `templates/deck-framework.html` (e.g. the runtime fixes
a new iframe-nav bug), re-fetch and **diff** their version against the verbatim block at
the top of our `croissan-deck.html`. Apply matching changes — but only inside the
"DO NOT EDIT" framework block, never in our token / per-deck styles.

## License & attribution

This integration is internal to Croissan Studio. The open-design framework conventions
it follows are MIT-licensed (see [`nexu-io/open-design/LICENSE`](https://github.com/nexu-io/open-design/blob/main/LICENSE)).
The `templates/deck-framework.html` runtime that we copy verbatim into our deck is
attributed in-file.
