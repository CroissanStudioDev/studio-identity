# Decks & presentations — visual spec

Канонический визуальный язык для слайдов: КП (коммерческие предложения), питч-деки,
event-деки. Числа и спеки в этом доке — извлечённые из мастер-фрейма «Самая Новая»;
рабочие исходники (логотипы, мастер-фреймы, фирменные плашки) лежат в приватном
архиве студии — попроси у фаундера, если нужен доступ.

> Для нарративной структуры (какие слайды в каком порядке) — [`../brand/proposal-structure.md`](../brand/proposal-structure.md).

---

## Slide canvas

| Параметр | Значение |
|---------|----------|
| Соотношение | **16:9** |
| Размер | **1280 × 720 px** (это точный размер мастер-фрейма; рендер на 1920×1080 — то же 16:9) |
| Outer padding (default) | **80 px** сверху и слева, **72–80 px** справа, **72 px** снизу |
| Vertical gap H1 → lead | **24 px** |
| Сетка | absolute positioning. Слайды фиксированного размера, не auto-layout, не адаптив |

---

## Surfaces (slide backgrounds)

Три фирменных фона, и одна отдельная поверхность для кейсов:

| Назначение | Фон | Когда |
|-----------|-----|-------|
| Brand (большинство слайдов) | `#2727CA` | Обложки, разделители глав, контент-слайды, тарифы |
| Light | `#FFFFFF` (`--background`) | Логотипо-стрипы, длинные читалки, сравнения |
| Black (премиум-обложки) | `#000000` | Видеозаставки, премиальные обложки, высокий контраст |
| **Graphite (case studies)** | **`#252527`** | Слайды кейсов с product-скриншотами. **Не используй чистый чёрный** — графит мягче для скриншотов |

`#252527` встречается на слайдах кейсов в КП. Это **не** замена чёрному; чёрный остаётся
обложечным фоном. Graphite — рабочая поверхность для слайдов с подложенными скриншотами.

---

## Type scale (real values from the master)

Все размеры — точно как в мастер-фрейме. Tracking везде ≈ -2% ширины символа.

| Роль | Шрифт | Размер | Line-height | Tracking | Цвет |
|-----|-------|--------|-------------|----------|------|
| **H1 (slide title)** — стандартный | **Golos UI Bold** | 90 px | 1.0 | −1.8 px (−2%) | white на brand, brand-dark на white |
| **H1 (case-study)** — облегчённый | **Golos UI Medium** | 90 px | 1.0 | −1.8 px | white, со вторичной частью на 60% (split-color title) |
| **Lead / subtitle** | **Golos Text Regular** | 48 px | 1.2 | −0.96 px | white at **opacity 80%** на тёмных |
| **Caption / pre-strip text** | **Golos Text Regular** | 32 px | 1.2 | −0.64 px | white at 80% |
| **Card body (chip большой)** | **Golos Text SemiBold** | 32 px | 1.2 | −0.96 px | `#BCBCFF` (на brand) или white |
| **Tag / sticker / metric chip** | **Golos UI Medium** или **Inter Medium** | 18 px | 1 / 1.2 | −0.36 px | white |

Notes:
- **Не сокращай 90 px H1**. Если заголовок не помещается — два-три line breaks; если всё ещё не лезет — переписывай заголовок короче.
- Lead имеет `max-width: 800 px` — это удерживает 2–3 строки оптимальной длины.
- На графитном фоне H1 чаще ставится **Medium**, не Bold — заголовок становится менее «крикливым», скриншот рядом важнее.
- **Split-color H1**: основная часть — белая, акцентная (название клиента, NDA, стек) — `rgba(255,255,255,0.6)`. Используется для шапки кейса.

---

## Color tokens *внутри* слайда

На бренд-синем фоне:

