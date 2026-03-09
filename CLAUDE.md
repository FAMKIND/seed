# Seed — Claude Code Instructions

## Project Overview

Seed is an open source design system built and maintained by [FAM](https://famkind.com). It serves as the foundation for FAM's broader open source ecosystem and is used directly as the base layer for **Lime**, FAM's primary product. Seed is built for mission-driven artists, designers, and builders who need a clean, composable UI foundation.

- **Repo:** github.com/FAMKIND/seed
- **Maintainer:** FAM (famkind.com)
- **Status:** Active open source development
- **Used by:** Lime and other FAM ecosystem projects

## Visual Direction

Seed's aesthetic is minimal, intentional, and content-forward. The primary references are:

- **Linear** — tight spacing, sharp type hierarchy, purposeful motion
- **Notion** — clean document-like layouts, low visual noise
- **Granola** — warm minimalism, considered whitespace

Key principles:
- No decoration for its own sake — every visual element earns its place
- Typography leads; color and iconography support
- Light mode first; dark mode as a first-class variant, not an afterthought
- Prefer subtle over stark: muted grays, restrained radius, controlled shadows

## Tech Stack

| Layer | Tool |
|---|---|
| Framework | Next.js (App Router) |
| Styling | Seed CSS (custom, see below) |
| Component docs | Storybook |
| Design source | Penpot |
| Package manager | npm |
| Language | TypeScript |

Design tokens and component specs flow from **Penpot** into the codebase. When implementing components, always check Penpot for the canonical spec before writing styles.

### Seed CSS

Seed does not use Tailwind CSS or any third-party CSS framework. Styling is handled by **Seed CSS** — a custom CSS custom property and utility system we are building as part of this project.

**Why:**
- **Self-reliant** — no upstream dependency that can change, break, or add build complexity
- **Open source** — the styling layer is fully ours to document, extend, and publish alongside components
- **Community-maintained** — contributors own the full stack; no need to understand a third-party framework's conventions
- **No external CSS dependencies** — consumers of Seed get one coherent system, not a mix of our components and someone else's utility classes

All styles use CSS custom properties for tokens and scoped class names for component styles. Utility classes (spacing, layout, typography helpers) are generated from the same token definitions.

## Design Principles

1. **Composable over monolithic** — small, single-purpose components that combine cleanly
2. **Accessible by default** — WCAG AA minimum; use semantic HTML, ARIA only where native semantics fall short
3. **Tokens first** — spacing, color, typography, and radius should reference design tokens, never raw values
4. **Predictable API surface** — prop names should be consistent across components (e.g. `size`, `variant`, `intent`)
5. **No magic** — avoid clever abstractions; prefer explicit and readable over terse and clever
6. **Seed CSS-native** — use Seed CSS custom properties and utility classes; avoid inline styles, CSS modules, and third-party utility frameworks

## Build Order

Build Seed in this sequence to establish solid foundations before composing higher-order components:

1. **CSS custom properties** — define all raw values as `--seed-*` variables (color palette, spacing scale, type scale, radius, shadow, motion duration/easing)
2. **Design tokens** — semantic token layer mapping raw variables to roles (`--color-surface-primary`, `--space-component-gap`, etc.); exported as both CSS and TypeScript
3. **Seed CSS utilities** — generate utility classes from tokens (spacing, layout, typography helpers); establish reset/base styles
4. **Primitives** — Box, Text, Icon, Divider, Stack, Grid
3. **Inputs** — Button, Input, Textarea, Select, Checkbox, Radio, Switch, Slider
4. **Feedback** — Badge, Tag, Spinner, Progress, Toast/Snackbar, Tooltip
5. **Navigation** — Tabs, Breadcrumb, Pagination, Sidebar, Navbar
6. **Overlay** — Modal, Drawer, Popover, Dropdown, Command Palette
7. **Data display** — Avatar, Card, Table, List, Stat
8. **Layout** — Page shell, Section, Container, Responsive grid system
9. **Patterns** — Form layouts, Empty states, Loading states, Error states

Each layer should be documented in Storybook with controls, accessibility notes, and usage guidelines before moving to the next.

## Conventions

### File & Folder Structure

```
src/
  components/
    button/
      Button.tsx
      Button.stories.tsx
      index.ts
  tokens/
    colors.ts
    spacing.ts
    typography.ts
  hooks/
  utils/
```

- One component per folder; folder name matches component name in PascalCase
- Always export from an `index.ts` barrel file
- Story files live alongside the component, not in a separate `/stories` directory

### Naming

- **Components:** PascalCase (`ButtonGroup`, `InputField`)
- **Props:** camelCase; boolean props prefixed with `is` or `has` (`isDisabled`, `hasError`)
- **Tokens:** kebab-case as CSS custom properties (`--seed-color-surface-primary`); camelCase in TS (`colorSurfacePrimary`)
- **Story names:** match the component name exactly; use `Default` as the primary story

### Component API Patterns

- Use `variant` for visual style (`default`, `outline`, `ghost`, `destructive`)
- Use `size` for scale (`xs`, `sm`, `md`, `lg`)
- Use `intent` for semantic meaning (`info`, `success`, `warning`, `error`)
- Spread `...props` onto the root element to support all native HTML attributes
- Use `asChild` (Radix pattern) when polymorphic rendering is needed

### Git

- Branch naming: `feat/component-name`, `fix/issue-description`, `chore/task`
- Commit style: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`)
- PRs should reference the Penpot spec or a GitHub issue when adding new components

### Storybook

- Every exported component requires at least one story
- Use `@storybook/addon-a11y` checks before marking a component complete
- Document props via autodocs; add manual notes for non-obvious behavior
