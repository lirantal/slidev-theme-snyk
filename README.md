# slidev-theme-snyk

A dark-first, elegant [Slidev](https://github.com/slidevjs/slidev) theme for the Snyk brand. Built for developer presentations with refined typography, smooth transitions, and a full component library.

## Install

Add the following frontmatter to your `slides.md`. Start Slidev then it will prompt you to install the theme automatically.

```yaml
---
theme: snyk
---
```

For local development (this repo), use `theme: ./` instead.

## Quick Start

```bash
npm install
npm run dev        # Preview with example.md
npm run build      # Build static site
npm run export     # Export to PDF
npm run screenshot # Export to PNG
```

## Theme Configuration

Configure the theme via `themeConfig` in your headmatter (first frontmatter block):

```yaml
---
theme: snyk
colorSchema: dark
themeConfig:
  handle: "@yourhandle"       # Your social handle shown in footer
  slideNumbers: true          # Show slide numbers in footer (default: false)
  footerBranding: handle      # 'handle' or 'logo' (default: auto)
---
```

### Available Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `handle` | `string` | — | Your social/account tag (e.g. `@lirantal`). Shown in the footer by default when set. |
| `slideNumbers` | `boolean` | `false` | Show page numbers in the bottom-right footer |
| `footerBranding` | `'handle' \| 'logo'` | auto | What to show in the bottom-left footer. Defaults to `handle` if one is set, otherwise shows the Snyk logo. |

## Fonts

The theme ships with these default fonts (loaded from Google Fonts):

| Role | Font | Usage |
|------|------|-------|
| Sans (body) | Nunito Sans | Body text, lists, descriptions |
| Serif (headings) | Sora | All heading levels, UI labels |
| Mono (code) | JetBrains Mono | Code blocks, inline code |

Override in headmatter:

```yaml
---
fonts:
  sans: Nunito Sans
  serif: Sora
  mono: JetBrains Mono
---
```

## Color Palette

All colors are exposed as CSS custom properties on `:root` and can be overridden in scoped `<style>` blocks:

| Variable | Default | Usage |
|----------|---------|-------|
| `--snyk-bg-dark` | `#0D0B1A` | Primary slide background |
| `--snyk-bg-surface` | `#161228` | Cards, panels |
| `--snyk-bg-accent` | `#1E1740` | Highlighted sections |
| `--snyk-bg-card` | `#1A1530` | Card interiors |
| `--snyk-primary` | `#6A5ACD` | Brand purple, accents |
| `--snyk-primary-light` | `#8B7CF7` | Lighter purple |
| `--snyk-accent-teal` | `#00D4AA` | Teal accent (data, badges) |
| `--snyk-accent-blue` | `#10B2F3` | Blue accent |
| `--snyk-text` | `#FFFFFF` | Headings, key text |
| `--snyk-text-secondary` | `#A8A3C0` | Body text |
| `--snyk-text-muted` | `#6B6588` | Captions, footnotes |
| `--snyk-border` | `#2A2445` | Borders, dividers |

Light mode is supported — cover, section, and end layouts stay dark while content slides switch to a light palette.

## Transitions

The default slide transition is `snyk-fade` (a subtle fade + upward motion). Override per-slide:

```yaml
---
transition: fade
---
```

Built-in transitions: `snyk-fade`, `fade`, `slide-left`, `slide-right`, `slide-up`, `slide-down`.

Click animations (`v-click`) use a refined `opacity + translateY(8px)` with 200ms ease-out.

## Layouts

All layouts use a dark background by default and support light mode.

| Layout | Description | Props |
|--------|-------------|-------|
| `cover` | Hero title slide with gradient background and Snyk logo | — |
| `cover-alt` | Split layout: content left, image/slot right | `image` |
| `intro` | Speaker/about-me slide with avatar | `avatar` |
| `section` | Section divider with gradient accent line | — |
| `default` | Standard content slide | — |
| `center` | Centered content | — |
| `two-cols` | Two columns; use `::right::` for the second column | — |
| `two-cols-header` | Header + two columns; use `::left::` and `::right::` | — |
| `image-right` | Content left, image right | `image` |
| `image-left` | Image left, content right | `image` |
| `image-full` | Full-bleed background image with overlay text | `image` |
| `quote` | Large quotation with decorative mark | — |
| `fact` | Big number/stat with gradient text | — |
| `end` | Closing slide with Snyk logo | — |
| `full` | Full-screen, zero padding | — |

### Layout Examples

```md
---
layout: cover
---
# My Title

---
layout: image-right
image: /my-screenshot.png
---
# Content on the Left

---
layout: two-cols
---
# Left Side
Content here

::right::

# Right Side
More content

---
layout: fact
---
# 288%
ROI with Snyk

---
layout: intro
avatar: https://github.com/username.png
---
# Your Name
**Role at Company**
```

## Components

All components are auto-imported and available in any slide.

### SnykLogo

Renders the official Snyk logo with dark/light mode support.

```md
<SnykLogo />
<SnykLogo mode="dark" height="40px" />
```

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `mode` | `'dark' \| 'light' \| 'auto'` | `'auto'` | Which logo variant to show |
| `height` | `string` | `'28px'` | Logo height |

### Badge

Colored tag/label.

```md
<Badge>Default</Badge>
<Badge variant="teal">Beta</Badge>
<Badge variant="danger">Critical</Badge>
```

| Prop | Type | Default |
|------|------|---------|
| `variant` | `'primary' \| 'teal' \| 'danger' \| 'blue'` | `'primary'` |

### GradientText

Applies a purple-to-teal gradient to inline text.

```md
# <GradientText>AI Security</GradientText>
```

| Prop | Type | Default |
|------|------|---------|
| `from` | `string` | `var(--snyk-primary-light)` |
| `to` | `string` | `var(--snyk-accent-teal)` |

### StatCard

Metric card for stats and KPIs.

```md
<StatCard value="288%" label="ROI" description="Year over year" color="teal" />
```

| Prop | Type | Default | Required |
|------|------|---------|----------|
| `value` | `string` | — | Yes |
| `label` | `string` | — | Yes |
| `description` | `string` | — | No |
| `color` | `'purple' \| 'teal' \| 'blue'` | `'purple'` | No |

### FeatureCard

Card with emoji icon, title, and description.

```md
<FeatureCard icon="🔍" title="Discover" description="Find every agent tool" />
```

| Prop | Type | Default | Required |
|------|------|---------|----------|
| `title` | `string` | — | Yes |
| `description` | `string` | — | No |
| `icon` | `string` | `'🔒'` | No |

### IconCard

Card with a named `#icon` slot for custom icon content.

```md
<IconCard title="Visibility" description="See everything">
  <template #icon>🔍</template>
</IconCard>
```

| Prop | Type | Required |
|------|------|----------|
| `title` | `string` | Yes |
| `description` | `string` | No |

### BarChart

Horizontal bar chart for benchmarks and data visualization.

```md
<BarChart :data="[
  { label: 'Category A', value: 85 },
  { label: 'Category B', value: 62, color: '#00D4AA' },
]" :max-value="100" />
```

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `data` | `Array<{ label, value, color?, suffix? }>` | — | Bar data (required) |
| `maxValue` | `number` | Auto (max of data) | Scale maximum |
| `showValues` | `boolean` | `true` | Show value labels |

### ComparisonChart

Side-by-side dual-bar comparison.

```md
<ComparisonChart
  label-a="Before"
  label-b="After"
  :data="[
    { label: 'Speed', valueA: 30, valueB: 80 },
    { label: 'Coverage', valueA: 45, valueB: 92 },
  ]"
/>
```

| Prop | Type | Default |
|------|------|---------|
| `data` | `Array<{ label, valueA, valueB, suffix? }>` | — (required) |
| `labelA` | `string` | `'Before'` |
| `labelB` | `string` | `'After'` |
| `colorA` | `string` | `var(--snyk-text-muted)` |
| `colorB` | `string` | `var(--snyk-accent-teal)` |
| `maxValue` | `number` | `100` |

### Quote

Styled blockquote with attribution.

```md
<Quote author="Jane Doe" role="CISO, Acme Corp">
  Security has to move at the speed of AI.
</Quote>
```

| Prop | Type | Required |
|------|------|----------|
| `author` | `string` | No |
| `role` | `string` | No |
| `avatar` | `string` | No |

### Screenshot

Browser-framed screenshot with shadow and glow.

```md
<Screenshot src="/my-screenshot.png" alt="Dashboard view" />
```

| Prop | Type | Default |
|------|------|---------|
| `src` | `string` | — (required) |
| `alt` | `string` | `''` |
| `rounded` | `boolean` | `true` |

### TimelineItem

Step indicator for process flows. Stack multiple for a timeline.

```md
<TimelineItem step="1" title="Install" description="Run the CLI" active />
<TimelineItem step="2" title="Scan" description="Detect all tools" />
```

| Prop | Type | Default | Required |
|------|------|---------|----------|
| `step` | `string \| number` | — | Yes |
| `title` | `string` | — | Yes |
| `description` | `string` | — | No |
| `active` | `boolean` | `false` | No |

## CSS Utility Classes

Available in any slide for quick styling:

| Class | Description |
|-------|-------------|
| `.gradient-text` | Purple-to-teal gradient text fill |
| `.gradient-text-purple` | Purple-only gradient text |
| `.glow-card` | Card with border, rounded corners, hover glow |
| `.glass-card` | Frosted glass card with backdrop blur |
| `.snyk-badge-primary` | Purple badge styling |
| `.snyk-badge-teal` | Teal badge styling |
| `.snyk-badge-danger` | Red badge styling |
| `.snyk-divider` | Full-width gradient divider line |
| `.snyk-glow-line` | Short gradient accent line |

## Global Footer

A persistent footer appears on all slides except `cover`, `cover-alt`, `end`, and `full` layouts. It shows the Snyk logo on the left. Slide numbering is opt-in via `themeConfig.slideNumbers`.

## Assets

Place images and screenshots in the `public/` folder and reference them with absolute paths:

```md
![Alt text](/my-image.png)
```

The theme expects two logo files in `public/`:

- `snyk-logo-dark.png` — logo for dark backgrounds
- `snyk-logo-light.png` — logo for light backgrounds

## Contributing

```bash
npm install
npm run dev          # Start theme preview with example.md
npm run build        # Production build
npm run export       # Export to PDF
npm run screenshot   # Export to PNG
```

Edit `example.md` to preview changes. Layouts live in `layouts/`, components in `components/`, and styles in `styles/layout.css`.
