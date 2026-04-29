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

