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
 
### Step 5: Generate the Slidev Markdown deck
Create or rewrite the target `.md` deck file (commonly `example.md`) so it matches the blueprint.
 
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
 
**Done when:** The deck file exists and contains all slides from the blueprint in order, including notes.
 
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
