# Seed by FAM

A minimal, open source design system for mission-driven builders.

---

## What is Seed?

Seed is the design foundation for the FAM open source ecosystem. It provides tokens, components, and patterns — color, typography, spacing, and a growing library of plain HTML + CSS components. It is used directly as the base layer for **Lime**, FAM's primary product.

Built for mission-driven artists, designers, and builders who need a clean, composable foundation without opinionated frameworks getting in the way.

**Seed has no external CSS dependencies.** There is no Tailwind, no Bootstrap, no third-party utility layer. The entire styling system — tokens, utilities, and components — is built and maintained here, in the open.

Icons: Seed uses [Dew](https://github.com/FAMKIND/dew) — 52 essential SVG icons with outline and fill variants.

---

## How Seed Names Things

Every Seed token follows a simple pattern: `root.stem.bud.flower`

Think of it as answering four questions in a row:

| Part | Question it answers | Think of it as... |
|------|-------------------|-------------------|
| **root** | "What kind of message is this?" | The **intent** — calm, good, warn, bad, selected |
| **stem** | "Where do I apply it?" | The **layer** — bg, text, icon, border |
| **bud** | "How intense should it feel?" | The **volume knob** — subtle, normal, bold |
| **flower** | "What moment is this?" | The **state** — default, hover, active, disabled |

### Roots — the why

Each root carries a meaning:

- **calm** — neutral ground, informational, resting
- **good** — success, growth, positive
- **warn** — caution, attention, slow down
- **bad** — error, destructive, urgent
- **selected** — chosen, active, this one

### Buds — the volume knob

Same intent, different intensity:

- **subtle** — present but quiet (tinted backgrounds, soft borders)
- **normal** — everyday default
- **bold** — demands attention (strong fills, high-contrast text)

### Flowers — the moment

When does this style show up?

- **default** — at rest, no interaction
- **hover** — pointer is over it
- **active** — being pressed
- **disabled** — can't be used right now

### Reading a token out loud

The best test: read it left to right like a sentence.

- `warn.bg.subtle.hover` → "warning background, gently, on hover"
- `selected.border.bold.active` → "selected border, strongly, while pressed"
- `good.text.normal.default` → "positive text, normal strength, at rest"

### Fill in the blank

Once you get the pattern, you can guess any token:

```css
/* A soft success background at rest */
background: var(--good-bg-subtle-default);

/* Bold warning text on hover */
color: var(--warn-text-bold-hover);

/* Selected border, strongly, while pressed */
border-color: var(--selected-border-bold-active);
```

Neutrals step outside this pattern — they use `soil` directly: `--soil-{stem}-{role}` (e.g. `--soil-bg-canvas`, `--soil-text-muted`). No intent, no state. Just the ground everything else grows from.

---

## Token Tiers

Seed organises tokens into three tiers:

**Tier 1 — Raw Palette**
The base color values. Named by family and step: `--seed-lime-500`, `--seed-soil-200`. Never reference these directly in components — they exist only to feed Tier 2.

**Tier 2 — Semantic Tokens**
The layer components always reference. Maps raw values to roles and intent. Defined per theme using `[data-theme="light"]` and `[data-theme="dark"]`. This is where `--good-bg-bold-hover` and `--soil-border-subtle` live.

**Tier 3 — Scale Tokens**
Theme-agnostic values for typography, spacing, radius, shadows, grid, and z-index. Defined once on `:root` and shared across both themes: `--seed-space-4`, `--seed-radius-md`, `--seed-text-lg`.

---

## Usage

Import the token file and any component stylesheets you need:

```css
@import 'tokens/tokens.css';
@import 'components/button/button.css';
```

Set a theme on your root element:

```html
<html data-theme="light">
  <!-- or data-theme="dark" -->
</html>
```

Use semantic tokens in your styles:

```css
.card {
  background:    var(--soil-bg-surface);
  border:        1px solid var(--soil-border);
  border-radius: var(--seed-radius-md);
  padding:       var(--seed-space-6);
  color:         var(--soil-text);
}

.badge--success {
  background: var(--good-bg-subtle-default);
  color:      var(--good-text-normal-default);
  border:     1px solid var(--good-border-subtle-default);
}
```

---

## Palette

Seed ships with four color families:

**Soil** — warm neutral scale, the ground everything grows from
`#F9F8F4` → `#141210` (11 steps: 0, 50, 100–900, 950)

**Lime** — primary accent, growth and success
`#E4F9BE` → `#055C2E` (7 steps: 100–700, plus 950 for deep ink)

**Yellow** — energy, caution, attention
`#FEFEF0` → `#A89E00` (7 steps: 100–700)

**Brick** — error, urgency, destructive actions
`#FAEEEC` → `#6A2018` (7 steps: 100–700)

---

## Components

Each component lives in `components/{name}/` with a `.css` file and a `.html` demo page. All components reference Seed semantic tokens — zero hardcoded colors, automatic light/dark theming.

### Button `components/button/`

Variants, sizes, icon support, loading state.

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

Status labels with dot indicators and interactive variants.

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

Surface container with header, body, footer, and flush/bordered variants.

```html
<div class="seed-card">
  <div class="seed-card__header">Title</div>
  <div class="seed-card__body">Content goes here.</div>
  <div class="seed-card__footer">Footer</div>
</div>
```

### Avatar `components/avatar/`

Initials-based or image avatars in multiple sizes and intent colors.

```html
<span class="seed-avatar seed-avatar--md seed-avatar--brand">JD</span>
<span class="seed-avatar seed-avatar--md seed-avatar--good">OK</span>

<!-- Sizes: --xs  --sm  --md  --lg  --xl -->
```

### Input `components/input/`

Text inputs, textarea, select, checkbox, radio, and toggle.

```html
<div class="seed-field">
  <label class="seed-label" for="email">Email</label>
  <input class="seed-input" id="email" type="email" placeholder="you@example.com">
</div>

<!-- States: default, focus, error (--error), disabled -->
```

### Toggle `components/toggle/`

Animated on/off switch.

```html
<label class="seed-toggle">
  <input type="checkbox" role="switch">
  <span class="seed-toggle__track"><span class="seed-toggle__thumb"></span></span>
</label>
```

### Tabs `components/tabs/`

Horizontal tab strip with underline and pill variants.

```html
<div class="seed-tabs">
  <button class="seed-tab seed-tab--active">Overview</button>
  <button class="seed-tab">Activity</button>
  <button class="seed-tab">Settings</button>
</div>
```

### Divider `components/divider/`

Horizontal and vertical separators, with optional label.

```html
<hr class="seed-divider">
<hr class="seed-divider seed-divider--labeled"><span>or</span>
```

### Table `components/table/`

Sortable, selectable data table with avatars, badges, and responsive scroll.

```html
<table class="seed-table">
  <thead><tr><th class="seed-th">Name</th>…</tr></thead>
  <tbody><tr class="seed-tr"><td class="seed-td">…</td>…</tr></tbody>
</table>
```

### Toast `components/toast/`

Notification toasts with intent variants and dismiss button.

```html
<div class="seed-toast seed-toast--good" role="alert">
  <span class="seed-toast__icon dew dew-check-circle" aria-hidden="true"></span>
  <span class="seed-toast__body">Saved successfully.</span>
  <button class="seed-toast__close" aria-label="Dismiss">…</button>
</div>

<!-- Intents: --good  --warn  --bad  --calm -->
```

### Chat `components/chat/`

Message thread with composer, typing indicator, reactions, and container modes.

```html
<div class="seed-chat-container">
  <div class="seed-chat-messages">…</div>
  <div class="seed-chat-composer">…</div>
</div>
```

### Dropdown `components/dropdown/`

Click-toggled menu with icons, keyboard hints, sections, and disabled items.

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

Hover tooltips (4 directions, multiline) and click-toggled rich popovers.

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

Drag-and-drop dropzone with file list, progress bars, and compact trigger.

```html
<div class="seed-dropzone" role="button" tabindex="0" aria-label="Upload files">
  <span class="seed-dropzone__icon dew dew-upload" aria-hidden="true"></span>
  <p class="seed-dropzone__label">Drop files here or <span class="seed-dropzone__link">browse</span></p>
</div>
```

### Media `components/media/`

Aspect-ratio containers with skeleton, video overlay, caption, badge, and gallery grid.

```html
<div class="seed-media seed-media--16x9 seed-media--rounded">
  <img src="photo.jpg" alt="Description">
</div>

<!-- Aspect ratios: --16x9  --4x3  --3x2  --1x1  --auto -->
<!-- Gallery -->
<div class="seed-media-grid seed-media-grid--3">…</div>
```

### Feedback `components/feedback/`

Empty states, skeleton loaders, progress bars, and spinners.

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

Wayfinding breadcrumb trail and page controls.

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

Full-page shell with collapsible left panel, top bar, and fluid content area. Includes a live design system preview at `components/layout/layout.html`.

---

## Roadmap

| Version | Focus |
|---|---|
| **v0.1** | Design token system — palette, semantic tokens, scale ✓ |
| **v0.2** | Core components — Button, Badge, Card, Avatar, Input, Toggle, Tabs, Divider, Table, Toast ✓ |
| **v0.3** | Overlay & nav — Chat, Dropdown, Tooltip, Popover, Upload, Media, Feedback, Breadcrumbs, Pagination ✓ |
| **v1.0** | Full Storybook, accessibility audit, public docs site |

---

## Updating Icons

Seed uses [Dew](https://github.com/FAMKIND/dew) as a git submodule for icons. To pull the latest Dew icons:

```bash
cd icons/dew && git pull origin main
```

When cloning Seed fresh, initialize the submodule with:

```bash
git submodule update --init --recursive
```

---

## License

MIT — free to use, fork, and build on.

Made with care by [FAM](https://famkind.com).
