<script setup lang="ts">
withDefaults(defineProps<{
  label?: string
  href?: string
  source?: string
  align?: 'left' | 'center' | 'right'
}>(), {
  label: 'Reference',
  align: 'left',
})
</script>

<template>
  <aside class="snyk-footnote" :class="`snyk-footnote-${align}`" aria-label="Slide reference">
    <div class="footnote-rule" />
    <div class="footnote-body">
      <span v-if="label" class="footnote-label">{{ label }}</span>
      <a v-if="href" :href="href" target="_blank" rel="noreferrer" class="footnote-source">
        <slot>{{ source }}</slot>
      </a>
      <span v-else class="footnote-source">
        <slot>{{ source }}</slot>
      </span>
    </div>
  </aside>
</template>

<style scoped>
.snyk-footnote {
  position: absolute;
  right: 3rem;
  bottom: 3rem;
  left: 3rem;
  z-index: 8;
  display: flex;
  align-items: flex-start;
  gap: 0.7rem;
  color: var(--snyk-text-muted);
  font-family: 'Nunito Sans', sans-serif;
  font-size: 0.72rem;
  line-height: 1.35;
  pointer-events: auto;
  transform: translateY(calc(var(--snyk-footnote-stack, 0) * -1.2rem));
}

.snyk-footnote + .snyk-footnote {
  --snyk-footnote-stack: 1;
}

.snyk-footnote + .snyk-footnote + .snyk-footnote {
  --snyk-footnote-stack: 2;
}

.snyk-footnote + .snyk-footnote + .snyk-footnote + .snyk-footnote {
  --snyk-footnote-stack: 3;
}

.snyk-footnote-center {
  justify-content: center;
  text-align: center;
}

.snyk-footnote-right {
  justify-content: flex-end;
  text-align: right;
}

.footnote-rule {
  width: 32px;
  height: 1px;
  margin-top: 0.48rem;
  flex: 0 0 auto;
  background: linear-gradient(90deg, var(--snyk-action), var(--snyk-action-secondary));
  opacity: 0.75;
}

.snyk-footnote-center .footnote-rule,
.snyk-footnote-right .footnote-rule {
  display: none;
}

.footnote-body {
  display: grid;
  grid-template-columns: max-content minmax(0, 1fr);
  align-items: baseline;
  column-gap: 0.5rem;
  max-width: 580px;
}

.footnote-label {
  color: var(--snyk-text-secondary);
  font-family: 'Sora', sans-serif;
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.footnote-source {
  color: var(--snyk-text-muted);
  min-width: 0;
}

a.footnote-source {
  border-bottom-color: rgba(0, 188, 255, 0.35);
}

a.footnote-source:hover {
  color: var(--snyk-glow-blue);
}

.footnote-source :deep(p) {
  display: inline;
  margin: 0;
  color: inherit;
  font-size: inherit;
  line-height: inherit;
}

:global(html:not(.dark) .snyk-footnote) {
  color: #6E6C7A;
}

:global(html:not(.dark) .footnote-label) {
  color: #4A4A55;
}

:global(html:not(.dark) .footnote-source) {
  color: #6E6C7A;
}
</style>
