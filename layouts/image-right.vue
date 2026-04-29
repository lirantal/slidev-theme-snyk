<script setup lang="ts">
defineProps<{
  image?: string
  class?: string
}>()
</script>

<template>
  <div class="slidev-layout image-right">
    <div class="content-side">
      <slot />
    </div>
    <div class="image-side">
      <img v-if="image" :src="image" alt="" class="side-image" />
      <slot v-else name="right" />
    </div>
  </div>
</template>

<style scoped>
.content-side {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem 3rem;
}

.image-side {
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background: var(--snyk-bg-surface);
}

.side-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
