<script setup lang="ts">
withDefaults(defineProps<{
  title: string
  description?: string
  icon?: string
}>(), {
  icon: '🔒',
})
</script>

<template>
  <div class="feature-card glow-card">
    <div class="feature-icon">{{ icon }}</div>
    <h3 class="feature-title">{{ title }}</h3>
    <p v-if="description" class="feature-desc">{{ description }}</p>
    <slot />
  </div>
</template>

<style scoped>
.feature-card {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.feature-icon {
  font-size: 1.8rem;
  margin-bottom: 0.25rem;
}

.feature-title {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 1.05rem;
  color: var(--snyk-text);
  margin: 0;
}

.feature-desc {
  font-size: 0.9rem;
  color: var(--snyk-text-secondary);
  line-height: 1.5;
  margin: 0;
}
</style>
