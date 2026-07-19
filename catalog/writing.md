# Writing base slop catalog

Phase 3 raw material for the writing base surface: general prose tells mined from six vetted phase 2 sources plus field observations from reading model output directly, each with one bad and one good example. This is the base layer every text surface shares; the docs/README and UI copy overlays add only their medium-specific deltas on top of it. Feeds the phase 4 rule distillation, and the bad/good pairs double as phase 6 eval fixtures.

Sources mined:
- wiki-signs: Wikipedia: Signs of AI writing (WikiProject AI Cleanup)
- humanizer: humanizer skill v2.8.2 (blader)
- excess-vocab: Delving into LLM-assisted writing via excess vocabulary (Kobak et al., Science Advances 2025)
- llm-grammar: Do LLMs write like humans? Grammatical and rhetorical styles (Reinhart et al., PNAS 2025)
- llm-style-notebook: LLM writing styles bibliography (Alex Reinhart, updated June 2026)
- orwell: Politics and the English Language (Orwell, 1946)

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default or in aggregate); currency is current (typical of 2025-2026 models) or fading (mostly 2023-2024 era, rarer now).

One thing didn't make the cut: humanizer's subjectless-passive-fragment pattern ("No config needed. Results preserved automatically.") is product microcopy, not general prose, so it belongs to the UI copy overlay instead of here. A general caveat from humanizer applies across several entries below regardless: a single em dash, one curly quote, or one instance of formal vocabulary proves nothing by itself, these are tells in clusters and at frequency, not in isolation.

## Vocabulary and register

### Worn metaphor vocabulary

Tags: contextual, current. Sources: wiki-signs, orwell, llm-grammar.

Words like tapestry, landscape, testament, weave, and interplay get reached for because they're the path of least resistance, the same mechanism Orwell named in "dying metaphors" eighty years earlier. The concentration is extreme: instruction-tuned models use tapestry, camaraderie, and palpable at 100 to 170 times the rate found in comparable human writing. Wikipedia's cleanup catalog treats the flagged word list as a moving target rather than a fixed one: the favorites shift as new model generations take over, so the specific set worth watching for keeps turning over even though the underlying reaching-for-the-nearest-cliche habit doesn't.

Bad:

> (constructed) Their palpable camaraderie wove an intricate tapestry of trust.

Good:

> (constructed) They trusted each other and worked well together.

### Excess style verbs

Tags: contextual, current. Sources: wiki-signs, humanizer, excess-vocab, llm-style-notebook.

The verb cluster: delve, underscore, showcase, foster, garner, highlight, enhance. Kobak et al.'s PubMed analysis found these words showing up at extreme ratios versus the pre-ChatGPT baseline, skewed toward verbs and adjectives more than earlier vocabulary shifts were, with a measurable share of 2024 abstracts carrying at least one of these markers. It's not a fixed list forever: Reinhart's bibliography tracks these same words rising sharply in 2023-2024 psychology writing and already declining by 2025 as writers and detection pressure adapted, with adoption skewed toward lower-ranked institutions and non-native English speakers. That means the exact words listed here are already dated; what stays current is the mechanism, an unusual, elevated-frequency cluster of over-formal verbs worth checking for, refreshed release over release rather than this fixed list forever.

Bad:

> meticulously delving into the intricate web... comprehensive grasp of the intricate interplay

Good:

> (constructed) looking at the complex relationship

### Latinate register inflation

Tags: contextual, current. Sources: orwell, llm-style-notebook.

Choosing an elaborate, foreign-derived word over the plain native one to sound more scientific or authoritative. Orwell's own list is utilize, phenomenon, eliminate, cul de sac, status quo, and his rule was blunt: never use a long word where a short one will do. Reinhart's bibliography finds the instruction-tuned version of the same habit measurably in current models too, a shift toward Romance-origin vocabulary after tuning, suggesting the tuning process itself pushes toward formal, prestige-coded language rather than the plainer register a base model produces.

Bad:

> phenomenon, utilize, eliminate, cul de sac, status quo

Good:

> (constructed) thing, use, remove, dead end, current state

### Copula avoidance

Tags: contextual, current. Sources: wiki-signs, humanizer.

Swapping a plain is/are for something that sounds more considered: serves as, boasts, functions as, marks. Wikipedia's cleanup catalog documents a measurable decline in is/are usage in academic writing post-2023; humanizer independently names the identical substitution as one of its core language patterns.

