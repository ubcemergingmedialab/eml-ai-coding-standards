# Themes

Override only CSS custom properties (and optionally dark-slide gradient stops). Keep component CSS unchanged.

## Default: `eml` (UBC Emerging Media Lab)

```css
:root {
  --brand-navy: #002145;
  --brand-blue: #0055b7;
  --accent: #40b4e5;
  --paper: #f4f1ea;
  --ink: #0e1a28;
  --muted: #5b6b7c;
  --card: #ffffff;
  --ok: #1a7a4c;
  --caution: #b45309;
  --no: #b42318;
  --pill-yes-bg: #14532d;
  --pill-yes-fg: #bbf7d0;
  --pill-partial-bg: #78350f;
  --pill-partial-fg: #fde68a;
  --pill-no-bg: #7f1d1d;
  --pill-no-fg: #fecaca;
  --pill-caution-bg: #713f12;
  --pill-caution-fg: #fde68a;
  --dark-grad-a: #001a36;
  --dark-grad-b: #002145;
  --dark-grad-c: #00152c;
  --glow: rgba(64, 180, 229, 0.18);
  --font-ui: "Segoe UI", system-ui, sans-serif;
  --font-display: "Segoe UI", "Iowan Old Style", Georgia, system-ui, sans-serif;
}
```

Dark slide background in the shell uses `--dark-grad-*` and `--glow`.

## Creating a custom theme

Ask the user for (or infer):

| Token | Role |
|-------|------|
| `--brand-navy` | Dark slide base + light-slide primary text |
| `--brand-blue` | Kickers / accents on light slides |
| `--accent` | Kickers / progress / bullets on dark slides |
| `--paper` | Light slide background; dark-slide title text |
| `--ink` / `--muted` | Body text on light slides |

**Rules**

1. Keep **relative contrast**: dark slides → light text; light slides → dark text.
2. Recolor `--glow` to a translucent version of `--accent`.
3. Set `--dark-grad-a/b/c` to navy-adjacent shades of the brand (avoid flat single color).
4. Pill colors may stay semantic (green/amber/red) unless the user wants a monochrome set.
5. Do not swap to Inter/Roboto/Arial-only stacks unless requested; keep a display + UI pair.

## Example alternate: high-contrast mono

```css
:root {
  --brand-navy: #111111;
  --brand-blue: #222222;
  --accent: #e8e4dc;
  --paper: #f7f5f0;
  --ink: #111111;
  --muted: #555555;
  --dark-grad-a: #0a0a0a;
  --dark-grad-b: #111111;
  --dark-grad-c: #050505;
  --glow: rgba(232, 228, 220, 0.12);
}
```

## Mapping from older token names

If editing `docs/slides.html` directly, map:

| Legacy | Theme token |
|--------|-------------|
| `--ubc-navy` | `--brand-navy` |
| `--ubc-blue` | `--brand-blue` |
| `--cyan` | `--accent` |
