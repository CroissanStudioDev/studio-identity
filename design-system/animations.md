# Animations

Restraint over flair. Animations exist to communicate state changes — not to entertain.

## Rules

- **Duration**: 150–300 ms for micro-interactions. Anything longer feels broken.
- **Properties**: animate **only `transform` and `opacity`**. Never `width`, `height`, `top`, `left` —
  they trigger layout and tank performance.
- **Reduced motion**: `prefers-reduced-motion` is respected globally in `globals.css`. Don't override.
- **Easing**: default Tailwind `ease-out` is fine; `ease-in-out` for symmetric loops.

## Transitions

```tsx
className="transition-all duration-300"        // standard
className="transition-colors"                  // color-only changes
className="transition-transform duration-300 ease-out"
```

## Hover effects

```tsx
className="hover:bg-[var(--brand-primary-hover)]"
className="hover:scale-105"          // cards
className="hover:opacity-90"         // images
className="group-hover:text-primary-60"  // when inside a `group`
```

## Custom keyframes

Defined in `globals.css`. Use sparingly:

```css
@keyframes pulse-right { /* used by focus cards */ }
.animate-pulse-right { animation: pulse-right 1.5s ease-in-out infinite; }
.focus-card-3d { transform: rotateX(...) rotateY(...) ... }
```

If you add a new keyframe, add `will-change: transform` and `backface-visibility: hidden` like the
existing ones — keeps it on the GPU.

## motion (framer-motion successor)

We use [`motion`](https://motion.dev) for drag interactions and complex sequences. Live example:
`components/sections/poloroids.tsx`.

**Hydration gotcha**: when a `motion.div` has an `initial` prop or animates `style.x`/`style.y`,
add `suppressHydrationWarning`. `motion` rounds transforms to 3 decimals on SSR but uses full
precision on the client, which produces a benign-but-noisy hydration diff.

```tsx
<motion.div suppressHydrationWarning style={{ x: 100, y: 50 }} />
```

## Don'ts

- Don't animate page-load (entry) of every section — it gets old fast and hurts LCP.
- Don't chain animations longer than ~600 ms total.
- Don't ignore `prefers-reduced-motion` for "important" animations. There is no exception.
