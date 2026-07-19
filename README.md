# unslop

A skill that keeps AI artifacts (slop) out of everything an AI agent produces: prose, docs, UI copy, code, frontend design, and naming. Existing anti-slop skills cover prose. unslop covers all the surfaces in one skill.

Slop is more than `delve` and em dashes. It's the purple accent on every landing page, the `utils.py` dumping ground, the test that only asserts a mock was called, the README with a badge row and a roadmap nobody tracks, the invented character named Elara. unslop carries rules for all of it.

## How it works

The skill runs in two modes:

- Prevent, the default: before generating anything, the agent reads the rules for the surfaces the task touches and follows them from the start.
- De-slop: hand the agent existing content (a file, a diff, pasted text) and it finds the artifacts and rewrites them without changing meaning.

`SKILL.md` is a router with no rules of its own. The rules live in `references/`, one short file per surface, loaded only when that surface is in play:

| File | Covers |
|---|---|
| `writing.md` | general prose, the base layer for the two overlays |
| `docs.md` | READMEs and documentation, as a delta on the writing base |
| `ui-copy.md` | interface and marketing copy, as a delta on the writing base |
| `code.md` | code and tests |
| `frontend.md` | visual and interaction design |
| `naming.md` | names for code, files, products, and invented people |

Each rule is written for both modes: a `Prevent:` line to follow while generating and a `Detect:` line with the criteria for auditing. Tells that are literal strings (banned words, hex colors, leaked citation markup) sit in ban lists that can be checked mechanically.

> [!NOTE]
> The skill contains no example snippets, on purpose. Bad examples prime the very pattern they warn against, and good examples anchor a uniform style, which is its own kind of slop. The bad/good pairs live in `catalog/` as working material and eval fixtures instead.

## How it was made

The rules are distilled from documented patterns, not from one person's taste. Three steps, run for each surface:

1. Gather and verify sources: community tell catalogs, prior anti-slop skills, practitioner articles on AI-looking design and code, research papers on machine-generated text, and a few classic style references as counterweights. The annotated list is in [SOURCES.md](SOURCES.md).
2. Mine the sources, plus direct observation, into a raw catalog: 159 patterns, each with a bad and a good example, tagged always-wrong or context-dependent, and current or fading in newer models. The fading tag matters because slop moves; rules against yesterday's tells distort today's output. The catalog lives in [catalog/](catalog/).
3. Distill the catalog into the rule files the skill ships. Literal tells became greppable ban lists, structural tells became criteria precise enough to test output against, and overlapping patterns were merged. Every rule carries both the prevent and the detect phrasing.

## Install

The skill is a folder in the common agent-skill format: a `SKILL.md` with frontmatter, plus the `references/` it loads. Clone the repo or download it as a ZIP (the Code button on GitHub), then copy `skills/unslop` into your harness's skills directory:

```bash
git clone https://github.com/nattergabriel/unslop.git
cp -R unslop/skills/unslop /path/to/project/.claude/skills/unslop
```

How you get the folder doesn't matter; where it ends up does. For Claude Code that's `.claude/skills/unslop` in a project, or `~/.claude/skills/unslop` for every project. For harnesses using the `.agents` convention it's `.agents/skills/unslop`.

> [!IMPORTANT]
> Copy the whole folder, not just `SKILL.md`. It's a pure router; without `references/` next to it there are no rules to load.

## Use

Nothing to invoke for prevent mode: the agent picks the skill up from its description whenever a task touches one of the surfaces. For de-slop mode, ask directly ("de-slop this file", "remove the AI tells from docs/"). Harnesses with slash commands can also run it explicitly, as `/unslop` in Claude Code.
