<script setup lang="ts">
defineProps<{
  avatar?: string
  class?: string
}>()
</script>

<template>
  <div class="slidev-layout intro" :class="$attrs.class">
    <div v-if="avatar" class="intro-avatar">
      <img :src="avatar" alt="" class="avatar-img" />
    </div>
    <div class="intro-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.intro-avatar {
  flex-shrink: 0;
}

.avatar-img {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--snyk-border);
  box-shadow: 0 0 40px var(--snyk-glow);
}

.intro-content {
  flex: 1;
}
</style>
