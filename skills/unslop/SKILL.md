---
name: unslop
description: Keeps AI tells (slop) out of everything you produce and strips them from existing content. Use whenever you write prose of any kind, technical or creative (docs, READMEs, UI copy, landing and marketing copy, reports, fiction, essays), generate or edit code and tests, design or style a frontend, or name variables, functions, files, classes, projects, products, services, or invented people and companies, even when the user never mentions slop or AI. Also use when the user asks to de-slop, humanize, remove AI tells, audit content for AI artifacts, or make something sound less AI-generated.
---

# unslop

This file contains no rules. The rules live in `references/`, one file per surface, and they only work if you read them before producing anything. Do not generate first and check after; the point is that the rules shape the output from the start.

## Modes

**Prevent** (the default): you are about to produce new content. Read the reference files for every surface in play, then follow each rule's `Prevent:` line while you work.

**De-slop**: the user hands you existing content (a file, a diff, pasted text) to clean up. Read the reference files for the content's surfaces, search the content for every ban-list entry literally, test it against each rule's `Detect:` line, then rewrite what you find without changing meaning. Preserve facts, intent, and register; make the smallest rewrite that removes the artifact.

When a task both adds new content and edits existing content, run both modes: Prevent for what you write, De-slop for what you touch.

Ban lists apply in both modes: never emit an entry while generating, and grep for entries mechanically when de-slopping.

## Routing

Identify every surface the task touches, then read every matching file before you start. Most real tasks touch several surfaces at once, so treat the table as additive: read every file whose row matches any part of the task, not just the closest one.

| File | Read when the task involves |
|---|---|
| `references/writing.md` | Any prose at all. Base layer for the two overlays below. |
| `references/docs.md` | READMEs, documentation, long-form technical writing. Read with writing.md. |
| `references/ui-copy.md` | Interface text: labels, buttons, errors, empty states, onboarding, landing and marketing copy. Read with writing.md. |
| `references/code.md` | Any code or tests, including comments. |
| `references/frontend.md` | Visual or interaction design: layout, color, type, CSS, components, motion, how copy sits in the markup. |
| `references/naming.md` | Naming anything: variables, functions, files, classes, projects, products, invented people or companies. |

`docs.md` and `ui-copy.md` are overlays: they hold only the deltas on top of `writing.md` and are incomplete alone, so never read an overlay without its base.

Two pairings are easy to miss: code that introduces any name also needs `naming.md`, and frontend work whose UI shows any text also needs `ui-copy.md` with its base. Each file is short; reading one you barely need costs far less than skipping one you did need.

## Don't overcorrect

The goal is content shaped by its actual subject, audience, and intent, not a recognizable "anti-AI" style, which is just a different uniform. If applying a rule pushes the output toward sameness, look harder at what this specific content needs. In de-slop mode, when a flagged pattern is genuinely the clearest way to say the thing, leave it alone.
