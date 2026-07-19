# Naming slop catalog

Phase 3 raw material for the naming surface: variables, functions, classes, files, projects, products, and invented entities like characters or example personas. Mined from six vetted phase 2 sources plus tells observed directly in model output, feeds phase 4's rule distillation, and the bad/good pairs double as phase 6 eval fixtures. Two sources measure real corpora (code_transformed's GitHub commit data, the Sci-Fi naming and Elara studies' generation counts); the rest are practitioner catalogs, with Ousterhout's chapter serving as the positive standard the tells are judged against.

Sources mined:
- code-transformed: code_transformed: LLM influence on code (Xu et al., EACL 2026)
- scifi-naming: The Sci-Fi naming problem (Laforge, 2025)
- elara: 2025 Name of the Year is Elara (Wattenberg, Namerology)
- ai-naming-defaults: Naming Conventions Making AI Code Readable (Joshi, 2026)
- naming-smells: Naming smells (Hilton, 2016)
- ousterhout-names: A Philosophy of Software Design, Choosing Names chapter (Ousterhout), used here as the counter-standard

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default or in aggregate); currency is current (typical of 2025-2026 models) or fading (mostly 2023-2024 era, rarer now).

## Vague and imprecise words

### Semantically empty generic names

Tags: contextual, current. Sources: ai-naming-defaults, naming-smells, ousterhout-names, own.

Nouns so generic they tell the reader nothing they didn't already assume: data, item, thing, value, result, info, temp, obj, and the same failure as foo/bar leaking out of throwaway examples into real code. Ousterhout calls generic naming the single most common failure in the "Choosing Names" chapter (generic names get "confused with other things"); Hilton's independent catalog makes the same point ("you already knew that without the vague name"); a 2026 guide to AI naming defaults confirms `data`, `item`, `thing`, `result` as the actual default AI code reaches for.

Bad:

> data

Good:

> userEmail

### A real word applied to the wrong concept

Tags: always, current. Sources: naming-smells, own.

A name that is correctly spelled and reads as confident, just attached to the wrong concept, which is worse than a vague name because nothing signals the reader to double-check it. Hilton catalogs this as applying "order" or "carrier" to concepts they don't actually match. The AI-generation version is a name that asserts a stronger guarantee than the implementation delivers, common wherever a model is filling in behavior it hasn't verified.

Bad:

```python
def get_average(scores):
    return statistics.median(scores)
```

Good:

```python
def get_median(scores):
    return statistics.median(scores)
```

### Reaching for a vague catch-all instead of fixing the design

Tags: contextual, current. Sources: ousterhout-names, own.

When a name is hard to choose because the thing it names actually bundles two or three unrelated concerns, the fix is to split the thing up, not to paper over the difficulty with a vague catch-all (options, config, context, data). Ousterhout: struggling to name something well "could indicate the variable may need a more straightforward definition." AI-generated code takes the catch-all instead of the split almost every time, since inventing a name costs nothing and restructuring the call site does.

Bad:

```python
def render(options):
    # options bundles theme, pagination state, and an auth token
    ...
```

Good:

```python
def render(theme, page, auth_token):
    ...
```

## Verbs, booleans, and collections

### Inconsistent or imprecise verb choice across a codebase

Tags: always, current. Sources: ai-naming-defaults, naming-smells, ousterhout-names.

