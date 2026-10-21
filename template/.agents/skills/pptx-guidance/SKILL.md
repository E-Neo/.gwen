---
name: pptx-guidance
description: Use when an Agent needs to generate or improve a PowerPoint presentation (.pptx). Complements the gwen skill, which covers tool usage.
---

# Slide writing guidance

We are the technology insights team of an infrastructure-software company.
A deck must have "logic" - logic here usually means a *story* that reads
smoothly and holds together. A deck is not a flat list of facts: it should
combine objective facts with a point of view on trends.

## Research

Keep the research, not just the deck. Every fact that reaches a slide should be
traceable back to something you wrote down.

- **`references/` is the source of truth.** When you search the web, write what
  you found into Markdown files under the project's `references/` - links,
  quotes, dates, and the numbers you extracted, with the question you were
  answering at the top of each file. Write slides from those files, not from
  memory: a later reader must be able to re-check a claim without repeating the
  search.
- **`references/media/` holds the raw material.** Screenshots, diagrams and
  charts collected while researching go there, each with its origin recorded in
  the Markdown file that cites it.
- **`media/` holds only what ships.** Copy an asset into `media/` when a slide
  actually uses it, so the build depends on nothing outside the project.

These are the project's paths, not this skill's: `references/` next to this file
holds layout examples, not research.

## Overall structure

A complete deck usually contains a cover, chapter pages, and an end page.
Larger decks (dozens of pages) add a contents page before each chapter.

The structure follows "macro -> micro -> macro". Chapter pages fall into
three roles:

- **Hat pages** - the overview that leads into the next run of pages;
  typically one before each chapter.
- **Content pages** - the body of the argument.
- **Insight pages** - the takeaway of the preceding content; usually one
  final insight page right before the end page.

## Anatomy of a single slide

A slide is made of three parts: a **title**, **body**, and a **takeaway**
(the insight).

Typography defaults: font `Microsoft YaHei`. Do not put a space between
digits/Latin letters and Chinese characters. Avoid obviously
AI-generated-looking punctuation such as `·`, `「」`, `『』`.

### The title is a claim

The title must state a point directly - typically "an observation + what the
observation implies". A topic keyword is not a title.

- Bad: "NV G3.5 Technical Introduction"
  - Why: this is only a keyword. A reader scanning titles gets no
    information, and many readers only ever read the title - if the title is
    weak, the slide is lost.
- Good: "NV adds a G3.5 layer - GPU connects to remote storage directly to
  accelerate inference, long-context Agent workloads see TPS 5×↑"
  - Why: it names the observation ("NV adds a G3.5 layer"), briefly explains
    the new term (GPU connecting to remote storage to accelerate inference),
    then says what it means and what it's worth. Quantify whenever possible
    ("TPS 5×↑", "cost 50%↓").

Default title style: 24pt bold red (`C7000A`), left-aligned, at the top of
the slide, ideally a single line.

### Body

The body is flexible and information-dense, but it must have logic, and each
page carries exactly one logical thread. Common patterns:

- **Bad -> Good**: the left side explains what is wrong with the current
  state (AS-IS / others / ...), the right side explains the better state
  (TO-BE / ours / ...) and its value, joined by a small grey arrow (about
  2 x 2cm); keep the arrow small and the two panels full-height.
- **Phased evolution**: give the characteristics and representative of each
  phase, then derive the needs of each phase below, and finally the future
  trend. See [`references/phase-evolution.toml`](references/phase-evolution.toml)
  and [`references/cards.toml`](references/cards.toml).
- **Macro -> micro**: a big logic on the left, expanded into several small
  logics on the right. For example: an AS-IS -> TO-BE on the left with two or
  three resulting technology trends on the right; or a software stack with a
  few key points marked in red (`➊➋➌...`) and the points expanded on the
  right. A common asset for macro -> micro layouts is the perspective floor
  (in `media/`): it "opens" toward the detail, so rotate it so the
  trapezoids' **long side points at the details** and the **short side
  points at the macro side**; it works well as a visual separator between a
  stack and its annotation column.
- **Classification**: split the topic into several relatively independent
  small logics along some dimension; each block tells its own story.

The body is case-by-case, but these reusable building blocks cover most
patterns:

- **Pentagon + chevron combo** for phased evolution as the upper half of the
  page; list each phase's characteristics and needs below.
- **Staircase** for phased evolution.
- **Block diagrams** - this is the style most readers respond to. Any logic
  expressible as boxes (software stacks, architecture) should be drawn as
  boxes. See [`references/stack.toml`](references/stack.toml).
