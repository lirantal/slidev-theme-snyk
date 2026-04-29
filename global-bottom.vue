<script setup lang="ts">
import { computed } from 'vue'
import { useNav } from '@slidev/client'
import configs from '#slidev/configs'

const { currentLayout, currentPage, total } = useNav()

const hiddenLayouts = ['cover', 'cover-alt', 'end', 'full']

const showSlideNumbers = computed(() => configs.themeConfig?.slideNumbers === true)
</script>

<template>
  <footer v-if="!hiddenLayouts.includes(currentLayout)" class="snyk-footer">
    <div class="footer-left">
      <img src="/snyk-logo-dark.png" alt="Snyk" class="footer-logo" />
    </div>
    <div v-if="showSlideNumbers" class="footer-right">
      {{ currentPage }} / {{ total }}
    </div>
  </footer>
</template>

<style scoped>
.snyk-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.6rem 1.5rem;
  color: var(--snyk-text-muted);
  font-size: 0.7rem;
  font-family: 'Sora', sans-serif;
  pointer-events: none;
  z-index: 10;
}

.footer-left {
  opacity: 0.35;
}

.footer-logo {
  height: 16px;
  width: auto;
}

.footer-right {
  opacity: 0.5;
  letter-spacing: 0.05em;
}
</style>
