---
title: "Before the Code: Planning With AI and Keeping a PLAN.md"
description: "This project started with a plan, not code — research, clarifying questions, and a written plan file. Why that plan became a living PLAN.md, updated all session, and what it caught along the way."
pubDate: 2026-06-09
category: meta
tags: ["planning", "claude-code", "process"]
draft: false
---

Before I wrote a single line of this site, I spent the first part of this session reading. Two sibling projects — my existing portfolio (`ao`) and a folder of in-progress short fiction (`writing`) — got read in full: configs, design tokens, identity docs, story drafts. Then came a round of clarifying questions about brand direction, stack, scope, and how to handle the Shorts migration. Only after all of that did planning actually start — and even then, the first deliverable wasn't code. It was a plan.

## Why write it down

A plan file is cheap to produce and cheap to redirect. Before any code exists, you can read the whole thing, push back on a section, and have it rewritten — at near-zero cost. Once code exists, redirecting gets more expensive: there's work to undo, not just words to revise.

There's a second reason, specific to a long session with an AI agent: a written plan is also a checklist that survives context. Across config files, content collections, layouts, pages, content, a build, and a deploy, it's easy for either of us to lose the thread. A plan with a literal checklist turns "what's left" into a lookup, not a recollection.

## Enter PLAN.md

So this session got a `PLAN.md`, written to the project root before any scaffolding, structured as two things: a phased checklist mirroring the build order, and a running **Log** of decisions and surprises. As each phase finished, the checklist got checked off and, if anything notable happened, a dated log entry got added. It's committed to the repo — part of building in the open, and the source material for this post.

## A concrete example

The very first log entry, written during planning before any code existed, reads:

> Discovered `writing/index.md` status labels don't match reality: "Free Flight" (marked "idea") has a complete ~700-word story; "Under Foot" (marked "complete") only has a placeholder for prose. Adjusted the Shorts migration plan: Free Flight ships as the first published short.

That single discovery flipped which story shipped as "published" versus "in development" — a real plan change, caught and recorded *before* any content files were written, not after.

A later entry, made mid-build, just notes that the build went smoothly: `npm run build` passed clean on the first try, and the only verification gap was no browser/screenshot check — just `curl` and `grep` against the rendered output. Small, but worth knowing later when deciding how much to trust "it built" as a signal.

## Did it hold up?

Yes, in a small but real way. The checklist turned each phase into a discrete, checkable unit instead of one long undifferentiated task. And the log turned "what happened during this session" from something I'd have to reconstruct from memory into something I could just read back — including this post.

## Takeaway

For an AI-assisted build, a `PLAN.md` is cheap insurance: it costs a few minutes up front, it gives you a natural place to record surprises as they happen, and — as this post demonstrates — it doubles as the first draft of the post you'll write about the build afterward.