- **Label + content boxes**, two variants:
  - Equal-width cards: the label is black bold, centered, in a borderless
    `#ccecff` box; the content box is `#f2f2f2`-filled with a `#d3d3d3`
    border. Use the `card_header` / `card_body` named styles (defined in the
    template's `main.toml`). See [`references/cards.toml`](references/cards.toml).
  - Label riding the top edge: the label is `#0000ff` bold, white fill, no
    border, centered, straddling the top edge of a round rectangle
    (`rect_radius` 0.1) with a `#d3d3d3` border and white fill. Use the
    `frame` / `frame_label` named styles. See
    [`references/frames.toml`](references/frames.toml).
  - Use one variant consistently within a page; different pages may use
    different variants for variety. A label must still be a claim, not a bare
    keyword.
- **Tables**: a table is for contrast - one simple logic, usually two options
  compared across a few shared dimensions. Draw the grid with `line` shapes
  and the cells with `text` shapes (no header fill, no vertical bars, small
  cell margins), keep it to about a quarter of the slide, and put it inside a
  frame card. A table rarely owns a slide - the rest of the slide should read
  the table. See the third frame of
  [`references/frames.toml`](references/frames.toml).

### Numbers

A number is the strongest thing on a slide, so it has to be earned twice.

- **Every quantified number carries a source.** A figure with no source is a
  guess the reader cannot check. Name the source in the `source` style
  (10.5pt grey italic) on the slide, and keep the supporting detail in
  `references/`.
- **Never let a number stand alone.** A big bold figure floating in the middle
  of a card or frame says nothing: no unit, no comparison, no consequence. Put
  it in a sentence that gives what it measures, what it is compared with, and
  what follows from it.
- **Write change as value + arrow + dimension.** The arrow always sits
  immediately after the value; the word after it names the dimension that
  moved. Drop "up" and "down" - the arrow already says the direction.
  - `TPS 5×↑`, `5×↑ faster`, `50%↓ cheaper`, `latency 40%↓`,
    `tokens 3×↑ per request`.
  - Multiples take `×`, shares take `%`; keep the unit attached. Dimensions
    such as `33.88 x 19.05cm` are not changes and keep their plain `x`.
  - An arrow states direction, not good news: `error rate 5%↑` is bad,
    `cost 50%↓` is good. The dimension word has to make clear which one you
    mean.
- **Emphasize inside the sentence.** Bold red or blue on the value and arrow is
  fine - **5×↑** - but the sentence does the work, not the type size.
- **Bad:** a card containing `5×↑` and the label "faster".
- **Good:** "Long-context Agent inference runs **5×↑** faster once the GPU
  reads remote storage directly." (source: ...)

Numbers must agree wherever they appear - title, body, takeaway, `references/`.
Round the same way each time, and do not silently swap one metric for another.

### Layout principles

- **Balance and symmetry.** Work out the geometry against the slide size: a
  13.34 x 7.5in deck is 33.88 x 19.05cm, the horizontal centre is 16.94cm,
  and the content region is roughly 2.7-15.9cm (takeaway at ~16.25cm).
  Prefer symmetric columns, e.g. left `x = 1.5cm, w = 15cm` and right
  `x = 17.4cm, w = 15cm`, so the margins mirror each other. A lopsided
  layout reads as unfinished.
- **Margins on text.** Any shape carrying text needs an inner margin so the
  text does not touch the edges; the default is
  `margin = ["0.13cm", "0.25cm", "0.13cm", "0.25cm"]`
  (top/right/bottom/left). To position text precisely instead, split the
  shape: one `rect` for the border (no text) plus a separate `text` shape
  you place yourself (then `margin = 0`).
- **Stack diagrams.** Keep the stack to about half the slide and explain it
  on the other half. Annotate **components**, not just layers: put a circled
  number on the specific box (e.g. above a particular product) and explain
  that component next to the stack. See
  [`references/stack.toml`](references/stack.toml).

Body font is generally 12pt; important parts are bold red or blue. Sources
are 10.5pt grey italic (`#a3a3a3`). Keep the palette small - black, white,
red, blue, grey - and use red/blue for emphasis only, sparingly.

Our slides are information-dense; avoid obvious empty areas. Write body text
to support the title and takeaway, not for its own sake: every item should
relate logically to the rest of the page.

### The takeaway is a claim

The takeaway sits at the bottom of the slide and is the landing point of the
whole page. Some readers look at only the title and the takeaway, so it
deserves the same care as the title.

A takeaway usually has two parts: **so-what** and **now-what** - the first
half summarizes the trend, the second half suggests a direction.

Default takeaway style: 16pt bold blue (`#0000ff`), horizontally centered,
ideally a single line of at most 50 characters.

## Review

A page is finished when the measure says it is dense, the logic says it holds,
and your eyes say it draws cleanly - in that order.

### Density first

Run `gwen measure` before you open the rendered deck. It reports composition and
content facts per slide, so a half-empty region shows up as a number instead of
something you miss while skimming.

```sh
gwen measure            # every slide
gwen measure --page 4   # one slide while iterating
```

Empty space is not "clean" or "breathing room": read `whitespace`, `largest_void`
and `density` - a large void away from the edges, or a page much less dense than
the rest of the deck, is the empty space you would have missed by eye. Fill it
with evidence, a second column, an annotation or a wider panel - then measure
again. Open the `.pptx` only once the numbers look right; measure finds
emptiness, your eyes find collisions, overflow and bad line breaks.

### The logic pass

Reading order is the reader's only path through the page. After every edit, read
the deck top to bottom and test three levels:

- **Sentence.** Does each sentence follow from the one before it? A claim needs
  its evidence within reach.
- **Page.** Does every element serve the title, and does the body land on the
  takeaway? Anything that does not carry the thread is cut or moved, not
  decorated.
- **Deck.** Do the pages build macro -> micro -> macro, without repeating or
  contradicting each other?

Two failures to hunt for:

- **Internal inconsistency.** A figure, name or claim means the same thing
  everywhere, in every slide and in the sources. If two pages disagree, one of
  them is wrong.
- **Unpaid setups.** Raise it or drop it. A term, example or question you
  mention and never develop leaves the reader waiting; a mention you do not pay
  off is worse than no mention. Define an obscure term in a few words the first
  time it appears, before you argue with it.

Then read it again. The logic of each sentence, each page and the whole deck is
polished, not written.
