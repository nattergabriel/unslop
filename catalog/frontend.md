# Frontend design slop catalog

Phase 3 raw material for the frontend-design surface: tells for AI slop in layout, color, typography, spacing, motion, and component choices, mined from the vetted phase 2 sources plus direct observation of AI-generated frontends. This feeds phase 4's rule distillation; the bad/good pairs double as phase 6 eval fixtures.

Sources mined:
- impeccable-visual: Slop by Impeccable (Bakaus), visual rules
- shn-design-slop: Scoring Show HN for AI design patterns (Krebs, 2026)
- anthropic-frontend: Improving frontend design through Skills (Anthropic, 2025)
- frontend-skill: Anthropic frontend-design SKILL.md
- purple-gradient: Why Your AI Keeps Building the Same Purple Gradient Website (Gajjar)
- age-of-average: The Age of Average (Murrell, 2023), a counter source that predates AI tools; kept where it documents a convergence AI now reproduces or amplifies, flagged as weaker AI-specific evidence
- own: direct observation, not traceable to the sources above

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default, in aggregate, or at high frequency); currency is current (typical of 2025-2026 model output) or fading (mostly 2023-2024 era, rarer now).

## Color and surface

### Purple/violet as the reflexive accent

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, anthropic-frontend, purple-gradient, age-of-average, own.

The single most corroborated tell in the catalog: a purple-to-violet gradient, often paired with cyan on dark backgrounds, used as the default "modern tech" accent with no brand rationale behind it. The causal chain is documented: Tailwind's `bg-indigo-500` was an arbitrary component-demo choice that saturated tutorials scraped into training data over the following years, and Anthropic's own account names purple-on-white one of three defaults Claude converges to absent other direction. Krebs's 2026 Show HN audit gives it a name, "VibeCode Purple." Gajjar notes the same pages tend to spread risk evenly across several similarly-saturated hues rather than commit to one dominant color, and Murrell had already clocked purple, alongside turquoise, as the default "safe" brand accent in pre-AI logo redesigns.

Bad:

> (constructed) A dashboard's primary buttons, chart highlights, and hero background all use the same `#8b5cf6` purple-to-cyan gradient with no relationship to the product or brand.

Good:

