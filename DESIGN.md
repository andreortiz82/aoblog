# Design System — aoblog

The visual language for aoblog, Andre Ortiz's build journal. Ported from
[`ao`'s DESIGN.md](https://github.com/andreortiz82/ao/blob/main/DESIGN.md) —
same editorial aesthetic, type system, color tokens, and emphasis system —
trimmed to what a content-first site actually needs. See "Differences from
`ao`" below for what was deliberately left out or changed.

Implementation lives in `src/styles/global.css`. This file documents the
*decisions and rationale*; the CSS is the source of truth for exact values.

---

## Maintenance Protocol

- Update this file when a visual, typographic, spacing, or logo decision
  changes.
- `src/styles/global.css` implements these decisions — don't duplicate
  values here, describe intent and point to the token/class name.
- `PLAN.md` tracks the build itself (checklist + log); this file tracks the
  resulting design system.
- If aoblog diverges from `ao`'s DESIGN.md, record it under "Differences
  from `ao`" rather than letting the two drift silently.

---

## Aesthetic

Minimalist editorial: white surface, black ink, one red accent, restrained
type contrast as the primary expressive tool. No gradients, no
illustrations, no stock imagery. Inherited wholesale from `ao` — see
[the post on adopting `ao`'s DESIGN.md](src/content/blog/2026-06-09-the-design-md-file.md)
for why that worked and what was ported versus skipped.

---

## Logo

- Mark: `public/aologo.svg` — the "ao" mark (a triangle + a ring), single
  color, `viewBox="0 0 200 99"`.
- Inlined as `src/components/Logo.astro` with `fill="currentColor"`, so it
  follows whatever text color class it's given (`text-ink`).
- Header usage: `<Logo class="h-10 w-auto text-ink" />` — mark only, no
  wordmark text alongside it. (`Header.astro` keeps a commented-out
  `{SITE_TITLE}` span in case a wordmark is reintroduced later.)

---

## Color

Tokens defined in `src/styles/global.css` under `@theme inline`.

| Role | Token | Value |
|---|---|---|
| Page surface | `--color-background` | `#ffffff` |
| Card / widget surface | `--color-paper` | `#fafafa` |
| Primary text | `--color-ink` | `#0a0a0a` |
| Secondary text | `--color-ink-2` | `#404040` |
| Tertiary / metadata | `--color-ink-3` | `#737373` |
| Divider / border | `--color-line` | `rgba(0,0,0,0.08)` |
| Subtle inner divider | `--color-line-soft` | `rgba(0,0,0,0.04)` |
| Accent | `--color-accent` | `#dc2626` |
| Accent tint | `--color-accent-soft` | `#fef2f2` |
| Text selection | `--color-highlight` | `#fee2e2` |

**Rules:**
- The accent is used sparingly: italic emphasis in headings (see Emphasis
  System) and the active-state underline color is still ink, not accent —
  red is reserved for the emphasis word, not UI chrome.
- `--color-accent-soft`, `--color-line-soft`, and `--color-highlight` were
  ported from `ao` for parity but aren't load-bearing yet beyond
  `::selection` — fine to lean on them as the site grows.

---

## Typography

Three typefaces, same roles as `ao`. Mixing them without a role reason is
an error.

- **Fraunces** (`--font-serif`) — display serif. Page H1s, post and short
  titles, and `.prose-plain` h2–h4 (italic, weight 450).
- **Instrument Sans** (`--font-sans`) — body copy, descriptions, UI text.
  Default `font-family` on `html`.
- **JetBrains Mono** (`--font-mono`) — metadata: `.nav-link`, `.meta-tag`,
  inline code.

Loaded via the Google Fonts `@import` at the top of `global.css` (Fraunces
variable axes, Instrument Sans 400/500/600, JetBrains Mono 400/500/700).

---

## Emphasis System — Italics

Italicized `<em>` fragments inside `h1`/`h2`/`h3` render in
`--color-accent`. One fragment per headline — the clause carrying the most
semantic weight.

```css
h1 em, h2 em, h3 em {
  font-style: italic;
  color: var(--color-accent);
}
```

**Example in the codebase:** the homepage hero is `Creative *Blog*` —
"Blog" renders italic and red.

---

## Layout & Spacing

- Content column: `max-w-3xl mx-auto px-6` — used by `BaseLayout`,
  `Header`, and `Footer` for consistent alignment.
- Main content area: `py-12`.
- Header: `h-16` flex row, logo mark on the left, nav links on the right.
  No bottom border — kept open rather than boxed off from the page.
- Footer: `border-t border-line`, `py-8`, mono uppercase metadata text.

---

## Components

- **`.nav-link`** — JetBrains Mono, 12px, uppercase, `+0.08em` tracking.
  `ink-3` at rest, `ink` on hover/active, with a 1px underline that
  scales in from the left (`scaleX`, 0.35s `cubic-bezier(0.65,0,0.35,1)`).
- **`.meta-tag`** — pill badge for category/status/genre: mono uppercase
  `0.7em`, `--color-line` border, `999px` radius.
- **`.prose-plain`** — markdown body content (blog posts, shorts).
  `max-width: 680px`; h2–h4 in Fraunces italic; blockquotes in `ink-2`
  italic with a left border; images get `0.25rem` radius.

---

## Differences from `ao`

- **Header has no bottom border.** `ao`'s header sits in a bordered band;
  aoblog's floats directly on the page.
- **Logo is mark-only in the header** — no wordmark text next to it (vs.
  `ao`'s logo + nav pairing).
- **No motion/widget system.** `ao`'s `DESIGN.md` documents hero word
  stagger, logo pulse-dot, widget crossfades, etc. — all tied to React
  islands aoblog doesn't have. The only motion here is the `.nav-link`
  underline transition.
- **No shadcn aliases or iteration-card variants** — those exist in `ao`
  for its interactive demo components and have no equivalent here.
- Accent-soft/line-soft/highlight tokens are present for parity but mostly
  unused so far (see Color rules above).
