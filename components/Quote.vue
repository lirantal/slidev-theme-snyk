<script setup lang="ts">
defineProps<{
  author?: string
  role?: string
  avatar?: string
}>()
</script>

<template>
  <div class="snyk-quote">
    <div class="quote-mark">"</div>
    <div class="quote-body">
      <slot />
    </div>
    <div v-if="author" class="quote-attribution">
      <img v-if="avatar" :src="avatar" alt="" class="quote-avatar" />
      <div>
        <div class="quote-author">{{ author }}</div>
        <div v-if="role" class="quote-role">{{ role }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.snyk-quote {
  position: relative;
  padding-left: 0.5rem;
}

.quote-mark {
  position: absolute;
  top: -1.5rem;
  left: -0.5rem;
  font-size: 5rem;
  font-family: 'Sora', sans-serif;
  color: var(--snyk-primary);
  opacity: 0.2;
  line-height: 1;
  pointer-events: none;
}

.quote-body {
  font-size: 1.3rem;
  line-height: 1.5;
  color: var(--snyk-text);
  font-style: italic;
  font-weight: 300;
  margin-bottom: 1.25rem;
}

.quote-body :deep(p) {
  color: var(--snyk-text);
  font-size: inherit;
  line-height: inherit;
}

.quote-attribution {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.quote-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
}

.quote-author {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--snyk-text);
  font-style: normal;
}

.quote-role {
  font-size: 0.8rem;
  color: var(--snyk-text-muted);
  font-style: normal;
}
</style>
