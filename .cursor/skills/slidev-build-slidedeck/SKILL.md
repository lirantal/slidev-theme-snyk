---
name: slidev-build-slidedeck
description: Builds a complete Slidev slide deck Markdown file from the user’s notes, docs, or web links. Use when the user says things like “turn these notes into a Slidev deck”, “make slides from this doc”, “create a conference talk deck”, “draft a workshop slidedeck”, “convert this outline into Slidev markdown”, or “use these links as sources and write the slides”. Do NOT use for general writing tasks that are not a Slidev deck.
license: MIT
compatibility: Works in repositories that use Slidev (Markdown-based decks). If sources are web links, requires network access to read them. For validation, requires Node and the repo’s existing build scripts.
metadata:
  author: Cursor Agent
  version: 1.0.0
---
 
# Slidev Build Slidedeck
 
# Instructions
 
### Step 1: Identify the deck’s intent and constraints
Decide what the deck must achieve and the boundaries it must respect.
 
- Extract or infer:
  - **Audience** (who it’s for)
  - **Outcome** (what they should know/do after)
  - **Tone** (e.g., conference talk, internal training, product update, workshop)
  - **Length target** (slide count and/or minutes)
  - **Delivery style** (talk vs workshop vs read-along)
  - **Hard constraints** (required sections, required messages, must-include links, forbidden content)
- If the user provided a repo/theme context, prefer its existing layouts/components and writing style.
 
**Done when:** You can state the deck’s “one sentence promise” and you know the target length, tone, and constraints.
 
---
 
### Step 2: Collect and distill source material (notes, docs, links)
Turn messy inputs into a structured content backbone.
 
- If the user provided **links**, read them and capture:
  - 3–7 **key claims** (with short supporting details)
  - **Numbers/stats** that deserve “fact” slides
  - **Examples/demos** worth showing (code, screenshots, flows)
  - **Quotes** worth pulling verbatim
- If the user provided **text notes**, normalize them into:
  - a “source material summary” section (bulleted)
  - a list of **must-include artifacts** (code blocks, diagrams, checklists, tables)
 
**Done when:** You have a compact source summary that can drive slide decisions without re-reading everything.
 
---
 
### Step 3: Design the talk structure (narrative arc)
Create a section-level outline that controls pacing and attention.
 
Use an explicit arc appropriate to the content, for example:
 
- **Hook → Context → Deep dive / Demos → Implications → Defense / Solutions → Takeaways → Resources → Q&A/End**
 
For each section, define:
 
- **Goal** (why this section exists)
- **Slide range budget** (e.g., Slides 1–5)
- **What the audience should remember**
 
**Done when:** You have 4–7 named sections with goals and rough slide ranges that sum to the target length.
 
---
 
### Step 4: Expand into a slide-by-slide blueprint (numbered)
Write a concrete plan that is easy to execute and hard to derail.

For each slide, specify:

- **#** (explicit numbering)
- **Layout** (e.g., `cover`, `intro`, `section`, `default`, `fact`, `quote`, `center`, `two-cols`)
- **Title**
- **Content instructions** (what must appear on the slide)
- **Presenter notes intent** (what the speaker says, timing cue, or the key beat)

Prefer the pattern:

- **Section divider** slides (`layout: section`) to reset attention
- **Fact/stat** slides (`layout: fact`) when you have a single strong number
- **Demo/flow** slides that show a **step sequence** (often best as a diagram + bullets)
- **Quote** slides for a single punchline / authoritative guidance

**Done when:** Every slide has a purpose, layout choice, and enough instruction that you can write it without inventing new structure mid-way.

---

### Slide content style guide (MUST follow)

These rules govern how content appears on every slide. Violating them produces cluttered, article-like slides that no speaker wants to present.

#### Less is more — ruthlessly cut text
- A slide is NOT an article paragraph. If you can say it out loud, it belongs in presenter notes, not on the slide.
- **Maximum 2-4 short bullet points** per slide, or one key visual/code block. Never both a wall of bullets AND a component grid.
- Each bullet should be a punchy phrase, not a full sentence. Cut every word that doesn't earn its place.
- If a slide has more than ~40 words of visible text (excluding code blocks), it's too dense. Split it.

#### Spread ideas across multiple slides
- **One idea per slide.** If you're tempted to put two concepts on one slide, make two slides instead.
- Build a message across a sequence: slide 1 poses the question, slide 2 delivers the reveal, slide 3 adds the "so what." The speaker's voice connects them — the slides don't need to repeat each other.
- Use `layout: center` for single-line reveals and dramatic moments. Let the audience read one thing and listen to you explain it.

#### Don't repeat yourself
- If a title or concept appeared on the previous slide, don't restate it. Move forward.
- Subtitles and body text should add new information, not rephrase the title.

