<script setup lang="ts">
withDefaults(defineProps<{
  step: string | number
  title: string
  description?: string
  active?: boolean
}>(), {
  active: false,
})
</script>

<template>
  <div class="timeline-item" :class="{ 'timeline-active': active }">
    <div class="timeline-marker">
      <span class="timeline-step">{{ step }}</span>
    </div>
    <div class="timeline-body">
      <div class="timeline-title">{{ title }}</div>
      <div v-if="description" class="timeline-desc">{{ description }}</div>
      <slot />
    </div>
  </div>
</template>

<style scoped>
.timeline-item {
  display: flex;
  gap: 1rem;
  padding-bottom: 1.25rem;
  position: relative;
}

.timeline-item:not(:last-child)::after {
  content: '';
  position: absolute;
  left: 17px;
  top: 38px;
  bottom: 0;
  width: 2px;
  background: var(--snyk-border);
}

.timeline-active:not(:last-child)::after {
  background: linear-gradient(180deg, var(--snyk-primary), var(--snyk-border));
}

.timeline-marker {
  flex-shrink: 0;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--snyk-bg-accent);
  border: 2px solid var(--snyk-border);
  z-index: 1;
}

.timeline-active .timeline-marker {
  background: var(--snyk-primary);
  border-color: var(--snyk-primary-light);
}

.timeline-step {
  font-family: 'Sora', sans-serif;
  font-weight: 700;
  font-size: 0.8rem;
  color: var(--snyk-text-muted);
}

.timeline-active .timeline-step {
  color: white;
}

.timeline-body {
  padding-top: 0.3rem;
}

.timeline-title {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  color: var(--snyk-text);
  margin-bottom: 0.2rem;
}

.timeline-desc {
  font-size: 0.85rem;
  color: var(--snyk-text-secondary);
  line-height: 1.5;
}
</style>