> (constructed) A developer-tools product commits to a single dark amber (#D97706) as its one accent color against near-black, used for every CTA, active state, and chart highlight, with no gradient anywhere on the page.

### Warm cream and terracotta as the "tasteful" default

Tags: contextual, current. Sources: impeccable-visual, frontend-skill, own.

When a model avoids purple it often lands on a second reflexive palette instead: a warm cream or beige background, Anthropic's own skill names the specific shade, near `#F4F1EA`, paired with a high-contrast serif display face and a terracotta accent. It reads as "editorial" and safe rather than as a decision grounded in the actual subject.

Bad:

> a warm cream background (near #F4F1EA) with a high-contrast serif display and a terracotta accent

Good:

> (constructed) A cookware brand's site uses the cast-iron grey and the deep enamel red already visible in its own product photography, not a generic cream-plus-terracotta template.

### Dark navy with a single neon accent

Tags: contextual, current. Sources: shn-design-slop, frontend-skill, own.

The third reflexive palette: a permanent dark theme with no light option, on near-black or navy, paired with one saturated accent (acid-green or vermilion in Anthropic's framing), and set with medium-grey body text and all-caps section labels rather than a genuinely high-contrast scheme. It shows up about as often as the light-mode purple-and-white default, just inverted.

Bad:

> Perma dark mode with medium-grey body text and all-caps section labels.

Good:

> (constructed) A synth-hardware product site stays dark because the hardware itself is dark, uses near-white (#F2F2F0) body text for real contrast, and reserves its one signature red for the power-LED motif already present in the product photos.

### Glow decoration on dark backgrounds

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop.

Oversized, saturated colored blur shapes and colored `box-shadow` glows are dropped behind hero elements on dark backgrounds purely as ambient decoration, with no connection to what actually needs visual weight on the page.

Bad:

(constructed)

```css
.hero-orb {
  position: absolute;
  width: 400px; height: 400px;
  background: #8b5cf6;
  filter: blur(80px);
  box-shadow: 0 0 60px 20px rgba(139, 92, 246, 0.4);
}
```

Good:

(constructed)

```css
.hero-orb { display: none; } /* dropped; nothing behind the hero needed the glow */
.status-dot--live {
  box-shadow: 0 0 12px 2px rgba(34, 197, 94, 0.5); /* the one glow left, and it means something */
}
```

### Gradients smeared across every surface, or none at all

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, anthropic-frontend.

The failure runs in both directions. One mode: gradients everywhere at once, `background-clip: text` fills on headings, repeating diagonal stripes as generic section filler, a purple gradient laid over an otherwise plain white page, buttons and borders all gradient-filled with no single deliberate use. The other mode, which Anthropic names as an equally common default: a flat, single solid-color background with no texture, depth, or atmosphere anywhere on the page. Both are the same underlying problem, an unexamined default rather than a decision about where depth actually belongs.

Bad:

(constructed)

```css
h1 {
  background: linear-gradient(90deg, #8b5cf6, #06b6d4);
  -webkit-background-clip: text;
  color: transparent;
}
body { background: repeating-linear-gradient(45deg, #f5f3ff 0 40px, #ede9fe 40px 80px); }
```

Good:

(constructed)

```css
h1 { color: #1a1a1a; }
body { background: #faf9f7; }
.hero { background: radial-gradient(circle at top left, #fff7ed, #faf9f7 60%); } /* the one deliberate use of a gradient on the page */
```

### Glassmorphism without a layering reason

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, own.

Frosted-glass, translucent, blurred panels are applied to cards and navbars as a decorative default regardless of whether anything is actually layered behind them to justify the blur. It is common enough as an unmodified default in component libraries that Krebs's detector scores it as a distinct CSS-framework tell from general glassmorphism use, and it shows up constantly as a sticky, blurred, translucent navbar dropped onto pages where nothing behind it ever scrolls under it.

Bad:

(constructed)

```css
.card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}
```

Good:

(constructed)

```css
.modal-overlay {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px); /* reserved for the one element that actually overlays content */
}
.card { background: #ffffff; border: 1px solid #e5e5e5; }
```

## Typography

### Overused "safe" fonts, unpaired

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, anthropic-frontend, purple-gradient, own.

Typeface choice converges on a small rotating set: Inter above all, plus Roboto, Open Sans, Lato, Arial, Geist, Space Grotesk, and Instrument Serif as the "distinctive" alternates. Krebs finds Inter used for everything on a page, especially the centered hero headline; Anthropic names the same set as the safe choice that dominates web training data. Often it is not just the wrong font but the only font, one family declared for both display and body text with no pairing at all.

Bad:

> (constructed) A SaaS landing page sets its centered H1, nav, and body copy all in Inter, with no secondary typeface anywhere on the page.

Good:

> (constructed) A rare-books dealer's site pairs Freight Display for headings with Freight Text for body copy, both licensed specifically for the project and unrelated to any common generator default.

### Italic serif dropped into a sans hero

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop.

Either the entire hero headline is set in an oversized italic serif against an otherwise sans-serif page, or, in the lighter version of the same tell, a single accent word within an Inter headline is set in serif italic while the rest stays roman sans.

Bad:

> (constructed) The hero headline "Build the future, faster" is set in Inter throughout, except the word "future," which switches to an italic serif mid-sentence.

Good:

> (constructed) The full headline "Build faster, ship sooner" is set in one weight of the same sans used throughout, with emphasis carried by size and color rather than a mid-sentence typeface switch.

### Oversized full-sentence headline

Tags: contextual, current. Sources: impeccable-visual.

A complete grammatical sentence, "We help teams ship better software faster than ever before," is set at 60-80px and left to dominate the entire hero viewport, where a shorter headline would do the same work in less space.

Bad:

> (constructed) "We help teams ship better software faster than ever before" set at 72px, spanning the full hero viewport.

Good:

> (constructed) "Ship on Friday" set at 56px, with the explanatory sentence moved to an 18px subhead beneath it.

## Type and layout mechanics

### Text contrast that fails WCAG

Tags: always, current. Sources: impeccable-visual, shn-design-slop.

Body text sits below the 4.5:1 contrast ratio WCAG AA requires (3:1 for large text), most often as grey text on a saturated colored background, or as a dark-theme body color tuned to just clear the legal minimum rather than for actual readability.

Bad:

(constructed)

```css
body { color: #999999; background: #ffffff; } /* ~2.85:1 */
.hero { color: #888888; background: #6d28d9; }
```

Good:

(constructed)

```css
body { color: #1f1f1f; background: #ffffff; } /* 15.6:1 */
.hero { color: #f5f3ff; background: #6d28d9; } /* 7.9:1 */
```

### Skipped heading levels

Tags: always, current. Sources: impeccable-visual.

An `h1` is followed directly by an `h3` with no `h2` between them, or the equivalent skip elsewhere in the outline. Screen readers navigate by heading hierarchy, so the skip breaks the document outline even though it renders fine visually.

Bad:

(constructed)

```html
<h1>Pricing</h1>
<h3>Enterprise plan</h3>
```

Good:

(constructed)

```html
<h1>Pricing</h1>
<h2>Enterprise plan</h2>
```

### Broken or placeholder image sources

Tags: always, current. Sources: impeccable-visual.

`img` tags ship with empty, missing, or placeholder `src` values standing in for content that was never actually produced.

Bad:

(constructed)

```html
<img src="" alt="Team photo">
<img src="/placeholder.jpg" alt="Product screenshot">
```

Good:

(constructed)

```html
<img src="/assets/team-2026.jpg" alt="Team photo">
```

### Content that overflows or gets wrongly clipped

Tags: always, current. Sources: impeccable-visual.

Two mirror-image overflow bugs: content wider than its parent spills past the container into unintended horizontal scroll, or a parent with `overflow: hidden` clips an absolutely positioned child, like a tooltip or dropdown, that was meant to escape it.

Bad:

(constructed)

```css
.card { position: relative; overflow: hidden; }
.tooltip { position: absolute; top: -12px; } /* clipped by the card */
```

Good:

(constructed)

```css
.card { position: relative; }
.tooltip { position: absolute; top: -12px; z-index: 10; } /* moved out of any clipping ancestor */
```

### Justified text with no hyphenation

Tags: always, current. Sources: impeccable-visual.

Body copy is set `text-align: justify` in a narrow column with no hyphenation, producing uneven word-spacing rivers down the paragraph.

Bad:

(constructed)

```css
p { text-align: justify; max-width: 32ch; }
```

Good:

(constructed)

```css
p { text-align: left; max-width: 65ch; }
```

### Body text set too small and too tight

Tags: always, current. Sources: impeccable-visual.

Font size drops below 12px and line-height below 1.3x, cramming multi-line body copy together well past comfortable reading.

Bad:

(constructed)

```css
p { font-size: 11px; line-height: 1.1; }
```

Good:

(constructed)

```css
p { font-size: 16px; line-height: 1.6; }
```

### No breathing room around text

Tags: always, current. Sources: impeccable-visual.

Text sits flush against the edges of whatever contains it: a badge with 2px of padding inside a 1px border, body copy with zero horizontal padding against the raw viewport edge, or a paragraph left to run the full width of a wide viewport with no `max-width` at all.

Bad:

(constructed)

```css
.badge { padding: 2px; border: 1px solid #ccc; }
p { padding: 0; max-width: none; } /* runs full viewport width */
```

Good:

(constructed)

```css
.badge { padding: 6px 12px; border: 1px solid #ccc; }
p { max-width: 70ch; padding: 0 16px; margin-inline: auto; }
```

### Letter-spacing pushed past legible in either direction

Tags: always, current. Sources: impeccable-visual.

Either display type is tightened destructively past `-0.05em`, or body paragraphs are given wide tracking above `0.05em` that belongs on short uppercase labels, not running text.

Bad:

(constructed)

```css
h1 { letter-spacing: -0.05em; }
p { letter-spacing: 0.08em; }
```

Good:

(constructed)

```css
h1 { letter-spacing: -0.01em; }
p { letter-spacing: normal; }
.label { letter-spacing: 0.05em; text-transform: uppercase; font-size: 12px; }
```

### Flat scale: no contrast between type or spacing steps

Tags: always, current. Sources: impeccable-visual.

Two versions of the same failure: heading and body sizes sit within a narrow band with no real contrast between levels (h1 24px, h2 20px, body 16px), or an identical spacing value is applied everywhere regardless of whether elements are closely related or not, so nothing reads as grouped.

Bad:

(constructed)

```css
h1 { font-size: 24px; } h2 { font-size: 20px; } p { font-size: 16px; }
.card > * { margin-bottom: 24px; } /* same gap for every relationship */
```

Good:

(constructed)

```css
h1 { font-size: 40px; } h2 { font-size: 22px; } p { font-size: 16px; } /* >=1.25 ratio between steps */
.card-title + .card-subtitle { margin-top: 4px; }
.card + .card { margin-top: 32px; }
```

### Long passages set in all caps

Tags: always, current. Sources: impeccable-visual.

Multi-sentence body paragraphs are rendered with `text-transform: uppercase`. Readers recognize words by shape, ascenders and descenders included, and all-caps removes that shape entirely, so it works for a three-word label and actively hurts a paragraph.

Bad:

(constructed)

```html
<p style="text-transform: uppercase;">OUR PLATFORM HELPS DISTRIBUTED TEAMS SHIP CODE FASTER BY AUTOMATING THE PARTS OF REVIEW THAT DON'T NEED A HUMAN.</p>
```

Good:

(constructed)

```html
<p>Our platform helps distributed teams ship code faster by automating the parts of review that don't need a human.</p>
```

## Components and page structure

### Thick, one-sided colored card border

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, own.

A card carries a thick colored border restricted to one edge, top or left, as a decorative accent unrelated to what the card contains, often on a card whose corners are already rounded, so the straight accent line fights the curve. It is one of the more recognizable AI-UI tells in this catalog, showing up across pricing tables, feature cards, and testimonial blocks alike.

Bad:

(constructed)

```css
.card {
  border-radius: 16px;
  border-left: 4px solid #8b5cf6;
}
```

Good:

(constructed)

```css
.card {
  border-radius: 8px;
  border: 1px solid #e5e5e5;
}
```

### Border, radius, and shadow copied everywhere without intent

Tags: contextual, current. Sources: impeccable-visual, purple-gradient, shn-design-slop.

The same small set of tokens gets pasted onto every element regardless of size or purpose: 24px+ border-radius that turns every shape into an identical soft blob, box-shadow at almost exactly 0.1 opacity on every card, and a thin 1px border stacked with a large diffuse shadow on the same element, committing to neither a defined edge nor a soft elevation. Shipping an unmodified shadcn/ui install is the same failure at the framework level: every card, button, and input keeps the library's shared default radius and shadow with zero customization.

Bad:

(constructed)

```css
* { border-radius: 24px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); border: 1px solid #e5e5e5; }
```

Good:

(constructed)

```css
.card { border-radius: 8px; box-shadow: 0 1px 2px rgba(0,0,0,0.06); }
.tag { border-radius: 999px; } /* full pill reserved for tags and buttons */
.button { border-radius: 6px; box-shadow: none; }
```

### Cards inside cards

Tags: contextual, current. Sources: impeccable-visual.

A bordered, shadowed card contains another bordered, shadowed card for a sub-item, doubling up redundant containers instead of using spacing and typography to carry the same hierarchy.

Bad:

(constructed)

```html
<div class="card">
  <h3>Team plan</h3>
  <div class="card"><p>5 seats included</p></div>
</div>
```

Good:

(constructed)

```html
<div class="card">
  <h3>Team plan</h3>
  <p class="card-detail">5 seats included</p>
</div>
```

### Centered hero plus three identical icon-topped cards

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, purple-gradient.

The default AI homepage shape: a centered hero in a generic sans, followed by a three-column grid of feature cards, each one an identical icon tile stacked above a heading above one line of copy. Krebs's Show HN audit scores this as one of its tells, and Gajjar's account of the median AI-generated landing page names the same tri-column icon grid as its hallmark component.

Bad:

> (constructed) A centered "Everything you need to ship faster" headline in Inter, followed by three identical cards, each a rounded-square icon tile over a heading over one sentence, evenly spaced in a 3-column grid.

Good:

> (constructed) A left-aligned hero naming the specific product, followed by a two-column comparison table showing the three capabilities customers actually ask about against the competitor most of them are switching from.

### Generic three-stat hero banner

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop.

A row of large-number, small-label statistics, often exactly three ("10K+ Users / 99.9% Uptime / 24/7 Support"), shown banner-style under the hero regardless of whether the numbers tie to anything the company can actually stand behind.

Bad:

> (constructed) "10K+ Users / 99.9% Uptime / 24/7 Support" displayed as a three-column stat row beneath the hero.

Good:

> (constructed) "Processed 40,000 invoices for 60 finance teams last quarter" stated as a single sentence, linked to the underlying case study.

### Badge pill above the hero headline

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop.

A small, uppercase, letter-spaced pill, "NEW · AI POWERED," or a version tag, sits directly above an oversized hero headline on nearly every generated landing page, whether or not there is an actual announcement behind it.

Bad:

> (constructed) A pill reading "NEW · AI POWERED" centered directly above the H1, with no corresponding changelog or announcement anywhere else on the site.

Good:

> (constructed) The same launch note lives as one line in the site's changelog page, and the hero opens straight on the headline.

### Decorative numbers, kickers, and eyebrows

Tags: contextual, current. Sources: impeccable-visual, shn-design-slop, frontend-skill.

Large stylized "01, 02, 03" numerals label sections that are not actually sequential, and every section heading gets its own small uppercase tracked kicker ("OUR FEATURES," "OUR PROCESS," "OUR VALUES") repeated section after section. Anthropic's skill states the underlying rule directly: these structural devices should encode something true about the content, not decorate it.

Bad:

> (constructed) A "02" numeral above a "Why choose us" section with no ordering relationship to the "03" section that follows it, and an "OUR FEATURES" kicker above one heading, "OUR PROCESS" above the next.

Good:

> (constructed) Numerals appear only above the three actually sequential onboarding steps; every other section uses a plain heading with no kicker at all.

### Generic template aesthetic, ungrounded from the subject

Tags: always, current. Sources: frontend-skill, age-of-average, own.

A recognizable off-the-shelf look, warm cream with hairline rules and zero border-radius in dense newspaper-like columns is Anthropic's own named example, gets applied to a page regardless of what the page is actually for. Murrell documented the same convergence in interiors and brand design years before AI tools existed: identical "clean, minimal, industrial" spaces in Brooklyn, Osaka, and Santiago, indistinguishable from each other. The fix Anthropic's skill names is the only one that works: ground color, motif, and structure in the subject's own materials, instruments, and vernacular, not a template that could belong to anyone.

Bad:

> a broadsheet-style layout with hairline rules, zero border-radius, and dense newspaper-like columns

Good:

> (constructed) A woodworking-tool catalog builds its palette and grid from the actual grain and edge-tool photography it already has, a layout that would look wrong applied to anything else.

### Amateurish hand-drawn SVG illustration

Tags: contextual, current. Sources: impeccable-visual.

A hand-coded inline SVG blob illustration is used as hero or section decoration and reads as crude or amateur rather than as a real asset.

Bad:

(constructed)

```html
<svg viewBox="0 0 200 200"><path d="M20,100 Q60,20 100,100 T180,100" stroke="#8b5cf6" fill="none"/></svg>
```

Good:

(constructed)

```html
<img src="/assets/hero-illustration.svg" alt="Diagram of the deployment pipeline">
```

### Emoji standing in for icons

Tags: contextual, current. Sources: shn-design-slop, own.

Emoji characters stand in as navigation icons, feature markers, or bullet points in place of a real icon set, in the nav and sidebar per Krebs's audit, but just as often in feature lists and empty states too.

Bad:

(constructed)

```html
<nav>
  <a href="/dashboard">📊 Dashboard</a>
  <a href="/settings">⚙️ Settings</a>
</nav>
```

Good:

(constructed)

```html
<nav>
  <a href="/dashboard"><IconChart /> Dashboard</a>
  <a href="/settings"><IconSettings /> Settings</a>
</nav>
```

### Green checkmark bullets on every pricing line

Tags: contextual, current. Sources: own.

Every line item in a pricing card gets the same generic green checkmark bullet, whether it is a real differentiator or a baseline feature every plan includes, so the checkmark stops signaling anything.

Bad:

(constructed)

```html
<ul class="pricing-features">
  <li>✓ Email support</li>
  <li>✓ 99.9% uptime SLA</li>
  <li>✓ Unlimited projects</li>
  <li>✓ Dedicated account manager</li>
</ul>
```

Good:

(constructed)

```html
<ul class="pricing-features">
  <li>Unlimited projects</li>
  <li class="highlight"><IconCheck /> Dedicated account manager</li>
</ul>
```

### Stock hero-image compositions

Tags: contextual, current. Sources: age-of-average (documents a pre-AI convergence; the source predates generative image tools, so the AI-specific link is weaker evidence than the rest of this catalog).

The same handful of compositions recur across unrelated brands' hero and marketing imagery: the medicine-cabinet "shelfie," a mirror reflecting the sky, water-droplet refraction, a fake scenic backdrop behind an unrelated product. Murrell documented this in advertising photography before AI image tools existed; it shows up just as readily in AI-generated and AI-selected hero imagery now, inheriting rather than originating the convergence.

Bad:

> (constructed) A skincare brand's hero image shows a bathroom mirror reflecting a clear blue sky, the same composition used on the perfume brand's site the designer pulled the reference from.

Good:

> (constructed) A skincare brand's hero photographs its own lab bench and the actual texture of its product, not a mirror held up against a stock sky.

## Motion

### Motion defaults to nothing, or to one fade-up-on-scroll for everything

Tags: contextual, current. Sources: anthropic-frontend, purple-gradient.

Two versions of the same underachievement. Anthropic and Gajjar both name it as a median default: no animation beyond a subtle opacity fade or basic hover state, nothing orchestrated. Left to add "polish" instead, the same simple `opacity` plus `translateY` scroll-reveal gets applied to literally every section and card on the page, one effect repeated until it stops reading as intentional.

Bad:

(constructed)

```css
.reveal { opacity: 0; transform: translateY(20px); }
.reveal.in-view { opacity: 1; transform: translateY(0); transition: all 0.4s; }
/* applied identically to every section, card, and list item on the page */
```

Good:

(constructed)

```css
/* one orchestrated page-load sequence with staggered delays, nothing on scroll */
.hero-title { animation: rise 0.5s ease-out both; }
.hero-sub   { animation: rise 0.5s ease-out 0.1s both; }
.hero-cta   { animation: rise 0.5s ease-out 0.2s both; }
```

### Bounce and elastic easing on interface motion

Tags: contextual, fading. Sources: impeccable-visual.

Button and element transitions use a springy, elastic bounce curve borrowed from physical-motion design, a texture that read as current a few years ago and now feels dated for ordinary interface feedback.

Bad:

(constructed)

```css
.button { transition: transform 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6); }
```

Good:

(constructed)

```css
.button { transition: transform 0.15s ease-out; }
```

### Images that scale or rotate on hover by default

Tags: contextual, current. Sources: impeccable-visual.

Product and hero images get a default `scale` or `rotate` transform on hover as decoration, whether or not the image is actually interactive.

Bad:

(constructed)

```css
img.product-shot:hover { transform: scale(1.05) rotate(1deg); }
```

Good:

(constructed)

```css
.product-card:hover { border-color: #999; } /* the card carries the hover affordance; the image stays still */
```

### Animating layout-triggering properties

Tags: always, current. Sources: impeccable-visual.

Transitions target `width`, `height`, `padding`, or `margin` directly, forcing the browser to recompute layout on every frame instead of animating compositor-friendly properties.

Bad:

(constructed)

```css
.accordion-panel { transition: height 0.3s; }
```

Good:

(constructed)

```css
.accordion-panel { display: grid; grid-template-rows: 0fr; transition: grid-template-rows 0.3s; }
.accordion-panel.open { grid-template-rows: 1fr; }
```