#### Be punchy and fun
- Prefer surprising, playful, or provocative framing over dry descriptions.
- Rhetorical questions, strikethroughs for comedic effect, single-word reveals — these are your tools.
- The title alone should make someone curious. "What Do You Call Software That..." beats "OpenClaw Architecture Overview."

#### Let the speaker talk
- The slide provides the visual anchor. The presenter notes provide the full narrative.
- If you find yourself writing a paragraph on a slide, move 80% of it to presenter notes and leave only the hook on the slide.

#### Bad vs Good examples

Bad (overloaded, article-style):
```md
# Meet OpenClaw: "Everything Siri Was Supposed to Be"

An open-source AI assistant that lives on your machine. It connects to
WhatsApp, Telegram, Slack. It reads your emails, manages your calendar,
executes shell commands, controls your browser, and **remembers everything**.

- **Gateway** — Central orchestration (WebSocket + HTTP)
- **Skills** — Modular capabilities from ClawHub registry
- **Channels** — WhatsApp, Slack, Telegram, Discord bridges
- **Tools** — Shell, filesystem, browser, APIs
- Full shell access to your machine
- Read/write to all your files
- Send messages on your behalf
- Access environment variables & credentials
- Persistent memory across sessions
```

Good (split across 3 slides, concise, builds tension):
```md
# What Do You Call Software That...

- Accepts instructions via **Telegram**
- Has **full control and access** to your machine
```
Then a reveal slide:
```md
# ~~A Trojan~~ OpenClaw
```
Then the implications:
```md
# OpenClaw

Open-source AI assistant that uses **Skills** from a public registry

<FeatureCard icon="💀" title="One Bad Skill"
  description="Total control over the agent and everything it touches." />
```

#### Decompose lists into slide sequences

When you have a list of N related items (3 threat categories, 4 steps, 5 principles), do NOT dump them into one bullet-point slide. Instead, decompose into a sequence:

1. **Overview slide** — show the list as a visual summary (numbered cards, a simple grid). No details, just labels. This sets up "here are N things, let me walk you through each."
2. **One slide per item** — each gets its own centered slide with a breadcrumb (e.g. "Lethal Trifecta — 1 of 3"), a title, a short subtitle, and empty space for a visual or screenshot. The speaker notes carry the full explanation.
3. **Synthesis slide** (optional) — a punchline that ties them together after the walkthrough.

Bad (everything on one slide):
```md
# The Lethal Trifecta

- **Access to private data** — credentials, emails, files, API keys, environment variables — all in the agent's reach
- **Exposure to untrusted content** — emails, web pages, chat messages, documents — all flow through the agent's context window
- **Ability to communicate externally** — send emails, post to webhooks, make API calls, compose messages on your behalf

Now add persistent memory and shell access — compromised agents become persistent insider threats.
```

Good (overview + 3 deep-dive slides):
```md
<!-- Overview: visual summary with numbered cards -->
# The Lethal Trifecta

[1: Private data] [2: Untrusted content] [3: External comms]
```
Then one slide per item:
```md
<!-- Breadcrumb keeps the audience oriented -->
Lethal Trifecta — 1 of 3
# Access to Private Data
Credentials, emails, files, API keys — all in the agent's reach

<!-- space for screenshot or visual below -->
```
Then the synthesis:
```md
Now add **persistent memory** and **shell access**

Compromised agents become persistent insider threats
```

This pattern works for any enumerated concept: attack stages, architecture layers, defense strategies, research findings. The number in the breadcrumb gives the audience a progress indicator and the speaker room to tell each story fully.
 
---
 
### Step 5: Generate the Slidev Markdown deck
Create or rewrite the target `.md` deck file (commonly `example.md`) so it matches the blueprint.
Apply the slide content style guide from Step 4 to every slide.
 
- **Headmatter** (first `---` block) must include:
  - `title`, theme choice, and any repo-required config
  - `layout` for slide 1 if slide 1 is not the default (do not create a second frontmatter block just to make a cover slide)
- For each slide:
  - Use `---` slide separators
  - Set per-slide `layout:` frontmatter when needed
  - Include the slide’s visible content
  - Add **presenter notes** as HTML comments `<!-- ... -->`
- Choose the most legible representation for the content:
  - Code blocks with selective highlighting for “read it out loud” moments
  - Mermaid diagrams for flows/architectures
  - Tables only when comparisons matter more than storytelling
  - Progressive disclosure (`v-click` / `v-clicks`) when the slide should be spoken line-by-line
 
- **After writing each slide, check:** Could this be split into two simpler slides? Is there text here that should be in presenter notes instead? If the slide has both a paragraph AND a component grid, it is too much -- pick one.

