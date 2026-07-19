# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

unslop is an open source agent skill that keeps AI artifacts (slop) out of everything an agent produces: prose, docs, UI copy, code, frontend design, and naming. Existing anti-slop skills only cover prose; covering all surfaces in one skill is the point.

This is a skill project, not an application. There is no build, lint, or test toolchain.

## Layout

- `skills/unslop/` is the deliverable: `SKILL.md`, a pure router, plus `references/` with one rules file per surface.
- `catalog/` is the pattern catalog the rules were distilled from: bad/good pairs per surface, tagged always-wrong or context-dependent and current or fading. It stays out of the skill and doubles as eval fixtures.
- `SOURCES.md` is the annotated source list the catalog was mined from.

## Design constraints

These are deliberate decisions; hold them when editing the skill:

- SKILL.md stays a pure router: mode definitions and routing only, never rules.
- No example snippets inside the skill. Bad examples prime the very pattern they warn against, and good ones anchor a uniform style. Examples belong in `catalog/`.
- Every rule carries both phrasings: a `Prevent:` line for generation and a `Detect:` line for auditing existing content.
- Ban lists hold only literal, mechanically greppable strings and symbols. Structural tells become rules instead.
- `docs.md` and `ui-copy.md` are deltas on `writing.md`, never standalone.
- Keep every file short. The files load into context, so length is a cost.
- The skill's own files must pass the skill's own rules: no em dashes, sentence-case headings, no manufactured structure.
