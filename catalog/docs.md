# Docs and README slop catalog

Phase 3 raw material for the docs and README overlay: tells specific to software documentation and READMEs, mined from five vetted phase 2 sources plus field observations, each with one bad and one good example. This overlay assumes the writing base catalog underneath it and only adds the delta the docs medium introduces. Feeds the phase 4 rule distillation, and the bad/good pairs double as phase 6 eval fixtures.

Sources mined:
- ai-docs: What's wrong with AI-generated docs (Ferri-Benedetti, passo.uno, 2025)
- kill-ai-slop: kill-ai-slop field guide (yetone)
- llvm-policy: LLVM AI Tool Use Policy
- slop-burden: An Endless Stream of AI Slop (Baltes, Cheong, Treude, 2026)
- diataxis: Diataxis (Procida)

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default or in aggregate); currency is current (typical of 2025-2026 models) or fading (mostly 2023-2024 era, rarer now).

A few mined patterns don't get their own entry. ai-docs's title-casing tell and kill-ai-slop's marketing-voice tell ("it's not just X, it's Y", "say goodbye to X") are the base catalog's title-case-headings and not-only-but-also entries wearing a doc-shaped hat, with no docs-specific delta, so they aren't repeated here; most of the rest of kill-ai-slop's 33-tell catalogue is visual UI material that belongs to the frontend design surface. One exception is highlighted-keywords-midparagraph: it needs no CSS or rendering, it shows up directly in markdown prose, so it gets its own entry below instead of being swept into the frontend pile. llvm-policy turned out to be entirely about PR, commit, and contribution-review discipline, the git surface PLAN.md marks out of scope for now, not doc content itself, so none of its patterns appear below. slop-burden's Stack Overflow and DevRel-layoff observations describe ecosystem-wide degradation rather than a pattern checkable in a specific doc; they inform the framing of the truthfulness entries below without becoming entries of their own.

## README genre reflexes

### READMEtitis

Tags: contextual, current. Sources: ai-docs, kill-ai-slop, own.

Ferri-Benedetti's core complaint about AI-generated docs is that they default to the genre of a hastily thrown-together GitHub README instead of a deliberate house style, a "frankentongue made of cliches and bad practices." In README form specifically that means a badge row across the top that reads as pure decoration (kill-ai-slop: "manufacturing fake buzz; in bulk each stops meaning anything"), an emoji glued to every section heading ("a glyph before every point is louder, not clearer"), and a rocket in front of "Getting Started" whether or not the project ships fast.

Bad:

```markdown
![Build](https://img.shields.io/badge/build-passing-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue) ![Stars](https://img.shields.io/badge/stars-1.2k-yellow) ![PRs Welcome](https://img.shields.io/badge/PRs-welcome-orange)

## 🚀 Getting Started

## ⚡ Features

## 🔒 Security
```

Good:

```markdown
![CI](https://img.shields.io/github/actions/workflow/status/acme/widget/ci.yml)

## Getting started

## Features

## Security
```

### Scattered mid-paragraph bolding

Tags: always, current. Sources: kill-ai-slop.

Bolded or colored words dropped mid-paragraph as if a highlighter swept over the text at random, so that nothing is actually emphasized. kill-ai-slop names this as a general tell, but it needs no CSS or rendering to show up: it lands directly in plain markdown prose, docs and READMEs included, as scattered bold phrases with no shared reason for being bold.

Bad:

```markdown
Our library handles **authentication**, **rate limiting**, and **caching**
automatically, so you can focus on **your actual product** instead of
**infrastructure concerns**.
```

Good:

```markdown
Our library handles authentication, rate limiting, and caching
automatically, so you can focus on your product instead of infrastructure.
```

### Invented stat row

Tags: always, current. Sources: kill-ai-slop, own.

Three round, unverified numbers dropped into a README as social proof on a project with no track record to back them, functioning as set dressing rather than evidence: the numbers aren't measured, they're chosen to look impressive.

Bad:

> 10k+ developers · 99.9% uptime · 24/7 support

Good:

> (constructed) Used in production by 12 teams as of July 2026; see [adopters.md](./adopters.md) for the list.

### Aspirational roadmap checkboxes

Tags: contextual, current. Sources: own.

A "Roadmap" section listing generic future milestones as checkboxes, mobile app, enterprise features, AI-powered insights, that reflect no actual planning decision, just the shape of a roadmap. A real roadmap with real checkboxes, tied to issues or dates, is fine; the tell is the invented, evenly-spaced items that could belong to any product.

Bad:

```markdown
## Roadmap

- [x] Core functionality
- [ ] Mobile app
- [ ] Enterprise features
- [ ] AI-powered insights
```

Good:

```markdown
## Roadmap

- [x] CLI (shipped v1.0, June 2026)
- [ ] Windows support (tracked in #214)
```

### Comparison tables no one asked for

Tags: contextual, current. Sources: own.

