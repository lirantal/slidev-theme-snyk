<script setup lang="ts">
withDefaults(defineProps<{
  mode?: 'dark' | 'light' | 'auto'
  height?: string
}>(), {
  mode: 'auto',
  height: '28px',
})
</script>

<template>
  <span class="snyk-logo-wrap">
    <img
      v-if="mode === 'dark'"
      src="/snyk-logo-dark.png"
      alt="Snyk"
      class="snyk-logo-img"
      :style="{ height }"
    />
    <img
      v-else-if="mode === 'light'"
      src="/snyk-logo-light.png"
      alt="Snyk"
      class="snyk-logo-img"
      :style="{ height }"
    />
    <template v-else>
      <img
        src="/snyk-logo-dark.png"
        alt="Snyk"
        class="snyk-logo-img snyk-logo-dark-only"
        :style="{ height }"
      />
      <img
        src="/snyk-logo-light.png"
        alt="Snyk"
        class="snyk-logo-img snyk-logo-light-only"
        :style="{ height }"
      />
    </template>
  </span>
</template>

<style scoped>
.snyk-logo-wrap {
  display: inline-flex;
  align-items: center;
  line-height: 0;
}

.snyk-logo-img {
  width: auto;
  object-fit: contain;
}

.dark .snyk-logo-light-only,
html.dark .snyk-logo-light-only {
  display: none;
}

html:not(.dark) .snyk-logo-dark-only {
  display: none;
}
</style>