**Done when:** The deck file exists and contains all slides from the blueprint in order, including notes. Every slide passes the "squint test" -- if you squint at it, you should see structure and whitespace, not a wall of text.
 
---
 
### Step 6: Verify and iterate until it builds and reads well
Close the loop with a concrete “works end-to-end” check, then refine.
 
- Validate:
  - The deck **builds** with the repo’s build command (or at least runs in dev)
  - No broken layouts/components
  - Pacing works: the hook is immediate, sections feel balanced, and takeaways are explicit
  - Presenter notes exist for every slide that needs speaking guidance
- If build fails or a slide reads weak:
  - Fix the smallest unit (one slide at a time)
  - Re-run the build/dev check
  - Repeat until done
 
**Done when:** Build/dev succeeds and the deck’s story matches the arc + slide blueprint.
 
---
 
## Examples
 
User says: "Turn these rough notes into a 25-minute conference talk deck in Slidev. Use these three blog posts as sources."
 
Actions:
1. Identify audience, outcome, tone, and slide budget (~25–35 slides).
2. Read the links and extract key claims, stats, demo candidates, and quotes.
3. Propose a narrative arc with 5–7 sections and slide ranges.
4. Produce a numbered slide blueprint with chosen layouts (`cover`, `section`, `fact`, `default`, `quote`).
5. Write the Slidev `.md` deck with presenter notes on every slide.
6. Build/preview, then iterate on any broken slide or weak pacing until it works.
 
Result: A complete, buildable Slidev markdown deck with a coherent narrative and speaker notes.
 
---
 
User says: "Make a workshop slidedeck from our internal doc. It should be hands-on with exercises."
 
Actions:
1. Extract constraints (hands-on, exercise cadence, timebox).
2. Distill the doc into modules and exercise checkpoints.
3. Create a structure that alternates concept → demo → exercise → debrief.
4. Draft slides with explicit exercise instructions and expected outputs.
5. Add presenter notes for facilitation cues and timing.
6. Verify the deck runs and the exercises are unambiguous, then refine.
 
Result: A workshop deck optimized for facilitation, with clear exercises and timing notes.
 
---
 
User says: "Convert this outline into slides and make it look good in our theme."
 
Actions:
1. Infer the intended narrative arc from the outline.
2. Convert each outline node into a slide blueprint with layouts chosen for emphasis.
3. Use the repo’s existing layouts/components and typography patterns.
4. Generate the Slidev markdown and verify it renders correctly.
 
Result: A theme-consistent Slidev deck that matches the outline but reads like a real talk.
 
---
 
User says: "Here are 10 links—make a deck that summarizes them and ends with practical recommendations."
 
Actions:
1. Read and summarize each link into 1–2 bullets, then cluster into themes.
2. Create sections: context, theme clusters, synthesis, recommendations, resources.
3. Use `fact` slides for standout stats and `quote` slides for key pull-quotes.
4. Produce the Slidev deck with a final checklist/recommendations section.
5. Verify build/dev, iterate until it’s concise and coherent.
 
Result: A synthesized Slidev deck with clear recommendations and traceable source-derived content.
 
---
 
## Troubleshooting
 
Error: The first slide is blank or the cover appears as slide 2.
Cause: The deck headmatter (first `---` block) is always slide 1; a second `--- layout: cover ---` block created an extra slide.
Solution: Put `layout: cover` (and any cover props) inside the headmatter and remove the extra “cover frontmatter” slide.
 
---
 
Error: Slides render blank after changing a layout/component.
Cause: A layout/component crashed at runtime or required props are missing.
Solution: Preview in dev, identify the failing slide, simplify to `layout: default`, then reintroduce components incrementally until the break is found.
 
---
 
Error: The deck builds but pacing feels off (too dense, too slow, or missing a punchy hook).
Cause: The arc and slide blueprint weren’t explicit enough, so content drifted into walls of text.
Solution: Rebuild the blueprint: add section divider slides, promote key numbers into `fact` slides, split dense slides, and add progressive disclosure (`v-clicks`) where the speaker needs control.
 
---
 
Error: Web links provided, but the deck contains generic filler or misses key details.
Cause: Source material wasn’t distilled into concrete claims/stats/examples before drafting slides.
Solution: Re-run the source distillation step, extract 3–7 concrete claims + 2–4 stats + 1–3 demos, then update the blueprint and regenerate the affected slides.

---

Error: Slides read like article paragraphs with too much text, two-column bullet grids, or long descriptions.
Cause: Content was dumped onto the slide instead of being split across multiple slides and offloaded to presenter notes.
Solution: Apply the style guide. For each overloaded slide: (1) move explanatory text to presenter notes, (2) keep only the punchy hook or key visual on the slide, (3) split into 2-3 slides that build the story progressively. One idea per slide. If the slide has more than ~40 words of visible text, it needs splitting.