An unsolicited "Us vs. Competitor A vs. Competitor B" table stamped into a README, all checkmarks for the home project and a mix of X marks and shrugs for everyone else, sourced from nowhere. Comparison tables earn their place in a migration guide or a genuine feature matrix; the tell is reaching for one as decoration when nobody asked how this project stacks up against anything.

Bad:

```markdown
| Feature | Us | Competitor A | Competitor B |
|---|---|---|---|
| Speed | ✅ | ❌ | ⚠️ |
| Ease of use | ✅ | ✅ | ❌ |
| Reliability | ✅ | ⚠️ | ❌ |
```

Good:

```markdown
| | v1 config format | v2 config format |
|---|---|---|
| Env vars | `.env` file | `config.yaml` |
| Auth | API key in header | OAuth token |
```

### Unsolicited extra doc files

Tags: always, current. Sources: own.

Claude generates markdown files nobody requested, SUMMARY.md, IMPLEMENTATION_NOTES.md, CHANGES_MADE.md, that document the work session rather than the product, cluttering the repo with artifacts of the process instead of knowledge a reader would look for.

Bad:

```text
docs/
  README.md
SUMMARY.md
IMPLEMENTATION_NOTES.md
CHANGES_MADE.md
```

Good:

```text
docs/
  README.md
```

### Table of contents for a doc that doesn't need one

Tags: contextual, current. Sources: own.

An auto-generated table of contents with anchor links added to a README short enough to read top to bottom in ten seconds, structural overhead standing in for actual navigation need. A TOC earns its place once a doc has enough sections that jumping around actually helps; below that it's furniture.

Bad:

```markdown
## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Installation
`npm install widget`

## Usage
`widget run`

## License
MIT
```

Good:

```markdown
## Installation
`npm install widget`

## Usage
`widget run`

## License
MIT
```

## Boilerplate sections with no project-specific content

### Generic prerequisites and setup steps

Tags: contextual, current. Sources: own.

A "Prerequisites" section listing things true of nearly every project, a computer with internet access, basic command-line familiarity, instead of the actual version constraints and services this specific project needs.

Bad:

```markdown
### Prerequisites

- A computer with internet access
- Basic understanding of the command line
- Node.js installed
```

Good:

```markdown
### Prerequisites

- Node.js 20 or later (`node -v` to check)
- A Postgres instance reachable at `DATABASE_URL`
```

### Boilerplate Contributing and License prose

Tags: contextual, current. Sources: own.

Generic contribution steps, fork, branch, pull request, that are true of any GitHub repo and say nothing about how to actually develop against this one: no setup command, no test command, no style tool. The License section suffers the same way, a full paragraph of stock MIT-license prose where a one-line pointer to the file would do.

Bad:

```markdown
## Contributing

Contributions are welcome! Please fork the repository, create a feature branch, and submit a pull request. We appreciate all contributions, big or small!

## License

This project is licensed under the MIT License. See the LICENSE file for details.
```

Good:

```markdown
## Contributing

Run `make setup` to install dependencies and pre-commit hooks, then `make test` before opening a PR. We use `ruff` for linting; `make lint` catches most issues.

## License

MIT, see [LICENSE](./LICENSE).
```

### Admonition callouts used for every line

Tags: contextual, current. Sources: kill-ai-slop.

A docs admonition box turned into universal decoration: every step, every aside, every changelog row wrapped in its own callout until every line looks like an important note and none of them are. kill-ai-slop names the general pattern; in docs it shows up as GitHub's `[!NOTE]` syntax (or a MkDocs/Docusaurus admonition) applied mechanically instead of reserved for the one or two things a reader genuinely needs flagged.

Bad:

```markdown
> [!NOTE]
> Run `npm install` first.

> [!NOTE]
> This step is optional if you're only reading the docs.

> [!NOTE]
> See the configuration section below.
```

Good:

```markdown
Run `npm install` first. This step is optional if you're only reading the docs; see [Configuration](#configuration) for details.

> [!WARNING]
> Skipping this step will break `npm run dev` on Node 22.
```

## Information architecture and audience

### Doc-type mode collapse

Tags: always, current. Sources: diataxis.

Diataxis names four distinct reader needs, tutorial, how-to guide, reference, explanation, and most AI-generated doc-structure problems come from collapsing them into one document. A getting-started tutorial gets padded with architecture explanation mid-step that the learner didn't ask for yet ("writers... anxious that their students should know things overload their tutorials with distracting and unhelpful explanation"); a how-to guide for an already-competent user opens with "What is TLS?" instead of the steps; and a single README tries to teach, instruct, describe, and justify all at once, so it serves none of the four needs fully. Diataxis calls this blurring "at the heart of a vast number of problems in documentation."

Bad:

```markdown
## Getting Started

TLS is a cryptographic protocol that provides secure communication over a
network by encrypting data in transit using a combination of symmetric and
asymmetric cryptography...

Now, to enable it, run:

    server.tls = true
```

