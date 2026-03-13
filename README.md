# Seed by FAM

A minimal, open source design token system for mission-driven builders.

---

## What is Seed?

Seed is the design foundation for the FAM open source ecosystem. It starts with tokens — color, typography, spacing, shadow — and grows into a full component library. It is used directly as the base layer for **Lime**, FAM's primary product.

Built for mission-driven artists, designers, and builders who need a clean, composable foundation without opinionated frameworks getting in the way.

**Seed has no external CSS dependencies.** There is no Tailwind, no Bootstrap, no third-party utility layer. The entire styling system — tokens, utilities, and components — is built and maintained here, in the open.

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

Import the token file into your project:

```css
@import 'tokens/tokens.css';
```

Then set a theme on your root element:

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

Seed ships with four color families in v0.1:

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

Seed components are plain HTML + CSS. Each lives in `components/{name}/` with a `.css` file and a `.html` demo page.

### Button `components/button/`

```html
<!-- Variants -->
<button class="seed-button seed-button--primary seed-button--md">Primary</button>
<button class="seed-button seed-button--secondary seed-button--md">Secondary</button>
<button class="seed-button seed-button--link seed-button--md">Link</button>
<button class="seed-button seed-button--danger seed-button--md">Danger</button>

<!-- Danger outlined: combine --danger with --secondary -->
<button class="seed-button seed-button--danger seed-button--secondary seed-button--md">Delete</button>

<!-- Sizes: --sm  --md  --lg -->
<!-- Disabled: add the disabled attribute -->
```

### Badge `components/badge/`

```html
<!-- Variants -->
<span class="seed-badge seed-badge--neutral seed-badge--md">Neutral</span>
<span class="seed-badge seed-badge--good seed-badge--md">Good</span>
<span class="seed-badge seed-badge--warn seed-badge--md">Warn</span>
<span class="seed-badge seed-badge--bad seed-badge--md">Bad</span>
<span class="seed-badge seed-badge--selected seed-badge--md">Selected</span>

<!-- With dot indicator -->
<span class="seed-badge seed-badge--good seed-badge--md">
  <span class="seed-badge__dot"></span>Active
</span>

<!-- Interactive (hover/active states) -->
<span class="seed-badge seed-badge--good seed-badge--md seed-badge--interactive">Good</span>

<!-- Sizes: --sm  --md  --lg -->
```

---

## Roadmap

| Version | Focus |
|---|---|
| **v0.1** | Design token system — palette, semantic tokens, scale ✓ |
| **v0.2** | Core components — Button, Badge ✓ · Input, Text, Stack, Icon |
| **v0.3** | Compositions — Card, Form, Navigation, Overlay |
| **v1.0** | Full Storybook, accessibility audit, public docs site |

---

## License

MIT — free to use, fork, and build on.

Made with care by [FAM](https://famkind.com).
