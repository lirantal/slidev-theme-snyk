<script setup lang="ts">
defineProps<{
  class?: string
}>()
</script>

<template>
  <div class="slidev-layout cover" :class="$attrs.class">
    <div class="cover-content">
      <slot />
    </div>
    <div class="cover-footer">
      <img src="/snyk-logo-dark.png" alt="Snyk" class="cover-logo" />
    </div>
  </div>
</template>

<style scoped>
.cover-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.cover-footer {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.25;
}

.cover-logo {
  height: 24px;
  width: auto;
}
</style>