Bad:

> ...serves as LAAA's exhibition space

Good:

> (constructed) ...is LAAA's exhibition space

### Significance inflation and legacy-speak

Tags: contextual, current. Sources: wiki-signs, humanizer, orwell.

Inflating a minor, unremarkable fact into something that stands as a testament, marks a pivotal moment, or leaves an indelible mark, phrasing wiki-signs found so generic it applies to nearly any subject, a kind of regression to the mean dressed up as analysis. Orwell caught the same move seventy years earlier from the other direction: big abstract words like values, freedom, and justice used as if their meaning were self-evident, standing in for an actual argument. The modern equivalents are impact, landscape, and framework.

Bad:

> marking a pivotal moment in the evolution of regional statistics

Good:

> (constructed) the office began publishing regional data quarterly

### Promotional travel-guide language

Tags: contextual, current. Sources: wiki-signs, humanizer.

Sales-pitch words, nestled, vibrant, breathtaking, rich cultural heritage, applied to a subject that was never being sold. It reads fine in an actual travel brochure; the tell is the same tone showing up on a town, a company, or a person with nothing to do with tourism.

Bad:

> Nestled within a breathtaking region...vibrant town with rich cultural heritage

Good:

> (constructed) The town, population 4,200, sits in a river valley.

### Elegant variation and lexical-diversity inflation

Tags: contextual, current. Sources: wiki-signs, humanizer, llm-style-notebook.

Cycling through near-synonyms, Soviet artistic constraints, non-conformist artists, these creators, instead of just repeating the one noun that's actually clearest, a habit wiki-signs traces to repetition-penalty tuning. It runs against the popular assumption that AI text is repetitive: corpus research finds LLM writing shows measurably greater lexical diversity than comparable human writing. The variation-seeking is real, it's just aimed at the wrong target.

Bad:

> Soviet artistic constraints...Non-conformist artists...Their creativity

Good:

> (constructed) Soviet artists worked under state constraints. These artists developed strategies to...

## Sentence and clause construction

### Not-only-but-also parallelism

Tags: contextual, current. Sources: wiki-signs, humanizer.

"Not only X, but also Y" retroactively frames a plain fact as a surprise reveal. Humanizer catalogs the marketing-flavored sibling, "it's not just a tool, it's a solution," often with a tailing negation like "no guessing" bolted on for punch.

Bad:

> not only a work of self-representation, but a visual document

Good:

> (constructed) a work of self-representation and a visual document

### Manufactured false contrast

Tags: contextual, current. Sources: wiki-signs.

Two related moves: denying an expected trait outright before asserting the real one ("not grounded in visual mastery, but in performative enactment") purely to manufacture depth, and the milder "X rather than Y," which does the same work with less rhetorical weight. Wiki-signs catalogs the rather-than form as its own construction, used to manufacture rhetorical tension between two options that didn't actually need to be set against each other.

Bad:

> not grounded in visual mastery, but in what...terms performative enactment

Good:

> (constructed) grounded in performative enactment

### Rule-of-three triplet padding

Tags: contextual, current. Sources: wiki-signs, humanizer, llm-grammar.

Adjectives and short phrases get forced into groups of exactly three, fast, reliable, and secure, to simulate a thoroughness that isn't there. Reinhart's Biber-feature analysis confirms the underlying habit: instruction-tuned models coordinate short phrases well above the human rate, strongest in GPT variants. That's phrasal coordination, joining short phrases and adjectives. Clausal coordination, joining full clauses with and, is a distinct mechanism that splits by model family instead of running in one direction: GPT under-uses it relative to humans while tuned Llama over-uses it, so which way the tell points depends on which model produced the text.

Bad:

> Construction and Renovation...Electrical and Plumbing...Hobby and Craft

Good:

> (constructed) Construction, electrical, and plumbing supplies

### False ranges

Tags: contextual, current. Sources: humanizer.

"From X to Y" implies a continuum running between two poles. When the listed items aren't actually points on a scale, marketing to manufacturing to legal, say, the range reads as decoration standing in for a plain list.

Bad:

> (constructed) from marketing to manufacturing to legal

Good:

> (constructed) in marketing, manufacturing, and legal

### Participial tack-on for fake depth

