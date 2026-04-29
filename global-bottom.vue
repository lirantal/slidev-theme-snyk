<script setup lang="ts">
import { computed } from 'vue'
import { useNav } from '@slidev/client'
import configs from '#slidev/configs'

const { currentLayout, currentPage, total } = useNav()

const hiddenLayouts = ['cover', 'cover-alt', 'end', 'full']

const showSlideNumbers = computed(() => configs.themeConfig?.slideNumbers === true)

const handle = computed(() => configs.themeConfig?.handle as string | undefined)

const footerBranding = computed(() => {
  const explicit = configs.themeConfig?.footerBranding as string | undefined
  if (explicit === 'logo') return 'logo'
  if (explicit === 'handle') return handle.value ? 'handle' : 'logo'
  return handle.value ? 'handle' : 'logo'
})
</script>

<template>
  <footer v-if="!hiddenLayouts.includes(currentLayout)" class="snyk-footer">
    <div class="footer-left">
      <span v-if="footerBranding === 'handle' && handle" class="footer-handle">{{ handle }}</span>
      <img v-else src="/snyk-logo-dark.png" alt="Snyk" class="footer-logo" />
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

.footer-handle {
  font-weight: 600;
  font-size: 0.75rem;
  letter-spacing: 0.02em;
}

.footer-right {
  opacity: 0.5;
  letter-spacing: 0.05em;
}
</style>
