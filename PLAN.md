# aoblog — Build Plan

A living checklist + log for bootstrapping aoblog: an Astro 5 + Tailwind v4 + MDX
build journal, shipped with a deliberately "undesigned" baseline, real first
content (a Day One post + Shorts migration), and pushed to GitHub.

Full plan/rationale: see the plan that produced this file (architecture,
schemas, content outlines, design baseline).

## Checklist

- [x] 1. Write `PLAN.md` (this file) — phased checklist + seeded Log
- [x] 2. `npm init -y` + install pinned deps (Astro 5, Tailwind v4, MDX, React, sitemap)
- [x] 3. Write `.gitignore`, `astro.config.mjs`, `package.json` scripts, `tsconfig.json`, `README.md`
- [x] 4. Write `src/env.d.ts`, `src/consts.ts`, `src/content.config.ts`, `src/styles/global.css`
- [x] 5. Write components (BaseHead, Header, Footer, FormattedDate) + layouts (BaseLayout, PostLayout)
- [x] 6. Copy Under Foot cover image to `public/covers/`, write `public/favicon.svg`
- [x] 7. Write first 5 content files: Day One post + 4 Shorts entries
- [x] 8. Write 6 page files (index, about, blog index/slug, shorts index/slug)
- [x] 9. `npx astro sync` → `npm run dev` manual check → `npm run build` → `npm run preview`
- [x] 10. Write second post (`planning-with-ai`) drawing on this file's Log → rebuild
- [x] 11. `git init` + commit, then `gh repo create andreortiz82/aoblog --public --source=. --push`
- [x] 12. Vercel import (manual, user step — CLI not authenticated)

## Phase 2 — Adopt `ao`'s DESIGN.md system

- [x] 13. Add `aologo.svg` mark to the header (new `Logo.astro` component)
- [x] 14. Port relevant parts of `ao/DESIGN.md` into `global.css`: Fraunces / Instrument Sans / JetBrains Mono, ink/paper/accent tokens, italic-accent emphasis system, mono nav-link style, serif italic prose headings
- [x] 15. Apply new typography to header, footer, and page headings (index, about, blog/shorts indexes, post layout)
- [x] 16. Rebuild + verify
- [x] 17. Write a post on the benefits of keeping a `DESIGN.md`
- [x] 18. Commit + push

## Log

- 2026-06-09 — Discovered `writing/index.md` status labels don't match reality:
  "Free Flight" (marked "idea") has a complete ~700-word story; "Under Foot"
  (marked "complete") only has a placeholder for prose. Adjusted the Shorts
  migration plan: Free Flight ships as the first published short.

- 2026-06-09 — `npm install` for the pinned Astro 5 stack reports 2 known
  advisories (XSS in `define:vars`, server-island replay), both fixed only by
  jumping to Astro 6. Pinning to 5.x was a deliberate choice (matches `ao`'s
  proven config) — accepted for now, worth revisiting before this becomes a
  public-facing brand site.

- 2026-06-09 — Full build (steps 2-9) went smoothly: `npm run build` passed
  with zero errors on the first try, all 5 content frontmatter files validated
  against the zod schemas, all 9 routes returned 200 in `npm run preview`.
  Only verification gap: no browser/screenshot check, just curl + grep against
  the rendered HTML and CSS — confirmed system fonts only (no webfont
  `@import`), nav active-state underline wins the cascade (`.underline` is
  defined after `.no-underline` in Tailwind's generated output), and the
  Free Flight migration has no leftover heading or source-only sections.

- 2026-06-09 — Pushed to GitHub: https://github.com/andreortiz82/aoblog
  (public, branch `main`). Remaining: import the repo on Vercel (manual —
  CLI is installed but not authenticated), then update `astro.config.mjs`'s
  `site:` field once a domain is assigned and push again.

- 2026-06-09 — Pivot from the original "design a brand new identity later"
  plan: instead of a from-scratch system, aoblog adopts `ao`'s existing
  `DESIGN.md` (Fraunces/Instrument Sans/JetBrains Mono, ink/paper/red-accent
  tokens, italic-accent emphasis, mono nav-link underline), modified where
  appropriate — the bespoke widget CSS (iteration cards, stage grids, shadcn
  aliases) from `ao` is left out since aoblog has no React islands that need
  it. The "undesigned" baseline from Phase 1 is now the documented "before"
  in the DESIGN.md post rather than a long-lived state.

- 2026-06-09 — Phase 2 done: header now carries the `aologo.svg` mark (new
  `Logo.astro`, inlined with `currentColor`), `global.css` carries the
  Fraunces/Instrument Sans/JetBrains Mono stack plus ink/paper/accent tokens
  and the italic-accent emphasis system, nav links use the mono
  underline-on-active style, and page/post H1s are set in Fraunces (the
  homepage wordmark is `ao*blog*` using the emphasis system). `npm run build`
  passed clean for all 11 pages on the first try. Wrote a third post on what
  a `DESIGN.md` buys you, drawing on this exact port as the example.

- 2026-06-10 — Manual tweaks landed: header dropped its bottom border and
  grew the logo to `h-10`, the wordmark text next to it is commented out
  (mark-only), and the homepage hero is now `Creative *Blog*`. Wrote
  `DESIGN.md` at the project root to document the resulting system —
  tokens, type roles, emphasis system, logo usage, and an explicit
  "Differences from `ao`" section — as the authoritative reference for
  future visual changes.

- 2026-06-10 — aoblog will use shadcn/ui going forward. Renamed every
  color token in `global.css`'s `@theme inline` to shadcn naming
  (`--color-ink` → `--color-foreground`, `--color-paper` → `--color-muted`,
  `--color-ink-3` → `--color-muted-foreground`, `--color-line` →
  `--color-border`/`--color-input`, `--color-accent` →
  `--color-destructive`/`--color-ring`, `--color-accent-soft` →
  `--color-accent`, plus new `--color-primary`, `--color-secondary`,
  `--color-card`, `--color-popover`, and a `--radius` scale), kept
  `--color-ink-2` as the one aoblog-specific addition with no shadcn
  equivalent, and dropped the unused `--color-line-soft`/`--color-highlight`
  (selection now reuses `--color-accent`/`--color-destructive`). Updated
  every `text-ink*`/`bg-paper`/`border-line` Tailwind class across
  components and pages to match. Rewrote `DESIGN.md` to be self-contained
  — synced with `ao`'s structure, no "ported from / differences from `ao`"
  framing — documenting the new token table and a Radius section.
  `npm run build` passed clean for all 11 pages.
