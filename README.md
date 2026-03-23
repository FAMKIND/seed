# Seed by FAM

A minimal, open source design system for mission-driven builders.

---

## What is Seed?

Seed is the design foundation for the FAM open source ecosystem. It starts with tokens — color, typography, spacing, shadow — and grows into a full component library. Built for mission-driven artists, designers, and builders who need a clean, composable foundation without opinionated frameworks getting in the way.

It is used directly as the base layer for **Lime**, FAM's primary product.

**Seed has no external CSS dependencies.** There is no Tailwind, no Bootstrap, no third-party utility layer. The entire styling system — tokens, utilities, and components — is built and maintained here, in the open.

Icons: Seed uses [Dew](https://github.com/FAMKIND/dew) — 52 essential SVG icons with outline and fill variants.

---

## How Seed Names Things

Every Seed token follows a simple pattern: `root.stem.bud.flower`

| Part | Question it answers | Think of it as... |
|------|-------------------|-------------------|
| **root** | "What kind of message is this?" | The **intent** — calm, good, warn, bad, selected |
| **stem** | "Where do I apply it?" | The **layer** — bg, text, icon, border |
| **bud** | "How intense should it feel?" | The **volume knob** — subtle, normal, bold |
| **flower** | "What moment is this?" | The **state** — default, hover, active, disabled |

### Roots

- **calm** — neutral ground, informational, resting
- **good** — success, growth, positive
- **warn** — caution, attention, slow down
- **bad** — error, destructive, urgent
- **selected** — chosen, active, this one

### Reading a token out loud

- `warn.bg.subtle.hover` → "warning background, gently, on hover"
- `selected.border.bold.active` → "selected border, strongly, while pressed"
- `good.text.normal.default` → "positive text, normal strength, at rest"

```css
background:   var(--good-bg-subtle-default);
color:        var(--warn-text-bold-hover);
border-color: var(--selected-border-bold-active);
```

Neutrals use `soil` directly: `--soil-{stem}-{role}` (e.g. `--soil-bg-canvas`, `--soil-text-muted`).

---

## Token Tiers

**Tier 1 — Raw Palette**
Base color values: `--seed-lime-500`, `--seed-soil-200`. Never reference in components directly.

**Tier 2 — Semantic Tokens**
What components always reference. Defined per theme via `[data-theme="light"]` / `[data-theme="dark"]`. Where `--good-bg-bold-hover` and `--soil-border-subtle` live.

**Tier 3 — Scale Tokens**
Theme-agnostic values for typography, spacing, radius, shadows, grid, z-index. Defined once on `:root`: `--seed-space-4`, `--seed-radius-md`, `--seed-text-lg`.

---

## Brand Palette

**Primary — Lime** `#E4F9BE` → `#055C2E`
Growth, success, the primary brand color.

**Secondary — Meadow** `#F0FBEA` → `#559A40`
The light green of the lime segments. Softer, more approachable.

**Accent — Yellow** `#FEFEF0` → `#A89E00`
Energy, attention, the yellow of the lime logo.

**Neutrals — Soil** `#F9F8F4` → `#141210`
Warm neutral ground. The base for all surfaces, text, and borders.

Brick (`#FAEEEC` → `#6A2018`) is used internally for `bad-*` semantic tokens (error, danger, destructive states) but is not part of the public brand palette.

---

## Typography

**Primary UI font:** `--seed-font-ui` — Montserrat (Semibold for wordmark, Regular/Medium for UI)
**Serif/Display font:** `--seed-font-serif` — Lora

The design system preview includes a **live font-pairing switcher** (Brand → Typography) that lets you try 15+ open source alternatives from Google Fonts — including Mozilla Text, Mozilla Headline, Fira Sans, Playfair Display, Fraunces, and more. Selections persist via localStorage.

---

## Usage

```css
@import 'tokens/tokens.css';
@import 'components/button/button.css';
```

```html
<html data-theme="light">
  <!-- or data-theme="dark" -->
</html>
```

```css
.card {
  background:    var(--soil-bg-surface);
  border:        1px solid var(--soil-border);
  border-radius: var(--seed-radius-md);
  padding:       var(--seed-space-6);
  color:         var(--soil-text);
}
```

---

## Components

Each component lives in `components/{name}/` with a `.css` file and a `.html` demo page. All components reference Seed semantic tokens — zero hardcoded colors, automatic light/dark theming.

### Button `components/button/`

```html
<button class="seed-button seed-button--primary   seed-button--md">Primary</button>
<button class="seed-button seed-button--secondary seed-button--md">Secondary</button>
<button class="seed-button seed-button--danger    seed-button--md">Danger</button>
<button class="seed-button seed-button--link      seed-button--md">Link</button>

<!-- Icon-only -->
<button class="seed-button seed-button--secondary seed-button--md seed-button--icon-only" aria-label="Edit">
  <span class="seed-button__icon dew dew-pencil" aria-hidden="true"></span>
</button>
<!-- Sizes: --sm  --md  --lg -->
```

### Badge `components/badge/`

```html
<span class="seed-badge seed-badge--neutral  seed-badge--md">Neutral</span>
<span class="seed-badge seed-badge--good     seed-badge--md">Good</span>
<span class="seed-badge seed-badge--warn     seed-badge--md">Warn</span>
<span class="seed-badge seed-badge--bad      seed-badge--md">Bad</span>
<span class="seed-badge seed-badge--selected seed-badge--md">Selected</span>
<!-- With dot -->
<span class="seed-badge seed-badge--good seed-badge--md">
  <span class="seed-badge__dot"></span>Active
</span>
<!-- Sizes: --sm  --md  --lg -->
```

### Card `components/card/`

```html
<div class="seed-card">
  <div class="seed-card__header">Title</div>
  <div class="seed-card__body">Content goes here.</div>
  <div class="seed-card__footer">Footer</div>
</div>
```

### Avatar `components/avatar/`

```html
<span class="seed-avatar seed-avatar--md seed-avatar--brand">JD</span>
<span class="seed-avatar seed-avatar--md seed-avatar--good">OK</span>
<!-- Sizes: --xs  --sm  --md  --lg  --xl -->
```

### Input `components/input/`

```html
<div class="seed-field">
  <label class="seed-label" for="email">Email</label>
  <input class="seed-input" id="email" type="email" placeholder="you@example.com">
</div>
<!-- States: default, focus, error (--error), disabled -->
```

### Toggle `components/toggle/`

```html
<label class="seed-toggle">
  <input type="checkbox" role="switch">
  <span class="seed-toggle__track"><span class="seed-toggle__thumb"></span></span>
</label>
```

### Tabs `components/tabs/`

```html
<div class="seed-tabs">
  <button class="seed-tab seed-tab--active">Overview</button>
  <button class="seed-tab">Activity</button>
  <button class="seed-tab">Settings</button>
</div>
```

### Divider `components/divider/`

```html
<hr class="seed-divider">
```

### Table `components/table/`

```html
<table class="seed-table">
  <thead><tr><th class="seed-th">Name</th>…</tr></thead>
  <tbody><tr class="seed-tr"><td class="seed-td">…</td>…</tr></tbody>
</table>
```

### Toast `components/toast/`

```html
<div class="seed-toast seed-toast--good" role="alert">
  <span class="seed-toast__icon dew dew-check-circle" aria-hidden="true"></span>
  <span class="seed-toast__body">Saved successfully.</span>
  <button class="seed-toast__close" aria-label="Dismiss">…</button>
</div>
<!-- Intents: --good  --warn  --bad  --calm -->
```

### Chat `components/chat/`

```html
<div class="seed-chat-container">
  <div class="seed-chat-messages">…</div>
  <div class="seed-chat-composer">…</div>
</div>
```

### Dropdown `components/dropdown/`

```html
<div class="seed-dropdown">
  <button class="seed-button seed-button--secondary seed-button--md seed-dropdown__trigger">
    Options <span class="seed-button__icon dew dew-chevron-down"></span>
  </button>
  <ul class="seed-dropdown__menu" role="menu">
    <li class="seed-dropdown__item" role="menuitem">Edit</li>
    <li class="seed-dropdown__divider" role="separator"></li>
    <li class="seed-dropdown__item seed-dropdown__item--danger" role="menuitem">Delete</li>
  </ul>
</div>
```

### Tooltip & Popover `components/tooltip/`

```html
<!-- Tooltip -->
<span class="seed-tooltip seed-tooltip--top">
  <button class="seed-button seed-button--secondary seed-button--sm">Hover me</button>
  <span class="seed-tooltip__tip" role="tooltip">Appears above</span>
</span>

<!-- Popover -->
<div class="seed-popover seed-popover--align-start" data-popover>
  <button data-pop-trigger>Info</button>
  <div class="seed-popover__content" data-pop-content role="dialog">
    <p class="seed-popover__title">About this field</p>
    <p class="seed-popover__body">Details here.</p>
  </div>
</div>
```

### Upload `components/upload/`

```html
<div class="seed-dropzone" role="button" tabindex="0" aria-label="Upload files">
  <span class="seed-dropzone__icon dew dew-upload" aria-hidden="true"></span>
  <p class="seed-dropzone__label">Drop files here or <span class="seed-dropzone__link">browse</span></p>
</div>
```

### Media `components/media/`

```html
<div class="seed-media seed-media--16x9 seed-media--rounded">
  <img src="photo.jpg" alt="Description">
</div>
<!-- Aspect ratios: --16x9  --4x3  --3x2  --1x1  --auto -->
<div class="seed-media-grid seed-media-grid--3">…</div>
```

### Feedback `components/feedback/`

```html
<!-- Empty state -->
<div class="seed-empty">
  <p class="seed-empty__title">Nothing here yet</p>
  <p class="seed-empty__body">Create something to get started.</p>
</div>

<!-- Progress -->
<div class="seed-progress"><div class="seed-progress__bar" style="width:60%"></div></div>

<!-- Spinner -->
<span class="seed-spinner" role="status" aria-label="Loading"></span>
```

### Breadcrumbs & Pagination `components/nav/`

```html
<!-- Breadcrumbs -->
<ol class="seed-breadcrumbs">
  <li><a class="seed-breadcrumb" href="#">Home</a></li>
  <li class="seed-breadcrumbs__separator" aria-hidden="true"><span class="dew dew-chevron-right"></span></li>
  <li><span class="seed-breadcrumb seed-breadcrumb--active" aria-current="page">Settings</span></li>
</ol>

<!-- Pagination -->
<nav class="seed-pagination">
  <button class="seed-page" aria-label="Previous page"><span class="dew dew-chevron-left"></span></button>
  <button class="seed-page">1</button>
  <button class="seed-page seed-page--active" aria-current="page">2</button>
  <button class="seed-page">3</button>
  <button class="seed-page" aria-label="Next page"><span class="dew dew-chevron-right"></span></button>
  <span class="seed-pagination__info">1–10 of 84</span>
</nav>
```

### Layout `components/layout/`

Full-page shell with collapsible left panel, top bar, and fluid content area. Open `components/layout/layout.html` for the live design system preview — includes the brand guidelines, all component demos, and the font-pairing switcher.

---

## Roadmap

| Version | Focus |
|---|---|
| **v0.1** | Design token system — palette, semantic tokens, scale ✓ |
| **v0.2** | Core components — Button, Badge, Card, Avatar, Input, Toggle, Tabs, Divider, Table, Toast ✓ |
| **v0.3** | Overlay & nav — Chat, Dropdown, Tooltip, Popover, Upload, Media, Feedback, Breadcrumbs, Pagination ✓ |
| **v0.4** | Brand system — Name & Logo guidelines, Meadow palette, font-pairing switcher ✓ |
| **v1.0** | Storybook, accessibility audit, public docs site |

---

## Updating Icons

Seed uses [Dew](https://github.com/FAMKIND/dew) as a git submodule for icons:

```bash
# Pull latest icons
cd icons/dew && git pull origin main

# When cloning fresh
git submodule update --init --recursive
```

---

## License

MIT — free to use, fork, and build on.

Made with care by [FAM](https://famkind.com).