| Токен | Значение | Где |
|-------|----------|-----|
| Текст primary | `#FFFFFF` | H1, важное |
| Текст secondary | `#FFFFFF` at opacity 0.8 | Lead, caption |
| Card surface | `linear-gradient(180deg, rgba(14,14,181,0) 0%, rgba(14,14,181,0.3) 100%)` поверх `#2D2DFC` | Number-box / chip |
| Card text | `#BCBCFF` | Текст внутри chip |
| Chip variant — accent | `#2D2DFC` solid | Метрика-«звезда» (главная цифра) |
| Chip variant — muted | `rgba(255,255,255,0.2)` | Соседние метрики |
| Sticker (на фото) | `rgba(0,0,0,0.25)` + `backdrop-blur-[20px]` | «Slides Tag» поверх фото |

На графитном (`#252527`) фоне:

| Токен | Значение |
|-------|----------|
| Placeholder/empty box | `rgba(255,255,255,0.03)`, `rounded-[15px]` |
| Chip — accent | `#2D2DFC` |
| Chip — muted | `rgba(255,255,255,0.2)` |

---

## Reusable components (внутри слайда)

### Number-box / chip (на бренд-фоне)

```
rounded-[32px]
padding: pt-32 pb-28 px-32   (асимметрия — снизу 28, сверху 32)
background: linear-gradient(180deg, rgba(14,14,181,0) 0%, rgba(14,14,181,0.3) 100%)
            on top of solid #2D2DFC
text: Golos Text SemiBold, 32px, tracking -0.96px, color #BCBCFF
height: 87px (фикс)
```

### Polaroid photo card (для команды/портретов)

```
bg: white
shadow: drop-shadow(0px 4px 10px rgba(0,0,0,0.25))
padding: pt-30 pb-40 px-20    ← асимметрия: низ толще (полароид)
rounded-[1px]                 ← минимальный радиус, почти прямоугольник
inner photo:
  rounded-[4px]
  inset shadow: inset 0px 2px 12px rgba(0,0,0,0.1)
rotation: ±2°…±4° (каждый полароид немного разный)
```

### Slides Tag (sticker) — поверх фото

```
backdrop-blur-[20px]
bg: rgba(0,0,0,0.25)
rounded-[100px] (pill)
padding: px-24 py-12
text: Golos UI Medium 18px, line-height 1.2, white
text-shadow: 0px 0px 8px rgba(0,0,0,0.2)
rotation: ±1°…±7° (slightly tossed)
```

### Metric chip (для кейс-стади)

Solid pill, без gradient, без blur:

```
rounded-[100px]
padding: px-24 py-16
text: Inter Medium 18px (or Golos UI Medium), white, line-height 1
gap-[16px] между чипами

variants:
  - accent  : bg #2D2DFC                  (одна «звезда»)
  - muted   : bg rgba(255,255,255,0.2)    (остальные)
```

### Logo strip (под caption)

```
gap: 58 px
opacity: 0.8
heights: 48 px (yandex, t1) или 41–42 px (megafon, positive, …) — оригинальные пропорции, не натягивай
caption above strip: 32 px Regular, line-height 1.2, opacity 0.8
```

---

## Slide kinds — пять реальных шаблонов

Не «жанры», а конкретные шаблоны, которые встречаются в КП:

1. **Cover** — H1 (90 Bold) + 3D mark inline + caption «Гордимся теми…» + logo strip снизу. Бренд-фон.
2. **Section divider** — тот же H1+lead layout, что и cover, но без логотипов. Лид — одной строкой («Дальше — часть успешных решений от нас»). Много пустоты — это пейс.
3. **Content with chips** — H1 + lead + 2×2 grid из number-box'ов. Используется для «что мы делаем», «процесс», «команда (роли)».
4. **Team intro** — H1 + полароидные фото + плавающие sticker'ы с фактами о людях. Самый «человеческий» слайд деки.
5. **Case study** — graphite `#252527` фон, **H1 Medium с split-color**, lead, metric chips, скриншот-карточка с лёгким наклоном, иногда ручная стрелка-аннотация.

Никогда не запускай больше **3 одинаковых kind подряд** — пейс плоский. Чередуй: cover →
divider → content → case → case → divider → content.

---

