<script setup lang="ts">
defineProps<{
  image?: string
  class?: string
}>()
</script>

<template>
  <div class="slidev-layout image-full">
    <img v-if="image" :src="image" alt="" class="bg-image" />
    <div class="image-full-overlay">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.bg-image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
