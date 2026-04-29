<script setup lang="ts">
defineProps<{
  title: string
  description?: string
}>()
</script>

<template>
  <div class="icon-card glow-card">
    <div class="icon-card-icon">
      <slot name="icon" />
    </div>
    <h3 class="icon-card-title">{{ title }}</h3>
    <p v-if="description" class="icon-card-desc">{{ description }}</p>
    <slot />
  </div>
</template>

<style scoped>
.icon-card {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.4rem;
}

.icon-card-icon {
  font-size: 1.5rem;
  margin-bottom: 0.25rem;
  color: var(--snyk-primary-light);
}

.icon-card-title {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  color: var(--snyk-text);
  margin: 0;
}

.icon-card-desc {
  font-size: 0.85rem;
  color: var(--snyk-text-secondary);
  line-height: 1.5;
  margin: 0;
}
</style>
