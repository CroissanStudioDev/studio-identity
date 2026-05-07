# Accessibility

Non-negotiable. WCAG **AA** is the floor.

## The nine rules

1. **`aria-label` on icon-only buttons.**
   ```tsx
   <button aria-label="Закрыть меню">
     <X aria-hidden="true" />
   </button>
   ```

2. **`aria-hidden="true"` on decorative icons** that sit next to text already conveying the meaning.
   ```tsx
   <Zap aria-hidden="true" size={20} /> Скорость
   ```

3. **`aria-pressed` on toggle buttons.**
   ```tsx
   <button aria-pressed={isActive}>…</button>
   ```

4. **External links carry `rel="noopener noreferrer" target="_blank"`.** Mandatory.

5. **Heading hierarchy: H1 → H2 → H3** without skip-levels. Exactly **one `<h1>`** per page.

6. **Touch targets ≥ 44×44 px.** `<Button>` enforces this; for custom controls, use padding.

7. **Contrast.** Minimum `text-primary-60` on the light background. On dark or colored backgrounds,
   manually check **4.5:1** for body text, **3:1** for large/H1.

8. **Error states.**
   ```tsx
   <p role="alert" className="text-error text-sm">Укажите телефон или Telegram</p>
   ```
   Concrete and actionable. «Ошибка» is not an error message.

9. **Form labels.** Every input has a real `<label htmlFor="id">` matching `<input id="id">`.
   Placeholder-only labels are a hard fail.

## Forms — extra checks

- Required fields are marked visually **and** programmatically (`required`, or `aria-required="true"`).
- Submit button text says what it does («Отправить», «Создать бриф») — never «OK».
- After submit, focus moves to the response (success message or first error).

## Motion

`prefers-reduced-motion` is wired globally in [`design-tokens.css`](design-tokens.css). Animations
collapse to ~0ms automatically. Don't override.

## Keyboard

- Every interactive element is reachable with `Tab`.
- `focus-visible:ring-[3px]` is built into our buttons. Custom interactive elements must show a focus
  ring (`focus-visible:outline-2 focus-visible:outline-brand` minimum).
- Modals trap focus and restore it on close. Use shadcn's `Dialog`, which handles this.

## Pre-ship a11y checklist

- [ ] Tab through the page top to bottom — no traps, every focus visible.
- [ ] Run Lighthouse Accessibility — 100. Anything less is a real defect.
- [ ] Keyboard-test every modal: open, navigate, close, focus restored.
- [ ] Screen-reader spot check: VoiceOver reads each section in order, with sensible labels.
- [ ] Zoom to 200% in Chrome — layout doesn't break, no horizontal scroll.
