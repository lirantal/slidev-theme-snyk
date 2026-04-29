<script setup lang="ts">
defineProps<{
  image?: string
  class?: string
}>()
</script>

<template>
  <div class="slidev-layout cover-alt">
    <div class="cover-alt-content">
      <slot />
    </div>
    <div class="cover-alt-image">
      <img v-if="image" :src="image" alt="" />
      <div v-else class="cover-alt-placeholder">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.cover-alt-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--snyk-bg-surface);
}
</style>