Tags: contextual, current. Sources: wiki-signs, humanizer, llm-grammar.

A present-participle clause gets stapled onto a sentence, leaning on his agility, further enhancing its significance, to manufacture analytical weight the sentence hasn't earned. Reinhart et al.'s Biber-feature study found this construction far more common in instruction-tuned GPT-4o and Llama 3 than in human writing, while their own base models stayed close to the human baseline, meaning tuning adds the habit rather than the underlying model producing it natively.

Bad:

> Bryan, leaning on his agility, dances around the ring

Good:

> (constructed) Bryan uses his agility to dance around the ring

### Nominalization and abstract-subject stacking

Tags: contextual, current. Sources: llm-grammar.

Verbs and adjectives get converted into abstract nouns, reducing deforestation instead of cutting down forests, well above the human rate in instruction-tuned models, with base models again close to baseline. The same study found "that"-clauses used as grammatical subjects, that the policy failed is well documented, showing up at a similarly elevated rate, a different route to the same impersonal, abstracted register.

Bad:

> reducing deforestation, habitat destruction, and pollution

Good:

> (constructed) cutting down forests, destroying habitats, and polluting less

### Passive voice as a weak tell

Tags: contextual, fading. Sources: orwell, llm-grammar.

Orwell's rule was never use the passive where the active will do, and "mistakes were made" is the textbook case of a passive hiding who did what. Treat this one carefully, though: the best available current-model evidence contradicts the folk claim that AI overuses passive voice. GPT-4o produces agentless passives at roughly half the human rate, so passive-voice density isn't a dependable AI signal for current instruction-tuned models, even though avoiding an unmotivated passive remains good advice on its own terms.

Bad:

> (constructed) Mistakes were made.

Good:

> (constructed) We made mistakes.

### Filler and padding phrases

Tags: always, current. Sources: humanizer, orwell, llm-style-notebook.

In order to, due to the fact that, at this point in time, has the ability to: phrases that add nothing a single plain word wouldn't say better. Orwell named the same habit in 1946, render inoperative for stop, it is a fact that for nothing at all, and his rule was simple: if a word can be cut, cut it. Reinhart's bibliography finds the contemporary version running through formulaic connective bundles too, in the context of, with respect to, in terms of, clustering together at a higher type-to-token ratio than natural human phrasing. The same padding impulse shows up at the word level as unnecessary hyphenation, hyphenating "high-quality" in predicate position where no hyphen is needed.

Bad:

> In order to reduce costs due to the fact that demand fell

Good:

> (constructed) To reduce costs because demand fell

### Manufactured drama fragments

Tags: contextual, current. Sources: humanizer.

Short, emphatic sentence fragments stacked for artificial weight. One clipped fragment lands; a run of them across a paragraph reads as a writing tic rather than a rhythm choice.

Bad:

> It had no preference. No aesthetic. No nostalgia.

Good:

> (constructed) It had no preference, no aesthetic sense, no nostalgia.

### Aphorism formulas

Tags: contextual, current. Sources: humanizer.

Templates like "X is the Y of Z" or "X becomes a trap" stand in for an actual, checkable observation. They sound insightful because the shape is familiar, not because there's a specific claim underneath.

Bad:

> Complexity is the tax we pay for convenience.

Good:

> (constructed) Teams over-optimize and miss user context.

### Colon-heavy sentence splicing

Tags: contextual, current. Sources: own.

A colon replaces almost every conjunction and full stop, introducing an aside, a list, and a consequence with the identical rising-then-landing shape until every third sentence reads the same way. It's a quieter cousin of em-dash overuse: no punctuation-tell catalog flags a colon the way it flags a dash, so this one survives most cleanup passes unnoticed.

Bad:

> (constructed) The result was clear: adoption fell, and the cause was obvious: pricing.

Good:

> (constructed) The result was clear. Adoption fell because of pricing.

## Response shape and stance

### Essay shape for simple questions

Tags: contextual, current. Sources: own.

A yes/no or single-fact question gets an intro, several headed sections, and a closing summary regardless of what was actually asked, because the model's most heavily trained shape is the explainer, not because the question called for one. Ask whether adding a database index always speeds up reads, and the essay-shaped answer opens with an overview section, moves through a trade-offs section, and closes with a summary restating that it depends. Different from conclusion boilerplate below, which is about the closing formula specifically: this is the whole structure getting imposed on content that never needed it.

