---
name: pptx-guidance
description: Use when an Agent needs to generate or improve a PowerPoint presentation (.pptx). Complements the gwen skill, which covers tool usage.
---

# Slide writing guidance

We are the technology insights team of an infrastructure-software company.
A deck must have "logic" - logic here usually means a *story* that reads
smoothly and holds together. A deck is not a flat list of facts: it should
combine objective facts with a point of view on trends.

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

Typography defaults: font `Microsoft Yahei`. Do not put a space between
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
  accelerate inference, long-context Agent workloads see TPS up 5x"
  - Why: it names the observation ("NV adds a G3.5 layer"), briefly explains
    the new term (GPU connecting to remote storage to accelerate inference),
    then says what it means and what it's worth. Quantify whenever possible
    ("TPS up 5x", "cost down 50%").

Default title style: 24pt bold red (`C7000A`), left-aligned, at the top of
the slide, ideally a single line.

### Body

The body is flexible and information-dense, but it must have logic, and each
page carries exactly one logical thread. Common patterns:

- **Bad -> Good**: the left side explains what is wrong with the current
  state (AS-IS / others / ...), joined by a wide, borderless grey arrow; the
  right side explains the better state (TO-BE / ours / ...) and its value.
  See [`references/bad-to-good.toml`](references/bad-to-good.toml).
- **Phased evolution**: give the characteristics and representative of each
  phase, then derive the needs of each phase below, and finally the future
  trend. See [`references/phase-evolution.toml`](references/phase-evolution.toml)
  and [`references/staircase.toml`](references/staircase.toml).
- **Macro -> micro**: a big logic on the left, expanded into several small
  logics on the right. For example: an AS-IS -> TO-BE on the left with two or
  three resulting technology trends on the right; or a software stack with a
  few key points marked in red (`➊➋➌...`) and the points expanded on the
  right. A common asset for macro -> micro layouts is
  ![perspective-floor](references/perspective-floor.svg) - rotate it so the
  short edge faces the "macro" side and the long edge the "micro" side.
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
  - Equal-width boxes: the label is black bold 14/16pt in a borderless
    `#ccecff` box; the content box is `#f2f2f2`-filled with a `#d3d3d3`
    border. See [`references/title-content-boxes.toml`](references/title-content-boxes.toml).
  - Label riding the top edge: the label is `#0000ff` bold 14/16pt, white
    fill, no border, and kept narrow so there is not much dead space; the
    content is a round rectangle (`rect_radius` 0.1) with a `#d3d3d3` border
    and no fill. See [`references/title-on-border.toml`](references/title-on-border.toml).
  - Use one variant consistently within a page; different pages may use
    different variants for variety. A label must still be a claim, not a bare
    keyword.
- **Tables sketched with lines/rectangles**. See
  [`references/table.toml`](references/table.toml).

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
