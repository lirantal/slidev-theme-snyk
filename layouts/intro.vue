<script setup lang="ts">
import { computed } from 'vue'
import configs from '#slidev/configs'

defineProps<{
  avatar?: string
  class?: string
}>()

const tc = computed(() => (configs as any).themeConfig ?? {})
const github = computed(() => tc.value.github ?? '')
const x = computed(() => tc.value.x ?? tc.value.twitter ?? '')
const website = computed(() => tc.value.website ?? '')
const hasSocials = computed(() => github.value || x.value || website.value)
</script>

<template>
  <div class="slidev-layout intro" :class="$attrs.class">
    <div v-if="avatar" class="intro-avatar">
      <img :src="avatar" alt="" class="avatar-img" />
    </div>
    <div class="intro-content">
      <slot />
      <div v-if="hasSocials" class="intro-socials">
        <span v-if="github">GitHub: {{ github }}</span>
        <span v-if="x">X: {{ x }}</span>
        <span v-if="website">{{ website }}</span>
      </div>
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

.intro-socials {
  margin-top: 1rem;
  display: flex;
  gap: 1rem;
  font-size: 0.875rem;
  color: var(--snyk-text-muted);
}
</style>
