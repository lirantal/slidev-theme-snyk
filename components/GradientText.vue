<script setup lang="ts">
withDefaults(defineProps<{
  from?: string
  to?: string
}>(), {
  from: 'var(--snyk-primary-light)',
  to: 'var(--snyk-accent-teal)',
})
</script>

<template>
  <span class="grad-text" :style="{ backgroundImage: `linear-gradient(135deg, ${from}, ${to})` }">
    <slot />
  </span>
</template>

<style scoped>
.grad-text {
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
</style>
