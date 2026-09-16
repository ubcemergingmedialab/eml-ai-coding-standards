# Slide components

Use these patterns inside `<div id="deck">`. Alternate `.slide` (dark) and `.slide.light`.

## Title / close (dark)

```html
<section class="slide active">
  <p class="kicker">Org or series</p>
  <h1>Short title</h1>
  <p class="lede">One supporting sentence.</p>
  <p class="meta">Context · date or URL</p>
</section>
```

First slide needs `active`. Closing slide: short `h1` + lede + meta with nav hints.

## Bullets (dark or light)

```html
<section class="slide">
  <p class="kicker">Section</p>
  <h2>Takeaway as title</h2>
  <ul class="plain">
    <li>Point one</li>
    <li>Point two</li>
  </ul>
</section>
```

## Numbered principle cards (prefer light)

```html
<section class="slide light">
  <p class="kicker">Principles</p>
  <h2>How we work</h2>
  <div class="grid cols-2">
    <div class="card"><span class="num">01</span><h3>Title</h3><p>Body</p></div>
    <div class="card"><span class="num">02</span><h3>Title</h3><p>Body</p></div>
  </div>
</section>
```

Full-width card: `style="grid-column: 1 / -1;"` on the card.

## Phase / sequence (dark)

```html
<div class="phase">
  <div class="step">
    <span class="pill yes">Phase 1</span>
    <h3>Name</h3>
    <p>Detail</p>
  </div>
  <div class="arrow">→</div>
  <div class="step">
    <span class="pill partial">Phase 2</span>
    <h3>Name</h3>
    <p>Detail</p>
  </div>
</div>
```

Pills: `yes` | `partial` | `no` | `caution`.

## Table (prefer light)

```html
<table>
  <tr><th>Col A</th><th>Col B</th></tr>
  <tr><td>…</td><td>…</td></tr>
</table>
```

## Two-column (list + callout)

```html
<div class="two-col">
  <ul class="plain">…</ul>
  <div class="card"><h3>Callout</h3><p>…</p></div>
</div>
```

## Process flow (prefer light)

```html
<div class="flow">
  <span class="n">Step A</span><i>→</i>
  <span class="n">Step B</span><i>→</i>
  <span class="n">Step C</span>
</div>
```

On light slides the shell already forces navy text on chips — do not override to white.

## Checklist cards (light)

```html
<div class="grid cols-2">
  <div class="card"><h3>Item</h3><p>Detail</p></div>
</div>
```

## Content rules

- One primary claim per slide (the `h1`/`h2`).
- Prefer ≤5 bullets; ≤6 cards visible.
- Use `<code>` for paths, commands, branch names.
- Escape `&` as `&amp;` in HTML text.
- Footer label: short deck name (e.g. `EML · Onboarding`).
