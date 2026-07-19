# unslop

Keep AI slop out of everything your agent produces.

unslop is a skill for Claude Code and any other harness that reads the agent-skill format. Existing anti-slop skills stop at prose; unslop also covers docs, UI copy, code, frontend design, and naming.

Slop is more than `delve` and em dashes. It's the purple accent on every landing page, the `utils.py` dumping ground, the test that only asserts a mock was called, the badge-row README with a roadmap nobody tracks, the invented character named Elara. unslop has rules for all of it.

## Install

```bash
git clone https://github.com/nattergabriel/unslop.git
mkdir -p your-project/.claude/skills
cp -R unslop/skills/unslop your-project/.claude/skills/
```

Any route to the same place works, ZIP download included. The final location is all that matters: `.claude/skills/unslop` for Claude Code (`~/.claude/skills/unslop` to get it everywhere), `.agents/skills/unslop` for harnesses using that convention.

> [!IMPORTANT]
> Copy the whole folder, not just `SKILL.md`. It's a pure router; without `references/` next to it there are no rules to load.

## Use

Nothing to invoke: the agent picks unslop up on its own whenever a task touches one of its surfaces, and the rules shape the output from the start. To clean up existing content instead, ask directly ("de-slop this file", "remove the AI tells from docs/"). If the agent doesn't pick the skill up on its own, invoke it manually, for example as a slash command.

## How it works

The skill runs in two modes:

- Prevent, the default: before generating anything, the agent reads the rules for the surfaces the task touches and follows them from the start.
- De-slop: hand the agent existing content (a file, a diff, pasted text) and it finds the artifacts and rewrites them without changing meaning.

`SKILL.md` only routes. The rules live in `references/`, one short file per surface, loaded just when that surface is in play:

| File | Covers |
|---|---|
| `writing.md` | general prose, the base layer for the two overlays |
| `docs.md` | READMEs and documentation, as a delta on the writing base |
| `ui-copy.md` | interface and marketing copy, as a delta on the writing base |
| `code.md` | code and tests |
| `frontend.md` | visual and interaction design |
| `naming.md` | names for code, files, products, and invented people |

Each rule is written for both modes: a `Prevent:` line to follow while generating and a `Detect:` line with criteria for auditing. Tells that are literal strings (banned words, hex colors, leaked citation markup) sit in ban lists that can be checked mechanically.

> [!NOTE]
> The skill contains no example snippets, on purpose. Bad examples prime the very pattern they warn against, and good examples anchor a uniform style, which is its own kind of slop.

## How it was made

The rules are distilled from documented patterns, not one person's taste. Three steps, run for each surface:

1. Gather and verify sources: community tell catalogs, prior anti-slop skills, practitioner articles on AI-looking design and code, research papers on machine-generated text, and a few classic style references as counterweights. The annotated list is in [SOURCES.md](SOURCES.md).
2. Mine the sources, plus direct observation, into a raw catalog: 159 patterns, each with a bad and a good example, tagged always-wrong or context-dependent, and current or fading in newer models. The fading tag matters because slop moves; rules against yesterday's tells distort today's output. The catalog lives in [catalog/](catalog/).
3. Distill the catalog into the rule files the skill ships. Literal tells became greppable ban lists, structural tells became criteria precise enough to test output against, and overlapping patterns were merged. Every rule carries both the prevent and the detect phrasing.
