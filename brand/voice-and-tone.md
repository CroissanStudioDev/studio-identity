# Voice & tone

How we sound — in headlines, body copy, CTAs, error messages, emails, decks, and anywhere a human reads us.

> **This file is the SoT for voice.** Other docs surface extracts of this — the
> enforcement layer in [`../agents/content-rules.md`](../agents/content-rules.md), the
> single-file context in [`../SUMMARY.md`](../SUMMARY.md), the open-design portable spec
> in [`../integrations/open-design/design-systems/croissan/DESIGN.md`](../integrations/open-design/design-systems/croissan/DESIGN.md).
> Edit voice principles here first; let the others drift back into sync.

## Core identity

- **Tone**: caring, smart, slightly bold (заботливый, умный, чуть дерзкий).
- **Key message**: «Зовите нас, когда нужен продукт с ИИ».
- **Position**: full-cycle AI studio. **Partner, not vendor.**

## Character

| Trait | What it means |
|-------|---------------|
| Slay, but with soul | Confident expertise without arrogance |
| Cautious, but brave | Thoughtful innovation, not hype |
| Deep, but not boring | Technical depth with human warmth |
| Pleasant, but not vanilla | Friendly with personality, never generic |

## Voice principles

- **Partnership over service** — «в партнёрстве с вами», not «для вас».
- **Human over corporate** — «Бережно собираем идеи», not «Осуществляем сбор требований».
- **Outcomes over features** — describe what the client achieves, not what we deliver.
- **Warmth over formality** — «Будем рады помочь», not «Готовы оказать услуги».
- **Concrete numbers over fuzz** — `15+`, `3+`, `2–4 недели` instead of «много» / «быстро».

## Headlines

- Direct, clear, with personality.
- Use «мы» and «вы» to create connection.
- Soft imperatives are fine («Зовите», «Давайте»).
- Negative tracking (`-tracking-[1.2px]`) for visual punch on H1.

✅ «Зовите нас, когда нужен продукт с ИИ»
✅ «Внедряем ИИ в существующие продукты и создаём новые с нуля»
✅ «Мы делаем продукты и меняем мир бок-о-бок уже 3 года»
✅ «Будем рады помочь вам — зовите, когда нужен продукт с ИИ»

❌ «Профессиональная разработка AI-решений»
❌ «Комплексные услуги по внедрению ИИ»

## Body text

- Lead with benefit or context.
- Conversational but informative.
- Em-dashes («—») for flow.
- Non-breaking spaces before short words («с&nbsp;ИИ», «за&nbsp;2–4&nbsp;недели»).

✅ «Мы ваша заботливая студия полного цикла. Бережно собираем идеи, оборачиваем их в технологии,
тестируем, запускаем — и всё это в партнёрстве с вами.»

❌ «Наша компания предоставляет полный спектр услуг по разработке и внедрению решений на основе
искусственного интеллекта.»

## CTAs

- Action-oriented, friendly, inviting.
- Often use «нам» to emphasize dialogue.

✅ «Написать нам» · «Начать проект» · «Создать бриф» · «Почитать блог» · «Связаться с нашей командой»

❌ «Оставить заявку» · «Заказать консультацию» · «Получить коммерческое предложение»

## Section transitions

- Soft, conversational connectors.
- Invite action without pressure.

✅ «Давайте начнём с вашей идеи. Мы спишемся или созвонимся, чтобы без сложных брифов начать работу»

❌ «Заполните форму для получения консультации»

## Errors and empty states

- Be specific. «Укажите телефон или Telegram», not «Ошибка».
- Stay warm. «Что-то пошло не так — попробуйте ещё раз через минуту» beats «Server error 500».
- Never blame the user.

## What to avoid

- Emoji as icons (use Lucide SVG instead — see [`../identity/iconography.md`](../identity/iconography.md)).
- Englishisms when a Russian word works fine.
- Smileys and exclamation stacks.
- Hyperbole («революционный», «инновационный», «уникальный»).
- Keyword stuffing (also hurts GEO — Princeton research).

## Language

- **Default: Russian.** All client-facing copy is in Russian unless the audience is explicitly English.
- Code, comments, commit messages, and internal docs may be Russian or English — be consistent within
  a single artifact.
- Technical terms (`RAG`, `LLM`, `MCP`, `ИИ-агент`) are fine in Russian text — they signal expertise (+32.7%
  GEO visibility per Princeton).