Good:

```markdown
## Getting started

Run this to enable TLS:

    server.tls = true

See [How TLS works in this server](./explanation/tls.md) for the background.
```

### Reference polluted with narrative and rationale

Tags: always, current. Sources: diataxis.

Reference material is supposed to be dry, accurate, and structured to mirror the system it describes. AI-generated reference sections instead wander into discursive justification for why something was designed a certain way, and order entries by whatever the model found most interesting rather than by the actual module or namespace structure, both of which belong in a separate explanation doc, not the lookup table.

Bad:

```markdown
### `Client.retry()`

We designed retry() this way because we believe resilience should be a
first-class concern in modern distributed systems, and early users kept
asking for it. Takes a `count` and an optional `backoff` strategy.
```

Good:

```markdown
### `Client.retry(count, backoff=None)`

Retries the last failed request up to `count` times. `backoff` is a callable
taking the attempt number and returning seconds to wait; defaults to no delay.
```

### No content-reuse strategy across a doc set

Tags: always, current. Sources: ai-docs.

LLMs write locally coherent pages with no sense of the doc set as a whole: ask for docs on three related features and each page re-explains the shared concept from scratch, slightly differently, with no cross-linking or single source of truth. Ferri-Benedetti frames this as a missing "global vision": deciding what not to repeat is as much a documentation skill as deciding what to include.

Bad:

```text
docs/projects.md:
"A workspace is a container that groups related projects under one billing
account..."

docs/billing.md:
"Workspaces let you group projects for billing purposes; each workspace has
its own..."

docs/api-keys.md:
"Recall that a workspace groups your projects together for organizational
and billing reasons..."
```

Good:

```text
docs/concepts/workspace.md:
"A workspace groups related projects under one billing account. [full
definition]"

docs/billing.md:
"Billing is scoped per workspace; see Workspaces for what that means."

docs/api-keys.md:
"API keys are scoped per workspace; see Workspaces."
```

### Features section listing adjectives instead of behavior

Tags: always, current. Sources: own.

A "Features" section names qualities the product supposedly has, fast, secure, flexible, scalable, without saying what it actually does that earns any of them. A competent reader can't act on "flexible", only on a specific mechanism; this is the copy-side twin of kill-ai-slop's rounded-icon-tiles-grid, the visual habit of tiling a feature grid with icons that rarely relate to the content underneath.

Bad:

```markdown
## Features

- ⚡ Fast
- 🔒 Secure
- 🔧 Flexible
- 📈 Scalable
```

Good:

```markdown
## Features

- Cold start under 50ms by keeping the runtime warm between invocations
- Secrets are encrypted at rest with per-tenant keys, never logged
- Config is a single YAML file; swap the storage backend without touching app code
```

## Truthfulness and product grounding

### Hallucinated commands, flags, and APIs

Tags: always, current. Sources: ai-docs, slop-burden.

Docs state a command, flag, or method that doesn't exist, in the same confident register as verified facts, with nothing flagging the uncertainty. Ferri-Benedetti is blunt about it: "LLMs lie even at the most basic level... they make up things constantly in plausible and hard-to-detect ways." Developers are reporting hitting this live in the wild too, slop-burden's fetch surfaced a single but pointed Reddit quote on it: "or it's just completely wrong or using a class that doesn't exist."

Bad:

> (constructed) Run `npm run generate:docs --strict` to validate your setup.

Good:

> (constructed) Run `npm run generate:docs` to build the docs. Add `--watch` to rebuild on file changes.

### Hollow docs missing the caveats or steps that make them usable

Tags: always, current. Sources: ai-docs, slop-burden.

Docs describe a feature accurately at the surface and stop there, missing exactly the caveats, edge cases, and known pain points that only come from actually using the product or reading its support history. Ferri-Benedetti calls the result "hollow" and says catching it takes "a caring, organic writer" familiar with the support queue. Developers are naming the same gap from the reading side: one Reddit poster put it as documentation and tutorials "missing key information and code samples needed to be able to implement something," evidence worth noting but thinner, a single quote from a qualitative study rather than a technical writer's direct analysis.

Bad:

> (constructed) This endpoint returns the resource.

Good:

> (constructed) This endpoint returns the resource. Note: pagination breaks past 10k rows (see #452); rate-limited to 5 req/s.

### Docs that restate the signature

Tags: always, current. Sources: own.

A reference entry just translates the signature back into a sentence, "gets the user by id" for `getUser(id: string): User`, without saying anything the signature didn't already show: what happens on a miss, whether it throws or returns null, whether the result is cached, what units a numeric parameter is in.

Bad:

```text
getUser(id: string): User
Gets the user by id.
```

Good:

```text
getUser(id: string): User
Fetches the user record. Throws NotFoundError if no user with that id
exists; never returns null. Result is cached for 60s per id.
```
