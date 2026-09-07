# AM Brew — Two Ways to Start With ₱5,000

A group presentation on the two reasoning paths an entrepreneur can take — **effectual**
(start from the means you already have) and **causal** (start from the goal and work
backward) — worked through one business we could actually start this week: morning coffee
and homemade cookies, sold before the 7:30 class.

Ten slides that also read as a normal web page on a phone.

**Entrepreneurial Mind · GEE 2000 · Section 66105**
Javier, Daniel L. · Balada, John Melvin A. · Francisco, Caine Wesley M. · Rafael, Juan
Miguel L. · Musa, Joshua Johan

## Live site

> https://unorfl.github.io/am-brew/

## Viewing it

| | |
|---|---|
| **Desktop / laptop** | `←` `→` or `Space` to move between slides. Thumbnail rail on the left. `Ctrl/⌘ + P` prints or saves one slide per page. |
| **Phone or tablet, landscape** | Full-screen deck. Swipe or tap the left/right half of the screen. The ⛶ button goes fullscreen. |
| **Phone or tablet, portrait** | Opens the reading view — the same material as one scrollable page, because a 16:9 slide in portrait puts body text at about 5px. Tap **Slides** for the deck, **Read** to come back. |

The URL tracks the current slide (`#1` … `#10`), so you can link someone straight to one
slide. Each slide also carries speaker notes in the file, one line on what to say.

## The numbers, in one place

| | |
|---|---|
| Iced coffee | ₱60 a bottle, earns **₱35** |
| Cookies | ₱35 a pack, earns **₱20** |
| Start-up | **₱3,500** of the ₱5,000 — ₱700 each from five of us. ₱1,500 kept back to restock. |
| The goal | **₱6,000 a month** by December → ₱1,500 a week → ₱500 a day → **10 bottles + 8 cookie packs**, three days a week |
| Stop rule | Three weeks. Half the ₱3,500 back, or we stop and sell the bag. |

Everything on the deck hangs off those first two lines, so if your costs are different,
change them there first and the rest follows.

## Slides

| | | |
|---|---|---|
| 01 | Cover | AM Brew, the group, the ₱5,000 |
| 02 | The Two Paths | Effectual vs causal — what each one decides by |
| 03 | Three Options | Coffee & cookies, cookies only, iced tea only |
| 04 | What We Risk | ₱3,500, and the stop rule |
| 05 | This Week | **The first action — five days, five jobs, ₱0 spent until Friday** |
| 06 | Goal Backward | ₱6,000 a month divided down to one bag a day |
| 07 | The Market | Our own building before the 7:30, and how the handover works |
| 08 | The Plan | **The execution steps — four months, one job and one number each** |
| 09 | Both Paths | Which path answered which question |
| 10 | Thank You | |

Slides 05 and 08 are the detailed ones on purpose. The rest are deliberately broad —
they are prompts to talk from, not scripts to read.

## Before you present it

The peso figures are our own estimates, not quotes from a supplier. Check them where you
actually shop and adjust slides 03, 04, 05 and 06 to match.

## Publishing (GitHub Pages)

Already on: **Settings → Pages → Deploy from a branch**, branch `main`, folder
`/ (root)`. Any push of `index.html` goes live at the URL above within about a minute.
Nothing needs a build step or a server on the hosting side — it is one self-contained
HTML file.

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
| `slides.html` | The ten 1920×1080 artboards. **Edit this for slide content.** |
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
