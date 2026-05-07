<script setup lang="ts">
withDefaults(defineProps<{
  variant?: 'primary' | 'teal' | 'danger' | 'blue' | 'success' | 'info'
}>(), {
  variant: 'primary',
})
</script>

<template>
  <span class="snyk-badge" :class="`snyk-badge-${variant}`">
    <slot />
  </span>
</template>
