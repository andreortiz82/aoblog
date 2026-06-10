# aoblog — CLAUDE.md

A build journal documenting design systems, brand, and product work done
with AI, plus a side channel of AI-assisted short fiction (`/shorts`).
Owner: **Andre Ortiz**.

---

## Maintenance Protocol

| File | Owns |
| --- | --- |
| [CLAUDE.md](CLAUDE.md) | Tech stack, commands, file structure, content schemas |
| [DESIGN.md](DESIGN.md) | Visual language, typography, color, logo — **authoritative** |
| [PLAN.md](PLAN.md) | Build checklist + running log of decisions/surprises |
| [README.md](README.md) | Minimal project overview |

**Update when:**
- Stack, commands, file structure, or content schema changes → **CLAUDE.md**
- A visual/typographic/spacing/logo decision changes → **DESIGN.md**
- A build phase completes, or a notable decision/surprise happens → **PLAN.md**

Cross-reference instead of duplicating — point to the authoritative file.

---

## Commands

```bash
npm run dev       # dev server → http://localhost:4321
npm run build     # production build → ./dist
npm run preview   # preview the dist build
npm run astro     # raw astro CLI (e.g. `npm run astro sync`)
```

---

## Stack

| Layer | Detail |
| --- | --- |
| Framework | Astro 5 — static-first, content collections via the Content Layer API |
| Styling | Tailwind v4 via `@tailwindcss/vite`. Theme lives entirely in `src/styles/global.css` — no `tailwind.config.js` |
| Content | MDX-capable (`@astrojs/mdx`), but posts/shorts are currently plain Markdown |
| Islands | `@astrojs/react` is installed but unused — no React components yet |
| Sitemap | `@astrojs/sitemap`, generated at build time |

---

## Project structure

```
src/
├── components/
│   ├── BaseHead.astro    # <head> meta, OG/Twitter tags, imports global.css
│   ├── Header.astro      # Logo + nav (Blog / Shorts / About)
│   ├── Footer.astro      # Copyright + link to andreortiz.com
│   ├── Logo.astro        # Inlines public/aologo.svg with currentColor
│   └── FormattedDate.astro
├── layouts/
│   ├── BaseLayout.astro  # <html> + Header + <main> + Footer
│   └── PostLayout.astro  # Shared by blog posts and shorts detail pages
├── content/
│   ├── blog/             # Blog posts — see schema below
│   └── shorts/           # Short fiction — see schema below
├── content.config.ts     # Zod schemas for both collections
├── consts.ts             # SITE_TITLE, SITE_DESCRIPTION
└── pages/
    ├── index.astro
    ├── about.astro
    ├── blog/{index.astro, [...slug].astro}
    └── shorts/{index.astro, [...slug].astro}
```

---

## Content collections

Defined in `src/content.config.ts` via `glob()` loaders over
`src/content/{blog,shorts}/**/*.{md,mdx}`.

### `blog`

| Field | Type | Notes |
| --- | --- | --- |
| `title` | `string` | |
| `description` | `string` | |
| `pubDate` | `date` | coerced from string |
| `updatedDate` | `date?` | optional |
| `category` | `enum` | `design-systems` \| `brand` \| `product` \| `meta` |
| `tags` | `string[]?` | optional |
| `draft` | `boolean` | default `false` |
| `heroImage` | `string?` | optional, used as OG image |

File naming convention: `YYYY-MM-DD-slug.md` (date-prefixed for sort order
and to match the `pubDate`).

### `shorts`

| Field | Type | Notes |
| --- | --- | --- |
| `title` | `string` | |
| `summary` | `string` | doubles as logline/dek |
| `genre` | `string[]` | e.g. `["sci-fi", "horror"]` |
| `status` | `enum` | `published` \| `in-development` |
| `format` | `enum` | `short` \| `serial`, default `short` |
| `pubDate` | `date?` | optional — only set once published |
| `cover` | `string?` | path under `public/`, e.g. `/covers/under-foot.png` |
| `draft` | `boolean` | default `false` |

Every short gets a detail page (`/shorts/[slug]`) regardless of `status` —
in-development entries render their synopsis instead of full prose.

---

## Styling

All tokens, fonts, and component classes (`.nav-link`, `.meta-tag`,
`.prose-plain`) live in `src/styles/global.css`. For the rationale behind
those choices — color roles, typeface roles, the italic-accent emphasis
system, logo usage — see [DESIGN.md](DESIGN.md).