Bad:

> (constructed) ## Understanding Database Indexes
> Database indexes are a fundamental part of query optimization, allowing the engine to locate matching rows faster than a full scan.
> ## Trade-offs to Consider
> While indexes speed up reads, they add overhead to every write and consume additional storage.
> ## Conclusion
> In summary, whether an index helps depends on several factors specific to your workload.

Good:

> (constructed) No. It speeds up reads that match the index but slows every write, and past a few indexes the query planner may start ignoring the extra ones anyway.

### Summary and conclusion boilerplate

Tags: contextual, current. Sources: wiki-signs, humanizer.

A rigid "despite challenges X, the future holds Y" formula closes out a section or a whole piece regardless of subject, generic enough that wiki-signs found it recurring across unrelated articles with matching structure: "despite its industrial prosperity, Korattur faces challenges typical of urban areas" reads the same whether the subject is a town, a company, or a technology. Humanizer's version of the same tic drops the content and keeps the shape: "the future looks bright, and exciting times lie ahead."

Bad:

> As the global economy evolves...faces new challenges and opportunities...future lies in its ability to adapt

Good:

> (constructed) Adoption slowed in 2024 after new tariffs; producers shifted to regional suppliers.

### Fragmented throwaway headers

Tags: always, current. Sources: humanizer.

A heading gets immediately followed by one sentence that just restates the heading before any real content starts.

Bad (constructed):

```markdown
## Pricing

Let's talk about pricing.

Three tiers: Free, Pro, and Enterprise...
```

Good (constructed):

```markdown
## Pricing

Three tiers: Free, Pro, and Enterprise...
```

### Throat-clearing openers

Tags: always, current. Sources: humanizer.

Three variants of the same delay tactic: fake-authority framing before the actual claim ("the real question is," "at its core," "fundamentally"), meta-announcements of what's about to be said ("let's dive in," "here's what you need to know"), and fake-candid hooks ("honestly?", "look,", "here's the thing"). All three spend a sentence announcing that an answer is coming instead of just giving it.

Bad:

> (constructed) Let's dive in and explore what you need to know about the new pricing tiers.

Good:

> (constructed) The new pricing has three tiers: Free, Pro, and Enterprise.

### Chatbot meta-commentary artifacts

Tags: always, current. Sources: humanizer.

Leftover chat-interaction phrasing tacked onto the end of an answer, "I hope this helps! Let me know if you have questions," that belongs to the conversational turn, not to the content itself.

Bad:

> (constructed) The migration script drops the old index and rebuilds it in the background. I hope this helps! Let me know if you have any other questions.

Good:

> (constructed) The migration script drops the old index and rebuilds it in the background.

### Knowledge-cutoff disclaimers and gap-filling

Tags: always, current. Sources: humanizer.

Two different things get bundled under this label. Honestly disclosing a real knowledge cutoff, "I don't have information on anything after my training data ends," is fine on its own and shouldn't be flagged. The always tag is about what happens next: quietly inventing plausible-sounding filler once the actual sources run out, "likely grew up in a middle-class family," dressed up as biography rather than flagged as a guess.

Bad:

> As of my last training update... likely grew up in a middle-class family

Good:

> (constructed) Her early life is not documented in available sources.

### Sycophantic tone

Tags: always, current. Sources: humanizer.

Praise or validation aimed at the reader before the actual content, "great question! you're absolutely right to be concerned," none of which does any work the answer itself doesn't already do.

Bad:

> (constructed) Great question! You're absolutely right to be concerned about this. Let's take a look: the deployment failed because the health check timeout was too short.

Good:

> (constructed) The deployment failed because the health check timeout was too short.

### Excessive hedging and hedged non-answers

Tags: contextual, current. Sources: humanizer, llm-grammar.

Stacking hedges until a claim commits to nothing, "could potentially possibly be argued that might have some effect," most visible when a direct question gets an answer engineered to avoid taking a position. The same evasiveness shows up at the word level too: Reinhart et al. found GPT-family models overuse downtoning adverbs, barely, nearly, slightly, well above the human rate, often stacked in the same sentence.

Bad:

> could potentially possibly be argued that might have some effect

Good:

> (constructed) may affect outcomes

### Missing hedges and personal engagement

Tags: contextual, current. Sources: llm-style-notebook.

