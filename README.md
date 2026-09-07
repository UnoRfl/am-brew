# Two Ways to Start With ₱5,000

An individual activity on the two reasoning paths an entrepreneur can take — **effectual**
(start from the means you already have) and **causal** (start from the goal and work
backward) — run through one business a Philippine college student could actually start
this week. Built as an eleven-slide presentation that also reads as a normal web page on
a phone.

**Entrepreneurship · Individual Activity**

| | |
|---|---|
| **The business** | Kape sa Klase — pre-ordered iced coffee, one building, three days a week |
| **Effectual answer** | Three things ₱5,000 could start, one picked, five dated actions this week, ₱3,800 of affordable loss with a written stop rule |
| **Causal answer** | ₱6,000 net profit a month by December, divided back down to 24 cups a day, with the market, the strategy and four months of execution steps |

## Live site

> https://unorfl.github.io/entrep-5k-start/

## Viewing it

| | |
|---|---|
| **Desktop / laptop** | `←` `→` or `Space` to move between slides. Thumbnail rail on the left. `Ctrl/⌘ + P` prints or saves one slide per page. |
| **Phone or tablet, landscape** | Full-screen deck. Swipe or tap the left/right half of the screen. The ⛶ button goes fullscreen. |
| **Phone or tablet, portrait** | Opens the reading view — the same material as one scrollable page, because a 16:9 slide in portrait puts body text at about 5px. Tap **Slides** for the deck, **Read** to come back. |

The URL tracks the current slide (`#1` … `#11`), so you can link someone straight to one
slide.

## Slides

| | | |
|---|---|---|
| 01 | Cover | Same money, two starting points |
| 02 | The Two Paths | Effectual vs causal, side by side — what each one decides by |
| 03 | Means at Hand | Who I am, what I know, who I know, and the ₱5,000 |
| 04 | Three Options | Three things ₱5,000 can start, with capital and margin for each |
| 05 | The Choice | Option 01, and the five dated actions for this week |
| 06 | Affordable Loss | ₱3,800, what I will not risk, and the stop rule |
| 07 | Goal Backward | ₱6,000 a month ÷ ₱23 a cup ÷ 12 selling days = 24 cups a day |
| 08 | The Market | Three floors, one building, 7:30 AM — and who is *not* the market |
| 09 | The Plan | The strategy in one line, then four months and four numbers |
| 10 | Both Paths | Which path answered which question |
| 11 | Thank You | |

## Before you present it

Two things are deliberately generic, because they are yours to fill in:

- **Your name and section.** The cover and the closing slide say *Entrepreneurship ·
  Individual Activity* and nothing more. Add your name in `build/parts/slides.html` (slide
  01's bottom block and slide 11) and `build/parts/mv.html` (the hero and the closing
  card), then rebuild.
- **The prices.** Every peso figure is a real quote from a grocery and an online
  packaging seller in the first week of September 2026, and the deck says so on slide 05.
  Re-quote them where you actually shop — the arithmetic on slides 05, 06 and 07 all
  hangs off ₱40 a cup and ₱17 of cost, so if your cost moves, `₱23` and `24 cups a day`
  move with it.

## Publishing (GitHub Pages)

Already on: **Settings → Pages → Deploy from a branch**, branch `main`, folder
`/ (root)`. Any push of `index.html` goes live at the URL above within about a minute.
Nothing here needs a build step or a server on the hosting side — it is one
self-contained HTML file.

## What's in the repo

| File | |
|---|---|
| `index.html` | The whole thing — slides, reading view, styles, scripts and the runtime, no external requests. |
| `favicon.svg` | Tab icon: one stem, two branches. |
| `og-cover.jpg` | Preview image used when the link is shared. |
| `build/` | The sources `index.html` is assembled from. Only needed if you want to change the content. |

## Editing the content

`index.html` is generated, so do not edit it by hand — the deck is authored as parts and
assembled:

```bash
cd build
python build.py        # rewrites ../index.html
python make-cover.py   # rewrites ../og-cover.jpg (needs Pillow)
```

| `build/parts/` | |
|---|---|
| `slides.html` | The eleven 1920×1080 artboards. **Edit this for slide content.** |
| `mv.html` | The portrait reading view — the same material reflowed. **Edit this too**, so both stay in sync. |
| `helmet.html` | The design system: palette, type scale, reading-view CSS. |
| `tail.html` | Entrance replay, pointer glow, swipe, rail and hash routing. |
| `loader.html` | The `<head>` and the script that unpacks the runtime into blob URLs. |
| `assets.html` | The runtime itself, gzipped and base64'd: React, the x-dc runtime, `deck-stage`. |

## How it renders

The deck is a Claude Design canvas: each slide is an absolutely positioned 1920×1080
artboard, and `deck-stage` scales the active one to fit whatever viewport it lands in, so
the same file is a projector deck, a laptop window and a phone screen. The palette is
`#161619` ground, `#F3F3F1` type, `#E2545C` accent, with ambient radial gradients drifting
behind each slide — the drift only runs on the slide you are looking at, and stops
entirely under `prefers-reduced-motion`.

Every slide was checked to fit its own frame: the artboards are 1080px tall and nothing
inside them overflows, so no line is clipped at any window size.
