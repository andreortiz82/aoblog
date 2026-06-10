# Design System — aoblog

The visual language for aoblog, Andre Ortiz's build journal: a minimalist
editorial identity — white surface, black ink, one red accent, typographic
contrast as the primary expressive tool.

Implementation lives in `src/styles/global.css`. This file documents the
*decisions and rationale*; the CSS is the source of truth for exact values.

---

## Maintenance Protocol

- Update this file when a visual, typographic, spacing, logo, or token
  decision changes.
- `src/styles/global.css` implements these decisions — don't duplicate
  values here, describe intent and point to the token/class name.
- `PLAN.md` tracks the build itself (checklist + log); this file tracks
  the resulting design system.
- `CLAUDE.md` tracks stack, commands, and content schemas.

---

## Aesthetic

**Restrained confidence.** No gradients, no illustrations, no stock
photography. The work speaks; the container steps back. Every choice
earns its presence — if it doesn't serve hierarchy or readability, it
doesn't ship.

The overall register is print editorial — close to a well-designed annual
report or book — executed as a web experience.

---

## Logo

- Mark: `public/aologo.svg` — the "ao" mark (a triangle + a ring), single
  color, `viewBox="0 0 200 99"`.
- Inlined as `src/components/Logo.astro` with `fill="currentColor"`, so it
  follows whatever text color class it's given.
- Header usage: `<Logo class="h-10 w-auto text-foreground" />` — mark
  only, no wordmark text alongside it. (`Header.astro` keeps a
  commented-out `{SITE_TITLE}` span in case a wordmark is reintroduced
  later.)

---

## Color

Tokens are defined in `src/styles/global.css` under `@theme inline`,
using [shadcn/ui](https://ui.shadcn.com) naming so shadcn components drop
in without remapping.

| Role | Token | Value |
|---|---|---|
| Page surface | `--color-background` | `#ffffff` |
| Primary text | `--color-foreground` | `#0a0a0a` |
| Secondary text | `--color-ink-2` | `#404040` |
| Card surface / text | `--color-card` / `--color-card-foreground` | `#ffffff` / `#0a0a0a` |
| Popover surface / text | `--color-popover` / `--color-popover-foreground` | `#ffffff` / `#0a0a0a` |
| Primary action fill / text | `--color-primary` / `--color-primary-foreground` | `#0a0a0a` / `#ffffff` |
| Secondary surface / text | `--color-secondary` / `--color-secondary-foreground` | `#fafafa` / `#0a0a0a` |
| Muted surface (code blocks, subtle bg) | `--color-muted` | `#fafafa` |
| Muted / metadata text | `--color-muted-foreground` | `#737373` |
| Accent surface (hover, selection bg) | `--color-accent` | `#fef2f2` |
| Accent text | `--color-accent-foreground` | `#dc2626` |
| Destructive / brand accent | `--color-destructive` | `#dc2626` |
| Destructive text | `--color-destructive-foreground` | `#ffffff` |
| Divider / border / input | `--color-border` / `--color-input` | `rgba(0,0,0,0.08)` |
| Focus ring | `--color-ring` | `#dc2626` |

**Rules:**
- The brand red (`--color-destructive` / `--color-accent-foreground`,
  `#dc2626`) is used sparingly: italic emphasis in headings (see Emphasis
  System), text selection, and focus rings. Never as a background fill on
  a large surface — `--color-primary` (ink) carries that role for solid
  fills (e.g. CTA buttons: solid ink, not accent — the CTA should feel
  inevitable, not urgent).
- `--color-ink-2` is an addition outside the standard shadcn set: a
  secondary text tone between `--color-foreground` and
  `--color-muted-foreground`, used for body copy on index pages, link
  hover, and `.prose-plain` blockquotes.
- Text always reads against white. No dark mode implemented.
- Border, input, and divider values use opacity (`rgba(0,0,0,0.08)`) so
  they stay legible against any slightly-tinted surface without needing
  variant tokens.

---

## Typography

Three typefaces, clearly separated roles. Mixing them without a role
reason is an error.

- **Fraunces** (`--font-serif`) — display serif. Page H1s, post and short
  titles, and `.prose-plain` h2–h4 (italic, weight 450). Variable font;
  italic is narrow and expressive — used for the Emphasis System below.
- **Instrument Sans** (`--font-sans`) — body copy, descriptions, UI text.
  Default `font-family` on `html`. Weights: 400 (body), 500 (medium
  emphasis), 600 (strong labels). Base size `17px`, line-height `1.6`.
- **JetBrains Mono** (`--font-mono`) — metadata: `.nav-link`, `.meta-tag`,
  inline code. Always small (`10px`–`12px`), uppercase, `+0.08em`–`0.12em`
  tracking.

Loaded via the Google Fonts `@import` at the top of `global.css` (Fraunces
variable axes, Instrument Sans 400/500/600, JetBrains Mono 400/500/700).

---

## Emphasis System — Italics

Italicized `<em>` fragments inside `h1`/`h2`/`h3` render in
`--color-destructive`. This is the primary expressive mechanism — not
decorative. One fragment per headline, marking the clause that carries the
most semantic weight. Never use `<strong>` or bold in display headings —
it competes with the serif weight and flattens rhythm.

```css
h1 em,
h2 em,
h3 em {
  font-style: italic;
  color: var(--color-destructive);
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
- Footer: `border-t border-border`, `py-8`, mono uppercase metadata text.
- Reading measure: `.prose-plain` content is constrained to `680px` —
  wide enough to feel generous, narrow enough that the eye doesn't hunt
  for the next line.

---

## Components

- **`.nav-link`** — JetBrains Mono, 12px, uppercase, `+0.08em` tracking.
  `--color-muted-foreground` at rest, `--color-foreground` on
  hover/active, with a 1px underline that scales in from the left
  (`scaleX`, 0.35s `cubic-bezier(0.65,0,0.35,1)`).
- **`.meta-tag`** — pill badge for category/status/genre: mono uppercase
  `0.7em`, `--color-border` border, `999px` radius.
- **`.prose-plain`** — markdown body content (blog posts, shorts).
  `max-width: 680px`; h2–h4 in Fraunces italic; blockquotes in
  `--color-ink-2` italic with a left border; images get `var(--radius)`.

---

## Radius

Shared scale backing Tailwind's `rounded-*` utilities and any shadcn
component radius props:

| Token | Value |
|---|---|
| `--radius` | `0.25rem` |
| `--radius-sm` | `0.125rem` |
| `--radius-md` | `0.25rem` |
| `--radius-lg` | `0.375rem` |
| `--radius-xl` | `0.5rem` |

Used today by `.prose-plain img`, code blocks (`pre`), and short cover
thumbnails.
