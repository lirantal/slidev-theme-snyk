<script setup lang="ts">
import { computed, inject } from 'vue'
import type { InjectionKey } from 'vue'
import configs from '#slidev/configs'

defineProps<{
  class?: string
}>()

const frontmatter = inject(
  '$$slidev-fontmatter' as unknown as InjectionKey<Record<string, any>>,
  {} as Record<string, any>,
)

function asMetaString(value: unknown): string {
  if (typeof value === 'string')
    return value.trim()
  if (Array.isArray(value))
    return value.map(v => (typeof v === 'string' ? v.trim() : '')).filter(Boolean).join(', ')
  return ''
}

const conference = computed(() =>
  asMetaString((configs as Record<string, unknown>).conference),
)

/**
 * Slidev headmatter uses `presenter` for presenter-mode (`boolean | 'dev' | 'build'`),
 * so we must not use `presenter ?? author` — `false` would hide `author`.
 * Optional string override: `presenterName` (theme) or a string `presenter` in YAML if you accept the conflict.
 */
const presenter = computed(() => {
  const c = configs as Record<string, unknown>
  const nameOverride = c.presenterName
  if (typeof nameOverride === 'string' && nameOverride.trim())
    return nameOverride.trim()
  const p = c.presenter
  if (typeof p === 'string' && p.trim())
    return p.trim()
  return asMetaString(c.author)
})

const showCoverMeta = computed(() => conference.value || presenter.value)

/** On-slide headline; optional `coverTitle` overrides deck `title` (e.g. shorter line than browser/export title). */
const coverHeadline = computed(() => {
  const c = configs as Record<string, unknown>
  return asMetaString(c.coverTitle ?? c.title)
})

const coverSubtitle = computed(() =>
  asMetaString((configs as Record<string, unknown>).subtitle),
)

const showCoverHeading = computed(() => coverHeadline.value || coverSubtitle.value)

const titleScale = computed(() => {
  const raw = frontmatter.coverTitleScale
    ?? (configs as Record<string, unknown>).coverTitleScale
  const n = Number(raw)
  if (!n || n <= 0) return 1
  return n / 100
})
</script>

<template>
  <div class="slidev-layout cover" :class="$attrs.class">
    <div class="cover-bg" />
    <div class="cover-content">
      <header v-if="showCoverHeading" class="cover-heading">
        <h1 v-if="coverHeadline" class="cover-title" :style="{ fontSize: `${3.5 * titleScale}rem` }">
          <GradientText>{{ coverHeadline }}</GradientText>
        </h1>
        <p v-if="coverSubtitle" class="cover-subtitle">{{ coverSubtitle }}</p>
      </header>
      <slot />
      <div v-if="showCoverMeta" class="cover-meta">
        <div v-if="conference" class="cover-meta-line cover-meta-conference">{{ conference }}</div>
        <div v-if="presenter" class="cover-meta-line cover-meta-presenter">{{ presenter }}</div>
      </div>
    </div>
    <div class="cover-footer">
      <img src="/snyk-logo-dark.png" alt="Snyk" class="cover-logo" />
    </div>
  </div>
</template>

<style scoped>
.cover-bg {
  position: absolute;
  inset: 0;
  background: url('/bg-dots-gradient.png') no-repeat center center;
  background-size: cover;
  opacity: 0.5;
  pointer-events: none;
}

.cover-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.cover-heading {
  max-width: 52rem;
}

.cover-title {
  white-space: pre-line;
}

.cover-meta {
  margin-top: 2rem;
  text-align: center;
  max-width: 42rem;
  font-family: 'Sora', ui-sans-serif, system-ui, sans-serif;
  font-size: 0.8125rem;
  line-height: 1.4;
}

.cover-meta-line {
  margin: 0;
  line-height: 1.35;
}

.cover-meta-conference {
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--snyk-text-muted);
  letter-spacing: 0.04em;
}

.cover-meta-presenter {
  margin-top: 0.35rem;
  font-size: 0.875rem;
  font-weight: 600;
  color: var(--snyk-text-secondary);
  letter-spacing: 0.02em;
  text-transform: none;
}

.cover-footer {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.25;
  z-index: 1;
}

.cover-logo {
  height: 24px;
  width: auto;
}
</style>
