---
title: "What a DESIGN.md File Buys You"
description: "aoblog just inherited its visual identity from another project's DESIGN.md in a single pass. That only worked because the design system was written down — tokens, type roles, and the reasoning behind them."
pubDate: 2026-06-09
category: design-systems
tags: ["design-systems", "documentation", "claude-code"]
draft: false
---

This site just changed its look — fonts, color tokens, an accent color, a logo, an italic-emphasis system for headings — in one pass, with no back-and-forth about hex values or font names. That was possible because none of those decisions had to be made today. They were already made, for a different project, and written down.

My main portfolio, `ao`, has a `DESIGN.md`: a file describing its visual language in plain language — color tokens and what each is *for*, a three-typeface system with a role for each, an "italic fragments turn red" emphasis system for headlines, spacing, and motion. Porting that to `aoblog` wasn't "copy `global.css` and hope nothing breaks" — it was read the rules, apply the ones that fit, and skip the ones that don't.

`aoblog` picked up the typefaces, the ink/paper/accent tokens, the mono nav-link underline, and the emphasis rule — now doing real work in the `ao*blog*` wordmark in the header. It did *not* pick up `ao`'s interactive-widget CSS (iteration cards, stage grids, shadcn aliases), since `aoblog` has no React islands that need them. Without `DESIGN.md`, that triage would've meant reading 550+ lines of CSS and guessing which rules were "the design system" versus "leftover from one widget." With it, the distinction was already made.

Code is the design system as it currently exists. A `DESIGN.md` is the design system as a set of *decisions* — portable, explainable, and arguable in a way a stylesheet alone isn't. The payoff isn't just for a human revisiting a project months later; it's for handing the same rules to an AI agent working on a different codebase, and getting a result that fits on the first try.
