<script setup lang="ts">
withDefaults(defineProps<{
  value: string
  label: string
  description?: string
  color?: 'purple' | 'teal' | 'blue'
}>(), {
  color: 'purple',
})
</script>

<template>
  <div class="stat-card glow-card">
    <div class="stat-value" :class="`stat-${color}`">{{ value }}</div>
    <div class="stat-label">{{ label }}</div>
    <div v-if="description" class="stat-desc">{{ description }}</div>
  </div>
</template>

<style scoped>
.stat-card {
  text-align: center;
  padding: 1.5rem 1rem;
}

.stat-value {
  font-family: 'Sora', sans-serif;
  font-size: 2.8rem;
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  margin-bottom: 0.4rem;
}

.stat-purple {
  background: linear-gradient(135deg, var(--snyk-action), var(--snyk-action-secondary));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.stat-teal {
  color: var(--snyk-accent-teal);
}

.stat-blue {
  color: var(--snyk-accent-blue);
}

.stat-label {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  color: var(--snyk-text);
  margin-bottom: 0.25rem;
}

.stat-desc {
  font-size: 0.85rem;
  color: var(--snyk-text-muted);
  line-height: 1.4;
}
</style>