This is the opposite face of hedging above, not a contradiction of it. The entry above is what happens when a model gets pushed toward a verdict and stalls; this is the default register of ordinary expository prose, which comes out flatter than comparable human writing because it under-uses hedges, boosters, attitude markers, and personal touches like rhetorical questions or "I think," not just when dodging a conclusion. The same research found overall adverb use running below the human rate too, more pronounced in instruction-tuned models, the same gap showing up one part of speech down.

Bad:

> (constructed) This approach improves performance and reduces costs across deployment environments.

Good:

> (constructed) I think this approach probably improves performance, though I haven't tested it under heavy load.

### Uniform rhythm and suspiciously clean prose

Tags: contextual, current. Sources: llm-style-notebook, llm-grammar, humanizer.

LLM text runs measurably more information-dense, explicit, and syntactically complex than comparable human writing in the same register, and without a writing sample to match, defaults to one generic voice regardless of context, the same register for a Slack message as for a report. Two details make it catchable: this prose also contains fewer grammatical errors than typical human writing in casual registers, itself a signal rather than a virtue where a human would leave in a typo or a comma splice, and fine-tuning a model on one person's actual writing sharply closes the gap, evidence the tell is a default setting, not something inherent to the model. Instruction tuning is the amplifier here: tuned models diverge from human patterns more than their own base models do.

Bad:

> (constructed) I have reviewed the pull request and identified several areas for improvement. The implementation demonstrates solid understanding of the requirements; however, there are opportunities to enhance code clarity and maintainability.

Good:

> (constructed) Looked at the PR, pretty solid overall. A few spots where the naming's confusing though, might be worth a pass.

### Diff-anchored writing

Tags: contextual, current. Sources: humanizer.

Describing something in terms of what changed from a prior state instead of what it is now, reading like a changelog entry embedded in ordinary prose. Fine in an actual changelog; a tell everywhere else it substitutes for a plain description.

Bad:

> (constructed) The new pricing page replaces the old three-tier layout and removes the annual-discount banner that used to sit above the fold.

Good:

> (constructed) The pricing page shows three tiers with monthly and annual toggles side by side.

### Fiction that over-explains its theme

Tags: contextual, current. Sources: llm-style-notebook.

LLM fiction tends to state its own moral outright rather than let it emerge from action, and favors tidy, single-track plots with less temporal complexity than human fiction manages. The tendency has a model-specific flavor too: Claude in particular leans toward flat, evenly-paced escalation rather than real peaks and troughs of tension, where GPT reaches for a dream sequence to resolve conflict and Gemini shifts focus onto a secondary character, though there's no evidence yet on whether these per-model fingerprints hold across newer versions.

Bad:

> (constructed) The old lighthouse keeper never spoke of the wreck, and in his silence, we understand that some griefs are too large for words.

Good:

> (constructed) The old lighthouse keeper never spoke of the wreck. When asked, he changed the subject.

## Formatting and markup

### Title case headings

Tags: contextual, current. Sources: wiki-signs, humanizer.

Every main word in a heading capitalized instead of sentence case, a strong enough tendency that both sources name it independently as a default rather than an occasional stylistic choice.

Bad:

> Strategic Negotiations And Global Partnerships

Good:

> (constructed) Strategic negotiations and global partnerships

### Excessive boldface

Tags: contextual, current. Sources: wiki-signs, humanizer.

Chosen terms and acronyms get mechanically bolded throughout a piece as if generating scannable key-takeaways, an inheritance wiki-signs traces back to READMEs, how-tos, and listicles.

Bad:

> **leveraged buyout (LBO)**...extensive use of **debt financing**

Good:

> (constructed) leveraged buyout (LBO)...debt financing

### Bold-header bullet lists

Tags: contextual, current. Sources: wiki-signs, humanizer.

Bullet items formatted as a bold header, a colon, then an explanation, instead of prose or a plain bullet, another README-shaped habit both sources flag as a structural default.

Bad:

> - **Standard Rotary Saws**: Typically used for drywall

Good:

> (constructed) Standard rotary saws are typically used for drywall.

### Markdown syntax leaking into plain text

Tags: contextual, current. Sources: wiki-signs.

Asterisks used for emphasis in a context that expects prose or a different markup system entirely, a chat-interface habit that survives copy-paste into wikitext or plain documents.

Bad:

