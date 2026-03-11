# Seed by FAM

A minimal, open source design token system for mission-driven builders.

---

## What is Seed?

Seed is the design foundation for the FAM open source ecosystem. It starts with tokens — color, typography, spacing, shadow — and grows into a full component library. It is used directly as the base layer for **Lime**, FAM's primary product.

Built for mission-driven artists, designers, and builders who need a clean, composable foundation without opinionated frameworks getting in the way.

**Seed has no external CSS dependencies.** There is no Tailwind, no Bootstrap, no third-party utility layer. The entire styling system — tokens, utilities, and components — is built and maintained here, in the open.

---

## The Metaphor

Seed's naming system follows a natural metaphor. Every token tells a story:

| Part | Role | Examples |
|---|---|---|
| `soil` | The ground — neutrals and structure | `soil-bg-canvas`, `soil-text-muted` |
| `root` | The why — semantic intent | `calm`, `good`, `warn`, `bad`, `selected` |
| `stem` | Where it applies | `bg`, `text`, `icon`, `border` |
| `bud` | How intense | `subtle`, `normal`, `bold` |
| `flower` | When / state | `default`, `hover`, `active`, `disabled` |

Token names follow the pattern: `--{root}-{stem}-{bud}-{flower}`

**Examples:**

```css
/* A soft lime background for a success state at rest */
background: var(--good-bg-subtle-default);

/* Bold warning text on hover */
color: var(--warn-text-bold-hover);
```

Neutrals use soil directly: `--soil-{stem}-{role}` (e.g. `--soil-bg-canvas`, `--soil-text-muted`).

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

## Roadmap

| Version | Focus |
|---|---|
| **v0.1** | Design token system — palette, semantic tokens, scale (current) |
| **v0.2** | Core components — Button, Input, Badge, Text, Stack, Icon |
| **v0.3** | Compositions — Card, Form, Navigation, Overlay |
| **v1.0** | Full Storybook, accessibility audit, public docs site |

---

## License

MIT — free to use, fork, and build on.

Made with care by [FAM](https://famkind.com).