The same operation gets a different verb depending on which file or session generated it: getUser in one module, fetchUser in another, loadUser in a third, forcing readers to hold three synonyms in mind for one action. The same imprecision shows up a level down as "get" used for something that actually computes or derives a value (Hilton's example: getScore for a function that runs a formula should be calculateScore), and as one name reused for two different concepts entirely, the exact bug Ousterhout traces to conflating fileBlock and diskBlock. None of these have a legitimate reason to coexist once they do; the inconsistency itself is the defect, not any individual verb choice.

Bad:

```js
// userService.js
function getUser(id) { ... }
// authService.js
function fetchUser(id) { ... }
// profileService.js
function loadUser(id) { ... }
```

Good:

```js
// userService.js, authService.js, profileService.js
function getUser(id) { ... }
```

### Missing boolean prefixes

Tags: contextual, current. Sources: ai-naming-defaults, naming-smells, own.

Boolean variables and parameters get named as bare nouns or adjectives, loading, permission, done, instead of is/has/can, so a reader can't tell a boolean apart from the data it gates without checking the type. This runs opposite to an older smell: Hilton flags is-prefixes as vestigial "Hungarian notation" in strongly typed languages where the type already carries the information. Current AI output undershoots the other way, dropping the prefix even in dynamically typed code where it's the only signal a reader gets.

Bad:

> loading, permission

Good:

> isLoading, hasPermission, canEdit

### Ambiguous singular/plural naming

Tags: contextual, current. Sources: ai-naming-defaults.

The same singular name used for both a single item and the collection holding many of them, so a reader can't tell whether a variable is scalar or array without reading the assignment. Joshi's 2026 guide to AI naming defaults names this directly: using the singular for both single items and arrays causes confusion at the call site.

Bad:

```js
const user = fetchAllUsers(); // actually an array
```

Good:

```js
const users = fetchAllUsers();
```

## Word shape and length drift

### snake_case bleeding into camelCase conventions

Tags: contextual, current. Sources: code-transformed.

LLM output carries a Python-flavored snake_case bias that shows up even in languages and codebases whose established convention is camelCase, causing drift within a single file rather than following what's already there. The bias is measured, not anecdotal: the proportion of Python function names using snake_case rose measurably across GitHub repos over the LLM-adoption period, described as an ongoing rise through the paper's most recent data point; C/C++ repos show the same pull toward snake_case, though noisier than the Python signal. The tell for review isn't "snake_case is wrong," it's a model overriding the codebase's own convention with its default.

Bad:

```js
// rest of the file uses camelCase throughout
function calculate_total(cart_items) {
  return cart_items.reduce((sum, i) => sum + i.price, 0);
}
```

Good:

```js
function calculateTotal(cartItems) {
  return cartItems.reduce((sum, i) => sum + i.price, 0);
}
```

### Over-explained, verbose naming

Tags: contextual, current. Sources: naming-smells, code-transformed, own.

Names built by stacking simple dictionary words instead of reaching for the one precise term that already exists, Hilton's "pidgin language" smell from 2016, is exactly the failure mode current AI naming reproduces by default rather than as an occasional lapse. Function and variable names have measurably lengthened in LLM-influenced repositories alongside the move away from abbreviations (an illustrative pair: ml, mlt becoming max_length, current_length); taken past the point of reasonable clarity, the same instinct produces names that restate every qualifier a function touches instead of naming what it does.

Bad:

> appointment_list, company_person, text_correction_by_editor

Good:

> calendar, employee, edit

### Cryptic abbreviations and symbol names

Tags: contextual, fading. Sources: naming-smells, code-transformed.

Ambiguous abbreviations that multiple different words commonly share (acc, pos, char, mod, auth) and bare symbolic operators borrowed from functional programming (the fish operator, `>=>`) used to be the default failure mode in hand-written code. Fresh LLM output rarely reproduces this now: single-letter variables and abbreviations are both in measured decline in LLM-influenced repos, and LLMs replace short forms with full words rather than the reverse. Worth checking for when de-slopping human-authored legacy code a model then extends, not something to expect a model to introduce on its own.

Bad:

> acc, pos, char, mod, auth

Good:

> (constructed) account, position, character, module, authentication

### Numeric and iteration suffixes

Tags: contextual, current. Sources: naming-smells, code-transformed, own.

Distinguishing two related things by a bare digit (employee2) tells the reader there are two of them but nothing about how they differ; Hilton's fix is a name for the actual distinction. Raw digit suffixes are measurably declining in LLM-influenced code, but the underlying shortcut persists in a different shape: word suffixes stapled onto a function or file that was just revised in place, Enhanced, Final, Updated, New, V2, rather than a name that reflects what changed or a clean rename. "Final" in particular is close to always false, since the file gets revised again.

Bad:

```python
def parseInvoiceFinal(data): ...
def parseInvoiceFinal_v2(data): ...
```

Good:

```python
def parse_invoice(data): ...  # handles multi-currency line items, see changelog
```

## Grandiosity and dumping grounds

### Grandiose class names

Tags: contextual, current. Sources: naming-smells, own.

Class and module names reach for maximum authority rather than description: Manager, Orchestrator, Engine, Processor, plus prefixes like Universal, Smart, and Intelligent that promise generality the implementation doesn't have. Hilton flags Manager specifically as failing to indicate function; the same failure now spreads across a whole family of grandiose nouns and adjectives that make a class sound architecturally important without changing what it actually is.

Bad:

> InvoiceManager

Good:

> (constructed) InvoiceApprover

### Utils and helpers dumping grounds

Tags: contextual, current. Sources: own.

A file or module named utils, helpers, common, or misc becomes a catch-all for anything that doesn't obviously belong somewhere else, so it accumulates unrelated functions over time and stops naming a concept at all. The fix isn't a better synonym for "misc," it's naming each file after what the functions inside it actually do together, which usually means there's more than one file.

Bad:

```text
src/
  utils.py   # date parsing, HTTP retries, currency formatting, slug generation
```

Good:

```text
src/
  dates.py
  http_retry.py
  currency.py
  slugs.py
```

## Invented people, products, and files

### AI-favorite names for invented people and example companies

Tags: contextual, current. Sources: elara, scifi-naming, own.

Ask several different models, independently, for a character, a user persona, or an example customer, and they converge on the same tiny pool of vowel-heavy, low-friction names. Wattenberg's 2025 Namerology piece names Elara as the standout AI-favorite based on Goodreads frequency, and the same article's broader inventory includes Elena, Clara, Nova, Luna, Aria, Lyra, Isabella, Mara, and surnames Voss and Vance appearing with unusual frequency. Laforge's independent test of sci-fi book descriptions found the same convergence: generated character names cluster on a small handful of repeated defaults, with each model tending toward its own signature name rather than a diverse spread; both sources trace the mechanism to models averaging toward the statistically densest pattern in their training data rather than sampling genuinely diverse names. The same pool covers fictional companies used in examples: Acme Corp, TechCorp, Globex, Initech, Contoso.

Bad:

> (constructed) Meet Elara, a data scientist at Acme Corp...

Good:

> (constructed) Meet Priya Ramanathan, a data scientist at Fenwick Analytics...

### Mythological and celestial names for real products and projects

Tags: contextual, current. Sources: scifi-naming, own.

The same convergence that produces Elara for characters produces Nexus, Orion, Atlas, Zenith, Apex, and Aether for products, internal tools, and side projects, mythological or celestial words chosen for gravitas rather than any connection to what the thing does. Laforge traces the mechanism to training-data density: for a narrow naming task the model's probability mass concentrates on a handful of statistically common patterns, and he notes explicitly that this generalizes past fiction to product and project naming.

Bad:

> (constructed) Project Nexus, Atlas, Zenith Platform

Good:

> (constructed) Ledger, an internal expense-reconciliation tool named for what it does

### Doc file names like FINAL_SUMMARY.md

Tags: contextual, current. Sources: own.

Ad hoc markdown files dropped at a repo root with names like SUMMARY.md, NOTES.md, FINAL_REPORT.md, or IMPLEMENTATION_PLAN.md are a giveaway that the file exists to summarize a conversation rather than to serve a reader later; the ALL_CAPS-plus-adjective pattern (FINAL, COMPLETE, UPDATED) is close to a fingerprint on its own. A file's name should say what it's for to someone who wasn't in the session that produced it.

Bad:

> (constructed) FINAL_SUMMARY.md, IMPLEMENTATION_COMPLETE.md, CHANGES_SUMMARY_UPDATED.md

Good:

> (constructed) migration-notes.md, auth-redesign.md