> *Wired*, *Refinery29*, and other prominent media

Good:

> (constructed) Wired, Refinery29, and other prominent media

### Malformed heading structure

Tags: contextual, current. Sources: wiki-signs.

Jumping from one heading level straight to a non-adjacent one instead of proper nesting, and a close cousin, a horizontal rule dropped immediately before a heading, redundant with the heading itself.

Bad (constructed):

```markdown
## Overview
...
#### Details
```

Good (constructed):

```markdown
## Overview
...
### Details
```

### Em dash cadence

Tags: contextual, current. Sources: wiki-signs, humanizer.

Disproportionately frequent em dashes for parenthetical asides. Humanizer calls it the single most reliable tell and enforces zero em or en dashes in its own rewrites, but both sources agree a lone dash proves nothing, it's the rate across a whole piece that gives it away, not any one instance.

Bad:

> (constructed) The plan—ambitious and untested—failed within weeks.

Good:

> (constructed) The plan, ambitious and untested, failed within weeks.

### Emoji decoration

Tags: contextual, current. Sources: wiki-signs, humanizer.

An emoji dropped into a heading or list item as decorative structure rather than as content that carries meaning.

Bad:

> (constructed) 🚀 Key Benefits

Good:

> (constructed) Key Benefits

### Curly quotes and smart punctuation

Tags: contextual, current. Sources: wiki-signs, humanizer.

Curly, "smart" quotes and apostrophes where the target format expects straight ones. Both sources agree one instance alone isn't reliable; it's a signal alongside other tells, or at a suspiciously consistent rate across a whole document.

Bad:

> "Hello"

Good:

> "Hello"

## Factual integrity and sourcing

### Vague attributions

Tags: always, current. Sources: wiki-signs, humanizer.

Attributing a claim to an unnamed collective, experts, observers, industry reports, when only one source, or none, actually supports it. Weasel wording that implies a consensus nobody has checked for.

Bad:

> Experts argue that...

Good:

> (constructed) Dr. Lin argued in a 2024 interview that...

### Notability and biography padding

Tags: contextual, current. Sources: wiki-signs, humanizer.

A biography crammed with media-coverage claims that echo notability-guideline language rather than natural prose, listing outlets without ever contextualizing the actual quote or claim, a pattern that has grown more common as 2025-era AI drafting tools spread. The same impulse produces a specific stock line, "maintains a strong digital presence, particularly on Instagram," distinctive enough to AI-written text that wiki-signs still flags it in its 2026 catalog.

Bad:

> She spoke about AI on CNN, was featured in Vogue, Wired, and the Toronto Star

Good:

> (constructed) She discussed AI regulation on CNN in March 2024.

### Markup artifact leakage

Tags: always, current. Sources: wiki-signs, own.

Chatbot-internal citation markup leaking straight into output when text gets copy-pasted without cleanup. Each tool has its own signature: ChatGPT's contentReference and oaicite, Gemini's [cite:1], Grok's grok_card, DeepSeek's lenticular brackets, Perplexity's ppl-ai-file-upload, still showing up across tools as of 2026.

Bad:

```text
the treaty was signed in 1815 contentReference[oaicite:3]
```

Good (constructed):

```text
the treaty was signed in 1815.
```

### Broken citation tells

Tags: always, current. Sources: wiki-signs.

Citations present in form but broken underneath: dead links, invalid DOIs or ISBNs, a DOI that resolves to an unrelated paper, missing page numbers, a named reference nothing actually points to.

Bad:

> (constructed) The technique reduces latency by 40 percent (Chen et al., 2021, doi:10.1000/xyz111), though that DOI resolves to an unrelated paper on marine sediment cores.

Good:

> (constructed) The technique reduces latency by 40 percent (Chen et al., 2021, doi:10.1000/xyz111), matching the cited study's own reported benchmark.

### Pronounced style-shift within a document

Tags: contextual, current. Sources: wiki-signs.

A single document showing an abrupt, detectable shift in quality or tone between sections, the fingerprint of uneven AI-assisted drafting rather than one consistent hand throughout.

Bad:

> (constructed) The quarterly results demonstrate a robust and multifaceted growth trajectory across all key business segments. its been a rly solid quarter tbh, numbers went up in basically every category we track.

Good:

> (constructed) The quarterly results show growth across all business segments. Revenue rose in every category we track this quarter.
