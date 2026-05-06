# AGENTS.md

Context for AI coding agents working on `slidev-theme-snyk`.

## What this repo is

This is a **Slidev theme** package for **Snyk**.

- **Slidev**: a Vue-powered, Vite-based, Markdown-first slide deck tool. Themes provide layouts, components, and styles that Slidev loads when a deck sets `theme: snyk`.
- **Theme surface area in this repo**:
  - `layouts/`: Slidev layout components (Vue SFCs) referenced by slides via `layout: ...`
  - `components/`: Vue components available to slide content
  - `styles/`: theme CSS + style entry (`styles/index.ts`, `styles/layout.css`)
  - `example.md`: local preview deck used by dev/build scripts

## Primary workflows (what “done” looks like)

- **Preview theme locally**: `npm run dev` (opens Slidev using `example.md`)
- **Production build**: `npm run build` (builds `example.md` into `dist/`)
- **Export artifacts**:
  - `npm run export` (PDF)
  - `npm run screenshot` (PNGs)

## Runtime + package manager expectations

- **Node**: Prefer **Node 24+** in this devcontainer (there is a system Node at `/usr/local/bin/node`).
  - This repo uses modern Slidev/Vite tooling that may require newer Node than some embedded editor runtimes.
- **npm**: This repo currently uses **npm + `package-lock.json`**.

### Important gotcha (Cursor embedded Node)

In this environment, `node` on PATH may resolve to Cursor’s embedded runtime (e.g. `~/.cursor-server/.../node`), which can be **older than the system Node** and can break native dependencies (notably `oxc-parser` bindings used by the Slidev toolchain).

If you hit errors like **“Cannot find native binding”** during `npm install` or `npm run build`, retry with the system Node first:

```bash
PATH=/usr/local/bin:$PATH npm install
PATH=/usr/local/bin:$PATH npm run build
```

## Updating Slidev

- Slidev packages are in `package.json` (`@slidev/cli`, `@slidev/types`).
- After upgrades, always validate with `npm run build` and ensure `example.md` renders.

## Slidev headmatter and slide structure

The first `---` fenced block in a `.md` file is the **headmatter**. It is always slide 1 — there is no Slidev option to skip it. It serves dual purpose:

- **Deck-wide config** — keys like `theme`, `title`, `fonts`, `transition`, `colorSchema`, `themeConfig`, `defaults` apply globally to every slide.
- **Slide 1 frontmatter** — keys like `layout`, `class`, or any custom per-slide prop (e.g. `coverTitleScale`) apply only to this first slide.

When creating or editing `example.md`, **never** add a separate `--- layout: cover ---` block after the headmatter to act as slide 1. That creates a duplicate: a blank default-layout slide 1 from the headmatter, and the cover as slide 2. Instead, put `layout: cover` inside the headmatter itself.

## Slidev layout development — patterns & pitfalls

### Accessing per-slide frontmatter in layouts

Layout components are **providers** of the slide context, not consumers. This means:

- **`useSlideContext()` from `@slidev/client` will crash** if called inside a layout component. It relies on `inject()` from a parent `SlideWrapper`, which hasn't provided the context yet when the layout's `setup()` runs.
- To read per-slide frontmatter from a layout, use `inject` with Slidev's internal injection key:
  ```ts
  import { inject } from 'vue'
  import type { InjectionKey } from 'vue'

  const frontmatter = inject(
    '$$slidev-fontmatter' as unknown as InjectionKey<Record<string, any>>,
    {} as Record<string, any>,
  )
  // Note: the key has a typo ("fontmatter") — this is Slidev's actual key.
  ```
- For **deck-level** (headmatter) config, use `import configs from '#slidev/configs'`.
- Prefer the per-slide `frontmatter` first, falling back to `configs` for global defaults.

### Vue template refs vs script refs

In Vue `<template>`, computed refs auto-unwrap — use `myComputed` not `myComputed.value`. Using `.value` in a template evaluates to `undefined` and silently fails (e.g. an inline style binding produces `NaN` and the browser ignores it).

### Styling text size in slide Markdown content

Tailwind/UnoCSS utility classes like `text-2xl`, `text-4xl` on a `<div>` often have **no visible effect** on text inside Slidev slides. Two reasons:

1. **Markdown inside `<div>` renders as child `<p>` elements.** The theme's `.slidev-layout p` rule sets a fixed `font-size` that overrides the parent div's inherited size.
2. **UnoCSS classes may lose specificity** against the theme's scoped CSS rules in `styles/layout.css`.

**Solution:** Use inline `style="font-size: ..."` directly on the element that contains the text — either write raw HTML (`<h2>`, `<p>`) with inline styles, or use Slidev's `<style>` block with scoped overrides. Do not rely on a parent div's font-size cascading into Markdown-generated children.

```md
<!-- BAD: div font-size won't reach the <p> inside -->
<div style="font-size: 2.5rem">

Some **markdown** text

</div>

<!-- GOOD: style on the actual rendered element -->
<h2 style="font-size: 2.5rem">Some <strong>markdown</strong> text</h2>
```

### Testing layout changes

After any change to a layout `.vue` file, **always verify** it still renders:
1. Check the dev server terminal for errors.
2. Navigate to a slide using that layout in the browser.
3. Run `npm run build` to catch build-time issues.

Layout bugs often fail silently — the slide simply goes blank with no console error visible in the terminal.

