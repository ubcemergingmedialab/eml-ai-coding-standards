---
name: eml-presentation
description: >-
  Build self-contained HTML slideshows in the EML briefing style (dark/light
  slides, kickers, cards, phase rows, flow chips, keyboard nav). Themeable via
  CSS variables; defaults to UBC Emerging Media Lab branding. Use when the user
  asks for a presentation, slideshow, slide deck, briefing slides, or
  eml-presentation style slides.
---

# EML Presentation

Create a **single HTML file** slideshow matching the lab briefing style used in `docs/slides.html`.

## Workflow

1. Clarify topic, audience, approximate slide count (prefer **12–20**), and output path (default `docs/<topic>-slides.html`).
2. Choose theme: **eml** (default) unless the user names another or supplies tokens — see [themes.md](themes.md).
3. Outline slides first (titles only). One idea per slide. Alternate dark ↔ light for density.
4. Copy [shell.html](shell.html) to the output path; replace `{{TITLE}}`, `{{FOOTER_LABEL}}`, and the slide sections.
5. Author slides using only the components in [components.md](components.md).
6. Apply theme tokens in `:root` (and dark gradient if needed).
7. Contrast check: on `.slide.light`, never use light/white text on pale cyan chips — use navy ink.
8. Tell the user: open the file in a browser; **F** fullscreen, **P** print/PDF, ← → / Space to navigate.

## Non-negotiables

- Self-contained HTML (inline CSS + JS). No Reveal.js, Marp, or CDN frameworks.
- Keep the shell’s CSS class names and nav script intact.
- Briefing tone: short titles, pointed bullets — link out to docs for depth.
- Do not invent new visual chrome (extra shadows, purple gradients, emoji rows).

## Reference deck

Canonical example: [`docs/slides.html`](../../../docs/slides.html) in this repo.
