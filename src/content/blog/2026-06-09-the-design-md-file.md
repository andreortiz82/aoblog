---
title: "What a DESIGN.md File Buys You"
description: "aoblog just inherited its visual identity from another project's DESIGN.md in a single pass. That only worked because the design system was written down — tokens, type roles, and the reasoning behind them."
pubDate: 2026-06-09
category: design-systems
tags: ["design-systems", "documentation", "claude-code"]
draft: false
---

This site just changed its look — fonts, color tokens, an accent color, a logo, an italic-emphasis system for headings — in one pass, with no back-and-forth about hex values or font names. That was possible because none of those decisions had to be made today. They were already made, for a different project, and written down.

## The source of truth

My main portfolio, `ao`, has a `DESIGN.md`: a single file describing its visual language — color tokens and what each one is *for*, the three-typeface system (a serif for display, a sans for body, a mono for metadata) with the role each plays, an "italic fragments turn red" emphasis system for headlines, spacing rhythm, and motion rules. It cross-references two sibling files — `AO.md` for brand voice and `CLAUDE.md` for the literal token names and CSS — but `DESIGN.md` itself is the part written in plain language: not just *what* the values are, but *why*.

That last part is what made today's work fast. Porting `ao`'s look to `aoblog` wasn't "go copy `global.css` and hope nothing breaks." It was: read the rules, apply the ones that fit, and consciously skip the ones that don't.

## What traveled, what didn't

`aoblog` picked up the typefaces, the ink/paper/accent color tokens, the mono-uppercase nav link with its underline animation, and the rule that an italicized word in a heading renders in the accent color — that's now doing real work in the new `ao*blog*` wordmark in the header. It did *not* pick up `ao`'s interactive-widget CSS (iteration cards, stage grids, shadcn aliases) — `aoblog` has no React islands that need them, and `DESIGN.md` made it obvious which parts were core visual language versus which were component-specific.

Without the document, that triage would've meant reading through 550+ lines of `global.css` and guessing which rules were "the design system" and which were "leftover from one widget." With it, the distinction was already made — by the person (well, the AI-and-human pair) who wrote it down the first time.

## A quiet form of consistency

There's a second effect, less about speed and more about coherence: `aoblog` and `ao` now visibly belong to the same person, without either site having to say so. The accent red, the way headings get one italicized word, the mono nav links — those are recognizable choices, and they're recognizable *because* they were specified once, generally, rather than invented twice, specifically.

This wasn't the original plan — [the build plan](https://github.com/andreortiz82/aoblog/blob/main/PLAN.md) called for `aoblog` to get its own from-scratch identity later, with the "undesigned" baseline from Day One as a placeholder. That's still true in spirit: the *content* and *voice* of this site are its own. But the visual system underneath didn't need to be reinvented to feel distinct — it needed to be applied with judgment, which is exactly what a written `DESIGN.md` makes possible.

## Takeaway

Code is the design system as it currently exists. A `DESIGN.md` is the design system as a set of *decisions* — portable, explainable, and arguable in a way a stylesheet alone isn't. The payoff isn't just for humans revisiting a project months later; it's for exactly this scenario — handing the same rules to an AI agent working on a different codebase, and getting a result that fits on the first try.