## Photos & screenshots

- Команда — полароидные карточки (см. компонент выше).
- Скриншоты продуктов — слегка повёрнутые карточки на graphite-фоне, без полароидной рамки.
- Декоративные стрелки/обводки — **рукодельные SVG**, не lucide. Выглядят как «нарисовано
  маркером». Поворачивай на странные углы (`-151.53deg` — ок).
- Все фото — реальные. Никаких stock-изображений.

---

## Russian niceties (в любом тексте)

- Em-dashes (`—`), не дефис.
- Русские кавычки «…».
- Non-breaking spaces (`&nbsp;`) перед короткими предлогами и однобуквенными словами:
  «с&nbsp;ИИ», «за&nbsp;2-4&nbsp;недели».
- Числа отделяй неразрывным пробелом: «110&nbsp;000 пользователей».

---

## Don'ts

- ❌ Drop-shadow'ы под текстом и карточками. Только под полароидами и стикерами.
- ❌ Stock-фото. Реальная команда, реальные скриншоты, реальные клиенты.
- ❌ Эмодзи в качестве иконок и декора.
- ❌ Mid-grey фоны. Только: brand, white, black, или graphite `#252527` (для кейсов).
- ❌ Заголовки меньше 90 px. Если не помещается — переписывай короче.
- ❌ Менять mark с 2D-флэта на 3D в одной деке туда-сюда — выбери один режим.
- ❌ Auto-layout «по-умному» — мастер на абсолютном позиционировании, дублируй фрейм и правь.
- ❌ Микшировать «Studio» и «Community» wordmark в одной деке.

---

## Universal slide chrome (применяется на каждом слайде)

Не зависит от типа слайда — это «рамка» всей деки:

| Элемент | Где | Спецификация |
|---------|-----|-------|
| Brand mark + wordmark | top-left, на каждом слайде | 28 px SVG + «Круассан Студио» в Golos Text Bold ≈14–16 px, gap 0.55em |
| Page number | bottom-right, на каждом слайде | `01 / 11` формат, Golos Medium ≈12–13 px, letter-spacing 0.16em (uppercase tracked), `font-variant-numeric: tabular-nums`, цвет — `paper-mute` (white at 55%) |
| Outer padding | весь фрейм | 7vh top/bottom, 6vw left/right (на 1920×1080 → ≈ 75.6 px / 115.2 px) |

Brand mark + wordmark **никогда не убираются** — даже на cover, даже на section-divider.
Page number обновляется руками при изменении количества слайдов.

---

## Pill / chip variants — пять штук, не больше

Pill — это **подпись** деки. Везде один shape (`rounded:999px`, `padding ≈ .85em 1.25em`,
Golos Medium ≈ 1vw), различаются только заливкой:

| Класс | Использование |
|-------|---------------|
| `pill.dark`    | bg `#0E0E14`, white text. Заголовок кейса, тег с акцентом |
| `pill.light`   | bg white, brand-blue text. CTA-чип, контактные пиллы |
| `pill.outline` | прозрачный, тонкая белая обводка (45%). Метаинформация: «3 недели», «Под ключ» |
| `pill.soft`    | bg `#3D3DE0` (cobalt-soft). Список услуг, гардероб, теги опций |
| `pill.deep`    | bg `#1F1FA8` (cobalt-deep). Альтернатива `soft` для контраста |

Хочется добавить шестой вариант — **сначала спроси**. Чем меньше, тем лучше пейс.

### Floating black badge

Pattern «лейбл над списком пиллов». Чёрный pill всплывает над сеткой soft-пиллов — как
наклейка-стикер. Используется на «one-stop shop» слайде («В&nbsp;них мы особо хороши»).

```css
.badge-floating { position: relative; }
.badge-floating .lab {
  position: absolute; top: -.85em; left: 1.2vw;
  background: #0E0E14; color: white;
  font-size: ~12px; padding: .5em .85em; border-radius: 999px;
}
```

---

## Card variants — три

Карточка на cobalt-фоне. Используется в «режимы», «этапы», «инфраструктура».

