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
- [ ] 12. Vercel import (manual, user step — CLI not authenticated)

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
