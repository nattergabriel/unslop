# UI copy slop catalog

Phase 3 raw material for the UI copy overlay: tells specific to interface and product marketing copy, buttons, labels, headings, empty states, error messages, landing and onboarding copy, mined from five vetted phase 2 sources plus field observations, each with one bad and one good example. This overlay assumes the writing base catalog underneath it and only adds the delta the short-form product copy medium introduces. Feeds the phase 4 rule distillation, and the bad/good pairs double as phase 6 eval fixtures.

Sources mined:
- impeccable-copy: Slop by Impeccable (Bakaus), Copy section
- ai-frontend-copy: How to fix the AI-generated look in your frontend (West, 2026)
- saas-copy-tells: 17 AI writing tells + blacklist (Olivia Cal, 2026)
- nng-ux: UX Writing Study Guide (Kaley, NN/g)
- mailchimp-style: Mailchimp Content Style Guide

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default or in aggregate); currency is current (typical of 2025-2026 models) or fading (mostly 2023-2024 era, rarer now).

Several mined patterns duplicate the base layer outright and don't get separate entries here: impeccable-copy's em-dash cadence (base's Em dash cadence), saas-copy-tells' predictable sentence rhythm (base's Uniform rhythm and suspiciously clean prose), transition and opener cliches and vague illustrative scenario openers (base's Throat-clearing openers, the "picture this" hypothetical setup is the same generic-preamble mechanism that entry already covers, and this catalog didn't find a UI-specific delta beyond it), listicle bold-header formatting (base's Bold-header bullet lists), high-frequency AI vocabulary and its word-blacklist families (base's Worn metaphor vocabulary; the marketing-specific slice of that blacklist feeds the vocabulary entries below instead of a standalone entry), and mailchimp's passive voice and negative framing (base's Passive voice as a weak tell, with the negative-framing half folded into the error-copy entry below). saas-copy-tells' humanizer over-correction artifacts is a general prose tell tied to running text through a humanizer tool, not something specific to short-form copy, so it belongs in the writing base rather than here. nng-ux's buried-or-distant error placement (styled subtly, positioned far from the field it describes) is a layout and visual-styling issue, not a copy issue, so it belongs to frontend design. One evidence note: saas-copy-tells' headline claims 17 tells but the fetch only confirmed 8 distinct numbered items in the rendered article; the entries below citing it draw only on what was actually found.

## Marketing vocabulary and claims

### Hype-verb vocabulary

Tags: contextual, current. Sources: impeccable-copy, ai-frontend-copy, saas-copy-tells, mailchimp-style.

A small set of inflated marketing verbs and adjectives, empower, unlock, transform, streamline, supercharge, leverage, seamless, world-class, enterprise-grade, next-generation, cutting-edge, robust, revolutionary, game-changer, stand in for saying what the product actually does. ai-frontend-copy names Empower, Unlock, and Transform as red-flag opening verbs specifically; impeccable's detector flags streamline, empower, supercharge, world-class, enterprise-grade, and next-generation as instant tells; mailchimp's word list extends the same family into culture-clichés that show up on about and careers pages (ninja, rockstar, wizard, unicorn, disruption, crushing it). Extends the base layer's Excess style verbs and Latinate register inflation entries: same reach-for-the-inflated-word mechanism, but the word list is marketing-specific and clusters hardest in headlines, hero copy, and CTAs rather than body paragraphs.

Bad:

> Supercharge your workflow. World-class, enterprise-grade, next-generation.

Good:

> (constructed) Export your report as a CSV in one click.

### Jargon and B2B-speak obscuring meaning

Tags: contextual, current. Sources: nng-ux, mailchimp-style.

Insider or B2B jargon, omnichannel, funnel, incentivize, thought leader, learnings, synergy, paradigm shift, stands in for plain description of what a feature does. This is a different failure from hype-verb inflation above: that one exaggerates, this one obscures. NN/g's plain-language guidance argues interface copy pays a higher price for jargon than an essay does, since it gets read in a rush by people who may not share the writer's vocabulary; mailchimp's corporate buzzword vocabulary pattern bans this same family of insider terms outright. Extends the base layer's Latinate register inflation entry with that medium-specific stake, skimmed and time-pressured copy has less room to survive an opaque word than a paragraph the reader can reread.

Bad:

> (constructed) Leverage our omnichannel orchestration layer to actualize synergies.

Good:

> (constructed) Send the same message across email, SMS, and chat at once.

### Hedged, referent-free benefit claims

Tags: contextual, current. Sources: ai-frontend-copy, saas-copy-tells, mailchimp-style.

Benefit copy that hedges ("aims to help improve your workflow") or leans on emotional inflation ("unlock the magic of connecting with your customers on a deeper level") instead of a plain, checkable claim. ai-frontend-copy's fix-it checklist requires at least one specific claim with a number precisely because the default is a comparative with nothing to compare against, faster, better, more powerful, than what. Extends the base layer's Excessive hedging and hedged non-answers entry: there the hedge dodges a factual verdict, here it softens a benefit claim a product page needs to state with confidence. One hedge on its own proves nothing; the tell is a whole feature section that never once lands on a concrete number.

Bad:

> (constructed) Now with faster performance.

Good:

> (constructed) 70% reduction in load time.

### No human moment in landing copy

Tags: contextual, current. Sources: ai-frontend-copy.

A whole page of landing or onboarding copy reads uniformly polished and corporate, with no sentence that sounds like a specific person wrote it. Extends the base layer's Uniform rhythm and suspiciously clean prose entry with the landing-page-specific form of the same default-voice problem: ai-frontend-copy's review checklist requires at least one sentence that sounds like a real person, precisely because the rest of the page defaults to press-release register otherwise.

Bad:

> (constructed) Our platform delivers best-in-class solutions engineered for scale.

Good:

> (constructed) Yeah, onboarding used to be a pain. We fixed it.

## Headlines, taglines, and positioning

### Abstract, buried-lede headlines and feature titles

Tags: always, current. Sources: ai-frontend-copy, nng-ux.

A feature title built from two vague abstract nouns (Seamless Integration) or a headline that buries its one concrete fact mid-sentence instead of leading with it, describing nothing a reader could act on. ai-frontend-copy names "Seamless Integration" as the canonical case; NN/g's headline guidance calls for short, keyword-leading headlines specifically because an abstract opener (an invented but typical one: "A New Way of Thinking About Productivity") hides the fact the reader is scanning for.

Bad:

> Seamless Integration

Good:

> Sync contacts from Salesforce every 15 minutes

### "Built for modern teams" placeholder positioning

Tags: always, current. Sources: ai-frontend-copy.

A generic productivity tagline used as hero copy that differentiates the product from nothing and no one. ai-frontend-copy calls "Built for modern teams" the textual equivalent of the AI purple gradient background, recognizable placeholder language that tells the reader this is a SaaS product and nothing else about it.

Bad:

> Built for modern teams. Unlock productivity.

Good:

> (constructed) Built for support teams handling 500+ tickets a day.

### Aphoristic manufactured-contrast taglines

Tags: contextual, current. Sources: impeccable-copy.

A short, punchy "X. Not Y." tagline used as a section-closer or hero line, standing in for an actual, checkable claim about what the product does. This is the standalone-tagline form of the base layer's Manufactured false contrast and Aphorism formulas entries: there the construction sits inside a sentence of running prose, here it's a whole marketing beat on its own, repeated at every section break down a landing page until the rhythm itself is the tell.

Bad:

> Not a feature. A platform.

Good:

> (constructed) It's a platform: build workflows, not just single features.

### Theater framing

Tags: contextual, current. Sources: impeccable-copy.

Dismissing a competitor's approach or an old way of doing things as "theater" instead of stating plainly what changed. The evidence here is thin, impeccable-copy names this pattern directly, but the mined index doesn't otherwise indicate how large or systematic the source's rule set is; the pattern is recognizable enough from direct model output to keep regardless, it substitutes a judgment word for a description.

Bad:

> We killed the growth theater.

Good:

> (constructed) We removed the vanity metrics dashboard and replaced it with weekly revenue reports.

## Manufactured trust

### Fabricated social proof numbers

Tags: always, current. Sources: own.

A specific-sounding customer count ("Trusted by 10,000+ teams") invoked as social proof with no source and no way to verify it. It works the same way the base layer's Vague attributions entry does for prose, a fake collective backing a claim nobody checked, except the medium-specific form is a number instead of "experts say." Landing pages reach for this exact figure right at the moment real customer counts aren't available yet, which is exactly when it's most likely invented rather than reported.

Bad:

> (constructed) Trusted by 10,000+ teams worldwide.

Good:

> (constructed) Used by 40 engineering teams, including Acme and Globex.

### Placeholder testimonials

Tags: always, current. Sources: own.

A testimonial quote attributed to a generic name and title with no company and no specific outcome, unreachable and unverifiable, the human-quote sibling of fabricated social proof numbers above. The tell isn't that a testimonial appears, it's that the quote could be pasted onto any product in any category without changing a word.

Bad:

> (constructed) "This tool changed how we work." — Sarah T., Product Manager

Good:

> (constructed) "We cut deploy time from 20 minutes to 3," says Priya Shah, Platform Lead at Acme.

## Buttons, links, and calls to action

### Generic command and link labels

Tags: contextual, current. Sources: nng-ux.

Button and link labels, OK, Submit, Yes, Learn More, Click Here, used without any surrounding context that describes the action or its consequence, forcing the user to guess what happens next. A generic label paired with a dialog body or heading that already states the consequence is a legitimate, conventional exception; the tell is a label carrying that whole burden of meaning on its own. NN/g's command-name guidance recommends 2 to 4 words that accurately describe the actual command and drop filler articles, and its 4 Ss for link labels (specific, sincere, substantial, succinct) rule out exactly this kind of destination-free link text when nothing else on the screen fills the gap.

Bad:

> (constructed) OK

Good:

> (constructed) Delete 3 photos

### "Get Started" as the only CTA verb

Tags: contextual, current. Sources: own.

The same CTA verb reused on every button across a product regardless of what it actually triggers, hero, pricing card, and footer all saying Get Started. One instance is fine; the tell is the aggregate, a whole site with a single CTA vocabulary because varying it by context never got considered.

Bad:

> (constructed) Hero button: Get Started. Pricing card: Get Started. Footer button: Get Started.

Good:

> (constructed) Hero button: Start free trial. Pricing card: Compare plans. Footer button: Talk to sales.

## Error, empty, and onboarding tone

### Vague or blaming error copy

Tags: always, current. Sources: nng-ux.

Error text that states only that something failed ("An error occurred"), blames the user for it ("Invalid input" instead of "That doesn't look like a valid email address"), or surfaces a raw technical code (404) instead of a human explanation. NN/g's guidance is explicit on all three: describe issues concisely and precisely, use a positive tone and avoid blame words like invalid or illegal, and use human-readable language instead of technical codes most users can't parse.

Bad:

> An error occurred.

Good:

> (constructed) This file is too large (12MB). Please upload a file under 10MB.

### Apology theater in error messages

Tags: contextual, current. Sources: own.

An error message that spends its whole length apologizing, sorry, oops, our bad, without describing what happened or what to do next, performing contrition instead of helping. Apologizing isn't the problem; an apology with no information or next step attached is.

Bad:

> (constructed) Oops! Something went wrong on our end. We're so sorry for the inconvenience!

Good:

> (constructed) Something went wrong while saving. Your changes are safe. Refresh the page to try again.

### Forced whimsy and puns override clarity

Tags: contextual, current. Sources: nng-ux, mailchimp-style.

Wordplay or a strained joke used in an error or empty state in place of clearly saying what happened. NN/g cites Disneyworld's search results page using puns instead of stating plainly that there were no results; mailchimp's own guidance is blunter still, don't go out of your way to make a joke, forced humor reads worse than no humor at all.

Bad:

> (constructed) Whoopsie-doodle! Looks like our server had one too many coffees!

Good:

> (constructed) Something went wrong on our end. Try again in a minute.

### Performative friendliness in onboarding

Tags: contextual, current. Sources: mailchimp-style, own.

Onboarding copy that condescends to the reader ("even for beginners like you!") or manufactures enthusiasm through exclamation marks and emoji instead of just explaining the next step. Mailchimp's style guide rejects condescension and exclusionary tone directly; the exclamation-heavy variant is the same instinct aimed at punctuation instead of word choice, both substitute performed warmth for a plain, capable-adult explanation.

Bad:

> (constructed) Don't worry, we made this super simple even for beginners like you!

Good:

> (constructed) Here's how to set up your first campaign.