| Класс | Когда |
|-------|-------|
| `card` (default) | bg `#0E0E14` (ink), `rounded-[18px]`, padding `2.6vh 1.6vw`. Стандарт |
| `card.featured` | bg white, текст brand-blue. Рекомендуемый вариант / звёздный режим / featured tier |
| `card.outline` | прозрачный, тонкая обводка (`var(--line)` = white at 18%). «Минимум» / альтернатива |

Внутри карточки три текстовых уровня:

```
.lbl  — uppercase tracked label (.14em letter-spacing, ~12px)
.ttl  — title in Golos Bold ~1.7vw
.desc — body in Golos Regular ~1vw, цвет paper-dim (white at 72%)
```

Цена в карточке этапа — `.price` в Golos 800, ~2vw, `tabular-nums`, `margin-top: auto`
(приклеена ко дну карточки).

---

## Stage-row — построчный pricing breakdown

На отдельном «итого» слайде разбиваем стоимость в строки с разделителями:

```
.stage-row {
  display: grid; grid-template-columns: auto 1fr auto;
  padding: 1.8vh 0;
  border-top: 1px solid var(--line);
}
.stage-row .num-lbl  /* «Этап 01», uppercase tracked */
.stage-row .nm       /* название, Golos SemiBold ~1.25vw */
.stage-row .pr       /* цена, Golos Bold ~1.4vw, tabular */
```

Под строками — финальная цифра в `.price-final`:

```
font-weight: 800;
font-size: ~9.5–11vw;
font-variant-numeric: tabular-nums;
letter-spacing: -.04em;
align: right;
```

Это единственное место, где допустим такой огромный размер шрифта. На обычных слайдах
80%+ ширины зарезервировано для текста, не цифры.

---

## Demo-grid — 4-кадровое демо

Используется когда нужно показать «один поток → разные результаты» (например, до/после
или несколько вариантов):

```
.demo-grid {
  display: grid; grid-template-columns: repeat(4, 1fr); gap: 1vw;
}
.demo-grid figure .img {
  aspect-ratio: 1/1; border-radius: 14px; overflow: hidden;
}
.demo-grid figure .cap {
  display: flex; justify-content: space-between;
  font-weight: 500; ~12px; color: paper-dim;
}
.demo-grid figure .cap .k { font-weight: 700; color: white; }
```

Каждый кадр — `<figure>` с подписью под ним: жирный «ключ» слева, метаинфа справа.

---

## Print / PDF export — обязательно

Деки **экспортируются в PDF** для отправки клиенту. CSS-template уже это умеет — не
выкидывай этот блок:

```css
@media print {
  @page { size: 1920px 1080px; margin: 0; }
  .slide {
    width: 1920px !important; height: 1080px !important;
    padding: 75.6px 115.2px !important;
    page-break-after: always;
  }
  #nav, #hint, #overview { display: none !important; }
}
```

Открыть в Chrome → Print → Save as PDF → формат A0 (или Custom 1920×1080) → готово.
Без этого блока vh/vw у тебя поедут под viewport принтера.

---

## Workflow

Два пути в зависимости от деки:

### Дизайнерский путь (мастер-фреймы в приватном архиве студии)

1. Дублируй последний шипнутый КП из приватного архива (или мастер «Самая Новая»). Не
   начинай с пустого листа.
2. Цифры и имена — из [`../brand/facts.md`](../brand/facts.md).
3. Структура: см. [`../brand/proposal-structure.md`](../brand/proposal-structure.md).
4. Экспорт — PDF 1× → клиент.

### HTML-путь ([`../assets/deck-template/`](../assets/deck-template/))

1. Скопируй `index.html` в новую папку.
2. Открой в браузере. Найди все `{{плейсхолдеры}}` и замени.
3. Поправь page numbers (`pn` спаны), если меняешь количество слайдов.
4. Print → Save as PDF.

Когда какой использовать — см. [`../assets/deck-template/README.md`](../assets/deck-template/README.md).
