<script setup lang="ts">
withDefaults(defineProps<{
  src: string
  alt?: string
  rounded?: boolean
}>(), {
  alt: '',
  rounded: true,
})
</script>

<template>
  <div class="screenshot-frame" :class="{ 'screenshot-rounded': rounded }">
    <div class="screenshot-bar">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </div>
    <img :src="src" :alt="alt" class="screenshot-img" />
  </div>
</template>

<style scoped>
.screenshot-frame {
  background: var(--snyk-bg-surface);
  border: 1px solid var(--snyk-border);
  overflow: hidden;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3), 0 0 60px var(--snyk-glow);
}

.screenshot-rounded {
  border-radius: 10px;
}

.screenshot-bar {
  display: flex;
  gap: 6px;
  padding: 8px 12px;
  background: var(--snyk-bg-accent);
  border-bottom: 1px solid var(--snyk-border);
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--snyk-border-light);
}

.screenshot-img {
  width: 100%;
  display: block;
}
</style>
