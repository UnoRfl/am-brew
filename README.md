# AM Brew — Two Ways to Start With ₱5,000

A group presentation on the two reasoning paths an entrepreneur can take — **effectual**
(start from the means you already have) and **causal** (start from the goal and work
backward) — worked through one business we could actually start this week: morning coffee
and homemade cookies, sold before the 7:30 class.

Twelve slides that also read as a normal web page on a phone — including what could
kill the business, and where our own plan is still thin.

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
| **Phone or tablet, portrait** | Opens the reading view — the same material as one scrollable page, because a 16:9 slide in portrait puts body text at about 5px. The bar names the section you are in and opens an index that jumps to any of the twelve; a hairline under it tracks how far through you are, and an arrow returns you to the top. Tap **Slides** for the deck, **Read** to come back. |

The URL tracks the current slide (`#1` … `#12`), so you can link someone straight to one
slide; `#r1` … `#r12` do the same for the reading view. Each slide also carries speaker notes in the file, one line on what to say.

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
| 09 | What Could Go Wrong | **The risks** — demand, food safety, people, money, and the ₱0 fix for each |
| 10 | Where It Is Thin | **The gaps in our own plan**, named before anyone else names them |
| 11 | Both Paths | Which path answered which question |
| 12 | Thank You | |

Slides 05 and 08 are the detailed ones on purpose. The rest are deliberately broad —
they are prompts to talk from, not scripts to read.

Slides 09 and 10 do different jobs. **09 is the business risk**: four things that could
end AM Brew, each with the one thing we do about it — and every one of those costs
nothing, because with five people and ₱3,500 not spending is the only insurance
available. **10 is the honest audit of the deck itself**: the prices are estimates and
not quotes, ₱6,000 a month assumes every week is a normal week, none of us has baked to
a deadline, and one insulated bag is a ceiling nobody has costed past.

## Before you present it

The peso figures are our own estimates, not quotes from a supplier. Check them where you
actually shop and adjust slides 03, 04, 05 and 06 to match — slide 10 says so out loud,
so the numbers on the deck should be real by the time you present it.

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

On a phone the reading view is what first paints, before `deck-stage` has even upgraded,
so a portrait screen never flashes a letterboxed slide on its way there. That also means
the reading view is reachable even if the shell never mounts at all — which is what used
to happen: the shell waited for `deck-stage` with `requestAnimationFrame` against a 20s
wall-clock budget, and rAF is throttled to nothing in a tab that is not visible, so a
link opened in a background tab burned the budget without a single poll and came up with
no **Read** button, no swipe and no fullscreen. It polls on a timer now, and picks the
tab back up on `visibilitychange`.
